---
source: agent
compiled_from:
  - agent-notes/raw/communication/2026-07-21-how-to-ask-for-help.md
  - agent-notes/raw/communication/2026-07-21-how-to-ask-for-help-hn.md
compiled_at: 2026-08-10
model: claude-fable-5
confidence: medium
---

# Asking for Help

Pradyumna Prasad's essay *How to ask for help from people who don't know you* argues that asking for help is a **learnable skill, not an innate trait** ("not an attribute you are assigned at birth like green eyes"). The whole essay reduces to **one principle: put yourself in their mind** — the same reader-centric discipline behind good writing and good speaking (cf. Winston's audience management in [[public-speaking]]). Everything else is heuristics you can reorder or drop, provided you keep modeling the recipient's perspective.

The unifying frame — mostly implicit in the essay, made explicit by the [Hacker News discussion](https://news.ycombinator.com/item?id=48761118) — is that **every heuristic is a way of reducing the recipient's cost**: the cognitive cost of understanding what you want, the effort cost of responding, and the risk cost of a bad outcome. "Put yourself in their mind" operationally means *model their cost function and lower it.*

## The four heuristics

### 1. Help is about people before projects → be worth helping

Someone helps your project only because they want to help *you*. So establish that you are worth helping, primarily by **demonstrating you are a serious person**. Anyone can *say* they want to learn ML or lift; seriousness is shown through **proof of work** — a trained model, a thoughtful blog post, a training vlog.

Prasad ranks three credibility sources from strongest to weakest:

1. **Proof of work** (strongest) — evidence you've actually done the thing.
2. **Personal connection** ("Steve suggested I reach out") — warmer, but you're *borrowing against someone else's credibility*: it backfires if they dislike Steve, or if you underdeliver and burn Steve's standing.
3. **Institutional credibility** (weakest — famous university, big employer) — at best proves you cleared a filter once, doesn't situate you to *this* person, and reads as status-signaling. Use sparingly; never as your only source.

**HN refinements on proof of work** (the discussion's richest thread):

- **Less effort, better ask beats more effort, worse ask.** `jackconsidine` sent 100 laborious handwritten notes with relatable backstory → *zero* replies; then short few-sentence emails with a clear ask → *15%* replies and better conversations. Effort spent on *your* narrative is not proof of work; effort spent making the ask legible to *them* is.
- **Unusual effort triggers suspicion.** `Aurornis` notes the handwritten notes failed twice over: hard to reply to (context-switch, transcribe the address), and *abnormal* — investing unusual attention/energy in a stranger is a known scam tell. Use normal channels with known etiquette.
- **Proof of work must go deep.** `Aurornis` again: a single blog post or a Claude-written GitHub repo doesn't cut it for someone fielding 10 requests a week; they can tell who did the work for its own sake from who staged a show. Reframed by `bbminner`: the real bar is just **"visible lack of effort is problematic"** — clear that low bar and other factors dominate.
- **Solve, don't wish.** `FinnLobsien`'s distinction: helpers respond to people who **want to solve the problem** (tried approaches, hit a specific wall) far more than to people who merely **want the problem to be solved** (doing as little as possible, hoping you'll do it). `devmor`: showing what you've already tried also hands the helper a jumping-off point and pre-empts back-and-forth.

### 2. Explain context — "so short as to be unsummarizable"

Once you've borrowed their attention, spend it judiciously — attention is "the most precious currency." Your context should be **so short it can't be compressed further**, and it should **connect to what they already know**. Don't brief your representative on your club's factionalism; explain how the club touches their legislative priorities. Don't tell a scientist you've loved science since childhood; tell them you reimplemented and extended their 2023 paper.

`lisper` sharpens this: for technical asks, **citing the person's own published work** is the single most effective attention-grabber — but `currymj` warns LLMs have made this cheap, so generic "I loved your work" is decaying toward a *negative* signal; the citation has to be real and specific.

### 3. Make the request easy to accept — lower the cost of yes

Four cost dimensions:

- **Magnitude** — ask for twenty minutes, not to read a 500-page manuscript in a week.
- **Specificity** — a concrete resource request beats "can I pick your brain?"
- **Friction** — hand them a forwardable blurb for an intro; ask in writing rather than demanding a call (cf. `nohello.net`; `freetime2`'s rule that a bare "Hello John" wastes the recipient because they can't gauge effort, urgency, or fit).
- **Boundedness** — ask for one discrete thing (read this post), not a recurring obligation (be my lifelong mentor). Land the small ask well and larger ones follow naturally.

**The specificity tension (the discussion's one real disagreement with the essay).** Prasad says "be specific," but `sokoloff` and `hyperultra` push back: an over-specific ask *raises* the risk of stepping on a landmine (the helper doesn't know the answer and won't side-quest for a stranger) and *forecloses serendipity* (the open version invites "No, but talk to X"). The resolution comes from `simon_brender`: aim specificity at **the judgment you actually need, having pre-solved the easy version yourself** — don't lock the helper into a narrow factual path they may not be able to walk.

**Pricing their time as a signal.** `mrtb`/`mtlynch`/`simon_brender` document the Jason Cohen / WPEngine tactic: offer to pay a stranger *above* their rate for a bounded one-off. Cohen messaged 40 WordPress consultants; 38 agreed to a call and none took the money. `simon_brender`'s reading — the money was never the point: **the offer proves you've costed their time before they had to, and won't waste it.** His two highest-leverage moves in cold outbound: (1) a bounded ask they can price in one read (Prasad's "unsummarizable"), and (2) evidence you already solved the easy version, leaving only the part that needs their judgment. This is the same machinery as consultative and credibility-based selling — see [[consultative-selling]] (pre-empt the buyer, give them the answer to the easy version) and [[credibility-based-selling]] (seriousness/proof of work as the substrate that makes any ask land). `gofreddygo` adds the Cialdini angle — "ask for a lot then back off," a rejection-then-retreat move from [[cialdini-influence]].

### 4. Make it easy to say no

The counterintuitive heuristic, and the one the discussion praised most. **The worst outcome is not a no — it's a pressured, begrudging yes.** Coercion (guilt, pestering) poisons the relationship for a half-hearted effort, and "a person who helps you with gritted teeth is one who will never help you again." Help freely given is effortless, like holding a door; it's also the foundation of a reciprocal relationship. If you get a no, thank them and move on (a line Prasad added by edit).

**Operational note (field-tested in cold outreach, 2026-08).** This heuristic prescribes *conduct*, not copy. The tempting misreading is to render it as a closing line that grants permission to decline — "if it's a busy stretch, no worries at all," "thanks either way." Those lines don't cheapen the no; they shrink the ask, signaling the request itself doesn't matter. The essay never prescribes such a sentence. The no is made easy structurally: the ask is bounded and specific (heuristic 3), the message carries zero guilt, and follow-up discipline (a bounded number of touches, then thank-and-move-on) covers the rest. End the message on the ask and any offered trade; the only *line* the essay prescribes is the thank-you after a no.

## The hard constraint: never lie

Every heuristic is optional except this one. All asks are attached to *you*; if the reader gets "even a whiff of something off," no ask — however small, specific, low-friction, and bounded — gets a yes. `crumby`'s example: "I've been working on your neighbor's house..." fails because everyone knows it's a lie.

## Cross-cutting lessons from the discussion

- **Calibrate before optimizing.** `shalmanese`: people misjudge how *competitive* their ask is by orders of magnitude — assuming someone is asked daily when it's once a year, or that their request is unique when it's the twelfth identical one that week. Be lightweight, dash it off, don't over-invest emotionally, and only optimize the ask once evidence shows the response rate is below expectation.
- **Following up is the neglected other half.** `Aurornis`: after someone helps, show you *tried* their advice. Asking, then ignoring or never acting, is the fastest way to end the relationship — and it's a *choice*.
- **Don't over-optimize for not irritating people.** `cj`: you built a professional network to use it; one person mildly annoyed once in a blue moon is fine — move on.
- **Pay it forward** (`jackconsidine`, `godelski`) — what's trivial for the asked is often cumbersome for the asker, purely from position. Contested by `jongjong` (reframes reciprocity as favor-trading/dependency) and defended by `sokoloff` (a fixed-pie fallacy — help is the substrate of complex society).
- **The canon** the thread keeps pointing to: Cialdini's *Influence* ([[cialdini-influence]]), Munger's psychology-of-misjudgment speech, and Eric S. Raymond's harsher *How To Ask Questions The Smart Way*.

## Sources
- Prasad, Pradyumna (2026). "How to ask for help from people who don't know you." <https://pradyuprasad.com/writings/how-to-ask-for-help/> — [[2026-07-21-how-to-ask-for-help|local copy]]
- Hacker News discussion (2026). "How to ask for help from people who don't know you (pradyuprasad.com)." <https://news.ycombinator.com/item?id=48761118> — [[2026-07-21-how-to-ask-for-help-hn|local copy]]
