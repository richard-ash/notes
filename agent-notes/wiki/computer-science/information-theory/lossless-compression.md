---
source: agent
compiled_from:
  - agent-notes/raw/computer-science/information-theory/2026-09-08-compression-is-prediction.md
compiled_at: 2026-09-08
model: claude-fable-5-1
confidence: high
---

# Lossless Compression and Prediction

Lossless compression and next-token prediction are the same problem seen from two sides. A compressor assigns short bit-strings to likely symbols and long ones to unlikely symbols, and to do that it needs a *model* that says how likely each symbol is given what came before. A language model's entire job is to produce that probability distribution. Annie Sexton's August 2026 explainer on the ngrok blog builds the equivalence up from run-length encoding to GPT-2; this article follows her structure, fills in the surrounding theory, and adds the practical reasons the equivalence stays mostly theoretical.

## Redundancy, not minification

Sexton opens by separating two things that both make files smaller. **Minification** strips what a machine does not need — comments, whitespace, long variable names — and takes a JavaScript function from 156 to 62 characters. It is never discussed as compression because it works by *discarding* content. **Compression** proper exploits **redundancy**: it re-encodes the same information more tightly and can reverse the process exactly.

The simplest example is **run-length encoding**. The 28-character string `AAAAAAAAABBBBCCDAAADDDDDDDDD` becomes `A9B4C2D1A3D9`: 224 bits of 8-bit ASCII down to 96. (The Web Clipper dropped the inline example strings from the raw capture. The ones in this article were reconstructed from Sexton's run-lengths and probability tables, and the arithmetic-coding examples were confirmed by decoding her final numbers against her tables.)

## The anatomy of a compressor

Sexton describes modern compressors (gzip, Brotli, zstd) as having three "organs," rarely used in isolation:

1. **Transforms** — preprocessing that makes data easier to compress. Run-length encoding is one; so is the LZ77 back-referencing of repeated substrings that gzip does. Transforms do not always shrink data; sometimes they *increase* redundancy so a later stage can exploit it (the Burrows–Wheeler transform in bzip2 is the classic case).
2. **Model** — a description of the data's shape: at minimum a table mapping each **symbol** (letter, byte, token) to a **probability**. This is where all the intelligence lives.
3. **Entropy coder** — the final stage that turns symbols plus probabilities into a raw bitstream. Entropy coders are fixed, deterministic, and lossless; there is nothing to tune in them. To compress better, improve the model.

The interface between stages 2 and 3 is the whole story: **probabilities go in, bits come out.**

## Entropy coders: turning probabilities into bits

### Arithmetic coding

Arithmetic coding represents an entire message as a **single number** in [0, 1). Start with the unit interval divided into sub-intervals proportional to each symbol's probability. For each symbol in the message, narrow the current interval to that symbol's sub-interval, then subdivide the new interval by the same proportions. After the last symbol you are left with a tiny interval; emit the number inside it that has the fewest binary digits.

Sexton's worked example is the string `ABABAAC` (A = 4/7, B = 2/7, C = 1/7). It ends in the interval [0.38730, 0.38855), and the shortest binary fraction inside is 0.3876953125 = 397/1024 — ten bits, against 56 bits of ASCII. The number is not a float. It is a **binary fraction** of exactly the length needed, not a 32- or 64-bit slot.

Decoding replays the process: given the same probabilities, the decoder checks which sub-interval the number falls in, records that symbol, narrows to that sub-interval, and repeats. The decoder must therefore have *exactly* the same model as the encoder — a constraint that matters enormously once the model is a neural network.

A skewed distribution compresses better. Her second string, `AAAAAAAAAABC` (A = 10/12), is twelve symbols long yet also fits in about ten bits:

| | `ABABAAC` | `AAAAAAAAAABC` |
|---|---|---|
| Length | 7 symbols | 12 symbols |
| Raw ASCII | 56 bits | 96 bits |
| Compressed | ~10 bits | ~10 bits |
| Bits / symbol | 1.38 | 0.82 |

### Huffman coding

Huffman coding assigns each symbol a **codeword** — a variable-length bit string — instead of encoding the message as one number. Sexton derives it from a guessing game: "I saw an animal downtown, it was a ___" with bird (1/2), squirrel (1/4), cat (1/8), fox (1/16), bear (1/16). Guessing in order of probability is a yes/no decision tree, and writing each path as 1s and 0s gives bird = `1`, squirrel = `01`, cat = `001`, fox = `0001`, bear = `0000`. Common symbols get short codewords, rare ones long; the number of guesses is the number of bits.

Huffman is what gzip and Brotli use, and it is optimal *among codes that spend a whole number of bits per symbol*. That is its limitation: if cat's probability were 0.3973 rather than 0.125, the ideal code length is 1.33 bits, and rounding up to a whole bit wastes some. Arithmetic coding does not round per symbol, which is why it gets within a couple of bits of the theoretical limit on a whole message. Its modern descendant, **asymmetric numeral systems**, is what zstd uses, because it delivers arithmetic-coding ratios at Huffman speed.

## Entropy is the floor — relative to a model

The ideal code length of a symbol with probability *p* is **−log₂ p bits**. Plugging in the animal probabilities reproduces the tree exactly: 1, 2, 3, 4, 4. The probability-weighted average of those lengths is the **Shannon entropy** of the distribution: the smallest average bits-per-symbol any lossless code can achieve for data drawn from it. Sexton's figures for her two strings (1.38 and 0.82 bits per symbol) are exactly their entropies; arithmetic coding hit the floor.

Three consequences Sexton draws, and one she leaves implicit:

- **There is no universal best compressor.** Entropy is defined *relative to a probability distribution*, so the floor moves when the model changes. That is why there is no "God-compressor": the only way to go lower is to find a model under which the data is less surprising.
- **Lossy compression escapes the floor by cheating.** JPEG and MP3 get smaller by throwing away detail nobody will miss. Everything here is about lossless compression, where the original is reconstructed bit for bit — though lossy codecs still use models and entropy coders for whatever they keep.
- **Shannon entropy and thermodynamic entropy share a formula.** Gibbs's expression in statistical mechanics is the same sum over −p log p. Sexton flags it as a curiosity; it is the reason "entropy" is one word.
- **(Implicit) Overconfidence has a price in bits.** A model that assigns probability *p* to what actually happens pays −log₂ p. Sexton's example: a model that gives "Bermuda" 0.82 after "The rain in" would pay 0.29 bits if it were right, but the real word is "Spain" at 0.02, which costs 5.64 bits. Compression turns calibration into a quantified cost.

## Context is what makes models good

A frequency table is an **order-0** model: `count / total`. Context changes probabilities dramatically. The letter U has probability ~0.028 in English (≈5.16 bits) but ~0.999 after a Q (≈0.001 bits). An **order-1** model conditions on the previous symbol; **order-N** conditions on the previous N. Mechanically the model becomes a family of probability tables, one per context, and the arithmetic coder uses a different partition of the interval at each step.

The payoff on "TO BE OR NOT TO BE":

| | order-0 | order-1 |
|---|---|---|
| Raw ASCII | 144 bits | 144 bits |
| Compressed | ~47 bits | ~21 bits |
| Bits / symbol | 2.59 | 1.16 |

One symbol of context more than halved the output. This is the lineage of PPM (prediction by partial matching), context mixing, and the PAQ family: keep making the predictor better. Sexton's pivot line: "Do you know what else is really good at prediction?"

## Language models are compressors

DeepMind's 2023 paper [*Language Modeling Is Compression*](https://arxiv.org/abs/2309.10668) (Delétang et al.) makes the equivalence explicit. An LLM generates text by taking the context, emitting a probability distribution over the next **token**, sampling one, appending it, and repeating. To compress instead of generate, keep everything except the sampling step: the next token is already known, so hand the model's distribution to an arithmetic coder and encode the *actual* token. The cost is −log₂ of whatever probability the model gave it, and a well-trained model puts the true token near the top.

Sexton's benchmark on the opening of *A Tale of Two Cities*:

| Model | Compressed size | Share of original |
|---|---|---|
| order-1 | 434 bits | 24% |
| GPT-2 | 176 bits | 10% |

GPT-2, "archaic" by 2026 standards, beats a context model by 2.5×. The DeepMind paper goes further: Chinchilla 70B, trained only on text, compresses ImageNet image patches to about 43% and LibriSpeech audio to about 16% of raw size, beating PNG (~59%) and FLAC (~30%) respectively. A good enough sequence predictor is a good compressor of anything sequential.

The deeper point is about training, not inference. LLMs are trained to minimize **cross-entropy**, and cross-entropy is exactly the average −log₂ p(actual token) the arithmetic coder charges. The loss curve of a language model *is* its compression ratio on the training distribution, in bits per token; perplexity is just 2 raised to that number. So "compression is prediction" is not an analogy: the objective function of the whole field is a compression objective. Chris Olah's [*Visual Information Theory*](https://colah.github.io/posts/2015-09-Visual-Information/) is the standard walkthrough of the math.

The lineage predates LLMs. Marcus Hutter's Hutter Prize (2006) rewards compressing Wikipedia text on the premise that better compression is better understanding, and the context-mixing compressors that won it were, in effect, small neural predictors feeding an arithmetic coder. The 2023 paper's contribution was showing that general-purpose predictors now dwarf the purpose-built ones.

## Why gzip still wins in practice

If LLMs compress so well, why does every HTTP response still negotiate `Accept-Encoding: gzip, br`? Sexton's answer is that compression tools shrink data *under resource constraints*, and the model's cost counts:

- **The decoder needs the model.** Arithmetic decoding requires the same probabilities the encoder used, so both browser and server would need identical multi-gigabyte weights, where gzip's "model" is a few kilobytes of tables built on the fly. This is also the minimum-description-length answer: the decoder's size is part of the compressed size, and for anything smaller than the model you are "shipping gigabytes to save a few KB."
- **Compute.** A forward pass per token to compress a stylesheet would destroy page-load time. Even for datasets that dwarf the model, the compute makes it impractical today.
- **(Implicit) Determinism.** Decoding requires *bit-identical* probabilities on both sides. Floating-point non-determinism across GPUs, batch sizes, or kernel versions can flip a probability in its last bit and corrupt the entire decoded stream, so LLM-based arithmetic coding needs integer or carefully reproducible inference. This is a real engineering obstacle the explainer does not mention.

Sexton's summary: compressing down to entropy has been solved since arithmetic coding in the late 1970s, and entropy coders now compete on speed and memory, not ratio. The only open problem is lowering the entropy itself, which means building better predictors.

## Connections

- [[latent-space]] — Kevin Kelly's image of an LLM as "a small zip file that contains all human knowledge" is literally true in this sense, and this article supplies the mechanism: the training objective is bits per token.
- [[agi-timelines]] — Karpathy's figure of roughly 0.07 bits stored per pre-training token for Llama 3 70B is denominated in the same currency: bits retained per token seen, against bits paid per token encoded here.
- [[ai-for-mathematics]] — Sanderson proposes compression as a reward for the "Galois instinct," the framing that makes a proof short. That is the Hutter Prize intuition applied to research.
- [[llm-knowledge-bases]] — compiling raw sources into a wiki is *lossy* compression. The fidelity risk that survey names is exactly the detail an entropy coder would never drop.
- [[the-bitter-lesson]] — general predictors trained at scale beat hand-built context models for the same reason they beat hand-built everything else.

## Sources
- Annie Sexton (2026). "Compression is prediction." <https://ngrok.com/blog/compression-is-prediction> — [[2026-09-08-compression-is-prediction|local copy]]
