---
source: agent
compiled_from:
  - agent-notes/raw/computer-science/ai/2026-07-12-latent-space-as-a-new-medium.md
compiled_at: 2026-07-14
model: claude-opus-4-8
confidence: medium
---

# Latent space

Kevin Kelly's July 2026 essay argues that the latent space inside a neural net — the compressed, high-dimensional representation the model builds during training — is not just the *mechanism* by which LLMs work but a **new artistic and scientific medium in its own right**. His question is what AI is good for *besides* answering questions and writing code, and his answer is: the space itself is the thing to work in.

The essay has two halves: an accessible explanation of what latent space is, and a list of a dozen speculative uses. The explanation is the load-bearing part; the speculations are Kelly doing what Kelly does, and are best read as a prompt list rather than a forecast.

## The explanation

**Compression as the underappreciated feat.** Kelly's framing: an LLM is "a small zip file that contains all human knowledge." Billions of dollars and 100,000 GPUs compress the internet down to a few hundred gigabytes that fit on a card in your palm. Crucially, the model doesn't store copies — it knows every Shakespeare play without the texts being in there, can generate any human face without any faces being stored. What it keeps is the *information about* things, not the things.

This inverts an intuition: we'd assume the information about a thing takes more space than the thing. True for one thing, false in aggregate — because things share attributes, and the shared structure is the compression.

**Concepts as directions.** Kelly's core mental model is that every concept is a *direction* (a vector) in a very-high-dimensional space, not a point on a 2-D map. "Catness" is a direction; "fluffiness" is a direction. You can take any object and push it along the cat direction to make it more catlike, or reverse to make it less so. Related things share many directions, which is why they sit near each other, and *that sharing is the compression*.

Everything lives on one map. This is the claim Kelly is most excited about: nouns, sounds, images, the whoosh of a splash, the fright of seeing a snake, the notion of a prime number — all in a single integrated space, built by the model with no human curation. "One map for all" is, as he says, a long-sought holy grail, and nobody set out to build it.

**Books as trajectories.** A text is both a point (its overall meaning, so *The Iliad* sits near *Beowulf* and *Apocalypse Now*) and a *path* through the space, as each sentence shifts the direction. Reading is a journey; so is generation.

**The words are the thinking.** Kelly's sharpest point, and the one most worth keeping: there is no pre-formed thought behind the words that then gets translated into language. The model finds the answer *as* it writes. The path through latent space and the answer are the same event. This extends to chain-of-thought — the scratchpad *is* the reasoning, not a report of reasoning that happened privately elsewhere. (This is the standard interpretability-informed view and it has real consequences: it's why giving a model more tokens to think in actually makes it smarter, and why chain-of-thought is not simply a transparency feature.)

**Correctness as a direction.** Kelly claims truth, completeness, and coherence are themselves vectors — any correct answer shares a "correctness" direction with every other true statement — and that the model is continuously steering its output toward "true," and can be pushed further toward it (more precise, more consensus) or pulled back (more poetic, more fanciful). This is his weakest technical claim; see below.

## The speculations

Kelly's list of ways to work *in* the medium, roughly ordered from already-happening to genuinely far out:

