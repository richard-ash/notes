---
source: agent
compiled_from:
  - agent-notes/raw/engineering/computer/development/2025-03-02-huntley-z80-clean-room.md
  - agent-notes/raw/engineering/computer/development/2025-03-03-ls-rs-readme.md
  - agent-notes/raw/engineering/computer/development/2025-07-21-chinese-wall-llm-code-editing.md
  - agent-notes/raw/engineering/computer/development/2026-10-12-huntley-nobody-types-code-by-hand.md
compiled_at: 2026-10-13
model: claude-fable-5-1
confidence: low
---

# Clean-Room Cloning with LLMs

**Clean-room cloning** is the use of language models to rebuild an existing program without copying it: one agent reads the original (its source, a disassembly, or just its behaviour) and writes a specification; a second agent with no access to the original implements that specification in whatever language or stack you choose. The name comes from the clean-room (or "Chinese wall") reverse-engineering process of the 1980s, in which one team documented a proprietary system and a separate team that had never seen it built a compatible replacement, the precedent being Phoenix Technologies' clone of the IBM PC BIOS. The LLM version replaces the two teams with two model contexts and the lawyers' review of the specification with, so far, nothing.

Geoffrey Huntley's "Z80 post" of 2 March 2025 is the origin of the pattern as a named technique in the agentic-coding literature, and he treats it as the first thing he did with the autonomous loops described in [[loop-engineering]]. This article compiles what is publicly visible of that post (it is now subscriber-only, so the walkthrough itself is missing; see the capture note in the raw file), Daniel Joyce's `ls`-to-Rust port that applied it the next day, Manatsawin Hanmongkolchai's July 2025 "Chinese Wall" paper, which formalises the same two-context structure for a different purpose, and Huntley's October 2026 retrospective. Confidence is `low` because the primary source is only partially retrievable.

## The pattern

| Step | Traditional clean room | LLM version (Huntley / Joyce) |
|---|---|---|
| Artifact | Proprietary binary or system | Source, or a binary via `objdump`, or observed behaviour |
| Team 1 | Engineers reverse-engineer and write a functional spec, reviewed to strip expression and keep function | A model reads the artifact and writes specs by functional area, in markdown |
| Wall | Team 2 provably never sees the original; the process is documented for litigation | A fresh context that is given only the specs |
| Team 2 | Builds a compatible implementation from the spec | A model (or a loop of them) implements the specs in the target language |
| Check | Compatibility testing against the published interface | Whatever tests the loop is given; in the public examples, none |

Huntley's own title describes a longer chain than the table: "Can a LLM convert C, to ASM to specs and then to a working Z/80 Speccy tape? Yes." The demonstration starts from a toy application he has the model write in C, goes down to assembly, back up to a specification, and then out to a working ZX Spectrum tape, so the point is that the model can cross representation levels (source, machine code, prose) in both directions, not just translate between languages. The companion post from the day before, "Yes, Claude Code can decompile itself. Here's the source code." (1 March 2025, also subscriber-only), gives the general claim: "These LLMs are shockingly good at deobfuscation, transpilation and structure to structure conversions," which he traces to an earlier experiment converting a Rust audio implementation to Haskell, and which he applied to produce a repository described as a "cleanroom transpilation of the official Claude Code npm package."

## The worked example: `ls` in Rust

Daniel Joyce's `ls-rs` (repository created and last pushed 3 March 2025; 34 stars by October 2026) is the one public, inspectable run of the technique, and the README, which Joyce says the model also wrote, documents the process:

1. **Binary analysis.** Run `objdump` on the GNU `ls` binary, examine the ELF64 x86-64 structure, identify key functions and their relationships.
2. **Specification generation.** Write specs by functional area: `core/` (filesystem, display, sorting), `security/` (permissions, SELinux), `i18n/` (localization, encoding), `options/` (formatting, filtering).
3. **Implementation.** Implement each spec in Rust with ordinary crates (`clap`, `libc`, `users`, `chrono`, `unicode-width`, `selinux`, `termcolor`).

The tooling was Cursor with Claude Sonnet 3.5. Joyce reports that the model generated "almost all (99.9%)" of the code, about 1,000 lines in roughly 45 minutes of back-and-forth, that the specs it produced were "pretty lean" and he was surprised how far it got on them, and that the output was "generally syntactically correct though sometimes a crate import would be missing."

