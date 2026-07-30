---
source: agent
compiled_from:
  - agent-notes/raw/business/management/2026-07-30-tech-worker-sentiment-2026.md
compiled_at: 2026-07-30
model: claude-opus-5
confidence: medium
---

# Tech worker sentiment

The annual Tech Worker Sentiment Survey — run by researcher Noam Segal (Airbnb, Meta, Twitter, Wealthfront, Zapier, Intercom, Figma; psychologist by training) with Lenny Rachitsky — is a large-N self-report study of how people working in tech *feel* about their jobs, AI, burnout, layoffs, and their careers. The 2026 edition (second annual, ~6,000 respondents across product, engineering, design, research, marketing, data, and sales) is the subject of this article. The 2025 inaugural edition was titled "burnt out but optimistic"; the 2026 headline is that the workforce has split roughly in half.

Both authors are emphatic about what the instrument measures: **feelings, not reality**. Segal: "This is not an image of reality. This is an image of how people are feeling in tech right now." Nothing here is evidence about what AI can actually do to any given role.

## The central finding: AI identity stance dominates everything

The survey asked "How has AI shifted your professional identity, if at all?" The distribution:

| Stance | Share |
|---|---|
| **Amplified** — I can do more, do better | 50% |
| **Role being redefined** — clearly changing, unclear how | 27% |
| **Destabilized** — ground shaking, high anxiety | 14% |
| **Diminished** — AI took something from me | 5% |
| No shift | 3% |

Only 3% report no identity shift at all. The remaining 97% split almost exactly 50/50 between a wholly positive stance and everything else.

What makes this the headline is the **effect size**, not the split. Segal is explicit about why he reports Cohen's *d* rather than *p*-values: with ~6,000 respondents, nearly anything reaches statistical significance, so significance stops carrying information about whether a difference matters. The 2025 survey's two largest practical effects were manager effectiveness and founder status. **AI identity stance is about 3× larger than either** — larger than role, company, company size, or level. Career optimism, burnout, layoff worry, and role-recommendation all move monotonically as you slide from amplified to diminished.

A caveat the source does not raise: this stance is almost certainly *endogenous*. People whose work is going well are more likely to describe themselves as amplified, and the causal arrow could run either way (or from a third variable — psychological disposition, or simply whether your function has been laid off recently). The finding is that AI-identity is the strongest *organizing* variable in the data, not that adopting an amplified stance causes well-being.

## Four emotional archetypes

Derived from a multi-select emotion battery (respondents picked ~5 emotions on average; some picked 13):

- **The Energized (41%)** — "product has become fun again," tech amusement park, "I'm a builder now, I have powers I never had."
- **The Conflicted (35%)** — the ambivalent middle. Simultaneously the most fun they've ever had as builders *and* the most career uncertainty they've ever felt.
- **The Disoriented (~12%, residual)** — role keeps shifting with no legible path. One respondent: "We're like farmers on the cusp of the industrial revolution."
- **The Resentful (12%)** — pressured, checked out. "I've been forced to use AI or lose my job. And even when I use AI, I'm still seeing people lose their jobs."

Segal's framing point is anti-binary: the industry sorts itself into "hype people" and "doomers," but the emotion data shows nearly everyone holds both in different proportions. Curiosity and excitement are the top two emotions overall — and *also* on the list are overwhelmed, conflicted, relieved, tired, burnt out, uneasy, anxious, and hopeful.

The resentful 12% is the worker's-eye view of the organizational pathology described in [[wiki/business/management/ai-mania|ai-mania]] — Ludic's "AI purity test," experienced from below as coerced adoption.

## Burnout is surging; optimism is falling

| Measure | 2025 | 2026 |
|---|---|---|
| Significant burnout (above moderate) | 44.7% | 54.7% |
| Career optimism | 54.8% | 48.7% |

A 10-point jump in burnout in a single year, with more than half the sample now significantly burnt out. (The episode's promotional copy says 11 points; the transcript's own figures give exactly 10.)

