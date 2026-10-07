---
name: git-commit
description: Git safety and commit conventions. Read before staging, committing, merging, rebasing, stashing, restoring, cleaning, resetting, or force-pushing.
---

# Git

Several sessions may share this working tree and index, so the diff carries **orphans**: changed paths, hunks, and index entries that belong to other tasks. Leave orphans in place and stay inside your task's scope.

## Committing

Done when the commit exists, the index holds nothing but this task's changes, and no hook was bypassed.

1. Stage explicit paths (`git add -- <paths>`), or for a mixed file stage only its intended hunks.
2. Inspect `git diff --cached`. When an orphan is staged, unstage it, keep the work, and ask the user before committing, naming the paths involved so they can sequence the commits.
3. Write the subject as `<type>[(scope)]: <subject>`, and pass that same subject explicitly to a squash merge (`gh pr merge --squash --subject "..."`).
4. Keep hooks enabled; a hook that fails or modifies files means fixing the cause and running the staging inspection again.

## History-changing commands

Two similar commands sit one keystroke apart here, and the wrong one destroys work. Each row pairs the command that keeps the work recoverable with the one that discards it; the right column needs the user's authorization for the specific work it destroys.

| Safe form | Destructive form |
|---|---|
| `git restore --staged -- <paths>` — unstages, keeps the edits | `git restore -- <paths>` — discards unstaged edits |
| `git stash push -m "<why>" -- <paths>` — purpose message, path scope | bare `git stash` — wide and anonymous |
| `git clean -n` with the planned pathspecs and filters — this list is the true deletion scope | `git clean -f` |
| `--force-with-lease` after a deliberate rewrite of a branch you own | `--force` on a shared or protected branch |

`git reset --hard` is the one command here with no safe form: it discards every path it touches, so it waits until you have confirmed each affected path is disposable.

## Rebase conflicts

Resolve a conflict when every affected file is one this task touched. When a conflict carries another session's work, stop and ask the user.
