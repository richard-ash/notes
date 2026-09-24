---
source: agent
compiled_from:
  - agent-notes/raw/communication/2026-09-23-how-to-write-with-an-llm.md
compiled_at: 2026-09-23
model: claude-fable-5-1
confidence: medium
---

# Writing with LLMs

Ptacek's *How To Write With An LLM* starts from a hard premise: **readers detect LLM prose "in the parts per trillion."** However much you scuff up and humanize it, an LLM paragraph registers to much of the audience "not as writing but as output," and drops you into "the uncanny valley between expression and output" — out of the reader's attention. So the bad news first: you have to write the piece yourself. The model is a **copyeditor, not a ghostwriter**: write, then feed the draft to a good model to find flaws.

The method rests on two rules that keep the model's influence out of the parts of the process where your voice lives, plus a workflow that hands it everything else.

## Rule One: you may not use a single word the model suggests

Ptacek's reasoning: frontier models are "supernaturally good at selecting pleasing turns of phrase" — "it's sort of their whole thing" — and the problems with what they suggest are subtle. His image is that the models are **wedged in a mode where everything they write is a magazine headline.** A headline is good; an article made of dozens of them is not.

Because the failure is subtle, he doesn't trust himself to catch it case by case, so the rule is absolute — "intellectual personal protective equipment." Any specific turn of phrase the model suggests is off limits, "even if you like the words, even if you're sure they're better than what you already have." Read this way, the rule is a **precommitment against your own inability to discriminate**, not a claim that every suggestion is bad. It knowingly trades some local improvements for the integrity of the voice.

The boundary the rest of the essay draws: the ban covers *words and phrases*. Structural findings — move this paragraph, this verb is buried, this passage repeats itself — are exactly what the model is for. Words are yours; findings are the model's.

## Rule Two: forbid encouragement

The subtler channel is what Ptacek calls the model's **"influence campaigns."** Hand any draft to an LLM and it replies "that's gold, Jerry!" — but a first draft has bad paragraphs, incoherent topic flow, and "at least 750 words you don't need." The model praises the structure, then the transitions, then the word choices, metaphors, and pop-culture references. "They're bad! All bad! Don't listen!"

The damage: praise makes you **double down on first-draft impulses.** Normally you'd edit, rethink, and replace paragraphs, and Ptacek's central claim is that **those rethinks are load-bearing parts of your voice.** Readers won't be able to name what's wrong, but they'll sense you've become "artificially-flavored." No LLM word ever entered the text; the model still made it worse by suppressing the revision that would otherwise have happened.

His mitigations, in the order he tried them:

- **The editor lie.** For a couple of years he opened every copyediting prompt claiming to be not the author but the editor of an online publication screening submissions. It helps, but the model overshoots, overfitting to the imagined "goals" of the "publication."
- **Current practice:** forbid encouragement explicitly in the prompt, then stay hypervigilant for praise anyway.
- **Corollary — don't take all the copyediting advice either.** He fed the finished piece to GPT-5 ("I didn't write this"), which said it was 20% too long. "It's probably right. But I'm not fixing it. I'm just gonna be me." Flaw-detection is input to your judgment, not a replacement for it.

## What the model is for: tireless flaw detection

The models are excellent at flagging problems, and "boy, do you have a lot of them." You *could* spot them mechanically, but that is tedious, exhausting work, and the model doesn't get tired. So it's better than you at noticing:

- Overused passive voice, **nominalized verbs and buried action**, and repeated turns of phrase or word choices (or, if you've been taking the model's word for everything, the opposite: underused passive voice).
- Intensifiers and hedges — "very," "really," "actually," "unfortunately" — "sprinkled all over the draft like sawdust stuck to the work bench."
- The two or three paragraphs that belong somewhere else in the piece and instantly improve clarity when moved.

The schematic for this kind of edit already exists: Joseph Williams's *Style: Lessons in Clarity and Grace*, which Ptacek (who got it from Richard Gabriel) says does for prose what Hanson's *C Interfaces and Implementations* does for C — "it turns copyediting into Java coding. Exactly the same tedium, exactly the same effectiveness." The prescription: read *Style* or something like it, take notes, **turn the notes into a list of prompts, and run them as passes over the draft.**

## The loop, and the fresh-context judge

1. Ask the model to spot problems.
2. For each problem, **rewrite the paragraph (or sentence, or section) yourself** — Rule One.
3. Show the original and the rewrite to a model and ask which is better.

Step 3 hits a variant of Rule Two: a model that watched you edit knows which version is new and knows you want to hear it's better. So **give the comparison to a model that has no context of your editing process.** This generalizes into a hygiene rule for any LLM-as-judge setup: separate the model that saw the process from the model that scores the artifact, for the same reason blind review exists.

Ptacek eventually built a tool to stop juggling tabs and re-persuading models that he is "a helpful but stern writing coach trying to help a student who might be good but might be terrible." His opening prompt to the coding agent asked for Python, HTMX, SQLite, and a local Tailwind build; a Notion-style prose editor with highlighting for editing passes; Genius-style sidebar commentary matched to highlights; forward/back stepping through suggestions; and multiple documents with revision tracking and user-flagged major revisions. The editing prompts then run through the Codex, Claude, or Antigravity CLIs. He is explicit that his prompt list is not the point: "whatever anybody comes up with on their own is better, for themselves, than someone else's."

## Why the two rules are one rule

The model's output can enter your writing through two channels: **directly**, as words you accept, and **indirectly**, as praise that suppresses the revision you would otherwise do. Rule One closes the direct channel; Rule Two closes the indirect one. What remains — detection — carries no voice, because a list of flagged nominalizations reads the same whoever produced it. That is why the division of labor is stable: the model's comparative advantage (tireless pattern-matching against a rulebook) and the human's (choosing words and deciding what to keep) don't overlap.

## Connections

- **Judgment atrophy, sharpened.** [[ai-judgment-atrophy]] holds that delegating cognitive work erodes the friction-built muscle of judgment. Rule Two describes a nastier mechanism: judgment isn't delegated, it's *dissolved* — the model persuades you the editing pass was unnecessary, so you never notice you skipped it.
- **Same shape as AI code review, stricter.** [[ai-code-review]] prescribes the same division — the model finds, the human decides — but nobody enforces a Rule One for code; people paste model-written fixes freely. The asymmetry: code has a compiler and tests as ground truth, prose has only the reader's ear, and the reader's ear is precisely the instrument that detects "output." So the rule must be stricter for prose.
- **Expertise as leverage.** [[expertise-as-llm-leverage]] argues the main prompting skill is domain expertise. Ptacek's method is only usable by someone who has internalized *Style*: the prompt list is derived from the book, and every flagged problem still needs a human to decide whether it *is* one. "Read *Style* first" is Goedecke's claim in a different domain.
- **The detector in the wild.** [[asking-for-help]] records the observation that LLM-cheapened "I loved your work" openers are decaying into a *negative* signal in cold email — the parts-per-trillion detector applied to correspondence. Rule One is the defense.
- **Reader-centric craft.** The go-shorter, go-simpler, learn-the-genre advice in [[public-speaking]] is what a *Style*-derived prompt list operationalizes; Bloom's "go shorter" is GPT-5's "20% too long."

## Sources
- Ptacek, Thomas & Erin (2026). "How To Write With An LLM." <https://sockpuppet.org/blog/2026/09/17/how-to-write-with-an-llm/> — [[2026-09-23-how-to-write-with-an-llm|local copy]]