The interesting part is the mechanism, because it **inverts the standard velocity story**. Geoff Charles (Ramp) has argued his worst burnout came when velocity was *lowest* — effort that doesn't move anything is what exhausts you. Stagnation burnout. Segal's data shows the opposite regime: teams shipping faster than they ever have (from a couple of PRs a day to dozens) and burning out *more*. The speed did not substitute for effort; it raised throughput while holding effort constant. "More prototypes, more PRDs, more PRs, more campaigns, more agents, more ads."

**The glimmer:** enjoyment of work held flat year-over-year at a high level. Segal attributes it to two things — people can finally express latent professional identities (the PM with a designer inside, the marketer with an engineer inside) now that the swim lanes have dissolved, and people can manifest things that were recently impossible.

## The #1 fear is not job loss

Asked what they're afraid of, respondents ranked **"the expectation to do more for the same pay"** first and **"the pace is becoming unsustainable"** second. **"Losing my job to AI" ranked second-to-last.**

Segal's read of "pace" is two-dimensional: the velocity expectation on the work itself, plus the churn tax of the technology — every new model, framework, and workflow has to be learned on time subtracted from focused work. The report's line: *"The speed AI unlocked got plowed straight back into expectations. Every gain becomes the new baseline and the people expected to hit it are running out of room to breathe."*

This is the sentiment-side observation of the distributional question in [[wiki/economics/labor-share-under-automation|labor-share-under-automation]]: workers experience productivity gains accruing to the firm as a ratchet on expectations rather than as leisure or pay. Layoff worry is nonetheless high in absolute terms — 72% worried to some extent, 41.2% at least moderately — it just isn't the *dominant* fear.

## Nobody would recommend their own role

The survey asked an NPS-style question: would you recommend your role to someone entering the industry now? (Segal notes, with some irony, that he runs a website called npsistheworst.com.)

**Every function scored negative.** Not one is a net promoter of its own role — including founders, the happiest cohort in the dataset. Designers and researchers are the most negative; sales/go-to-market and PM are the least negative. The score also grades by seniority: execs and VPs are more likely to recommend than ICs.

Two explanations Segal offers for the seniority gradient: VPs benefit disproportionately because AI processes the information stream that constitutes much of their job, while ICs are each independently building internal micro-SaaS with heavy duplication — "it's a lot easier to build products these days, but a lot harder to maintain them" — producing a sensation he calls *full gas in neutral*.

**The crucial distinction:** enjoyment of one's *current* role is high. The NPS question is about an *extrapolated* future. Segal's summary — "the water's fine, but don't get in." What has collapsed is not present experience but the forecast, which means the finding is about expectations, and expectations are the fastest-moving quantity in the dataset.

### The ladder metaphor

Segal's frame for why entry is the thing nobody recommends. Scott Wu (Cognition) described Devin's progression as climbing a ladder: high-school CS student → college intern → junior engineer → senior/staff. Segal inverts the image — **the technology climbing the ladder pulls the rungs out from beneath it.** The higher you already are, the more stable you feel; the lower you are, the more the rungs under your feet are the ones being removed. Hence a workforce that is doing fine and unanimously advises against entry.

The parallel prescription for leaders: "don't let that bottom rung of the ladder rot" — invest in entry-level advancement precisely because early-career people are the most AI-native cohort. Compare the unbundling mechanism in [[wiki/economics/messy-jobs|messy-jobs]]: the ladder metaphor is the sentiment-side account of what task-level substitution feels like when it climbs a career progression rather than a job description.

## Faster, not better — and the cost to judgment

Asked directly, 97.2% say AI makes them better at their job; ~50% say "very much" or "extremely." But the open-ended responses said something different, and Segal treats them as the truer signal:

