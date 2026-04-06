---
source: agent
compiled_from:
  - agent-notes/raw/engineering/computer/development/2026-04-04-stacked-pull-requests.md
compiled_at: 2026-04-04
model: claude-opus-4-6
confidence: medium
---

# Stacked Pull Requests

A code-review discipline in which a single large change is decomposed into a chain of dependent, individually-reviewable pull requests — each branch stacked on top of the previous one. The goal is to dodge "code review fatigue," where PRs past ~500 LOC tend to receive a perfunctory "looks fine" and little substantive feedback.

## The core idea

Small PRs get meaningfully reviewed. Large PRs do not. Splitting work into a stack of focused diffs — where each sits on the branch of its predecessor — preserves the coherence of a multi-commit change while dramatically increasing review depth.

## Workflow

### 1. Start with a WIP exploration branch

Cut `somefeature` off `master`, commit freely, open a WIP pull request early. The WIP phase is for figuring out what you're building and surfacing the plan to teammates — it doesn't get merged. Once the direction is clear, close the WIP PR (keep the branch as a backup) and begin the stack.

### 2. Build the stack one logical commit at a time

From the WIP branch, create `somefeature1` and reset it to `master` — this puts all WIP changes into the working tree as unstaged edits. Then, repeatedly:

1. `git add --patch` to stage a single logical slice.
2. `git stash --include-untracked --keep-index` + run tests to verify the slice is self-contained.
3. Commit, push, open a PR against the previous branch in the stack (using `hub pull-request -b <prev-branch>` or equivalent).
4. Create the next branch, `git stash pop`, and repeat.

The resulting git graph is linear: each branch's base is the branch before it, forming a chain off `master`.

### 3. Address feedback with merge, not rebase

When a reviewer's comments arrive on, say, `somefeature2`, commit the fix there, then **merge that branch up the stack** into `somefeature3`, `somefeature4`, etc. Avoid rebasing — rebasing forces per-commit conflict resolution, which is wasted effort given the stack is squashed on merge anyway. The same logic applies to staying current with `master`: merge it in, don't rebase onto it.

### 4. Land the stack LAST to FIRST

Counterintuitive but critical: merge the *top* of the stack first, then walk back down to PART1. Merging PART1 first leaves every dependent PR pointing at a deleted base branch, which breaks them. Landing from the top down keeps each remaining PR's base valid until its turn.

Result: a single, well-reviewed commit on `master` per stack element (or a squashed merge of the whole stack, depending on team convention).

## Why it works

- **Reviewer attention scales inversely with diff size.** A 200-line PR provokes ~10x the substantive comments of a 2000-line PR.
- **Decomposition forces clarity.** Splitting a change into logical commits surfaces design seams the author might have glossed over.
- **Stacks ship faster than mega-PRs.** Each slice can land as soon as it's approved, rather than waiting for a single monolithic review.

## Temporal notes (2026-04-04)

The article dates to **2016** and some specifics have shifted:

- **GitHub now supports changing a PR's base branch.** The "merging PART1 breaks everything downstream" claim in the original is outdated — you can retarget dependent PRs via the UI or API after landing the bottom of the stack. This makes bottom-up landing more viable than the article suggests, though top-down still avoids the retarget step entirely.
- **Dedicated stacked-diff tooling now exists.** Tools like Graphite, `gh stack`, `git-spice`, Sapling, and `spr` automate branch creation, rebasing across the stack, and PR retargeting — eliminating most of the manual `git add --patch` / stash choreography described here. The underlying discipline is the same; the ergonomics are dramatically better.
- **The `hub` CLI has been largely superseded by `gh`** (GitHub's official CLI), which provides equivalent PR-creation commands.

The *practice* of stacked PRs is more relevant than ever — the *mechanics* described in the 2016 article should be read as the manual-git-only version.

## Sources

- Koonce, Grayson (2016). "Stacked Pull Requests: Keeping GitHub Diffs Small." <https://web.archive.org/web/20200620103416/https://unhashable.com/stacked-pull-requests-keeping-github-diffs-small/> — [[2026-04-04-stacked-pull-requests|local copy]]
