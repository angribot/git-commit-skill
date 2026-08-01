---
name: git-commit
description: Commit staged or unstaged work to Git. Use when the user asks to commit changes, or when another skill needs the commit procedure.
---

# Git Commit

Commit the current task's work, and only that work.

1. Run `git status --short` and `git diff`. Continue once every changed path in the worktree is accounted for as either part of this task or unrelated.
2. Stage the task's changes with `git add <paths>` or `git add -p`. Continue once the index holds the complete task and nothing else.
3. Run `git diff --cached --check`, then review `git diff --cached`. If the staged diff contains changes outside this task, stop and report them to the user.
4. Write the message with an English Conventional Commit header, `type(scope): description` (scope optional), and an imperative subject of at most 72 characters.
5. Run `git commit`, letting every hook run. The step is done when the commit succeeds; if a hook rejects it, fix the cause and commit again.
6. Run `git status --short` and report the new commit plus whatever remains uncommitted.

## Guardrails

Amend, rebase, push, force-push, or otherwise rewrite history only when the user explicitly asks for it.