Two of his own caveats matter more than the feature list. First: "I have NOT undertaken any heavy checking of the claims made in this file," and "some things may or may not be fully integrated or generated yet." Second, the repository has no test suite and no comparison against GNU `ls` output. So the one public artifact demonstrates the *production* half of the pattern and skips the *verification* half entirely, which is exactly the "missing 20%" of completeness and verification that Wulf describes in [[loop-engineering]], and the gap that [[correctness-oracles]] exists to fill. Note also that the natural oracle for a clone, differential testing against the original's behaviour, is available in a clean room (behaviour is not expression) and was not used.

## The Chinese Wall paper

Hanmongkolchai's "Applying the Chinese Wall Reverse Engineering Technique to Large Language Model Code Editing" (arXiv 2507.15599, 21 July 2025, cs.SE; an independent author's first paper, acknowledging Kasetsart University) takes the same two-context structure to a different problem: the copyright provenance of code-model training data. Frontier code models have undisclosed training sets that almost certainly include copyleft code (the paper cites Armin Ronacher's 2021 demonstration of Copilot reproducing Quake III's fast inverse square root verbatim, comments included). Models trained only on permissively licensed data (Comma on the Common Pile, Starcoder2) exist but are weak. The proposal:

> "a high quality model is used to generate detailed instructions for a weaker model. By doing so, a weaker but ethically aligned model may be used to perform complicated tasks that, otherwise, can only be completed by more powerful models."

Concretely, Gemini 2.5 Pro receives the task and the original code and is told to annotate it with step-by-step `EDIT:` comments and "NEVER any code"; the weak model then receives only the annotated code and implements the comments. Nothing else the strong model produced is visible to the editor. Evaluated on CanItEdit (105 hand-written Python editing problems, 20 samples each, "descriptive" and "lazy" prompt variants):

| Editor model | pass@1 alone → walled | pass@20 alone → walled |
|---|---|---|
| Comma v0.1 1T | 9.14 → 21.24 (+120%) | 20.00 → 33.33 (+66%) |
| Starcoder2 Instruct | 35.10 → 42.05 | 60.00 → 71.43 (~+20%) |
| phi4 | 54.71 → 68.67 | 73.33 → 72.38 |
| Gemini 2.5 Pro alone | 57.66 | 94.29 |

(Descriptive-prompt figures. The lazy-prompt column moves the same way.) phi4 behind the wall beats Gemini alone on pass@1 but loses slightly on pass@20, which the author reads as the technique not always helping an already-capable editor. The appendix's fast-inverse-square-root test is the clearest illustration of what the wall does: told to implement the algorithm, unaided Starcoder2 reproduces Quake's pointer-cast version almost line for line; behind the wall it writes a `union`/`uint32_t` version, structurally different from the original. Unaided Comma, which has never seen the Quake code, cannot produce the algorithm at all.

The paper is careful on two points the blog posts are not. It explicitly declines to claim "that the process will always completely satisfy every legal requirement that allowed the original reverse engineering technique to produce legally distinct code," and it concludes that the technique is not yet usable for its purpose because no competent model trained solely on public-domain data exists, so even the weak editor may carry restricted code in its weights. Its named relative is Aider's architect mode (a strong "architect" model instructing a weaker "editor"), with the difference that Aider's architect is allowed to write code and the goal there is edit quality, not provenance.

It does not cite Huntley, the Z80 post, or `ls-rs`; its precedent is a 2001 Computerworld piece on the Phoenix BIOS. Huntley's August 2025 tweet says the Z80 idea "has been productionised into a MCP server and a paper published," and this paper matches the date and the topic, but if it is the one he meant, the relationship is independent convergence rather than lineage.

## What the wall does and doesn't do

The three sources together separate two things the blog posts run together.

**Process separation.** Huntley's and Joyce's version guarantees that the implementing context never saw the original *in the conversation*. That is the part of the clean-room doctrine that is cheap to reproduce with LLMs, and it is why the resulting code is structurally unlike the original (different module boundaries, different idioms, a `union` where the original had a cast).

