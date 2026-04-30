---
source: agent
compiled_from:
  - agent-notes/raw/engineering/computer/development/2014-08-30-git-commit-messages.md
compiled_at: 2026-04-30
model: claude-opus-4-7
confidence: high
---

# Git Commit Messages

A discipline for writing the prose that accompanies every commit. The diff records *what* changed; only the message can record *why*. Beams argues a well-cared-for log turns `git blame`, `revert`, `rebase`, `log`, and `shortlog` from chores into instruments — and that "a commit message shows whether a developer is a good collaborator" (quoting Peter Hutterer).

## The seven rules

A widely-cited convention codified by Chris Beams in 2014, distilled from earlier writing by Tim Pope, Linus Torvalds, and the Git project itself:

1. **Separate subject from body with a blank line.** Many Git tools (`format-patch`, `log --oneline`, `shortlog`) parse the first line as the subject; without the blank line they break.
2. **Limit the subject line to ~50 characters.** Not a hard limit — a forcing function for concision. GitHub warns at 50, truncates at 72.
3. **Capitalize the subject line.** Trivial but consistent.
4. **Do not end the subject line with a period.** Punctuation wastes space in a constrained slot.
5. **Use the imperative mood in the subject line.** "Fix bug" not "Fixed bug" or "Fixes bug." Match what Git itself produces for `merge`, `revert`, etc. The test: *"If applied, this commit will ___."*
6. **Wrap the body at 72 characters.** Git never wraps automatically; do it manually so logs stay readable in 80-column terminals.
7. **Use the body to explain *what* and *why*, not *how*.** The diff shows how. Prose should record the problem being solved, the prior state and what was wrong with it, and why this solution was chosen over alternatives.

## Why bother

Beams frames the cost of bad commit logs as a vicious cycle: when history is unstructured, nobody reads it, so nobody invests in writing it well, so it stays unstructured. His core claim: re-establishing context for old code is expensive, and a good commit message is the cheapest way to amortize that cost across a project's lifetime. The future maintainer benefiting from the message is often the original author six months later.

Not every commit needs a body — `Fix typo in user guide` is fine alone. The discipline is knowing when one is warranted: any change whose motivation isn't obvious from the diff.

## Adoption beyond the seven rules

The 2014 essay is the most-linked single reference for commit-message style; many open-source contribution guides cite it directly. Two notable evolutions since:

- **[Conventional Commits](https://www.conventionalcommits.org/)** (2018) extends rule 5 with a structured prefix grammar — `feat:`, `fix:`, `chore:`, plus optional scope and `BREAKING CHANGE:` footers — designed to drive automated changelog generation and semver bumps. It's compatible with the seven rules but adds machine-readable structure on top of them.
- **Trailers** (`Co-Authored-By:`, `Signed-off-by:`, `Resolves: #123`) are now first-class in Git's tooling (`git interpret-trailers`), formalizing the metadata patterns Beams mentioned in passing.

## Connections

- **[[stacked-pull-requests]]** — the same atomic-commit instinct underlies stacked PRs. Beams's tip ("if you're having a hard time summarizing, you might be committing too many changes at once") is the seed of the atomic-commit / decomposed-PR discipline.
- **[[low-tech-devex]]** — Beams's closing pitch ("learn to love the command line, leave the IDE behind") is a precursor of the same argument: text-based, composable Git tooling beats GUI integrations once you've internalized the verbs.

## Sources

- Beams, Chris (2014). "How to Write a Git Commit Message." <https://cbea.ms/git-commit/> — [[2014-08-30-git-commit-messages|local copy]]
