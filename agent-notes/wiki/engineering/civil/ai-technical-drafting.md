---
source: agent
compiled_from:
  - agent-notes/raw/engineering/civil/2026-10-26-ai-can-draw-blueprints-now.md
compiled_at: 2026-11-02
model: claude-fable-5-1
confidence: medium
---

# AI technical drafting

Technical drawing, or drafting, is the production of scaled drawings that describe how a building, machine or other object is assembled. For architects it is the construction document set: the plans, elevations, sections, details, schedules and notes that a permit office reviews and a contractor builds from. Until 2026 generative AI had nothing to offer here. Image models could render a mood board but not a dimensioned plan, and language models produced "crude and cartoonish" linework when asked for one. This article anchors the claim, made by the architect Stephen Gallagher in a 26 October 2026 Substack essay, that the frontier models released between June and September 2026 crossed the threshold into professionally usable drafting, with Anthropic's Claude Opus 5.5 (released 22 September 2026) producing what he judges to be a permit-quality set for a simple house.

Confidence is `medium`. The source is a single practitioner's self-published experiment: one evaluator, one building, uneven human feedback across models, and "permit-quality" is the author's judgment rather than an issued permit. Gallagher is candid about all of this. What the article establishes well is the *shape* of the capability and the method the models use; what it establishes less well is how far the result generalizes beyond a simple single-family house.

## The two tests

**Test one: a construction set from scratch.** Gallagher gave 13 models the same starting folder: his own rough concept sketches for a simple house, plus a reference construction document set for a different house that he had drafted in AutoCAD years earlier (so the models could extract his drafting standards). The sketches were simple but, he says, complete enough that an experienced human drafter could produce a permit set from them. The models drew the sets directly, with no CAD software.

Results spanned the whole range:

- Claude Opus 3 (2024) refused to produce drawings at all.
- The 2025 and early-2026 models (Haiku 4.5, Opus 4.6, Opus 4.8, Fable 5, GPT-5.6 Sol) produced simple, cartoonish sets. None of the models released before September 2026 drew the floor plans without significant layout errors.
- The September 2026 cohort (Fable 5.1, Gemini 3.8 Flash, GPT-6 Astra, Grok 4.7, Opus 5.5, GPT-6.1 Sol, Gemini 4 Argon) was markedly better, with Grok 4.7 as the weak outlier ("amusingly bad" elevations).
- Only Opus 5.5 had both the spatial understanding and the drafting ability to get the house's dual-pitch roof massing right. Its first draft had errors at the rakes and eaves, which it corrected after a redline.

The important caveat, which Gallagher states up front, is that the models received unequal feedback. The worst got none, since they were not up to the task, and Opus 5.5, whose first draft was best, got the most: written comments and two rounds of redlined sets. He defends the asymmetry as realistic, since redlining a junior's draft set is how architecture offices actually work, but it means the comparison across models is not controlled. Redlining Opus 5.5 "felt surprisingly routine": its errors resembled those of a talented but inexperienced drafter, and it picked up the redlines as a person would, clipping the marked-up region, comparing it to its own drawing, writing itself notes, and revising the code.

Even the best set was not clean. The Opus 5.5 house has only one means of egress, which base International Residential Code allows but a Massachusetts amendment does not. Gallagher's sketch omitted the second egress, so the error is partly his, but a competent drafter would have caught it, and the two September OpenAI models did, adding stairs off the rear deck. His verdict is relative rather than absolute: with skilled guidance, Opus 5.5 is "arguably better than the low end of the human market right now" for single-family work, where a lot of mediocre sets get stamped.

**Test two: measured drawings in a master's style.** To isolate the craft of drafting from code knowledge and specifications, Gallagher gave Opus 5.5 a folder of plates from *Building Details*, the compilation of Frank Snyder's hand-drafted early-twentieth-century detail sheets, along with his own photographs and a disorganized stack of field sketches of a historic building he had measured years earlier. The task: draw the building's plans, elevations and details as Snyder would have composed them. This is in one respect harder than Snyder's own job, since Snyder worked from the buildings' working drawings while the model had to infer concealed assemblies from exposed surfaces. After progress deliverables and redlines, the model produced two sheets in Snyder's format. Gallagher's assessment: nowhere near Snyder's polish, with subtle construction errors an experienced architect would not make, but "better than the work produced by plenty of architecture firms," at a small fraction of the time and cost.

