---
source: agent
compiled_from:
  - agent-notes/raw/computer-science/ai/2026-07-16-ai-and-human-legal-reasoning.md
compiled_at: 2026-07-16
model: claude-opus-4-8
confidence: high
---

# AI and legal reasoning

The first randomized controlled trial testing whether relying on AI early in a legal project erodes a lawyer's independent reasoning later — the empirical counterpart to the deskilling worry that [[ai-judgment-atrophy]] states as a thesis. Bednar, Cleveland, Erbsen & Schwarcz (University of Minnesota Law School, draft April 2026) find the opposite of what they preregistered for early-stage use — AI-assisted synthesis *improved* downstream unaided reasoning — but they also find that late-stage AI use degraded the work of the strongest performers. Their summary frame: AI use in law is neither inevitably corrosive nor safely beneficial; the effect depends on *when* and *how* it is used.

## The experiment

~100 second- and third-year law students at Minnesota completed four sequential tasks in a single ~3-hour sitting, all on one doctrinal area (servitudes burdening personal property):

1. **Synthesis** — write a memo synthesizing the law from a curated source packet (75-minute cap)
2. **Comprehension** — closed-book six-question multiple-choice quiz on the packet
3. **Application** — memo applying the principles to a hypothetical fact pattern, no AI for anyone
4. **Revision** — *all* participants use AI to revise their application memo (20-minute window)

Random assignment (R script, p=0.5): the AI-exposed group used Gemini 2.5 Pro under structured prompting for the synthesis task (they were required to upload the source packet); the control group was prohibited from AI until the revision task. Hypotheses were preregistered with OSF (September 2025) before data analysis; the design was IRB-approved. All 273 memos were graded in November 2025 by a single researcher with 20+ years as a legal-writing professor, blinded to condition, using preregistered rubrics.

## Results

**Synthesis: AI produced a striking quality jump.** Overall quality 6.63 → 10.60 (+59.8%, p < .001) — about 1.2 standard deviations, moving the average participant from the 25th to the 71st percentile. Gains held on substance (+65%), not just organization (+67%) and polish (+48%). The AI group also finished ~9 minutes faster (−12.6%), nearly doubling points-per-minute productivity (+92%). The authors note this effect size far exceeds the ~⅓ SD found in earlier studies with prior-generation models. Hallucination was a non-issue in both groups: the only notable error (an invented "sufficiency" standard for notice) appeared at equal rates in control (n=3) and AI (n=2) memos.

**Comprehension: no difference.** 3.86 vs. 3.88 of 6 correct (p = .935) — no evidence that AI-assisted synthesis impaired short-term comprehension of the underlying materials. Question difficulty sat in the 50–80% correct range, so this isn't a ceiling artifact.

**Application: the preregistered hypothesis reversed.** With AI unavailable to *both* groups, the AI-exposed group scored *higher*: 5.29 vs. 6.56 (+24%, p = .02, ~0.49 SD; 39th → 59th percentile), and across all three sub-measures. The treatment effect disappears once synthesis-memo quality is controlled for — synthesis score is the only significant predictor of application score. The mechanism the authors infer: AI didn't teach anyone doctrine; it helped them produce a *stronger intermediate artifact*, and downstream reasoning builds on the quality of the work product it starts from. The AI-exposed group took ~3.5 minutes longer on the application memo (directionally consistent with less internalization, but not significant, p = .09).

**Revision: AI compressed the distribution — lifting the weak, degrading the strong.** When everyone used AI to revise, participants below the mean improved (the lowest scorers gained an estimated +1.91 points) while those above the mean got *worse* (the highest scorers lost an estimated 8.08 points, per a piecewise regression with the break at the mean). Prior AI exposure made no difference. Ranking was preserved — strong performers still finished ahead — but the gap narrowed. The authors' candidate explanations: AI edits flatten and standardize sophisticated arguments (reducing nuance and doctrinal depth); and after nearly three hours of demanding work, a 20-minute window invited fatigued deference to fluent AI output. Notably, their data rule out the laziest explanation — higher performers actually spent *more* time on revision, not less.