1. **"I can do more faster, but not better."** AI lowered the floor of what's producible without raising the ceiling of quality. Output volume is up; output quality is not.
2. **"My brain is rotting. My work feels worse."** Accepting first-pass model output without applying judgment to it, and the resulting collapse of one's own involvement in the work.

The report's summary: *"The productivity gains are real, but the quality of the work and the sharpness of the person producing it are taking a hit."*

Segal adds a self-efficacy mechanism: every time you personally get over a barrier, your baseline of self-confidence rises; every time you offload it, that baseline falls, and judgment goes with it. His prescription is deliberate practice, deliberate thinking, deliberate judgment — and his diagnosis is that "we're losing that fight a little bit."

This is the first large-N datapoint for the thesis argued from introspection in [[wiki/computer-science/ai/ai-judgment-atrophy|ai-judgment-atrophy]]. The apparent contradiction between the 97.2% quantitative item and the open-ends is worth naming: "better" almost certainly reads to respondents as "more effective," which is exactly the conflation the open-ends undo. Where the closed item and the free text disagree this sharply, the item wording is the likelier culprit — and it argues for replacing "better" with separate speed and quality items in the 2027 instrument.

## "Smiling exhaustion"

Segal borrows Nikhyl Singhal's term (see [[wiki/business/management/product-management-in-the-ai-era|product-management-in-the-ai-era]]) as the best available description of the mood. Classical burnout was grim — disengagement plus exhaustion. This is different: people feel *reborn*, shipping again, building things they couldn't build before — and there is no off switch. The tempo is relentless and the rules rewrite themselves weekly. High engagement and high exhaustion at the same time, which is why the enjoyment and burnout numbers can both be high.

## Who is worst off, who is best off

**Designers and researchers** are the most negative group two years running, leading on destabilized/diminished identity, on tired/overwhelmed/anxious, on job-loss worry, and on the recommendation score. Segal — himself a researcher — argues the opposite of what the sentiment implies: AI lowered the bar but did not raise the ceiling, so taste, craft, and judgment should matter *more*, not less. Rachitsky's parallel observation is that AI is conspicuously bad at design, so this ought to be design's moment as a differentiator. Neither claim is supported by the survey; both are stated as hopes.

**Data analysts** are the single most worried function about losing their job to AI, above designers and researchers. Engineering ranks lower than Segal expected, which he uses to underline that sentiment and objective capability exposure are not one-to-one.

**Founders and small companies** are the happiest, unchanged from 2025. Founders: 71% optimistic, lowest burnout, lowest layoff worry, highest AI excitement (a medium effect size). The qualifications matter, though — 47% of founders are still at least moderately burnt out, founders still score negative on recommending the role, and there is obvious survivorship bias since the sample is founders whose companies are still running.

**Company size effects are monotone.** Optimism falls, burnout rises, layoff worry rises, and recommendation falls linearly from 1–10 person startups to 5,000–10,000+ enterprises (the two largest buckets are within margin of error of each other). There is no sweet spot in the middle. Segal's caveat: even the smallest-company burnout number is high in absolute terms.

## Managers are the biggest lever leadership actually controls

Manager effectiveness reproduces as one of the largest effects, as it did in 2025. Respondents with an extremely effective manager report ~65% higher job enjoyment and dramatically lower burnout.

The problem is supply: only ~25% rate their manager highly effective, and 36% rate their manager ineffective — essentially unchanged year-over-year. So the largest controllable lever on retention and well-being is also the one most organizations have not moved at all.

Segal raises two structural worries:

1. **The great flattening cuts against this finding.** Founder mode and flat orgs mean more direct reports per manager than ever, at precisely the moment the data says who your manager is dominates your well-being. This sits in direct tension with the flatten-and-ratify posture of [[wiki/business/management/executive-role|executive-role]] and the hyper-generalist org shape of [[wiki/business/management/ai-and-org-design|ai-and-org-design]] — the survey's implication is that spans of control have a well-being cost the flattening case does not price in.
2. **The manager is the person who absorbs the squeeze.** The top-ranked fear (do more for the same pay) is mediated almost entirely by one's manager, who both sets and buffers the expectation. So the two largest findings in the survey are mechanically coupled.