## How the models draw

The drawings are not raster images. They are vector linework, scalable and editable in CAD. The models produced them by writing Python that describes the geometry and prints to PDF (or could emit DXF for AutoCAD). Gallagher notes the lineage: AutoLISP has let humans generate arbitrary linework from code since the 1980s, but no human would draft a one-off building that way because typing coordinates is slower than drawing them. A model that writes code faster than it could draw inverts that calculus, so code-as-CAD becomes the natural path.

The strong models all converged on the same loop: interpret the input sketches, write code to generate linework, render test prints, inspect the prints visually for correctness, revise the code, repeat until satisfied. Opus 5.5 added its own quality tooling, including a module that detected notes and tags obscuring linework and moved them. The difference between weak and strong models, in Gallagher's reading, is mostly **scale**: the strong ones worked longer, wrote far more code (over 15,000 lines of Python for the house set), rendered many more drafts, and ran many more inspect-and-revise iterations. The Opus 5.5 house set took twelve hours and "a few hundred dollars" of compute.

The resulting codebase was semi-parametric and brittle. When Gallagher edited the variable controlling the building's length, the elevations stretched and the plan dimensions updated, but many plan elements did not move because their coordinates were hardcoded. The code solved the specific problem well and would need substantial rewriting for a different building.

## Why now, and why so suddenly

Gallagher's explanation, offered as speculation, is that drafting is a **composite skill** built from vision, spatial reasoning and coding, and a composite cannot emerge until each component is reliably above some threshold. While the components improved gradually but stayed below threshold, drafting ability was flat at zero; once they all cleared it, the composite appeared within a few model generations. This is the same shape as the threshold-crossing that practitioners in software dated to late 2025 ([[agentic-engineering]] records Karpathy and Willison both placing it around November–December 2025). Drafting lagged coding by roughly nine months, which is consistent with the composite story: coding is one of the inputs, so it had to arrive first. It also fits Sanderson's picture in [[ai-for-mathematics]] of a spiky frontier where capabilities arrive domain by domain rather than all at once.

## Four levers still unpulled

Gallagher expects rapid further improvement because none of the obvious levers has been used yet:

1. **Tooling.** A large share of Opus 5.5's twelve hours went to extracting drafting standards from the reference set and writing a "sophisticated but convoluted" CAD program from scratch. Neither needs redoing per job. A pre-built drafting library and a standards file loaded at the start would raise both speed and quality, and end users can build these without the labs. A standalone building-code check module would catch errors like the missing egress. In the vocabulary of this vault, this is [[harness-engineering]]: the model is already capable and the environment is what is missing. The render-and-inspect loop is a visual oracle in the sense of [[correctness-oracles]], and the collision-check and code-check modules are the deterministic oracles that [[loop-engineering]] argues should replace prose instructions.
2. **Pre-training.** Better base models lift drafting even if nobody targets it.
3. **Post-training on adjacent skills.** Labs are already investing in coding, which drafting rides on.
4. **Post-training on drafting itself.** Once a lab targets it directly, Gallagher expects a narrow but large jump.

## The apprenticeship problem

Gallagher raises the same training dilemma that [[vibe-coding-apprenticeship]] and [[ai-judgment-atrophy]] describe for software. Students can now "vibe draft" a studio project in hours, which teaches them architecture about as well as a ChatGPT term paper teaches literature. Some schools may respond by requiring hand drafting, the blue-book exam of architecture. The harder problem comes after graduation: he can redline Opus 5.5 competently *because* he spent years drafting by hand and in CAD, and it is not clear how a graduate who never drafted will supervise a model that does. This is [[expertise-as-llm-leverage]] in another profession: the same model yields a permit set for an experienced architect and a plausible-looking liability for a novice. Firms that carry unproductive juniors long enough to build that judgment will pay for it against competitors who do not. [[understanding-as-the-bottleneck]] names the general form: production got cheap, understanding did not.

Footnote 5 adds a counterintuitive twist. CAD and BIM began as drafting tools and crept into early design, where their rigidity is a poor fit, because it was efficient for construction documents to pick up where early design left off. If the construction documents are drafted by a model from sketches, that workflow argument disappears, and early design could return to hand drawing.

## Fees and the demand for drawings

