---
source: agent
compiled_from:
  - agent-notes/raw/engineering/computer/design/2023-10-19-linear-design-process.md
compiled_at: 2026-04-05
model: claude-opus-4-6
confidence: medium
---

# Linear's Design Process

Linear's co-founder Karri Saarinen describes a design philosophy built on one core principle: **design is only a reference, never a deliverable**. The implication is radical simplicity — if the design file is never handed off, the overhead of maintaining it vanishes.

## The workflow

1. **Screenshot the live app** and design on top of it in Figma. The existing product is always the starting canvas, not a blank artboard.
2. **Minimal design system** — colors, type, icons, and some basic components. Anything else can be screenshotted or quickly recreated. There is no design-system team, no councils, no naming debates ("atomic" or otherwise).
3. **One design file per quarter per medium** (desktop, website, mobile). Each designer creates a page within the file for their projects — this makes cross-visibility easy. Files are split by medium because they grow too large otherwise and each medium has its own system.
4. **No process orthodoxy in the file.** Naming layers, using auto layout, building components — all optional, up to the individual designer.
5. **Prototypes only when needed** to communicate a flow or interaction.
6. **Once building starts, the design file becomes a reference.** The real design is the live app. The next iteration starts from there, closing the loop.

Linear also ships a Figma plugin that links designs to Linear issues and supports creating issues directly from Figma.

## What makes this distinctive

Most product teams treat design files as deliverables — pixel-perfect specs that engineering "implements." Saarinen inverts this: the app is the source of truth, and the design file is a disposable sketch that gets you to the next version. This has several consequences:

- **Reduced process overhead.** No time spent on design QA, redlines, or maintaining a massive component library that drifts from production.
- **Designers think in product, not in files.** Screenshotting the live app forces designers to start from reality rather than an idealized blank canvas.
- **Quarterly resets prevent cruft.** A new file each quarter means no one inherits a bloated, outdated Figma document.

The approach assumes a team where designers and engineers are tightly integrated and designers have strong product sense — it would likely break down in organizations where design-to-engineering handoff is the primary coordination mechanism.

## Sources

- Saarinen, K. (2023). "Primer on how we design at Linear." <https://x.com/karrisaarinen/status/1715085201653805116> — [[2023-10-19-linear-design-process|local copy]]
