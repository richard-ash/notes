---
source: agent
compiled_from:
  - agent-notes/raw/business/strategy/2002-06-11-strategy-letter-v.md
compiled_at: 2026-06-02
model: claude-opus-4-7
confidence: high
---

# Commoditize Your Complement

"Commoditize your complement" is one of the most-cited strategic heuristics in tech, articulated by Joel Spolsky in *Strategy Letter V* (2002). The framework explains why profitable companies systematically invest in driving down the price of *adjacent* goods they don't sell — and why so many large public companies, with fiduciary duties to shareholders, pour money into open source software that they then give away.

## The core micro-economic claim

Every product has **substitutes** (alternative purchases — chicken for beef) and **complements** (joint purchases — gas for cars, hardware for operating systems, babysitters for dinner reservations).

The load-bearing observation:

> Demand for a product increases when the price of its complements decreases.

Cheap flights to Miami raise hotel demand in Miami. Cheap PCs raise OS demand. Cheap babysitting raises restaurant demand. So:

> **Smart companies try to commoditize their products' complements.**

The lowest sustainable price of a complement is the *commodity price* — what arises when many competitors sell indistinguishable goods. A company that succeeds in commoditizing its complement gets to charge more for its own product while watching demand expand.

## The IBM and Microsoft case studies

Spolsky's framework retrofits two famous outcomes:

- **IBM** used off-the-shelf parts and published the *IBM-PC Technical Reference Manual* to commoditize **add-ins** (memory, drives, graphics cards, printers). Cheap add-ins → more PC demand.
- **Microsoft**, in licensing PC-DOS to IBM, refused exclusivity — allowing Compaq and hundreds of OEMs to legally clone the PC. **Microsoft commoditized the PC itself**, which made MS-DOS (its complement) enormously more valuable. "That's why Bill Gates can buy Sweden and you can't."

The XBox is the same play with mixed results: commodity PC hardware inside the console, plus DirectX as a graphics abstraction to commoditize video chips so games become more profitable. Spolsky notes the hardware side backfired in 2002 because commodity PC parts had already bottomed out on margins.

## Open source as a complement-commoditization strategy

The framework's most provocative application is to open source. Spolsky argues that the major corporate sponsors of OSS are acting in self-interest, not ideology:

| Sponsor | Their product | Complement they commoditize | Mechanism |
|---|---|---|---|
| **IBM** | IT consulting | Enterprise software | Funding Linux, Apache, Eclipse |
| **Netscape** (early) | Web servers | Web browsers | "Freeware" browser since 1994 |
| **AOL/Time Warner** | Entertainment content | Entertainment delivery (browsers) | Continued Mozilla investment after server biz failed |
| **Transmeta** | CPUs | Operating systems | Paying Linus to hack on Linux |
| **Sun, HP** | Hardware | Windowing systems | Funding Ximian / Gnome |

Each is rational under "commoditize your complement." None requires the sponsor to have stopped believing in capitalism.

## The "free as in beer" fallacy

Spolsky pushes back on a recurring open-source argument that *zero price* means *zero cost*. He cites Linux developer Moshe Bar claiming kernel revisions can freely break existing device drivers because rewriting them is "free." This is a divide-by-zero error: debugged code carries **opportunity cost** and **time cost** even when no dollars change hands. Volunteer developer hours are scarce, and every project competes for the same finite pool.

When an economist talks about price, they mean **total cost of ownership** — setup time, retraining, process conversion. Free-as-in-beer software is still subject to economic gravity.

## Sun as the cautionary case

Spolsky's harshest analysis is of Sun Microsystems, which he calls "the loose cannon of the computer industry" for adopting strategies driven by anger at Microsoft rather than self-interest:

- Sun funded free software (Star Office, Linux, Apache, Gnome) — commoditizing **software**.
- Sun pushed Java's Write-Once-Run-Anywhere bytecode — commoditizing **hardware**.

