---
name: git-commit
description: Commit task changes when the user requests a commit or another skill needs the commit procedure.
---

# Git Commit

Commit exactly the current task's work.

1. Run `git status --short`, `git diff`, and `git diff --cached`. Continue once every changed path and hunk is accounted for as task-related or unrelated.
2. Stage only task-related changes. Use `git add <paths>` when the whole path belongs to the task; otherwise use `git add -p`. Continue once the index contains all and only the task's changes.
3. Run `git diff --cached --check` and review `git diff --cached`. Fix task-related errors. If any staged hunk belongs to unrelated work, stop and report it to the user. Continue once the check passes and every staged hunk belongs to the task.
4. Compose an English Conventional Commit message with the header `type(scope): description` (scope optional). Phrase the description imperatively and keep the header within 72 characters.
5. Run `git commit` and allow every hook to complete. If a hook fails or changes files, inspect the result and repeat the staging checks before retrying. Fix only task-related causes; report unrelated failures.
6. Run `git status --short`. Report the new commit hash and subject, plus any remaining uncommitted changes.
