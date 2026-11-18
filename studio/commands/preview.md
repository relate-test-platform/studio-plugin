---
description: Update a project's team preview with the latest changes
argument-hint: "[project name]"
allowed-tools: mcp__plugin_studio_studio__list_projects, mcp__plugin_studio_studio__get_project, mcp__plugin_studio_studio__update_preview
---

Update the team preview of the project named in "$ARGUMENTS" with the studio `update_preview` tool. If no project is named, use the one whose code this session is in (the slug in `studio.json`); if that doesn't work either, call `list_projects` and ask which project.

1. Call `get_project` to see where the code lives.
2. On the hosted hub (the project has no `folder`), the preview is built from the latest commit on GitHub `main`. Run `git status`. Commit uncommitted changes with a short message that says what changed, then push to `main`. If the work is on another branch, ask before merging it into `main`.
3. On a hub running on this Mac (the project has a `folder`), `update_preview` deploys the folder as it is. Nothing needs pushing.
4. Call `update_preview`. It takes about half a minute.

Only the team can open the preview, and teammates signed in to the hub open it without a password. Reply with the preview link. If it fails, show the error.

If the studio tools aren't available or answer that a token is missing or invalid, Claude isn't connected to the hub. Ask the user to open their Designer Hub profile, create an API token under API tokens, add the two lines it shows to the `env` section of `~/.claude/settings.json`, and restart Claude.