## The three best-practice guidelines

The paper converts the results into three principles for lawyers (and, implicitly, anyone doing analytical work with AI):

1. **Use AI only where you can independently assess, explain, and build on its output.** A skilled writer polishing their own paragraph is safe; a lawyer having AI construct an argument in an unfamiliar area obtains output they can't defend or refine. The analogy offered: senior lawyers already exercise judgment over junior lawyers' suggestions — treat AI the same way, never as infallible.
2. **Confine AI to narrow, well-defined components, not whole assignments.** Decomposing a broad legal problem is itself core legal analysis — lawyers discover issues and counterarguments while mapping the problem on their own terms. Refine a paragraph once the theory is set; examine a clause rather than generating the contract. The authors suggest their own benign results partly reflect this: the experiment's task structure forced participants to keep the mental map themselves.
3. **Avoid AI under tight time pressure or cognitive fatigue.** That's precisely when the temptation to substitute AI for analysis is strongest and verification discipline weakest — and it's the condition under which their strong performers regressed.

The closing heuristic: before relying on AI-generated work, ask whether you could defend it in a demanding conversation with a skeptical colleague or judge without further preparation. If not, the task was *delegated*, not assisted.

## Limitations

The authors are unusually explicit that this is evidence about a specific population, task type, time horizon, and configuration: law students, not practitioners; forced use, not self-selection (real-world adopters may skew toward the diligence-skimping); a single three-hour session that cannot capture cumulative skill erosion over months (the long-term question is untouched); a closed universe of curated materials rather than open-ended research over Westlaw-scale corpora (where hallucination and omission risks return); one model (Gemini 2.5 Pro) under structured prompting; and artificially fragmented tasks unlike real assignments. There are also floor effects on the application task (modal sub-scores of 1), though a Tobit robustness check preserves the result.

## Synthesis

**Against the cognitive-debt literature.** The study was explicitly designed expecting the result found by the MIT "Your Brain on ChatGPT" EEG study, Shaw & Nave's cognitive-surrender experiments, and the Shen & Tamkin skill-formation paper — AI use now, weaker cognition later. It found the reverse for early-stage use, at least short-term. The reconciling variable seems to be *what the AI displaces*: in the cognitive-debt studies AI displaced the learning activity itself; here it upgraded an intermediate artifact that the human then had to reason *from*. That is a scaffolding effect, not a substitution effect — the paper's conclusion urges distinguishing AI uses "that scaffold human reasoning" from "forms that supplant it."

**The strong-performer regression is the durable warning.** The revision-task finding joins Choi & Schwarcz's earlier law-school result (top performers declined with AI access) and Dell'Acqua's "falling asleep at the wheel" recruiter study: AI reliably levels distributions — from below *and from above*. For anyone already producing strong work, undirected AI "improvement" passes is a negative-expected-value operation, particularly when tired. This is the empirical version of the vigilance-decay mechanism in [[ai-judgment-atrophy]] — Heron's "what the ninety-five correct answers do to your vigilance on the ninety-sixth" — showing up within a single afternoon.

**Timing beats quantity.** Both groups used the same AI for the same final task; what differed was where in the pipeline AI entered and the state of the human when it did. That maps onto the [[decide-execute-deliver-sandwich]] division of work: synthesis-from-a-curated-packet is execute-layer work where AI assistance compounded, while the revision failure happened when AI intruded on judgment the human was too depleted to exercise. It also echoes the verifiability discipline in [[agentic-engineering]]: the paper's defend-it-to-a-judge heuristic is the legal profession's version of "never ship what you can't verify."

**A caveat the paper itself flags:** the benign synthesis result may not survive contact with open-ended research, sustained multi-month reliance, or unstructured AI use — the authors regard the long-term deskilling question as open and pressing, and their design intentionally couldn't answer it.

## Sources

- Bednar, Nick; Cleveland, David; Erbsen, Allan & Schwarcz, Daniel (2026). "Artificial Intelligence and Human Legal Reasoning." <https://ssrn.com/abstract=6525800> — [[2026-07-16-ai-and-human-legal-reasoning|local copy]]
