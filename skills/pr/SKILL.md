---
description: "Create a well-documented pull request from the commits on the current branch"
allow-tools: ["Bash"]
model: claude-sonnet-5
---

# Pull Request

Analyze the commits on the current branch since it diverged from the base branch and create a well-documented pull request.

## Instructions

1. Run `git status --porcelain` to check for uncommitted or untracked changes. If there are any, stage them and use the `semantic-commit` skill to commit them before continuing — do not open a PR with a dirty working tree.
2. Determine the base branch (default to `main`) and inspect what will go into the PR:
   - `git log <base>..HEAD --oneline` for the commit list
   - `git diff <base>...HEAD` for the full change set
3. Generate a descriptive PR title summarizing the change
4. Create a detailed description following the PR Template below:
   - Summary of the changes and why they were made
   - A bullet list of specific changes
   - A Screenshots section noting that screenshots should be added manually if the change is UI-facing (the skill cannot capture them)
5. Create the PR with `gh pr create --title "<title>" --body "<description>"`
6. Report the PR URL returned by `gh pr create`

## PR Template

```markdown
## Summary
Brief description of changes

## Changes
- List of specific changes made

## Screenshots
(if applicable)
```

## Important Notes

- If the current branch has no commits ahead of the base branch, inform the user and do not create a PR
- If the branch has no upstream, push it first (`git push -u origin <branch>`) before running `gh pr create`
- Never mention Claude, an AI assistant, or a session/tool in the PR title or description
