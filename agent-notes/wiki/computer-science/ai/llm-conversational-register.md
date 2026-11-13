---
source: agent
compiled_from:
  - agent-notes/raw/computer-science/ai/2026-11-12-natashatherobot-language-models-bad-at-language.md
compiled_at: 2026-11-12
model: claude-fable-5-2
confidence: medium
---

# LLM conversational register

The **conversational register problem** is the observation that language models, strong at code and math, are weak at one plain task: producing a sentence an ordinary person would say out loud. The anchor source is NatashaTheRobot's November 2026 post *Language Models are bad at Language*, a field report from building a Hindi-learning app. It is one developer's account with five examples and no measurements yet, so read it as a well-described symptom, not a finding.

## The use case that exposes it

Natasha is explicit that she is not asking a model to write for her. "Writing is thinking," she writes her own posts, and would keep doing so even if nobody read them. Her need is **language as product content**: real-world Hindi words and sentences for a learner, in place of what she calls the "stock Duolingo textbook" ones.

This is a different failure surface from the one in [[writing-with-llms]]. There the model's prose is too polished, "wedged in a mode where everything they write is a magazine headline," and the defense is to keep its words out of your draft. Here nobody's voice is at stake. The output is the deliverable, there are thousands of sentences, and each has to pass a native speaker's ear with no human rewriting it. A copyeditor-not-ghostwriter rule does not help when the job is ghostwriting at scale.

## Two layers of the same problem

**Hindi comes out formal.** Her Hindi-speaking friends call the output "academic formal Hindi," and she reports none of them rated any model's Hindi as sounding normal. Her explanation is the training data: models learn from "texts and news-type articles and official sources, which are written differently than a casual conversation would go."

**English comes out odd too.** Her workaround was to generate casual English first and translate. It failed at step one. She tried "Haiku, Gemini Flash, OpenAI, on different settings, different prompts," and gives five outputs with her objections:

| Model output | Her objection |
|---|---|
| "Your cloth bag is so full, do you carry vegetables home every day?" | No real person says this |
| "That bunch of yellow bananas hanging there would make the perfect quick breakfast tomorrow." | Awkward structure |
| "I wish I could read the newspaper as calmly as the man in the blue shirt on that stool." | Too specific and detailed |
| "Is your bicycle ready to take you on another ride after this tea?" | The bicycle is ready when the rider is |
| "Back home, I never see a bicycle with this much character." | A bicycle does not have character |

Her summary: "On the surface, all these sentences read ok. But look closer and think through it and they're essentially non-sensical." A human can fix each one in seconds. The complaint is that the model cannot be relied on for even one.

## What the examples have in common

The post does not analyze its own examples. Reading them together (this is the compiler's reading, not Natasha's):

- **Every sentence is grammatical.** The failure is pragmatic. Each one breaks an unwritten rule about what people bother to say: nobody narrates what both speakers can already see, nobody stacks three descriptors on a stranger, nobody asks a bicycle whether it is ready.
- **Speech is underspecified; these are overspecified.** "The man in the blue shirt on that stool" is how a caption or a novel points at someone. In conversation it is "that guy." The models write description where talk was asked for.
- **Each sentence tries to be interesting.** "Perfect quick breakfast," "this much character," "as calmly as." Ordinary talk is mostly dull on purpose. This is the same pull toward the pleasing phrase that Ptacek names in [[writing-with-llms]], showing up in a task where the pleasing phrase is the defect.
- **The sentences look scene-bound.** Cloth bag, bananas, a man on a stool, a bicycle, tea: they read like lines written to accompany a market-street picture. If the prompt asked for sentences about a scene, the prompt itself invites narration of visible detail. The post does not show its prompts, so this stays a guess, but it is the first thing to rule out.

The Hindi layer fits the same shape. Spoken Hindi is full of Urdu-derived and English words and drops much that the written standard keeps. That register is thinly written down, so a model trained on the written record learns the newsreader's Hindi and has little of the street's. Natasha's translate-from-English plan could not have escaped this even if the English had been good: translation carries the meaning across and then picks the target register from the same formal prior.

