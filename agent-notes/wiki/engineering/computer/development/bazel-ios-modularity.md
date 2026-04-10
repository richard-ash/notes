---
source: agent
compiled_from:
  - agent-notes/raw/engineering/computer/development/2025-10-05-slaying-the-bazelisk.md
compiled_at: 2026-04-10
model: claude-opus-4-6
confidence: medium
---

# Bazel and iOS Modular Architecture

Bazel is Google's open-source build system, originally designed for massive monorepos that span billions of lines of code across multiple languages. It treats a project as a **graph of explicit targets**: every target declares its sources and dependencies in a `BUILD.bazel` file, and the dependency graph is checked at build time. This rules out hidden or accidental coupling that ordinary build tools (including Xcode) will happily tolerate.

For iOS specifically, Bazel is rarely used at startup scale but is common at large mobile organizations (Google, Meta's Buck2 is a sibling tool, and many banks / e-commerce apps). The draw is twofold: **enforced module boundaries** and **incremental builds via content-addressable caching** — unchanged targets are never rebuilt.

This article compiles Janusz Polowczyk Kilis's walkthrough of migrating a side-project HackerNews reader ("Hacksy") to Bazel. It covers both the modular architecture pattern the migration required and the specific mechanics of making Bazel cooperate with Swift Package Manager.

## The public/private module pattern

Janusz frames the architectural problem this way: suppose you're building a new Settings screen that wants to reuse a cell from a large `LoyaltyPoints` feature module. The naive approach — depend directly on `LoyaltyPoints` — drags in that module's entire *transitive dependency graph*: all the loyalty offer view controllers, their networking, their images. Each extra dependency bloats the build and raises the risk of circular dependencies.

The solution is **dependency inversion** via paired public/private modules:

- **Public module** (`FooPublic`) — contains *only* protocols that describe what the feature exposes. No implementation, minimal dependencies.
- **Private module** (`Foo`) — contains the concrete view controllers, cells, providers. Implements the protocols from `FooPublic`.

Consumers depend only on the `FooPublic` protocols, never on `Foo`. You can swap, refactor, or entirely rewrite the private implementation without cascading changes. This is the same inversion principle behind [[stacked-pull-requests]]-friendly architectures: clean interface boundaries make changes local.

### Registration, resolution, and dependency containers

Each private module has a `ModuleConfiguration.swift` file that acts as a two-way contract with the app:

- `registerImplementations` — declares "here's what this module provides" by registering concrete types against the protocols from its public module.
- `resolveDependencies` — declares "here's what this module needs" by resolving protocols from *other* modules' public interfaces and storing them in an internal `DependencyContainer` singleton.

```swift
public final class ModuleConfiguration: ModuleConfiguring {
    public static func registerImplementations(in container: any ModuleKit.DependencyRegistering) {
        container.register(BookmarkedFragmentTableViewCellProviding.self) {
            return BookmarkedFragmentTableViewCellProvider()
        }
        // ...
    }

    public static func resolveDependencies(with resolver: any ModuleKit.DependencyResolving) {
        guard let commentsVCProvider = resolver.resolve(type: CommentsViewControllerProviding.self) else {
            assertionFailure("No Comments View Controller Provider found!")
            return
        }
        DependencyContainer.default.commentsViewControllerProviding = commentsVCProvider
    }
}
```

Consuming code then reads `DependencyContainer.default.commentsViewControllerProviding` at the call site. The pattern is heavier than constructor injection, but it scales cleanly across hundreds of modules because registration is the only place wiring lives.

## Why Bazel for a side project?

Janusz is candid: Hacksy did not need Bazel. It's a personal HackerNews reader. He did it because his first encounter with Bazel during an iOS internship had left him bewildered, and he wanted to beat the complexity the second time around. That's a useful framing — Bazel at this scale is a learning exercise, not an ROI play. At enterprise scale the calculus flips: Meta's engineering blog notes that without heavy build caching, Facebook iOS engineers "would have to spend an entire workday waiting for the app to build."

## Migration gotchas Janusz hit

### Directory structure must be "Sources/Resources" per module

Xcode is happy to scatter `.swift` files across any folder hierarchy. Bazel's `rules_apple` examples all assume a single `Sources/` directory per module (with arbitrary subfolders inside). Migrating a loosely-structured Xcode project means first restructuring every module to match, before a `BUILD.bazel` will work cleanly.

### Top-level app target needs the same shape

Adding `BUILD` and `MODULE` files to the repo root is not enough. The main app target also needs its own `Sources/` and `Resources/` directories. Without that, Bazel has no clear definition of what the top-level target is.

### SPM + Firebase + Bazel is the hard part

This is the issue Janusz spent a week on. Most documentation for adding external dependencies to Bazel iOS projects relies either on CocoaPods (being sunsetted) or the legacy `WORKSPACE` approach rather than the modern `bzlmod` system. Downloading the official Firebase release zip and adding binaries manually doesn't work cleanly either, because recent Firebase SDK changes mean `FirebaseCore` is no longer a standalone artifact in the distributed release (only `FirebaseCoreExtension`).

The working recipe is `rules_swift_package_manager` ([github.com/cgrindel/rules_swift_package_manager](https://github.com/cgrindel/rules_swift_package_manager)), which lets SPM and Bazel cooperate rather than compete:

1. Declare a `Package.swift` at the repo root listing external deps. The package `name` must match the `MODULE.bazel` module name.
2. Run `swift package resolve` to produce `Package.resolved`.
3. In `MODULE.bazel`, add `bazel_dep(name = "rules_swift_package_manager", ...)` and wire a `swift_deps` extension that reads both `Package.swift` and `Package.resolved`.
4. In `use_repo(...)`, list each Swift package alias. The naming rule: `swiftpkg_xxx` where `xxx` is the package identity, lowercased, with punctuation replaced by hyphens. So `firebase/firebase-ios-sdk` → `swiftpkg_firebase_ios_sdk`.
5. Depend on specific sub-products at each call site: `"@swiftpkg_firebase_ios_sdk//:FirebaseCore"`.
6. Run `bazel mod tidy` to finalize the `use_repo` directives.

Janusz chose to put Firebase *only* in `NetworkingKit` rather than as an app-wide dependency, matching the public/private module discipline — no reason for `CoreKit` or `HacksyUIKit` to know Firebase exists.

## Results on Hacksy

Even on a small-to-moderate codebase, the numbers are meaningful:

| Build | Xcode | Bazel | Improvement |
|---|---|---|---|
| Clean build (first run) | 160.7s | 75.9s | ~53% |
| Clean build (rerun) | 141.5s | 63.5s | ~55% |
| Incremental build | 8.3s | 4.16s | ~50% |

Janusz's headline: **Bazel cut clean build times roughly in half**. The effect compounds at monorepo scale.

## The other thing Bazel gives you: boundary enforcement

A diagnostic moment from the migration: Janusz had accidentally added a *private* module as a dependency in another module's `BUILD` file. Xcode never complained. Bazel refused to build, erroring that the module's visibility was private. This is the payoff of the explicit dependency graph — architectural mistakes that Xcode silently accepts become compile-time failures. For large teams this is the difference between clean architecture being a code-review aspiration and a build-system guarantee.

## When Bazel is worth it

Based on Janusz's experience and how Bazel is used at Google/Meta:

- **Worth it:** monorepos with dozens-to-thousands of modules; strict boundary enforcement across teams; build-cache reuse across many engineers; CI pipelines that benefit from fine-grained target invalidation.
- **Probably not worth it:** small apps, solo developers, teams happy with Xcode's implicit framework handling, or projects without the appetite to rewrite dependency management from scratch.
- **Educational:** forces you to think about dependency graphs explicitly and rewires how you conceptualize "adding a framework."

See also [[choose-boring-technology]] — Bazel is the opposite of a boring-technology choice for a side project. Janusz knows this and does it anyway for the learning, which is a legitimate reason outside of a production context.

## Sources
- Polowczyk Kilis, Janusz (2025-10-05). "'Slaying the Bazelisk' - Adventures in Modularity, Build Systems, and SPM Integration." <https://januszpxyz.github.io/software/2025/10/05/slaying-the-bazelisk-notes-on-modularity-and-build-systems.html> — [[2025-10-05-slaying-the-bazelisk|local copy]]
