---
name: git-commit
description: Git rules for safe staging, the commit message format, never-allowed commands, and rebase-conflict handling. Read before any commit, merge, or rebase.
---

# Git

Multiple sessions may be running in this cwd at the same time, each modifying different files. Git operations that touch unstaged, staged, or untracked files outside your own changes will stomp on other sessions' work.

## Committing

1. Run `git status` and account for every changed path before staging. In a shared worktree, leave paths belonging to other sessions untouched.
2. Prefer explicit staging (`git add <path1> <path2>`). Before committing, inspect `git diff --cached` and ensure it contains only the intended changes.
3. Use the Conventional Commits format `<type>[(scope)]: <commit message>` when this repository expects it. Keep the message informative and concise; keep hooks enabled.
4. For squash merges, pass an explicit Conventional Commit subject (`gh pr merge --squash --subject "..."`).

## Destructive or history-changing operations

Before discarding work, cleaning files, stashing, resetting, rebasing, or rewriting a remote branch, inspect the current state and make the scope explicit. Prefer reversible or narrow operations:

- Use `git restore <path>` or `git restore --staged <path>` for targeted changes.
- Use `git stash push -m "<description>" -- <paths>` when a stash is needed; verify its contents before dropping it.
- Before `git clean`, run `git clean -nd` and confirm the paths. Use `-i` when the scope is uncertain.
- Use `git reset --hard` only after confirming that all affected local work may be discarded.
- Never bypass hooks with `git commit --no-verify`.
- Use `--force-with-lease` only for a personal branch after rebase or another deliberate history rewrite; do not force-push shared or protected branches.

## Rebase conflicts

- Resolve conflicts only when you can account for the affected files and intended changes.
- If a conflict involves work from another session or an unclear ownership boundary, stop and ask the user.
- After resolving, inspect the diff and status before continuing.