## Her causal claims, weighed

- **Training-data skew** toward written and official text. Plausible, standard, and enough to explain the Hindi result on its own.
- **Regression.** She opens with "the em dash and 'delve' version of ChatGPT was as good as it was going to get," and plans to try older and open-source models "that might not be as nerfed on English." She gives no before-and-after comparison, so this is an impression. Her own planned test would settle it.
- **Deliberate fingerprinting.** She writes that "Anthropic already said they'll be 'fingerprinting' their models," that this means the output "will not be the 'logical' one," and that it explains why the text "reads like a confused first grader wrote it." The post cites nothing for the announcement and this compile did not confirm one. The mechanism also does not fit: published text watermarks (Google's SynthID-Text is the documented one) nudge the choice among near-equally-likely tokens so the mark is statistical and invisible to a reader. A watermark you could hear as awkwardness would be a failed watermark. And the oddness appears across three labs' models in her own test, which a single lab's policy cannot explain.
- **Detection.** She asks why X cannot use AI to catch bot replies that every human spots, and guesses that models are bad at recognizing normal language as well as producing it. That is a guess about a platform's incentives as much as about models; the post offers no evidence either way.

One confound she does not flag: she calls the models tested "frontier," but Haiku and Gemini Flash are their labs' small, cheap tiers. A small model is the sensible choice for bulk generation, and it is also the one most likely to be stiff. The claim "models cannot do this" is really "the models I could afford to run at volume did not do this with my prompts."

## The method is the durable part

The most useful move in the post is the last one. Having found no model that works out of the box, she declares herself "a RESEARCHER FIRST":

1. Generate rounds of English sentences across model and prompt combinations and find which combination works.
2. Hand-pick good English sentences, have several model and prompt combinations render them in Hindi.
3. Send the Hindi to native speakers to rate each line as normal or not, through a survey she admits is "long and tedious."

This is an eval built the only way this property can be evaluated. Naturalness has no compiler and no unit test; the instrument is a native ear. It is the same reason [[writing-with-llms]] gives for why prose rules must be stricter than code rules, and it is [[expertise-as-llm-leverage]] with a twist: she is the learner, so she cannot judge the Hindi herself and has to borrow the expertise. An app builder who can read the target language has a large advantage here that no prompt replaces.

It also suggests the fix she has not tried yet. If the model's prior is written text, the lever is to move it off that prior with examples of the real thing: transcribed speech, subtitles, chat logs, a few dozen native-approved lines as few-shot anchors, and a second pass that only asks "would someone say this?" Asking for "casual" in the instruction changes the adjectives and leaves the prior where it was.

## Where it sits

- **Jagged capability.** The piece is a clean instance of the jaggedness described in [[agentic-engineering]]: superhuman in verifiable domains, unreliable in one a child handles. Verifiability is the dividing line. Code and math give a training signal that says right or wrong; "sounds normal" gives none that scales.
- **Benchmarks.** Her closing caution, "not blindly trust it, no matter how much labs hype it up on their benchmarks," is the everyday-use version of the argument in [[ai-skepticism]]. Nobody publishes a leaderboard for sounding like a person at a vegetable stall.
- **Error tolerance by domain.** [[generative-ai-as-pattern-generation]] sorts uses by how much error the domain forgives. Language-learning content forgives almost none: a learner cannot tell a stilted sentence from a normal one and will memorize it, which is exactly why they are using the app.
- **Why readers care.** The reaction her friends had to the Hindi is the one [[ai-art-contamination]] measures for art: once a line registers as machine-made, the whole product is discounted, not just the line.

Her parting joke is that "English majors might be the most sought-out and highest-paid professionals in the future." The serious version is narrower and already true in her own project: the scarce input is a person who can say whether a sentence is normal, and the build is blocked until enough of them fill in a tedious survey.

## Sources
- NatashaTheRobot (2026). "Language Models are bad at Language 🤔." <https://www.natashatherobot.com/p/language-models-are-bad-at-language> — [[2026-11-12-natashatherobot-language-models-bad-at-language|local copy]]
