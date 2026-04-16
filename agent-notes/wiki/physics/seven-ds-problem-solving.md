---
source: agent
compiled_from:
  - agent-notes/raw/physics/2025-07-16-first-principles-reasoning.md
compiled_at: 2026-04-16
model: claude-opus-4-6
confidence: medium
---

# The Seven Ds and the Little s

A structured method for solving physics problems from first principles, formalized by Casey Handmer from the training regimen used by the Australian International Physics Olympiad (IPhO) team. Handmer argues this method — learnable in roughly two weeks — is radically underused, even among professional physicists, and that its absence from LLM training data is a key reason current models fail to reason about the physical world with genuine insight.

## The method

The eight steps are ordered by importance, not chronology (though in practice they are roughly sequential):

1. **Diagram** — Draw a half-page diagram capturing all necessary information. The act of diagramming engages spatial reasoning and prevents hasty assumptions. For LLMs, Handmer suggests "problem translation" into some analogous representational paradigm.

2. **Directions** — Establish a local coordinate system so all quantities share a consistent frame of reference.

3. **Definitions** — Assign unambiguous symbols to every relevant quantity. This creates a self-consistent symbolic ontology and surfaces definitional inconsistencies early.

After these three steps, the problem has been fully read into working memory. Handmer emphasizes this is often the hardest part: identifying the right question, the relevant figure of merit, and the definition of "optimal."

4. **Diagnosis** — A single-phrase summary of the physical principle to be applied (e.g., conservation of energy, vector algebra). The more fundamental the principle, the better. Roughly 4-5 methods handle 95% of problems.

5. **Derivation** — Starting from ~10 fundamental equations, derive the specific formula needed. This is explicitly *not* pattern-matching from a library of memorized formulas. Derivation is complete when you've reproduced the textbook result from first principles.

6. **Determination** (d'Algebra) — Combine derived equations algebraically to produce the answer in symbolic form. Box the final formula. This is where simplifying assumptions, expansions, and factorizations happen.

7. **Dimensions** — Verify that dimensional analysis is consistent on both sides of every equation. Also test against extreme values, obvious intuitions, and initial assumptions. Handmer marks a passing check with a smiley face. This step frequently catches dropped terms that neither humans nor LLMs otherwise notice.

8. **substitution** (lowercase, "the little s") — Only now plug in numerical values. This is the first and only time a calculator is used. "The calculator cannot deliver physical insight."

## Why LLMs fail the physicist Turing test

Handmer reports testing every major model (Claude, GPT, Gemini, Grok) with oral-exam-style physics questions. Despite strong performance on Olympiad-style and grad-qualifying-exam benchmarks, he argues no current model would pass a physicist Turing test. The failure modes:

- **Talking around the question** — generating lengthy text that never addresses the core physical insight.
- **Pattern-matching to web sources** — indexing on a blog post that discusses the topic (sometimes Handmer's own) rather than reasoning independently.
- **Algebraic sloppiness** — routinely dropping terms during symbolic manipulation, then spending pages justifying a dimensional error rather than catching it.
- **Obsequiousness as self-defeat** — the tendency to agree with the user undermines the critical self-evaluation needed in step 7.

Handmer attributes this to a training data gap: worked examples of this structured method are extremely rare in the common crawl. He sees three possible paths forward: generating 100-10,000x more training examples of the method, finding more sample-efficient training paradigms, or radically better system prompts.

## Implications for [[ai-scientific-reasoning|AI scientific reasoning]]

The post implies that current benchmarks — Olympiad problems, qualifying exams — measure the wrong thing. A model can score well by pattern-matching against known problem types while completely lacking the ability to derive novel physical insights. The seven-Ds method is precisely what bridges textbook problems to genuine first-principles reasoning about open questions.

Handmer's example questions (nuclear reactors on Mars, lunar dust grain-size attractors, battery-grid equilibria) are deliberately chosen to require this bridging: they have no clean textbook solution and demand chaining fundamental principles through unfamiliar territory.

## Sources
- Handmer, Casey (2025). "How to reason from first principles." <https://caseyhandmer.wordpress.com/2025/07/16/how-to-reason-from-first-principles/> — [[2025-07-16-first-principles-reasoning|local copy]]
