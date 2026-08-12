# git-commit

The Git section of AGENTS.md, extracted as a skill — the rules for git operations where multiple sessions may share the working tree:

- Commit only files YOU changed in THIS session; stage explicit paths, never `git add -A` / `git add .`.
- Commit message format: `{feat,fix,docs}[(scope)]: <commit message>` (optionally multiple lines), informative and concise.
- Never run `git reset --hard`, `git checkout .`, `git clean -fd`, `git stash`, `git add -A`, `git add .`, `git commit --no-verify`.
- Rebase conflicts: resolve only files you modified; if a conflict is in a file you did not modify, abort and ask the user; never force push.
