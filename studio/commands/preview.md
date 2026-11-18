---
description: Update a project's team preview with the latest changes
argument-hint: "[project name]"
allowed-tools: mcp__plugin_studio_studio__list_projects, mcp__plugin_studio_studio__get_project, mcp__plugin_studio_studio__update_preview
---

Update the team preview of the project named in "$ARGUMENTS" with the studio `update_preview` tool. If no project is named, use the one whose code this session is in (the slug in `studio.json`); if that doesn't work either, call `list_projects` and ask which project.

1. Call `get_project` to see where the code lives.
2. On the hosted hub (the project has no `folder`), the preview is built from the latest commit on GitHub `main`, so this is how changes reach the team:
   - **Save** the files (local only, nobody else sees them).
   - **Commit** them with a short message that says what changed (still local).
   - **Send them back** with `git push` to `main`. If the work is on another branch, ask before merging it into `main`.
3. On a hub running on this Mac (the project has a `folder`), `update_preview` deploys the folder as it is. Nothing needs pushing.
4. Call `update_preview`. It takes about half a minute.

Only the team can open the preview, and teammates signed in to the hub open it without a password. Reply with the preview link. If it fails, show the error.

If the studio tools aren't available, or answer that Claude Code isn't connected, run `/studio:setup`: it connects Claude Code to the Designer Hub through the browser.