Gallagher's economic section is the part most relevant to anyone selling to or working in architecture and engineering firms. A large fraction of an architecture firm's billings is technical drawing production. If drafting gets cheap, competition pushes fees down unless the *quantity* of drawing rises to compensate. His base case is that it will not rise much: construction documents are intermediate inputs, not final goods, and they are a small fraction of a building's development cost, which is dominated by construction itself and by commodity prices. Halving the cost of the drawing set barely moves the cost of the building, so it does not call forth many more buildings or sets. This is the inelastic case, and it stands in contrast to the road-capacity story in [[induced-demand]], where the cheapened good is itself the thing consumed.

He then gives two reasons the inelastic case could be wrong, and both are the complements move from [[prediction-machines]] (when an input gets cheap, demand shifts to whatever it complements):

- **Pricing accuracy.** Construction pricing is iterative: preliminary numbers from schematic drawings carry wide error bars, scope is adjusted, drawings are updated, and so on until a complete set supports a final price. Today nobody pays for a full set on a scope that may change. If full sets are cheap, it becomes rational to draw a complete set for every design iteration, so early pricing tightens and the scope-adjustment loop gets more efficient. Drawing becomes a tool of estimating rather than a deliverable that follows it.
- **Documentation inflation.** Owners may demand elaborate sets for small projects that currently get by with little, and more expansive sets for projects that already require them. Regulators, having seen the richer documentation, lock it in as mandatory.

Read against [[task-automation-vs-paradigm-replacement]], Gallagher's two scenarios are the two branches of that framework. If drafting is automated inside the existing workflow (architect designs, model drafts, architect redlines, firm stamps), the ATM parable applies and architects are repurposed toward design, coordination and liability. If cheap full sets change *when* and *how often* drawings get made, the workflow itself changes, which is the paradigm case. He does not pick a branch. One thing the essay leaves implicit is that the architect's seal, the legal act of taking responsibility for the set, is untouched by any of this. In the terms of [[decide-execute-deliver-sandwich]], drafting is the execute layer, and the decide (design intent, code interpretation) and deliver (stamp, permit, liability) layers are where the human fee will have to justify itself.

## Connections

- [[end-of-hand-written-code]] is the software profession's version of Gallagher's thesis, and he draws the parallel explicitly: architects are "poised to experience the shift that software engineers experienced during the past year," from producing the artifact to supervising a model that produces it. Gallagher's tone is elegiac where DHH's is euphoric, but the predicted end state is the same.
- [[generative-ai-as-pattern-generation]] gives Evans's point that error tolerance varies by domain. Construction documents have low tolerance (a missing egress is a code violation, not a stylistic choice), which is why the human redline loop remains load-bearing even when the first draft is good.
- [[traditional-architecture-preference]] documents a strong public preference for traditional, ornamented buildings and leaves open why so little of it gets built. One standing explanation is the cost of detailing. Gallagher's Snyder test, in which a model drafted ornamented historic details from photographs and field sketches, weakens that explanation at the margin. This is an inference from the two articles, not a claim either author makes.
- [[ai-skepticism]] poses deBoer's question "if everything is changing, why has nothing changed?" Gallagher's essay is a dated, concrete answer for one profession: as of spring 2026 nothing had changed in drafting, and by October 2026 something had. It is also an example of why the change is invisible from outside, since extracting the result took an expert twelve hours of guided work and the profession, he says, "seems mostly unaware."
- The model roster itself is a data point. Fable 5.1 (1 September 2026) and Fable 5 (June 2026) both appear in the test and both trail Opus 5.5 on this task, a reminder that the model a lab bills as its most capable overall is not always the strongest on a given composite skill.

## Open questions

- Does the result hold for anything more complex than a simple house? Gallagher's two subjects are a small new house and a small historic building. Commercial, institutional and multi-family work adds consultants, coordination across disciplines, and code regimes that the test did not touch.
- How much of the twelve hours was reusable? If the drafting library and standards extraction are amortized across jobs, as lever one proposes, the marginal cost of a set falls well below "a few hundred dollars," and the fee argument sharpens accordingly.
- Who redlines when the senior architects who learned by drafting have retired? Gallagher names the problem and offers no solution, and neither does the software literature this vault has collected.

## Sources

- Gallagher, Stephen (2026). "AI Can Draw Blueprints Now." *Stephen J. Gallagher* (Substack). <https://stephenjgallagher.substack.com/p/ai-can-draw-blueprints-now> — [[2026-10-26-ai-can-draw-blueprints-now|local copy]]
