---
source: agent
compiled_from:
  - agent-notes/raw/engineering/computer/development/2020-02-16-computers-can-be-understood.md
compiled_at: 2026-04-06
model: claude-opus-4-6
confidence: medium
---

# Computers Can Be Understood

Nelson Elhage's 2020 essay articulates a foundational engineering mindset: **any question about a computer system has a comprehensible answer, accessible through determined exploration**. Rather than treating modern software stacks as inscrutable black boxes, Elhage argues that developers can — and should — build understanding at every layer of abstraction, even if no single person masters every layer simultaneously.

## The core claim

Modern systems are staggeringly complex (transistors through microarchitecture through OS kernel through browser VM through application code), but each layer is built on deterministic, logical foundations. There is "no magic" — no layer where comprehensible rules give way to unknowable demons. Any behavior can be explained by digging through enough layers.

Three pathways make this practical:

1. **Open-source code** — most of the stack is readable.
2. **Documentation** — even closed-source hardware (e.g. Intel x86) publishes exhaustive specs.
3. **Reverse engineering** — when source and docs fail, determined engineers can still extract understanding. Security researchers routinely demonstrate this (e.g. Project Zero reverse-engineering Haswell's branch predictor for Spectre analysis).

## Practical manifestations

**Dependency literacy.** Elhage advocates keeping a local checkout of every major dependency's source and regularly reading it — not to memorize internals, but to build familiarity that pays off during debugging and design decisions.

**Cross-layer debugging.** The hardest bugs span abstraction boundaries (a kernel/userspace interaction, a compiler optimization exposing a logic error). These bugs are impossible to diagnose from a single layer and require engineers comfortable moving between layers. Elhage's favorite war story: diagnosing a single-bit cosmic-ray memory flip by reasoning across userspace, kernel, filesystem, and hardware.

**Mental models over memorization.** Rather than collecting rules and edge cases, Elhage builds compact models of a system's core primitives — the "algebra" that generates all observable behavior. His bash example: instead of memorizing quoting rules, he learned the expansion phases and their ordering, which both organized existing knowledge and extended to novel situations.

**Single-shot debugging.** Rich mental models enable backward reasoning from a single observation (a crash dump, a log line) to the root cause. Elhage cites Solaris kernel engineers at Oracle who set an explicit goal of root-causing 100% of kernel crashes from a single crash report — achievable because the kernel sits close to hardware with comparatively few layers to reason through.

**Security and performance.** Both domains inherently require multi-layer understanding. Attackers don't respect abstraction boundaries; performance engineers must reason about generated code and cache behavior. These fields select for — and further develop — the comprehensibility mindset.

## Pitfalls

Elhage is candid about where this mindset leads him astray:

**The need to understand becomes compulsive.** A belief in comprehensibility can harden into an inability to work with systems you don't yet understand. Elhage describes trying to stand up a simple AWS Lambda endpoint: instead of following a tutorial, he insisted on understanding every AWS component from scratch, ended up with 30 documentation tabs open, a broken endpoint, and eventually gave up. The desire to understand consumed the time budget that a pragmatic trial-and-error approach would have easily fit within.

**Reaching for hard tools before easy ones.** Elhage recounts spending days reverse-engineering a dependency bug that had already been fixed upstream in a newer version, and debugging disassembly when a coworker found a debug build in minutes. Having deep-dive skills doesn't mean they're always the right tool. He recommends: try the easy thing first (upgrade the dependency, reach for the debugger, cargo-cult from a working example), and only escalate when those fail.

## Connections to other ideas

This essay complements [[choose-boring-technology]] in an interesting way: McKinley argues for limiting the number of technologies you adopt (to conserve "innovation tokens"), while Elhage argues for deeply understanding whatever technologies you do adopt. Together they suggest a strategy of **few dependencies, deeply understood**.

The emphasis on mental models and first-principles understanding also contrasts with [[the-bitter-lesson]]'s argument that leveraging computation beats leveraging human understanding — though Elhage is writing about engineering practice (where human comprehension directly enables debugging and design) rather than AI research (where hand-engineered knowledge has historically lost to scale).

## Starting the practice

Elhage's tactical advice for developing this mindset:

- **Read your dependencies' source code.** Start with the framework or language runtime you use daily.
- **Ask generative questions:** "How would I have built this?"
- **Treat understanding as compounding.** Each system you study gives you patterns to match against the next one.
- He highlights Julia Evans as a model of publicly practicing this curiosity — learning systems deeply and writing about the process, not just the results.

## Sources

- Elhage, N. (2020). "Computers can be understood." <https://blog.nelhage.com/post/computers-can-be-understood/> — [[2020-02-16-computers-can-be-understood|local copy]]
