---
source: agent
compiled_from:
  - agent-notes/raw/engineering/computer/development/2015-03-30-choose-boring-technology.md
compiled_at: 2026-04-06
model: claude-opus-4-6
confidence: medium
---

# Choose Boring Technology

Dan McKinley's influential 2015 essay argues that startups and tech companies should default to well-understood, proven technology and spend their limited capacity for novelty only where it truly matters.

## Innovation tokens

McKinley introduces the metaphor of **innovation tokens**: every company gets roughly three. Each time you adopt an unfamiliar or unproven technology — a new language, a new datastore, a novel infrastructure pattern — you spend one. The supply is fixed and teams chronically overestimate how many they have. The implication is that technology novelty is a scarce budget, not a free lunch.

Spending a token on, say, a cutting-edge message queue means you cannot also spend one on a novel deployment system without courting serious risk. The key discipline is choosing *where* novelty delivers outsized value relative to the mission, and defaulting to boring everywhere else.

## Why boring is good

"Boring" does not mean "bad." McKinley defines boring technology as tools whose **capabilities and failure modes are well understood** — MySQL, Postgres, PHP, Python, Memcached, cron. The critical advantage is that boring tech has smaller **unknown unknowns**: the surprises that can sink a project or a company. New technology may be better on paper, but it carries a much larger surface area of things you haven't even thought to worry about yet.

McKinley frames this through the Rumsfeld matrix of known/unknown unknowns:

- **Known unknowns** (e.g., "we don't know what happens at 100% CPU") exist for all technology but are manageable.
- **Unknown unknowns** (e.g., "we didn't realize writes would trigger GC pauses") are vastly larger for new technology and far more dangerous.

## Optimize globally, not locally

McKinley argues forcefully against "best tool for the job" thinking. Every additional technology in the stack carries operational cost — monitoring, testing, onboarding, init scripts, cognitive overhead. The *true* best tool is the one that occupies the "least worst" position across as many problems as possible, because **the long-term cost of operating a system reliably dwarfs the short-term inconvenience of building it**.

This is a global optimization argument: local optima (picking the perfect tool for each sub-problem) produce a globally worse system when the interaction costs compound. McKinley draws on his Etsy experience, where the activity feeds system — built on the "boring" stack of PHP, MySQL, Memcached, and Gearman — later scaled 20x without targeted changes, precisely because a shared platform amplified every improvement.

## When to adopt something new

McKinley does not advocate never adding technology. He proposes a lightweight governance process:

1. **Try to solve the problem without adding anything new.** If the real motivation is that someone wants to use the shiny thing, stop here.
2. **Write down what makes the current stack prohibitively expensive** for this specific problem. Force the justification to be concrete.
3. **If the new choice overlaps existing tools, commit to migrating** the old functionality on a proposed timeline — avoid the "two databases forever" trap.
4. **Make it a company-wide conversation.** Technology choices have org-wide effects; they should not be unilateral.

## Implications

The essay has become a touchstone in engineering management and [[technology-strategy|technology strategy]] discussions. Its core insight — that novelty has a carrying cost that compounds across an organization — applies well beyond startups. It connects to broader ideas about [[engineering-simplicity|simplicity in engineering]] and the value of constraint as a creative force.

For founders and early-stage teams, the practical takeaway is stark: spend innovation tokens on your core differentiator (the thing that *is* your business), and ruthlessly default to boring everywhere else. The freedom that comes from technological restraint is the freedom to focus on harder, more important problems.

## Sources
- McKinley, Dan (2015). "Choose Boring Technology." <https://mcfunley.com/choose-boring-technology> — [[2015-03-30-choose-boring-technology|local copy]]