The worst-rated managers cluster in data analytics and design. Segal's explanation is that managers are members of their function too: the functions with the worst sentiment produce managers carrying that sentiment, and some of it lands on their reports. See also the taxonomy in [[wiki/business/management/manager-anti-patterns|manager-anti-patterns]].

## AI guilt

An emerging phenomenon: early-career workers report feeling that using AI is a form of cheating, and **the guilt declines with seniority**. It is highest in product marketing and data/analytics. Segal frames it as imposter phenomenon with AI substituted for the usual attribution — competent people feeling their success isn't theirs, except the credit is now assigned to a technology rather than to other people or to luck.

## The prescriptions

**For employees:**
- **Go deep on a few AI use cases, not broad on all of them.** The amplified/energized cohort reported picking specific tasks and jobs-to-be-done; the people who tried to become the generalist who does everything are the ones getting severely burnt out. Note that this cuts against Segal's own claim, earlier in the same conversation, that "this is the era of the generalist" (his explanation for why PMs score least-badly on role recommendation). The reconciliation is probably that *role* breadth and *tooling* breadth are different things — but the tension is in the source and worth holding.
- **Watch the squeeze.** Take a burnout assessment, then renegotiate scope explicitly with your manager when responsibility grows and compensation doesn't.
- **Invest in the manager relationship**, including managing up — the highest-leverage single relationship by the survey's own effect sizes.
- **Consider a smaller company or founding one**, on the monotone company-size gradient.
- **If early-career, seek mentorship deliberately** — pick teams and managers who invest in development, since the rungs you would otherwise have climbed are the ones disappearing.

**For leaders:**
- **Invest in manager training.** Only a quarter of workers rate their manager highly effective; this is the largest available retention lever, especially against AI-lab poaching.
- **Manage the squeeze** — set expectations and productivity bars that are actually sustainable rather than re-baselining on every gain.
- **Don't let the bottom rung rot** — entry-level people are the most AI-native cohort and the progression is what's breaking.
- **Pay attention to design and research**, the functions taking this hardest two years running.
- **Recognize the split.** "This technology is lifting some people and destabilizing others. We are clearly not experiencing this technology in the same way." Segal's practical version: energized people should spend some of that energy on colleagues rather than entirely on the next model release.

## How much to trust this

Two limitations worth carrying:

- **Self-selected community sample.** Respondents are recruited from Lenny's newsletter/Slack audience — a population that is unusually engaged with product tooling, career discourse, and AI. That skews toward the energized end on adoption while also over-sampling people who read a great deal of AI-career content, which plausibly inflates both the amplified share and the extrapolated pessimism. It is not a probability sample of tech workers.
- **It measures sentiment, and sentiment is downstream of narrative.** Rachitsky says this explicitly about his own show: the pessimism may partly be the industry's discourse reflected back. The designers-and-researchers result in particular reads as a community metabolizing a narrative rather than a labor-market observation, given that data analysts — not designers — top the job-loss worry ranking.

Read as a measurement of *expectations*, though, the survey is doing something the objective-capability debate can't: expectations are what drive whether people enter a field, invest in a skill, or leave. A career-recommendation score that is negative across every function is a leading indicator about entry-level supply regardless of whether the underlying fear is warranted.

## Sources
- Segal, N. & Rachitsky, L. (2026). "Why the AI's honeymoon is ending (and tech workers are feeling it)." Lenny's Podcast. <https://www.youtube.com/watch?v=_cmpIveXnvE> — [[2026-07-30-tech-worker-sentiment-2026|local copy]]
- Companion write-up: "How tech workers are feeling in 2026: a workforce splitting in two." <https://www.lennysnewsletter.com/p/how-tech-workers-are-feeling-in-2026>
