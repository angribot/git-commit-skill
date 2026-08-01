# git-commit-skill

An AI agent skill for creating safe, focused, and consistent Git commits.

When asked to commit changes, this skill:

- Reviews the working tree and separates task-related changes from unrelated work.
- Stages and commits only the files that belong to the current task.
- Validates and reviews the staged diff before committing.
- Uses English Conventional Commits messages.
- Runs Git hooks and reports the resulting commit and any remaining changes.

Unless explicitly requested, the skill does not amend commits, rebase branches, push changes, force-push, or otherwise rewrite Git history.
