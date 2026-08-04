---
source: agent
compiled_from:
  - agent-notes/raw/computer-science/ai/2026-08-03-goedecke-llms-reward-expertise.md
compiled_at: 2026-08-03
model: claude-opus-5
confidence: medium
---

# Expertise as LLM leverage

Sean Goedecke (GitHub) argues against the widespread view that prompting is a skill-free activity — that since everyone talks to the same models, a "skilled prompter" gets the same output as a first-timer. His counter-thesis: **the most important skill in prompting is expertise in the domain you're prompting for.** LLMs make everyone a generalist, but they reward the specialist far more.

## The Tao exhibit

Goedecke's evidence is Terence Tao's public ChatGPT conversation about the counterexample to the Jacobian Conjecture. His reaction — "this is not the same ChatGPT I talk to" — is the argument in miniature: same model, same weights, radically different output quality, and Goedecke says he couldn't reach Tao's endpoint "even with unlimited tokens to burn."

Four surface behaviors he extracts from the transcript:

- **Short, gist-level replies.** Tao responds to the thrust of a response, not point-by-point.
- **Expertise signalling changes the register.** Tao's phrasing shunts the model into "talking-to-mathematicians" mode rather than "explaining-to-amateurs" mode, and the outputs get correspondingly terse.
- **Oblique pushback.** Rather than flatly contradicting a wrong-looking response, Tao says things like "this looks more complex than I was hoping for."
- **The human picks the direction.** Tao makes his own leaps and suggestions and almost never takes the model's advice about where to go next.

The load-bearing move in the essay is refusing to stop there. These tips are *not* transferable on their own: "you can't prompt like Tao on mathematical questions just by following these tips." What makes them work is actually understanding the mathematics — knowing which idea to pull out of a multi-paragraph response, being able to propose an alternate formulation, and recognizing what "looks weird." The observable behaviors are downstream of the expertise, not a substitute for it.

This is a useful corrective to the prompt-engineering-as-technique genre generally: a transcript of an expert's session is a record of judgments, and copying the phrasing without the judgments gets you the phrasing.

## The codebase version

Goedecke maps the same structure onto software, where he claims first-hand experience: with a good *theory of your codebase* you can push an LLM much harder than with no familiarity, because you have your own sense of what a good solution looks like. That sense cashes out as specific interventions — "no, I think it could be simpler here," "but don't we already do X?", "can we express this problem in these familiar terms?"

He connects this to his earlier position that system design is dominated by concrete specifics rather than generic principles, and states the preference sharply: he'd rather have familiarity with the codebase than a deep general understanding of software systems. The Tao-style questions ("does X work here?", "given Y and Z, why A?") are only askable from inside the specifics. He can't ask them about the Jacobian Conjecture; he can about the systems he owns at GitHub.

## The human as bottleneck

The essay's forward-looking claim is that domain expertise remains valuable *even as models get stronger*, because for many tasks the difficulty is not in the model's knowledge but in communicating exactly what kind of solution the human wants: "the information is 'in the model' already, but it takes a very smart human to pull it out."

Note the shape of this argument — it is a claim about the *interface*, not about model capability. It survives capability increases by construction, which is also its weakness (see below). Goedecke is careful to allow the other mode: with no domain knowledge you can still cling onto the LLM and get *something*, which he considers genuinely fine. Most people will mix both approaches, being expert in some areas and not others.

## Connections

This is the same human-is-the-bottleneck conclusion as [[finding-your-unknowns]], approached from the opposite end. Shihipar treats the bottleneck as a *process* problem and offers a toolkit (blind-spot passes, interviews, references, quizzes) for surfacing unknowns you don't have the expertise to state; Goedecke treats it as a *stock* problem — the unknowns you don't have are the ones you already know the domain well enough not to have. The two are complementary rather than competing: Shihipar's techniques are what a non-expert does to buy some of what Goedecke says the expert already owns, and Shihipar's own worked example (asking Claude to teach him color grading before asking it to color-grade) is precisely an attempt to acquire enough expertise to steer.

It also cuts against the natural reading of [[ai-judgment-atrophy]]. Heron worries that delegation erodes the judgment muscle; Goedecke's mechanism implies the erosion is self-limiting in a nasty way — as your expertise decays, so does your ability to extract good output, so the tool gets worse exactly for the people who lean on it hardest. The two together describe a loop, not a tension. The Minnesota RCT evidence in [[ai-and-legal-reasoning]] is the closest thing to a test of it: AI-assisted work improved later unaided reasoning through stronger intermediate work product, which is the loop running in the benign direction.

The register-shifting observation ("talking-to-mathematicians" vs. "explaining-to-amateurs" mode) is a concrete instance of the steering described in [[latent-space]] — signalling expertise moves the model along a direction in its representation, and the "skill" is knowing which direction you want.

Finally, if the human is the bottleneck rather than the model, that constrains the [[patron-not-wizard]] picture: commissioning work you couldn't have specified is exactly the case where Goedecke expects the output to be mediocre. It also sits under the "taste as the human bottleneck" claim in [[agentic-engineering]] and gives it a mechanism — taste here is just domain expertise applied to output selection.

## Caveats

Goedecke himself flags the strongest objection, drawn from the Hacker News discussion: this is a thesis that reassures knowledge workers they are still valuable, which is a reason for suspicion independent of whether it's true. He agrees with the suspicion, and adds that by the time anyone studies it properly the landscape will have shifted again. The essay offers one exhibit and personal experience — no measurement of whether expert-guided sessions actually outperform naive ones at matched effort.

The sharpest counter-datapoint in the discussion is that OpenAI's own mathematical prompts were reportedly inexpert, which would suggest expertise isn't required to elicit discoveries. Goedecke's response relocates rather than removes the expertise: OpenAI employs expert mathematicians who check and filter the model's suggestions, and "you cannot currently skip that step." That is a real concession — it means expertise may be needed at *verification* time rather than *prompting* time, which is a much weaker claim than the essay's headline and points at a different division of labor (cheap generation, expensive expert filtering) than the steering story he tells with Tao.

## Sources

- Goedecke, Sean (2026). "LLMs reward expertise." <https://www.seangoedecke.com/llms-reward-expertise/> — [[2026-08-03-goedecke-llms-reward-expertise|local copy]]
