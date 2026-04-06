---
source: agent
compiled_from:
  - agent-notes/raw/education/2023-08-01-la-zones-of-choice.md
compiled_at: 2026-04-06
model: claude-opus-4-6
confidence: high
---

# Los Angeles Zones of Choice

The Zones of Choice (ZOC) program is a public school choice initiative in the Los Angeles Unified School District (LAUSD) that provides one of the strongest pieces of evidence that **within-district public school competition improves student outcomes and reduces neighborhood-based educational inequality**.

## Program Design

Starting in 2012, LAUSD created 16 small local high school "zones" covering roughly 30–40% of the district. Within each zone, families submit rank-ordered preference lists and a centralized assignment mechanism (analogous to a Boston/immediate acceptance mechanism) allocates students. The remaining neighborhoods continue under traditional attendance-zone boundaries, creating a natural experiment.

The program grew out of the **Belmont Zone of Choice**, a community-led pilot in Pico Union (downtown LA) that ran informally from 2007–2012. After the school board recognized its success, they formalized and expanded the model district-wide.

Key design features that distinguish ZOC from other choice programs:

- **Zone-level, not district-wide:** Small choice sets prevent the "choice overload" problem observed in other settings
- **Administrator-led information sessions:** Personalized outreach helps parents acquire information about school quality
- **Demographically homogeneous zones:** Because ZOC neighborhoods are highly segregated (88% Hispanic, 85% classified as poor), families cannot easily sort on peer demographics and instead select on school effectiveness — exactly the dimension that creates productive competitive pressure

## Results

Campos and Kearns (2023) use a difference-in-differences design to estimate market-level effects, comparing ZOC students to similar non-ZOC students over time. The effects are large and grow over the program's first six years:

| Outcome | Effect Size | Context |
|---------|------------|---------|
| ELA achievement | +0.16σ by year 6 | Closes 80% of the pre-ZOC achievement gap (0.2σ) |
| 4-year college enrollment | +5 percentage points | 25% increase from baseline; driven by CSU enrollment |
| High school graduation | +7–8 percentage points | 10–12% increase from baseline mean |

Parallel pre-trends support a causal interpretation. Results hold across both matched and unmatched samples and under intent-to-treat specifications.

## The Competition Mechanism

The paper's most important contribution is demonstrating **why** choice works in this setting — through competitive pressure on schools, not primarily through better student-school matching.

**Option Value Gain (OVG)** is a statistic capturing each student's expected welfare gain from the expanded choice set. It also serves as a **competition index**: schools whose students have high OVGs face more competitive pressure because those students have attractive alternatives. The theoretical model predicts, and the data confirm, that:

1. **Improvements concentrate at the bottom.** Quantile treatment effects show the largest gains in the bottom half of the school effectiveness distribution. The worst schools improved most.
2. **Effects are larger where competition is stronger.** Schools and students with higher OVGs show larger treatment effects.
3. **School quality (value-added) drives the gains, not match quality.** A decomposition shows improvements in school effectiveness account for most of the achievement effects. Better student-school matching plays only a minor role.

## Demand Side: Parents Care About Quality

From rank-ordered preference lists, the paper estimates that a 1σ increase in school effectiveness is associated with a 0.137σ increase in school popularity — larger than the 0.116σ effect of peer quality. This finding is robust to including school type, teacher attributes, and course offerings as controls.

This matters because it closes the loop: parents choosing on quality gives schools the incentive to compete on quality. The demographic homogeneity of ZOC zones may be crucial here — when families can't sort on observable peer attributes, they sort on effectiveness instead.

## Mechanisms and Schooling Practices

ZOC schools appear to have shifted toward **no-excuses-style practices**, evidenced by increased suspension rates. Students also improved college preparedness through stronger course portfolios and higher SAT scores (conditional on taking the SAT). These findings add to evidence that disciplinary practices associated with the no-excuses model can elevate outcomes in urban settings, though the authors note students in these settings were positive about the changes.

## Implications

The ZOC evidence challenges several prior findings in the school choice literature:

- **Competition works in the public sector.** Previous cross-district studies (Hoxby 2000, 2003; Rothstein 2007) reached mixed conclusions. ZOC provides within-district evidence that competition drives improvement.
- **Parents can identify quality.** Prior work found lower-income families were less sensitive to school quality (Hastings, Kane and Staiger 2005). In ZOC, the homogeneity of the population and the manageable size of choice sets may explain why families effectively select on quality.
- **Neighborhood quality is malleable.** School quality is a key determinant of [[neighborhood-effects|neighborhood effects]] on children. ZOC shows that school-level policy can improve a major component of neighborhood quality without requiring families to move — relevant to the broader literature on neighborhoods and opportunity (Chetty, Hendren and Katz 2016).

## Sources

- Campos, C. and Kearns, C. (2023). "The Impact of Public School Choice: Evidence from Los Angeles' Zones of Choice." NBER Working Paper No. 31553. <http://www.nber.org/papers/w31553> — [[2023-08-01-la-zones-of-choice|local copy]]