**Knowledge separation.** The clean-room doctrine also assumes the second team's heads are clean. A frontier model implementing GNU `ls` from a spec has, with near certainty, GNU `ls` in its weights, and the same goes for any widely cloned product. Hanmongkolchai's paper is an attempt to get knowledge separation by making the editor a permissively trained model, and its conclusion is that this does not yet work at useful quality. Huntley's practice gets process separation only. His own phrase for it, "running the LLM like a Bitcoin mixer for intellectual property," names the laundering reading himself, and the Common Pile authors' term "license laundering" appears in the paper for the same reason.

On legality, Huntley says only that it "is not legal in every jurisdiction, and you have to take the right approach." The standard reference points (not legal advice) are the US cases *Sega v. Accolade* (1992) and *Sony v. Connectix* (2000), which treated intermediate copying for reverse engineering as fair use, and the EU Software Directive's Article 6, which permits decompilation only for interoperability. None of them contemplated the implementing party being a model whose training set is the question. Both Huntley's posts and the paper are explicit that this is unresolved.

## Why Huntley thinks it matters

The 2025 posts frame the technique as a capability demonstration. By the October 2026 interview ([[loop-engineering]]) it has become his argument about industry structure. "Not enough people understood that post at the time. Take an existing application, clean-room it into specifications, then rebuild the software from those specifications, much like the way AMD's CPUs came out of Intel's." The evidence he offers that the pattern has arrived: the wave of Photoshop clones in the week before the interview, "services and MCPs" whose whole job is rebuilding existing software, and papers citing the idea. His conclusion is **infinite software**: "If you're selling software without infrastructure or some other lock-in, you're hosed. So the real question is: what is a moat in software now?"

That is the attacker's-side statement of the thesis already in the vault from the defender's side: Vernal's [[software-industry-barbell]] (near-zero production cost erodes replication, switching and integration moats) and Leach's [[minimum-viable-saleable-software]] (the zone where buying still beats building shrinks to what carries verification and maintenance labour). The clean-room pattern is the mechanism by which "replication cost" goes to zero for a competitor, and the `ls-rs` caveats are the reason Leach's verification-labour residue still exists.

Two further connections. Notion's [[spec-driven-development]] is the same spec-in-the-middle structure run forward, from intent to code, with the spec checked in as the source of truth; clean-room cloning runs it backward from code to spec and then forward again, and the quality of the whole thing is bounded by the spec, which in Joyce's run was "pretty lean." And Wilton's vendored reference implementation in [[correctness-oracles]] is the opposite use of the original: keep it in the room as the oracle to test against rather than wall it off, which is legally the harder position but the only one that yields a correctness guarantee.

## Open questions

- Whether a fresh model context counts as a wall in any jurisdiction has not been tested in court, and both the posts and the paper say so.
- The public example (`ls-rs`) was never verified against the original by its author; no public run of the pattern with a differential test suite has been found.
- The Z80 post's walkthrough, including the prompts used to produce the specification, is behind the paywall and is not represented here. If a subscriber copy becomes available, this article should be recompiled from it.

## Sources

- Huntley, Geoffrey (2025-03-02). "Can a LLM convert C, to ASM to specs and then to a working Z/80 Speccy tape? Yes." <https://ghuntley.com/z80/> — [[2025-03-02-huntley-z80-clean-room|local copy]] (public preview only; the post is subscriber-only).
- Joyce, Daniel (2025-03-03). "ls-rs: A Rust Implementation of ls." <https://github.com/DanielJoyce/ls-rs> — [[2025-03-03-ls-rs-readme|local copy]] (README).
- Hanmongkolchai, Manatsawin (2025-07-21). "Applying the Chinese Wall Reverse Engineering Technique to Large Language Model Code Editing." arXiv:2507.15599. <https://arxiv.org/abs/2507.15599> — [[2025-07-21-chinese-wall-llm-code-editing|local copy]].
- Huntley, Geoffrey (2026-10-12). "nobody should type code by hand anymore. here's what's left." <https://ghuntley.com/agency/> — [[2026-10-12-huntley-nobody-types-code-by-hand|local copy]]. The Z80 retrospective and the "infinite software" framing.