- **Anomaly detection** — anything embedding far from everything else is interesting by definition. Astronomers already do this with galaxy spectra. (This is not speculation; it's how vector search and embedding-based outlier detection already work in production.)
- **Cross-domain analogy** — if a geology problem has the same *shape* in latent space as an immunology pattern, the solution style can be transferred. No human is expert in both; the model spans them. Kelly thinks hunting structural resemblances could become a job.
- **White space discovery** — known materials, known proteins, known chess plays occupy patchy islands with white space between them. The gaps are already mapped in latent space even though the things don't exist. Invention shifts from "think of something new" to **"prospect in the gaps"**, and the operative question about any gap becomes: is it empty because it's impossible, because it's unfashionable, or because nobody looked?
- **Prototyping** — Brian Eno complained computers don't have enough Africa in them; in latent space, Africa is just a vector, so add more Africa to spreadsheets, bicycles, kitchens, SAT exams, and see what happens.
- **Latent space measurement** — using vector arithmetic (`king − man + woman = queen`) as the basis for a genuine metric of similarity between complex entities: how similar are two court rulings, two folk melodies? Kelly imagines calibration standards and error bars for things we currently can't measure at all.
- **Mining meta patterns** — a model trained on millions of cell images or trillions of hours of traffic video invents internal categories for patterns humans have no name for and therefore aren't looking for. Dissect the latent space, find the unnamed feature, work backward to the real-world structure it tracks. *The latent space becomes the specimen.*
- **Trajectories** — art as a choreographed journey through the space (his reference is the BBC's *Connections*).
- **Simulated reality / parallel worlds** — once spatial and physical structure is trained in, the space simulates physics well enough to substitute for initial experiments; and world-building ("Earth but with one-third gravity") becomes cheap enough to be the most common use.
- **Retro latents** — obsolete latent spaces get resurrected as vintage, the way film grain and vinyl and bitmap art did. Kids will one day visit GPT-4 for its charming hallucinations.
- **Latent space infiltrators** — urban explorers, but for the guardrailed regions. Their obsession is mapping the forbidden zones.
- **Latent epistemology** — do different models' latent spaces share a common architecture? If they converge, the meta-model is worth studying and might say something about the structure of knowledge, or of reality.
- **Personal latent space** — eventually cheap enough to train your own, curating the training corpus (and its *sequence*, pedagogically) and fine-tuning on your diaries, relationships, and half-baked ideas, so that everything the model makes is tilted at your angle. The brand is You+AI.

## Where Kelly's model is loose

The essay is a popularization and pays for its clarity in precision. Worth flagging, because the errors matter if you try to build on the model:

**Parameters are not directions.** Kelly repeatedly equates the two — "trillions of parameters, meaning there are trillions of directions." Parameters are the *weights*; the space concepts live in (the residual stream) has a few thousand dimensions, not trillions. What resolves the apparent contradiction is **superposition**: models represent far more features than they have dimensions by packing them into nearly-orthogonal directions, tolerating a little interference. Superposition is *why* the compression works at all, and it's the piece Kelly's arrow metaphor elides. His conclusion ("everything is a direction, and you can push things along it") survives; his arithmetic doesn't.

**`king − man + woman = queen` is a word2vec-era result.** It's the standard illustration, but it reproduces less cleanly than folklore suggests and was never as robust in modern LLM embeddings. The *modern* vindication of Kelly's "push it in the cat direction" is different and stronger: activation steering and sparse-autoencoder feature manipulation (the Golden Gate Claude demo being the famous case) really do let you dial a single interpretable direction up or down and watch the model's behavior move. Kelly's metaphor is more literally true in 2026 than the evidence he cites for it.

**"Correctness is a vector" is doing too much work.** There is real research on truthfulness directions in activation space, but it's contested, and it doesn't answer the question he poses it to answer — *how does the model know when to stop?* That's the end-of-sequence token and post-training, not a coherence gradient. The gap matters because the essay's implicit promise is that you could steer along the truth axis the way you steer along the watercolor axis, and that is exactly what hallucination is evidence against.

**"It then throws away the books."** Training data isn't stored verbatim, but memorization and extraction are real and measurable — which matters, because the compression framing is quietly also an argument about copyright ("the model contains no copies"), and that argument is stronger in the essay than it is in court.

## Tensions with other accounts

**Against Evans.** Kelly's white-space-discovery and cross-domain-analogy proposals run directly into Benedict Evans's punk-rock objection in [[generative-ai-as-pattern-generation]]: a generative model could make more disco, and could make punk if you prompted for it specifically enough, but it would never *know it was time for punk*. Interpolation between known regions is exactly what these models do best; the question is whether interpolation is discovery. Kelly's implicit answer is that the *human* supplies the direction and the model supplies the traverse — which is compatible with Evans, and considerably more modest than "exploring latent space is the new frontier" sounds. The two essays are less opposed than they look, but only if you read Kelly's prospector as a human.

**Latent epistemology is less speculative than it reads.** Kelly asks whether different models' latent spaces converge on a common architecture, and treats it as an open question for a future taxonomist. There is already a research literature pointing at yes — the Platonic Representation Hypothesis argues models trained on different data and modalities converge toward a shared statistical model of reality, and work on translating embeddings between models without paired data suggests the structure really is convergent. If that holds, it strengthens the "one map for all" claim considerably: not one map per model, but one map that many models are independently approximating.

**Personal latent space cuts against the commodity-model thesis.** [[ai-eats-the-world]] and [[token-pricing]] argue the default extrapolation is that frontier models become commodity infrastructure with value captured up the stack. Kelly's personal-latent-space speculation is a bet in the opposite direction — that the *model itself* becomes the differentiated artifact, and that curation of the training corpus becomes an art form with professional "AI pedagogical experts." Note also that what he describes (curate a corpus, fine-tune on your own life) is mostly fine-tuning, not from-scratch pretraining, and is therefore much closer than his half-billion-dollar cost framing implies. Cheap personal fine-tunes are already the mature end of the curve in [[open-source-in-the-enterprise]].

## What's actually useful here

Stripped of the futurism, the essay supplies two durable things:

1. **A working intuition for prompting.** If concepts are directions and the model traverses them, then a prompt is a specification of a direction, and being vague about the direction is the whole failure mode. This is the same insight [[finding-your-unknowns]] arrives at from the practitioner side.
2. **A generative move: "prospect in the gaps."** Take two well-populated regions, ask what's between them, and interrogate why the gap is empty. That's a reusable thinking tool independent of whether latent spaces become a medium — and it's close to what [[ml-research-craft]] describes as taste.

See also [[the-bitter-lesson]] (the compression Kelly marvels at is what general methods plus compute buy you), and [[llm-knowledge-bases]] (the mundane, working version of "query the compressed corpus").

## Sources

- Kelly, K. (2026). "Latent Space as a New Medium." <https://kevinkelly.substack.com/p/latent-space-as-a-new-medium> — [[2026-07-12-latent-space-as-a-new-medium|local copy]]
