---
source: agent
compiled_from:
  - agent-notes/raw/business/entrepreneurship/2026-10-22-boneyard-principle.md
compiled_at: 2026-10-22
model: claude-fable-5-1
confidence: medium
---

# The Boneyard Principle

David King and Mishti Sharma's 2022 Every essay names a pattern in consumer social: the category winner usually arrives after a "boneyard" of failed products that shared its high-level idea. Vine, Instagram video, and Mindie preceded TikTok; HotOrNot, Skout, and the Match.com app preceded Tinder; Flickr preceded Instagram and Snap. The principle has two halves. First, a graveyard of surface-similar failures is not evidence that the idea is dead, because the idea was never the unit of success. Second, what separates the winner from the boneyard is usually a set of UX details that make users **make fewer decisions** and **take fewer social risks**. The more opinionated the app is about how it should be used, the more plausible deniability it hands the user: "I'm not seeking attention, I'm just doing what the app tells me to do."

The essay is a practitioner argument, not a study, and the authors were building a consumer social app of their own at the time. Claims below are theirs unless marked as synthesis.

## Two mechanisms

**Cognitive load.** Every choice the product asks for before delivering value is a chance to lose the user, and new users cannot evaluate choices whose terms they do not yet understand (Vine's "Editor's Picks" vs "Popular Now" vs "All Posts"). The remedy is not "less friction" in the abstract but having the app make the decision: one feed instead of Home and Explore, one card instead of a search page, one prompt instead of a blank composer.

**Rejection risk.** Social products ask people to expose themselves: post a video nobody watches, follow someone who does not follow back, message a stranger who never replies. King and Sharma argue that the winners build guardrails against each of those exposures, and that the most effective guardrail is an alibi. If the app told you to do it, the act is not attention-seeking; if a trend told you to use that sound, the video is not a bid for originality.

The two mechanisms reinforce each other. An opinionated UX removes decisions *and* supplies the alibi, which is why the authors' closing advice is to become more opinionated, not less.

## TikTok out of the short-video boneyard

The essay's central comparison is Vine (2012) against TikTok/Musical.ly, with Instagram's 15-second video (2013) and Mindie (2013) as additional corpses.

- **Onboarding.** Vine required a login choice, two confirmation steps, name and phone number, location permission, and push permission before the first video. TikTok showed videos on first open with no account; account creation was reachable only by tapping the profile tab. Time to satisfaction was effectively zero.
- **Consumption.** Vine split Home (what you opted into) from Explore (what you had not found yet) and then split Explore again, plus search and hashtags. Its Find Friends flow offered four tabs (contacts, Twitter, Facebook, search), each of which was a trust or social-risk decision. TikTok collapsed explore and exploit into one full-screen feed: the only action was swipe, and the app learned taste from watch behaviour without any follow graph.
- **Signal.** The essay quotes Eugene Wei's *Seeing Like an Algorithm*: because one video fills the screen, every behaviour from the moment it starts (abandon early, loop, share) is unambiguous sentiment about that video, whereas an infinite scrolling feed cannot see where the eye rests and has to fall back on explicit likes. Synthesis: this is the same design move seen from the other side. Reducing the user to one decision at a time also produces one clean labelled example at a time, so the UX that minimizes cognitive load is also the UX that maximizes training signal. Tinder's swipe and HotOrNot's one-at-a-time rating have the same property.
- **Creation.** TikTok showed each new post to a small sample audience and widened distribution if it performed, a form of what Every elsewhere calls recursive publishing. Creators with zero followers could win, which lowers the rejection risk of posting. Licensed music (which Vine lacked and which sank Mindie in lawsuits) turned creation into riffing on existing sounds; the authors cite 40% of early Musical.ly videos originating from a creator cloning another video's soundtrack. Riffing on a trend is the alibi mechanism applied to creation.

The authors' verdict is that Vine "focused too much on its new media format and not enough on the UX innovations required to make that format successful," and that Twitter's marketing propped it up without building a consumption engine to drive creation. They generalize the point later against the claim that Locket's 2022 rise was "just TikTok virality": marketing can make a working formula visible, but it cannot substitute for an engine, "otherwise we might still be using Vine."

## Tinder out of the dating boneyard

Skout (2008) and the Match.com app (2009) ported desktop mechanics to mobile: fill out a long profile, browse hundreds of people, decide whom to contact, write, wait. The essay quotes a 2009 Guardian reviewer comparing Match to applying for a loan. HotOrNot (2000) had already introduced double opt-in a decade before Tinder, rating one person at a time and revealing only mutual likes. Tinder (2012, originally MatchBox) put that on mobile with a single decision per card: do you like these photos.

The rejection guardrails the authors itemize are specific:

1. A right swipe with no immediate match carries no information, because the other person may simply not have seen your card yet. A match is therefore an unexpected reward with slot-machine timing, while a non-match is not a rejection.
2. The messaging tab shows only matches, never a list of unanswered openers.

Synthesis: Tinder is also the example Bier uses in [[consumer-social-apps]] for the positive feedback loop that drives escape velocity (one match notifies two people). The two readings are compatible. The match mechanic is simultaneously a rejection shield for the individual and a fan-out mechanism for the network, and the second only works because the first makes people willing to swipe freely.

## Not every boneyard is worth digging

King and Sharma close with three qualifications.

- **Multiple winners.** Snap and Instagram are both "social photos" apps, but Snap's camera is one tap from launch and Instagram's is three taps deep. That difference decides what each app is for (quick disappearing messages vs browsing a beautiful feed) and therefore how its network assembles: Snap friend-oriented, Instagram audience-oriented. See [[snapchat]] for Spiegel's own account of why close ties beat more ties; the one-tap camera is the UX instantiation of that thesis.
- **Open categories.** A category with an existing winner can still host a differentiated entrant, for the same reason.
- **Dead boneyards.** Location-based social (Foursquare, Gowalla, 2009–2010) never produced a standalone winner despite many attempts; check-ins survived only as a feature inside Instagram and Snap Map. The authors do not offer a test for distinguishing a live boneyard from a dead one, which is the principle's main gap.

The essay's two open cases in 2022 were BeReal (vs FrontBack, 2013, same front-and-back camera format but no behaviour-forcing prompt) and Locket (vs the 2012 Locket, Screenpop, and Fave, all home- or lock-screen photo sharing). For BeReal the authors' one recommendation was to get *more* opinionated: harder penalties for late posts, streaks for on-time ones.

## Reading it against Bier

The essay sits in direct tension with Nikita Bier's playbook in [[consumer-social-apps]] on two points, and the tension is instructive.

- Bier says people and content beat "slick design and novel interactions," and that effort belongs on [[network-effects]] and the cold start. King and Sharma say the half-trillion-dollar difference between Vine and TikTok was UX. The reconciliation is that "UX" in the essay never means visual polish; it means decision architecture. TikTok's no-follow-graph feed is itself a cold-start solution, because consumption value no longer depends on who else the user knows. On that reading the essay is an argument about *which* UX decisions are cold-start decisions, not a counter-argument to Bier.
- Bier says long sign-up flows are fine if they raise activation, because tbh and Gas were worthless without school selection and contact import. The essay celebrates TikTok's zero-step onboarding. The general rule that covers both: ask for exactly the decisions the product needs before it can deliver value, which for a graph-dependent app is several and for a content-dependent app is none.

Two further connections. The boneyard is a trap for naive [[reference-class-forecasting]]: "short-form looping video" as a reference class had a 100% failure rate in 2014, but the class was drawn around the media format rather than the mechanism, and the mechanism (one-decision consumption, follower-free distribution) had no failures in it because nobody had tried it. And the whole thesis is a consumer-social instance of Sutherland's [[psychological-moonshots]]: the value was created by changing what the product asks of the user's mind, not by any change in the underlying technology, which was a phone camera and a video codec in every case.

Synthesis counterpoint: the direction of the winning UX move is not always toward fewer decisions. Hinge's 2016 relaunch (later marketed as "designed to be deleted") added structure back to dating, with written prompts and likes on specific parts of a profile, and grew for years in Tinder's shadow. The boneyard-exit move is more precisely "change which decisions the user makes and who bears the social risk" than "remove decisions," and Tinder's own low-stakes design created the dissatisfaction Hinge sold against.

## Temporal notes

- **BeReal** was the authors' live experiment. It was Apple's iPhone App of the Year for 2022, then lost most of its daily users through 2023, and was acquired by the French games publisher Voodoo in June 2024 for roughly €500M. The one-thing-to-do UX produced the spike; it did not hold a habit once the format's novelty wore off. This is weak evidence for the authors' "get more opinionated" prescription and stronger evidence that decision reduction is necessary but not sufficient. Bier's tests (the toilet test and recurring organic exposure on other networks) look like the more complete predictor.
- **Locket** survived as a mid-sized widget app rather than becoming a new network, roughly the outcome the authors hedged toward.
- **Short-video UX became the industry default.** Instagram Reels and YouTube Shorts adopted the full-screen single-video feed, and Meta shifted its feeds toward recommended rather than followed content from 2022. The "winner doesn't take all" clause held for companies (Instagram, Snap, and YouTube all persisted) but not for the UX pattern, which was copied everywhere. That is the expected outcome if the authors are right that the UX, not the format, was the invention.

## Sources

- King, David and Mishti Sharma (2022-04-11). "The Boneyard Principle: Why the Next Big Thing will Emerge from a Failed Idea." Every. <https://every.to/p/the-boneyard-principle> — [[2026-10-22-boneyard-principle|local copy]]