But Sun was a hardware company. Commoditizing both its product and its complement leaves nothing to charge for. "When the music stops, where are you going to sit down?" The prediction proved correct: Sun was eventually sold to Oracle in 2009, having failed to capture proprietary value on either layer. The deeper lesson is that the framework only works if you know which layer you're trying to defend.

## The asymmetry: software commoditizes hardware, not vice-versa

A subtle asymmetry Spolsky surfaces: **it is easy for software to commoditize hardware, but very hard for hardware to commoditize software.**

- A hardware abstraction layer (Windows NT's HAL) is a "tiny piece of code" that lets one OS run on many CPUs.
- But software has switching costs that don't go to zero even when the alternative is free. The cost of moving from Microsoft Office to StarOffice is non-zero — muscle memory, file format friction, tiny UI differences — so even free Office substitutes failed to commoditize Office.

Hard drives, by contrast, are perfectly interchangeable: pull one from an IBM, slam it into a Dell, boot. This asymmetry — hardware is genuinely fungible, software is sticky — explains why the commoditization plays of the PC era tended to converge on commoditized hardware with proprietary software riding on top.

## Why this framework keeps getting reused

"Commoditize your complement" survives because it predicts otherwise-puzzling behavior:

- **Google open-sourcing Android** (commoditize mobile OS to protect search).
- **Facebook open-sourcing PyTorch / React / Llama** (commoditize ML infrastructure / web frameworks / foundation models so the social-graph + ad-targeting layer captures the surplus).
- **Apple bundling free apps** (commoditize productivity software to sell hardware — though Apple is one of the few cases where the hardware-commoditizes-software direction has worked, via the App Store store-of-trust).
- **Nvidia open-sourcing CUDA libraries** (commoditize the ML software stack to sell GPUs).

The framework also explains the inverse: when an incumbent's complement becomes *expensive* or *concentrated*, the incumbent's margins compress. This is the diagnostic lens behind much of [[ai-platform-moats]] — Evans's argument that foundation-model companies are structurally squeezed because their upstream complement (TSMC chips, HBM memory) is monopolistic and their downstream complement (apps, distribution) is owned by incumbents who can switch model providers freely.

## Connections to related frameworks

- [[aggregation-theory]] — Thompson's framework can be read as a more recent specialization: aggregators don't just commoditize a complement, they commoditize **supply** (the upstream side of a value chain) by owning the demand-side relationship. Christensen's *Conservation of Attractive Profits* — which Thompson cites — is the broader principle: profits migrate to whichever adjacent layer becomes integrated when one layer modularizes. Spolsky's heuristic is the action-side prescription: deliberately *cause* the modularization of the adjacent layer.
- [[ai-platform-moats]] — Evans's argument that foundation models are commodity infrastructure can be read as someone successfully commoditizing the model layer from both ends (hyperscalers fund OSS models to commoditize the labs; chipmakers and app developers don't care which model they use).
- [[competitive-moats]] — Commoditizing your complement is one of the structural mechanisms by which a moat at one layer (PCs → OS, search → browser, ads → social graph) is reinforced by destroying margin at the adjacent layer.

## Temporal notes

The 2002 vintage shows in the case selection: Eazel, ArsDigita, VA Linux, Transmeta, the Netscape-as-Mozilla origin story, and Sun's death spiral are all historical now. But the framework itself has aged well — arguably better than most strategy frameworks of its decade, because it makes a falsifiable prediction (Sun's incoherent strategy will fail) that was vindicated by 2010.

The dominant 2020s application is **AI**, where every major player faces the same diagnostic question: which layer am I trying to defend, and am I funding the right complement to commoditize? Meta's Llama strategy is the cleanest contemporary instance — open-source frontier models to commoditize the labs and protect the ads-on-social-graph profit pool. Google's funding of Anthropic plus its own Gemini line is messier: it's trying to defend both search (commoditize models) and cloud (charge for models), which Spolsky would diagnose as Sun-like incoherence.

## Sources

- Spolsky, Joel (2002). "Strategy Letter V." Joel on Software. <https://www.joelonsoftware.com/2002/06/12/strategy-letter-v/> — [[2002-06-11-strategy-letter-v|local copy]]
