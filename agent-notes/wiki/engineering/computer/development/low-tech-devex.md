---
source: agent
compiled_from:
  - agent-notes/raw/engineering/computer/development/2024-05-20-in-praise-of-low-tech-devex.md
compiled_at: 2026-04-16
model: claude-opus-4-6
confidence: medium
---

# Low-Tech Developer Experience

Low-Tech DevEx (LTD) is a philosophy of developer tooling that favors long-standing, text-based, command-line tools over graphical IDEs and newer alternatives. The approach is grounded in the [[unix-philosophy]] tradition: small tools that do one thing well, accept text streams, and compose with each other.

## Core principles

Miell defines LTD as preferring tools that are:

- **Battle-hardened** — long track records of stability (decades, not years)
- **Small and self-contained** — few dependencies, no daemons or engines required
- **Text-based** — standard input/output, command-line interfaces
- **Composable** — chain together via Unix pipes and conventions
- **Portable** — work on any platform with a terminal

This overlaps significantly with the [[choose-boring-technology]] ethos of spending "innovation tokens" sparingly — but where that framework addresses production technology choices, LTD focuses specifically on the *personal developer environment*.

## Why LTD tools outperform over time

Miell argues a recurring pattern: engineers try the fancy GUI, then gradually realize the low-tech CLI approach is more productive. The advantages compound:

- **Portability.** vim runs on HPUX, inside Docker containers, on any cloud shell — anywhere you have a terminal. Try running VSCode inside a production container.
- **Speed.** No startup lag, no extension loading. Miell notes VSCode on an M2 Mac took 30+ seconds to become usable in a single-file folder.
- **Power.** Steep learning curves yield steep, long-lasting returns. The investment amortizes over a career.
- **Composability.** Fewer dependencies mean tools embed in each other naturally. vim inside Docker is trivial; VSCode inside Docker is a project.
- **Sustainability.** These tools have survived decades and won't disappear. No dependency upgrades, no forced rewrites.
- **User-aligned incentives.** LTD tools are built by and for users, not purchasers. Purchasers want GUIs and novelty; users want productivity.

## The LTD toolkit

Miell's opinionated list of essential LTD tools:

| Tool | Role |
|------|------|
| **shell** (bash/zsh) | Foundation — underpins everything else |
| **vim/emacs** | Text editing everywhere |
| **make** | Project task runner and onboarding interface |
| **Docker** | Portable, reproducible environments via CLI |
| **tmux/screen** | Terminal multiplexing — windows without a GUI |
| **git** | Distributed version control |
| **curl** | HTTP debugging, saveable as documentation |
| **ssh** | Remote access without GUI overhead |
| **cloud shell** | Pre-configured terminal in the browser |

Plus TUI tools like `k9s` (Kubernetes), `htop` (monitoring), `entr` (file-watch execution), and `nnn` (file browsing).

## Make as a developer interface

A central practical example: using Makefiles not for compilation but as a **project command menu**. A `make help` target that lists available commands serves as living documentation and an onboarding tool. Because Make targets can wrap Docker commands, the workflow becomes portable — anyone with `make` and Docker can run the project.

Miell contrasts this with Dagger, which pursues a similar goal (portable CI/CD via containers) but requires a dedicated engine, installation, and on Kubernetes, privileged access. Make requires none of these moving parts.

The tradeoff: Make's syntax has a steep *write* curve, but a shallow *use* curve. `make help` is immediately accessible to new team members even if writing new targets takes practice.

## Connections

The LTD philosophy connects to several broader ideas:

- [[choose-boring-technology]] shares the preference for proven tools but applies it to production systems rather than developer environments
- The [[unix-philosophy]] (write small programs that handle text streams) is the theoretical foundation LTD draws from
- [[internal-software-quality]] is complementary — LTD tools enable fast iteration loops that help maintain quality

## Sources

- Miell, Ian (2024). "In Praise of Low Tech DevEx." <https://blog.container-solutions.com/in-praise-of-low-tech-devex> — [[2024-05-20-in-praise-of-low-tech-devex|local copy]]
