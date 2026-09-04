# pr-skill

A Claude Code plugin that analyzes the commits on the current branch and creates a well-documented pull request, as a skill and slash command.

## Contents

| Type | Name | Description |
|---|---|---|
| Skill | `pr` | Auto-triggered workflow: analyze commits since the base branch, draft title/description, create the PR |
| Command | `/pr` | Explicitly kick off the pull request workflow |

## How it works

The skill inspects the commits and diff between the current branch and its base (`main` by default), drafts a title and a description following the template below, and opens the PR with `gh pr create`.

```markdown
## Summary
Brief description of changes

## Changes
- List of specific changes made

## Screenshots
(if applicable)
```

If the branch has no commits ahead of the base, the skill reports that and does not create a PR.

## How to Use

1. Add the marketplace and install the plugin (once per machine):

   ```
   /plugin marketplace add kudima03/claude-plugins
   /plugin install pr-skill@kudima03
   ```

2. Push the branch you want to open a PR from (the skill will push it for you if it has no upstream yet).

3. Trigger the workflow either by:
   - Running the command explicitly: `/pr`
   - Or just asking Claude Code to open a PR for your branch — the skill auto-triggers on requests like "open a PR" or "create a pull request"

4. Review the PR URL Claude Code reports.

## Prerequisites

- [Claude Code](https://claude.ai/code)
- `gh` (GitHub CLI) installed and authenticated
- `git` with commits on the current branch ahead of the base branch
