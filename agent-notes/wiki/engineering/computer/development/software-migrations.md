---
source: agent
compiled_from:
  - agent-notes/raw/engineering/computer/development/2026-04-09-migrations-tech-debt.md
compiled_at: 2026-04-09
model: claude-opus-4-6
confidence: medium
---

# Software Migrations

Large-scale software migrations — replacing one tool, system, or pattern with another across an entire organization — are the primary mechanism for reducing technical debt at scale. Will Larson argues they are in fact the *only* scalable fix, because individual engineers and teams naturally pick off low-hanging tech-debt fruit on their own, leaving only the cross-cutting, coordination-heavy work undone.

## Why migrations are unavoidable

Most tools and processes support roughly one order of magnitude of growth before they become ineffective. This isn't a failure of design — it's a sign of appropriate constraint-fitting (see [[choose-boring-technology]] for related reasoning about deliberate technology choices). As an organization scales, it therefore cycles through tools repeatedly, and the ability to execute migrations becomes a bottleneck on overall velocity.

Google engineers reportedly use the phrase "running to stand still" to describe a team whose entire capacity is consumed by dependency upgrades and pattern migrations, leaving nothing for product work. Every mid-sized company accumulates a queue of migrations it cannot staff: VMs to containers, monolith to services, old build system to new.

The cost of *not* migrating is worse than the cost of migrating — deferred migrations compound into larger rewrites.

## The Derisk → Enable → Finish playbook

Larson proposes a three-phase model drawn from his experience leading Uber's migration from Puppet-managed services to self-service provisioning.

### 1. Derisk

Start with the hardest cases, not the easiest. Write a design document and iterate it with the teams that have the most atypical patterns and edge cases. Then embed directly into one or two of those challenging teams to build and evolve the new system alongside them.

This ordering matters because each team that endorses a migration is placing a bet that the migration will actually finish. A half-completed migration is worse than none — it leaves teams stranded on an abandoned system and poisons trust for future efforts.

### 2. Enable

Before generating tickets for every team, invest in tooling to programmatically migrate the easy 90%. This dramatically reduces the organization-wide cost and increases the migration's success rate.

Then build self-service tooling and documentation as *products*: sit with teams as they follow your instructions, observe where they get stuck, and iterate. The best migration tools are **incremental and reversible** — teams can roll back immediately if something breaks.

Two extra days spent polishing documentation can save years across a large migration.

### 3. Finish

Getting to 100% adoption requires several tactics applied in sequence:

1. **Stop the bleeding** — ensure all *new* code uses the new approach (linter ratchets, updated templates). This turns time into an ally.
2. **Push status outward** — generate tracking tickets and surface migration progress to management, since teams that aren't migrating usually lack prioritization from leadership, not awareness.
3. **Finish it yourself** — the long tail of weird or unstaffed cases requires the migration team to dig into the nooks and crannies directly.

Larson emphasizes that recognition should be reserved primarily for *completion*, not commencement. Starting but not finishing a migration incurs net technical debt, so incentive structures must avoid rewarding partial work.

## Connections

The relationship between migrations and [[internal-software-quality]] is direct: Fowler argues that quality cruft slows teams within weeks, while Larson argues that cross-cutting migrations are the only way to address the cruft that individual teams can't fix alone. Together they describe a two-tier model of tech-debt management — local quality discipline plus organizational migration capability.

Larson revisits the Uber migration in [[judgment-in-ai-assisted-development]], comparing it with a 2026 migration at Imprint where coding agents handled implementation, shifting engineering time entirely from executing decisions to making them.

## Sources

- Larson, Will (2018). "Migrations: the sole scalable fix to tech debt." <https://lethain.com/migrations/> — [[2026-04-09-migrations-tech-debt|local copy]]