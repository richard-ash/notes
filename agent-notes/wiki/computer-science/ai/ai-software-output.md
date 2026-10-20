---
source: agent
compiled_from:
  - agent-notes/raw/computer-science/ai/2026-10-20-goedecke-ai-boom-modestly-successful-software.md
compiled_at: 2026-10-20
model: claude-fable-5-1
confidence: medium
---

# AI and the Supply of New Software

"If AI is so great, where is all the new software?" has been the standing sceptic's question about coding agents since 2025. The premise is simple: if agents multiply developer output, the world should be visibly flooded with new apps, games, plugins and tools, and it is not obviously so. This article compiles Sean Goedecke's 16 October 2026 answer, "AI is driving a boom in modestly successful software projects," together with the research write-up behind it (the `sgoedecke/where-is-the-software` repository on GitHub, read on the ingest date), and situates it against the three posts that posed the question. Goedecke is an engineer at GitHub (see also [[expertise-as-llm-leverage]]), which matters both because he sees agent-generated code volume first-hand and because the method he chose deliberately looks away from it.

His three-line answer:

- Between 2× and 20× more new software is being created, depending on the registry.
- There is no growth in *massively* successful new software, once AI tooling itself is excluded.
- There is roughly 2× growth in *modestly* successful new software: tools that a few hundred or a few thousand people install.

Confidence is `medium`: the data is one author's, collected mostly by AI research agents with spot-checks, the author's own stated error bar on individual numbers is ±20–30%, and the interpretive sections are explicitly speculation.

## The question and its lineage

Three earlier posts frame what Goedecke is answering.

