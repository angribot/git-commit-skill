---
name: git-commit
description: Git safety and commit conventions. Read before staging, committing, merging, rebasing, stashing, restoring, resetting, cleaning, or force-pushing.
---

# Git

Multiple sessions may share this working tree and index. Preserve unrelated changes and continue within your task's scope; unrelated working-tree changes alone are not a blocker.

## Committing

1. Run `git status` and inspect the diff to identify the changes intended for this commit. If a file mixes your changes with unrelated edits, identify the intended hunks; ask the user only if inspection cannot establish a safe boundary.
2. Stage explicit paths (`git add -- <paths>`) or only the intended hunks of mixed files. Before committing, inspect `git diff --cached` and ensure it contains only the intended changes. If the index contains unrelated changes, preserve them and ask the user how to coordinate the commit.
3. Follow the repository's message convention, using `<type>[(scope)]: <commit message>` when it expects Conventional Commits. Keep hooks enabled and fix hook failures rather than bypassing them.
4. For squash merges, pass an explicit subject following the same convention (`gh pr merge --squash --subject "..."`).

## Destructive or history-changing operations

Before discarding work, cleaning files, stashing, resetting, rebasing, or rewriting a remote branch, inspect the current state and make the scope explicit. Prefer reversible or narrow operations:

- To unstage your changes while preserving working-tree edits, use `git restore --staged -- <paths>`.
- `git restore -- <paths>` discards unstaged edits. Use it only when the user has authorized discarding those edits.
- Use `git stash push -m "<description>" -- <paths>` when a stash is needed; verify its contents before dropping it.
- Before `git clean`, preview the exact deletion scope with `-n`, matching the planned pathspecs and filtering flags. Confirm the listed paths may be deleted; ask the user if uncertain.
- Use `git reset --hard` only after confirming that all affected local work may be discarded.
- Use `--force-with-lease` only for a personal branch after rebase or another deliberate history rewrite; do not force-push shared or protected branches.

## Rebase conflicts

- Resolve conflicts only when you can account for the affected files and intended changes.
- If a conflict involves work from another session or an unclear ownership boundary, stop and ask the user.
- After resolving, inspect the diff and status before continuing.
