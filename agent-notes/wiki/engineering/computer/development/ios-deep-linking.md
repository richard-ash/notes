---
source: agent
compiled_from:
  - agent-notes/raw/engineering/computer/development/2025-03-24-deep-links-with-async-algorithms.md
compiled_at: 2026-10-09
model: claude-fable-5-1
confidence: medium
---

# iOS Deep Linking

A deep link is a URL that opens an app and lands the user on a specific screen rather than the home tab. Jacob Bartlett's framing: alongside push notifications, deep links are the technical cornerstone of retention, because the retention loop is *notification → tap → the right screen*. A broken or missing deep-link handler turns every push campaign into a trip to the home screen.

Structurally, Bartlett observes, a deep-link handler is **built once and injected everywhere, while routes are added constantly** at the request of product and marketing. That asymmetry is why the handler's interface matters more than any single route: it is the one piece of navigation plumbing that every coordinator in the app depends on.

This article compiles Bartlett's walkthrough of building such a handler on Apple's [Swift Async Algorithms](https://github.com/apple/swift-async-algorithms) package, using his open-source sample app [Linky](https://github.com/jacobsapps/Linky). The architecture is UIKit coordinators wrapping SwiftUI views in `UIHostingController`s, but the handler itself is independent of navigation style.

## How a URL reaches the app

Two mechanisms get a URL to an iOS app:

- **Custom URL scheme.** A URL Type entry in `Info.plist` maps a scheme like `linky://` to the bundle identifier. Trivial to set up; anyone can register the same scheme, so it is not secure.
- **Universal links.** Ordinary `https://` URLs on a domain you control. The mapping to the app lives in an `apple-app-site-association` file hosted on that domain. More setup, but once inside the app they are handled identically.

Inside a UIKit scene-based app, URLs arrive through three different callbacks; a pure SwiftUI app gets one modifier instead:

| Situation | Entry point | Where the URL is |
|---|---|---|
| Cold launch caused by a link | `scene(_:willConnectTo:options:)` | `connectionOptions.urlContexts` |
| App already running, custom scheme | `scene(_:openURLContexts:)` | the `UIOpenURLContext`'s `url` |
| App already running, universal link | `scene(_:continue:)` | `userActivity.webpageURL` |
| Pure SwiftUI | `.onOpenURL` on the root view inside `WindowGroup` | the closure argument |

Every entry point should do exactly one thing: hand the URL to the handler (`Task { await deepLink.open(url: url) }`). On cold launch, build the window and coordinator tree first, then open the URL.

Two development conveniences Bartlett recommends: trigger links from the terminal with `xcrun simctl openurl booted 'linky://addcontact'`, and to debug a cold launch, check "Wait for the executable to be launched" in the scheme's Run options so Xcode builds without launching and the `simctl` command starts the app under the debugger. While iterating, hardcoding a URL in `willConnectTo` is faster than either.

## The handler's interface

Bartlett splits the handler into ingress and egress:

```swift
public protocol DeepLinkHandler {
    func open(url: URL) async
    func stream(_ link: DeepLink) -> AsyncChannel<DeepLink>
}
```

`DeepLink` is an enum of every route the app understands. Its `String` raw values are regular expressions (`#"/favourites/?$"#`), and `link(from:)` returns the first case whose pattern matches the URL's absolute string, via a small `~=` operator wrapping `NSRegularExpression`.

Two implications the article leaves implicit:

- **Declaration order is precedence order.** `allCases.first` means an earlier case shadows a later one if both patterns match, and the patterns are anchored only at the end. Adding a route whose path is a suffix of an existing one will silently route to the wrong case.
- **The design carries no parameters.** The enum has no associated values, so `linky://contact/42` has no home here. The moment a route carries an identifier, the raw-value-as-regex trick stops working and the handler needs a parsed payload type instead. For a sample app this is fine; for a product it is the first thing to change.

## Why one channel per route

The implementation holds one `AsyncChannel<DeepLink>` per enum case. `open(url:)` parses the URL and `send`s the case into its channel; `stream(_:)` is a switch returning the matching channel.

`AsyncChannel` is the Async Algorithms analogue of a Combine subject, with one crucial difference: it applies **back pressure**. Bartlett describes this as buffering; more precisely, `send` suspends until a consumer's iterator takes the value, so the channel is a rendezvous point rather than a queue. That property does two things for deep linking:

1. **The `Task { }` wrapper inside `open(url:)` is load-bearing.** Without it, `open` would suspend until the matching coordinator happened to be iterating. With it, `open` returns immediately and the value waits.
2. **Cold-launch links are not lost.** If a URL arrives before the coordinator's listener loop has started, the send parks until it has. The classic "event fired before anyone subscribed" race does not exist. The flip side: a route whose coordinator never iterates leaves a suspended task hanging forever. Bartlett avoids this by starting `handleDeepLinks()` in every coordinator's `init`.

The reason for *separate* channels is the package's biggest gap relative to Combine: **no broadcasting or multicasting.** An `AsyncChannel` supports exactly one `for await` consumer; two iterators calling `next()` compete for values rather than each receiving a copy. So one channel per route, hidden behind `stream(_:)` so callers see a generic API. The cost is a hand-maintained N-way switch in two places: every new route touches the enum, both switches, and a new stored property.

The distinction is worth naming because it recurs everywhere. A Combine `PassthroughSubject` or Postgres `NOTIFY` ([[postgres-listen-notify]]) is fire-and-forget broadcast: every subscriber gets a copy, and nothing is delivered if nobody is listening. `AsyncChannel` is point-to-point hand-off with exactly one receiver and guaranteed delivery. Deep links happen to want the latter. Bartlett makes the point himself: a link should trigger exactly one navigation, so the single-consumer constraint is a feature here rather than a bug.

## Consuming the streams in coordinators

Each coordinator adopts `handleDeepLinks() async` and kicks it off from `init` with `Task { await handleDeepLinks() }`, so listeners exist before any URL can arrive.

**First attempt: a task group.** One child task per stream, each running its own `for await` loop. The group is mandatory: two sequential `for await` loops would never reach the second, because the first never terminates. It works, but Bartlett calls the ergonomics "hot garbage."

**Second attempt: `merge`.** `merge(stream(.recents), stream(.mostRecent))` combines the channels into one sequence, so each coordinator has a single `for await` and a `switch`. Single-consumer semantics survive, since each underlying channel is still iterated in exactly one place.

**Threading.** The merged loop runs on a background executor, and UIKit navigation from there trips Xcode's main-thread checker. The fix is to mark `navigate(to:)` as `@MainActor` and `await` it inside the loop, so each navigation suspends and hops to the main actor. The task-group version had sidestepped this with `@MainActor in` closures.

**An abandoned refactor.** Bartlett disliked that `import AsyncAlgorithms` leaked into every coordinator and tried a `mergeStreams(_:_:)` helper on the protocol. But `merge` is not variadic (`AsyncMerge2Sequence` and `AsyncMerge3Sequence` are distinct types), so each arity needs its own overload. He judged one leaked import cheaper than the helper and dropped it. It is [[wrong-abstraction]] in miniature: tolerate a little leakage rather than build an abstraction whose shape is dictated by a library quirk.

## The bug: a bus with two instances is not a bus

For a long stretch nothing worked. Breakpoints showed `open(url:)` and `stream(_:)` both firing, yet listeners never ran, except, puzzlingly, on the last tab. The memory graph debugger showed the cause: **one `DeepLinkHandlerImpl` instance per coordinator.**

Bartlett had registered the handler with the Factory dependency-injection library as `Factory(self) { DeepLinkHandlerImpl() }`, whose default scope is a fresh instance per resolution. The `SceneDelegate` was sending into channels on its own instance; each coordinator was listening to channels on another. The fix was `.scope(.singleton)`.

The general lesson: for any in-process message bus, **object identity is part of the contract.** Producer and consumers must share the instance, and DI containers default to transient lifetimes unless told otherwise. It is the same family of wiring mistake that the explicit registration-and-resolution discipline in [[bazel-ios-modularity]] exists to prevent.

## What Bartlett wanted instead

The API he could not build: a single broadcast channel inside the handler and a variadic `stream(_ links: DeepLink...) -> AsyncStream<DeepLink>` that filters it, so a coordinator writes `for await link in deepLink.stream(.recents, .mostRecent)` and no per-route storage exists. His sketch wraps a hypothetical `BroadcastChannel` in an `AsyncStream` continuation. A self-described Combine fan, he notes this is a few lines with `PassthroughSubject` and simply unsupported in Async Algorithms.

The fair reading of the whole exercise: broadcast is the one place where Combine is strictly more capable than Async Algorithms for app-level eventing. Everything else in the article, `merge`, `for await`, actor hopping, is at least as ergonomic in the concurrency world.

## Temporal notes

The article dates from March 2025.

- **Default main-actor isolation.** Swift 6.2 (Xcode 26, autumn 2025) added an opt-in build setting that makes a module's declarations `@MainActor` by default. In a project using it, the coordinator's `navigate(to:)` is main-actor isolated without annotation and the background-thread navigation bug does not arise; the explicit `@MainActor` becomes documentation rather than a fix.
- **Still no broadcast.** As far as this compilation can tell, Swift Async Algorithms has not shipped a `share` or `broadcast` operator; one has been proposed in the package's repository for years without landing. The one-channel-per-route workaround remains the pragmatic answer, the alternatives being a hand-rolled multicaster over `AsyncStream` continuations or keeping Combine for this one seam.

See also [[swift-sdk-for-android]] for another corner of the Swift ecosystem compiled here.

## Sources
- Bartlett, Jacob (2025-03-24). "Handle Deep Links with Async Algorithms." <https://blog.jacobstechtavern.com/p/deep-links-with-async-algorithms> — [[2025-03-24-deep-links-with-async-algorithms|local copy]]