**Mike Judge, "Where's the shovelware?" (Substack, 3 September 2025).** The sharpest statement of the sceptical case. Judge pulled aggregate supply series (Statista's App Store and Google Play release counts, Verisign domain registrations, SteamDB releases, GitHub activity via GH Archive on BigQuery) and found them flat: no hockey stick after 2022–23. He paired this with a six-week coin-flip self-experiment modelled on METR's study (developers believed AI made them 20% faster while measuring 19% slower) and found a median 21% slowdown, not statistically significant. His conclusion was that the productivity claims driving layoffs and salary pressure were unsupported and that self-described 10×-ers should "show receipts."

**Gallagher and Dimmendaal, "So where are all the AI apps?" (Answer.AI, 12 March 2026).** A PyPI cohort study: packages born after ChatGPT update more often (about 13 releases in year one versus about 6 for 2014-born packages), but the effect is concentrated in packages *about* AI (21–26 median releases a year for popular AI packages versus about 10 for popular non-AI ones). Their reading was that the measurable effect of generative AI on PyPI was not a Cambrian explosion but a burst of activity inside the AI ecosystem itself. An update note on the post records new package creation in March 2026 at over 25,000, nearly double March 2025, the first supply inflection in this literature.

**Nate Meyvis, "Where is all the new good software?" (12 October 2026).** Not data but a list of nine candidate explanations: quality gains instead of new products; more features in existing products; gains confined to the few who adopt new software; business and approval processes as the unchanged bottleneck; ephemeral chatbot use replacing durable products; private and internal software displacing public products; teams building more rather than improving; gains taken as leisure; and AI occasionally reducing software use by showing a project is not worth doing.

Goedecke's post, four days after Meyvis, is in effect an empirical pass over that list, and the research write-up scores several of the hypotheses explicitly (below).

## Method: count successes, not output

The design choice that distinguishes Goedecke's work from Judge's is to measure *usage* rather than *supply*, on platforms where usage is public. Around twenty registries that expose install, download, review or active-user counts were sampled: NVDA screen-reader add-ons, Home Assistant's HACS store, Obsidian plugins, Firefox and Chrome extensions, Steam, Modrinth and Nexus game mods, Blender extensions, Flathub, Raycast, Google Play, Decky Loader, WordPress plugins, the Atlassian Marketplace, CRAN and OctoPrint. Items were cohorted by listing date, and each cohort was counted against a low, a modest and a high usage bar. The baseline window is 2022–24; the comparison window is the second half of 2025 through 2026, on the write-up's timeline that Claude Code arrived in early-to-mid 2025, agentic coding went mainstream in the second half, Opus 4.5 shipped in November 2025 and Opus 5 in July 2026. Where the platform allowed it, cohorts were compared at equal age (first 60, 90 or 180 days), since a current-total metric flatters older projects.

Two reasons are given for looking at add-ons, mods and plugins specifically. First, usage is observable; GitHub's own view of agent-generated code volume says nothing about whether any of it is used. Second, it filters out software *about* AI. New hits in 2025–26 are overwhelmingly AI tooling (Homebrew's ≥1k-install formulae, Obsidian's ≥30k-download plugins), and Goedecke's position is that counting shovels tells you nothing about whether AI is producing software that solves ordinary problems. A gamer wanting multiplayer Halo CE in the browser or rollback netcode for Super Smash Bros. Brawl is the clean test case: nobody there is trying to change the world with AI.

The research itself was agent-driven, and the write-up is candid that several agent findings were overturned on checking: a Steam big-hit estimate overstated by about 35%, a Homebrew "above trend" that turned out to be packaging work, a missed Obsidian policy change, a misattributed +30% figure. That is worth holding alongside [[ai-code-review]] and [[correctness-oracles]]: agent-collected data about agent-produced software, spot-checked by one person, is the methodological floor here, not a footnote.

## Findings

**Supply grew a lot.** Show HN posts +91%; F-Droid admissions about 3× and new-app merge requests about 12×; Chrome extensions 6× (12.7k to 76.8k new listings, 2024H1 to 2026H1); Firefox add-ons 4.8×; NVDA add-ons from about 6 to about 27 a month; HACS integrations about 6×; Obsidian plugins about 20× after it ended manual review on 15 May 2026; Steam games 2.6× since 2021; monthly new iOS apps roughly 2.7× year on year to September 2026. Topic-level repository counts are the most striking: NVDA-related repositories 56 to 632, amateur-radio repositories 103 to 592, game-recompilation repositories from 41 to 617 a month. Google Play merely recovered to 2022 levels after a policy-induced dip, and OctoPrint is declining.

**Big hits did not.** Show HN posts at ≥100 points were up 4% against +91% for all posts. Steam games reaching ≥1k reviews in their first 90 days rose from 207 per half-year (2024) to 251 (2026H1), +20% against about 10% audience growth, with the ≥2k and ≥5k bars flat; an independent Zukowski series has ≥1k-review games at 88 in Q1 2024 and 96 in Q1 2026 while games with ≤50 reviews rose 48%. NVDA ≥10k downloads and HACS ≥1k installs were flat. Firefox ≥10k daily users fell from about 17 per half-year to 4–9; Chrome ≥100k users from 97 (2024H1) to 39 (2026H1 so far, age-confounded); WordPress ≥10k, Atlassian ≥1k and Nexus ≥10k all down. The new big hits that do exist are AI tooling.

**Modest successes roughly doubled, on about half the platforms.**

| Platform | Modest bar | Before → after | Verdict |
|---|---|---|---|
| NVDA add-ons | ≥1k downloads in 180 days | 18–34 per half-year → 78 (2026H1) | growth |
| HACS | ≈≥100 installs, scaled for user-base growth | ≈19 → ≈45 per quarter | growth |
| Obsidian | ≥3k downloads in 60 days (≈1k pre-growth) | 4–14 per quarter → 102 (2026Q2) | growth, confounded by end of review |
| Firefox | ≥10 / ≥100 daily users | 2.5× / 1.7× | growth |
| Chrome | ≥100 / ≥1k users | 2× / level with 2024H1 at a quarter of the age | likely growth |
| Steam | ≥100 reviews in 90 days | about +60% vs 2024H1; hit rate flat at ~12% | growth in proportion to supply |
| Modrinth | ≥1k lifetime downloads | 6.9k (2024) → 9.3k (2026 Jan–Sep); hit rate 53% → 30% | weak growth (+13% excluding AI-disclosed mods) |
| Nexus code mods | ≥100 downloads | +23% | weak growth |
| Blender | ≥1k downloads | 151–194 → 196 (2026H1) | weak growth |
| Flathub | ≥1k installs in 90 days | +50%, flat after normalising for platform growth | no |
| Raycast | ≥100 downloads | 222 → 197 per half-year (−11%, snapshot) | inconclusive |
| Google Play | ≥5k downloads at 23 weeks | tracks supply | no surge |
| WordPress | ≥100 active installs | flat at ~380 per half-year | no |
| Atlassian Marketplace | ≥100 installs | ~70 → ~30 per half-year | no |
| CRAN | ≥2k downloads, equal age | down | no |
| Decky Loader, OctoPrint | various | down | no |

The write-up's reading of the split: growth appears where the builders are also the users, the audience is consumers or hobbyists, and listing is cheap; it is absent in B2B and saturated markets (WordPress, Atlassian), academic niches (CRAN), shrinking platforms (OctoPrint) and heavily reviewed registries.

## Two things the headline hides

**The denominator.** A 2× rise in modest successes against a 4–20× rise in supply means the *hit rate* fell almost everywhere; Modrinth's went from 53% to 30%, and the write-up says Steam is the only platform where it held. Judge's "shovelware" framing and Goedecke's "boom" are therefore both consistent with the data. Judge's series ended in mid-2025, before the inflection on Goedecke's own timeline, and covered aggregate stores (app stores, domains) where Goedecke also finds no usage pattern; and most of the new supply is indeed shovelware in the sense that nobody installs it. What Goedecke adds is that the absolute number of things a few hundred people want roughly doubled anyway. The right mental model is not "AI makes everyone ship a hit" but "AI lets many more people attempt, at a lower per-attempt success rate, with a larger absolute yield." That is the same shape as the [[solopreneur-economy]] data from Stripe (more solo businesses forming, faster to revenue, with AI filling capability gaps) seen from the software side.

**The gate.** Supply is being throttled by human review wherever review exists. F-Droid merge requests grew about 12× while admissions grew about 3×; Flathub submissions went from 340–490 per half-year to 1,211 while listings rose 30%; HACS has roughly a 2,000-PR open backlog; the Blender approval queue grew from about 725 (April 2025) to about 2,170 (October 2026); Decky Loader merged 23 of 68 addition PRs in 2026H1 and none so far in 2026H2; Apple reviewed 9.10M submissions in 2025 against 7.77M in 2024 and rejected 371k as copycat or spam; Obsidian's ~20× came from abolishing review. The same thing shows up inside companies: in large open-source repositories (VS Code, Sentry, Supabase, Kibana, Grafana) merged PRs rose 1.4–2× but PRs per author only 10–40%, Faros reports +98% PRs with +91% review time, and LinearB reports AI-authored PRs waiting 4.6× longer. The binding constraint has moved from writing to reviewing, which is the thesis of [[ai-code-review]] and the "verification labour, not token price" point in [[minimum-viable-saleable-software]], now visible in registry queues.

## Why small, and why not big

Goedecke's explanation for the absence of growth at the top is labelled speculation. Large successful products have the visible features their users want (what would a new macOS or Gmail feature even be?), are technically paralysed by the features they already have, and ship improvements that are deliberately invisible: enterprise compatibility, internal reliability. For hobbyist projects he offers two candidates: a really good product idea is hard to have and AI does not help with that, which is the idea-side version of his own [[expertise-as-llm-leverage]] argument; or hits take years to compound and the current crop of thousand-user tools has not had time to become hundred-thousand-user tools. The write-up's own recommendation is to re-run the counts in Q2 2027.

The write-up also scores Meyvis's hypotheses. "Fewer bugs" is contradicted: Mozilla bugs filed +40%, regressions +37%, high-or-critical security bugs about 5×; CVEs 39,962 (2024) to 48,185 (2025); WebAIM's accessibility-error slope steepened 1.7× and the WCAG failure rate turned from improving to worsening; status-page incident rates are flat for non-AI services and 2–7× worse for AI-traffic-hit ones. "More features in existing products" is weak (AWS What's New posts flat at about 2,350 a year; the share of pre-2018 Steam games still receiving patches fell from 25.7% to 18.9%). "Adoption problem" is partly supported, "non-coding bottlenecks" supported, "more software not better software" strongly supported, and "gains taken as leisure" untested but consistent. FRED software investment is running +11–14% a year with no trend break, which is the macro-level version of the same picture that Moll and Imas model in [[ai-explosive-growth]]: a capabilities explosion that does not show up as an output explosion on the timescale people expected.

## The disclosure problem

Goedecke argues that voluntary AI-disclosure data is unusable for this question. Hobbyist communities dogpile admitted AI use, so the tag suppresses itself; Steam's AI-disclosure requirement (January 2024) and Modrinth's tag are both confounded that way, and the Modrinth +13%-excluding-disclosed figure should be read as a floor on AI's contribution rather than an estimate of it. His inference is therefore indirect: a 2× in successes against a 10× in attempts, exactly in the window when agentic coding went mainstream, is "clearly *something* to do with AI" even though no individual project can be attributed. This matches the pattern in [[ai-decompilation]], where the flagship projects' own READMEs say "with the help of" AI while the surrounding discourse says "automatically, by an AI," and the write-up's game numbers put a quantity on that wave: decomp.dev projects 38 to 145, DSOGaming unofficial-port articles from 0–2 to 21–22 a month, while official port headlines on Gematsu *fell* from 420 (2021) to 304 (2026 to September). The unofficial recompilation scene is where the AI-era port supply went, not the studios.

## Connections

- [[software-industry-barbell]]: Vernal predicted a "non-venture-addressable explosion of Substack-shaped small software" at the light end of the barbell. This is the first attempt to measure that end, and it finds the explosion in exactly the registries where a thousand users is a success and no investor is involved.
- [[institutionalized-vs-improvised-software]]: Evans's point that most people are not tool-builders and that the hard part is knowing what to build predicts Goedecke's "growth where builders are users" pattern. NVDA, HACS and Obsidian are communities of people building for themselves; WordPress and Atlassian are markets where someone else is the user.
- [[end-of-hand-written-code]]: DHH's 150k lines in a month is the production-side extreme; this article is the demand side, and the two together say that the ratio of written to used code is rising fast.
- [[ai-skepticism]]: deBoer's first question, "if everything is changing, why has nothing changed?", is the sceptic's version of the same puzzle. Goedecke's counts are the closest thing to a direct answer, and it is a modest one: something has changed, in the long tail of registries, at a few hundred users per project, and nothing has changed where deBoer is looking.
- [[ai-and-the-future-of-work]] and [[task-automation-vs-paradigm-replacement]]: the data so far is task automation inside existing paradigms (more plugins for existing hosts), not new paradigms, which is the condition under which those articles expect little visible displacement.

## Open questions

- Whether the Q2 2027 re-count shows the 2025–26 cohort of thousand-user tools climbing into the ≥10k bars, which would settle Goedecke's "it takes years" hypothesis against "ideas are the bottleneck."
- Whether gatekept registries clear their queues (by hiring, by automation, or by abolishing review as Obsidian did) and what happens to quality when they do.
- Whether the reliability deterioration (Mozilla, CVEs, WebAIM) is caused by AI-generated code, by AI-driven traffic, or by neither, since the write-up measures correlation only.
- Whether per-platform hit rates keep falling, which would mean the registries' discovery mechanisms, not the models, become the limiting factor on useful software reaching users.

## Sources

- Goedecke, Sean (2026-10-16). "AI is driving a boom in modestly successful software projects." <https://www.seangoedecke.com/ai-is-driving-a-boom-in-modestly-successful-software/> — [[2026-10-20-goedecke-ai-boom-modestly-successful-software|local copy]]. Publication date taken from the live page on the ingest date.
- Supplementary, read on the ingest date and not held as raw files: Goedecke's research write-up, <https://github.com/sgoedecke/where-is-the-software/blob/main/WRITEUP.md> (source of all per-platform figures and hypothesis verdicts above); Judge, Mike (2025-09-03). "Where's the shovelware? Why AI coding claims don't add up." <https://mikelovesrobots.substack.com/p/wheres-the-shovelware-why-ai-coding>; Gallagher, Alexis and Dimmendaal, Rens (2026-03-12). "So where are all the AI apps?" <https://www.answer.ai/posts/2026-03-12-so-where-are-all-the-ai-apps.html>; Meyvis, Nate (2026-10-12). "Where is all the new good software?" <https://www.natemeyvis.com/where-is-all-the-new-good-software/>.
