---
source: agent
compiled_from:
  - agent-notes/raw/education/2026-06-22-relative-age-social-capital.md
compiled_at: 2026-06-22
model: claude-opus-4-8
confidence: high
---

# Relative Age Effects

The **relative age effect** is the long-run advantage that accrues to children who are old *for their grade* — born just after a school-entry cutoff, so they are among the oldest in their cohort rather than the youngest. Because school cohorts are bounded by an arbitrary cutoff date, two children born only days apart can land in different grades, with one perpetually ~11 months older than its classmates and the other ~11 months younger. That small, quasi-random difference in *peer composition* turns out to shape test scores, leadership, careers, and — per Jacob and Bailey (2026) — the accumulation of **social capital**.

This is a textbook case of [[cumulative-advantage]]: a tiny initial edge (being slightly more mature than your classmates) compounds through positive feedback (more friends → leadership roles → social skills → socially-intensive careers) into large long-run inequality between children who are intrinsically near-identical.

## The identification problem and how it's solved

A naive comparison of old-for-grade vs. young-for-grade children confounds three collinear effects (Cascio and Schanzenbach, 2016):
1. **Age at school entry** — how developmentally ready you are when you start.
2. **Age at outcome** — you are simply older when measured.
3. **Age relative to peers** — your standing *within* the cohort.

The standard fix is a **fuzzy regression discontinuity** around the kindergarten cutoff: compare children born just before vs. just after the cutoff date. Birth timing within a few days of an arbitrary administrative line is as-good-as-random, so the discontinuity isolates the causal effect of *assigned* relative age. It is "fuzzy" because compliance is imperfect — some parents **redshirt** (deliberately delay entry so their child is oldest), and some accelerate. Since most non-compliance is younger-assigned children delaying, intent-to-treat estimates are a *lower bound* on the true effect.

A key conceptual move (Black, Devereux and Salvanes, 2011): the **absolute** age gap between oldest and youngest is at most twelve months and shrinks mechanically as a percentage as children age. So if an effect *persists into adulthood*, it cannot be driven by absolute age — it must be the relative-age channel. This persistence test is what lets researchers attribute adult outcomes to childhood peer standing rather than to simply being older.

## The human-capital puzzle and the social-capital answer

Earlier relative-age research focused on **human capital**: relatively older students score higher on tests in early grades (Bedard and Dhuey, 2006). But this test-score advantage *fades out* by the end of high school (Hurwitz, Smith and Howell, 2015) — much of it is a mechanical "age-at-test" artifact. This creates a puzzle: if the academic edge disappears, why do relatively older individuals remain overrepresented among CEOs, politicians, and Nobel laureates decades later?

**Jacob and Bailey (2026)** argue the answer is **social capital**, not human capital. Using 33 million U.S. Facebook users in a fuzzy RD around state kindergarten cutoffs, they measure social networks directly from observed friendship graphs rather than from survey self-reports. Their findings:

- **High school friendships:** relatively older *boys* make 11% more friends (0.11 SD). For *girls* the effect is ~zero — boys appear more sensitive to environmental/contextual factors. About **74% of the extra friendships are with girls**, pointing to mixed-gender clubs (band, choir, drama) rather than just same-gender sports.
- **Leadership:** the top ventile of within-school friendships is ~15× more likely to hold a leadership role. Relatively older boys are **42% more likely to become class president** — nearly 4× the Dhuey and Lipscomb (2008) estimate (which used coarser quarter-of-birth variation) — and 117% more likely to join the National Honor Society.
- **Persistence into the mid-thirties:** relatively older men make ~1.77 more friends per year (ages 21–30), end up with 21 more friends and ~7,880 more friends-of-friends, have more cohesive networks (higher support ratio), and are 4.2% more likely to be married. They also *initiate* a smaller share of friendships, suggesting they are seen as more valuable friends rather than merely more proactive.
- **Career sorting (a Roy model):** linking Facebook job titles to O*NET, relatively older men sort into occupations demanding more **social skills** (+0.04 SD) and non-routine analytical skills, are ~10% more likely to become **entrepreneurs**, and — strikingly — **14.4% *less* likely to become prominent academic scientists**. The negative science result is the cleanest refutation of the pure human-capital story: if cognitive ability were the channel, relatively older people should be *over*represented in science, not under. Instead, social capital steers men toward relationship-intensive careers and away from solitary ones.

The mechanism connects to the broader economics-of-social-skills literature (Deming, 2017): the labor market increasingly rewards social skills, so a childhood head start in building them has growing returns.

## External validity and policy

The effect replicates in six OECD countries (Canada, Finland, Japan, Norway, Sweden, UK) where kindergarten starts at ages 5, 6, or 7 — relatively older men have 3–5% larger networks in each. That the *start age* varies but the *relative* effect persists reinforces the core claim: what matters is being older than your peers, not how old you are when school begins.

Policy implications are uncomfortable:
- **Redshirting widens inequality.** White and high-income families are far more likely to redshirt sons (Bassok and Reardon, 2013), buying them the relative-age advantage — so the practice transmits social-capital and career advantages along existing class and race lines.
- **Delaying entry for all boys** (a Reeves 2022 proposal) would *not* eliminate the effect, because any cohort still has an oldest and youngest. The relative-age gap is structural to grouping children by cutoff date.
- The more tractable lever is **directly helping younger students build social connections** — encouraging extracurricular participation and leadership opportunities — rather than reshuffling cutoffs.

## Implications worth noting

- **Measurement leap.** Earlier social-capital work on relative age used cross-sectional surveys and found inconsistent results. Observed friendship graphs from a near-census of a birth-cohort generation are a qualitatively different instrument — though they rest on the assumption that Facebook friendships proxy real-world ties (Jones et al., 2013), and on self-reported demographics (validated against a 0.91 correlation with CDC birth-date distributions).
- **Gender asymmetry is the crux.** The effect being concentrated in boys, and the extra friendships being disproportionately cross-gender, is what links the childhood mechanism to adult outcomes (marriage, male-dominated leadership fields). It also means the "fix school cutoffs" framing is really about *boys'* social development.
- **A general template.** Relative age is one clean instance of how arbitrary institutional boundaries (cutoff dates, draft-eligibility months in sports, fiscal-year lines) inject quasi-random initial conditions that then compound — the same [[cumulative-advantage]] logic that makes cultural-market winners unpredictable.

## Sources
- Jacob, Matthew, and Mike Bailey (2026). "Who Leads? Relative Age Effects on Social Capital." SSRN working paper 6844065. <https://papers.ssrn.com/sol3/papers.cfm?abstract_id=6844065> — [[2026-06-22-relative-age-social-capital|local copy]]
