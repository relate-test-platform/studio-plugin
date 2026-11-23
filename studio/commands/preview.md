---
description: Update the team preview of the prototype you're working on
argument-hint: "[project name]"
allowed-tools: mcp__plugin_studio_studio__list_projects, mcp__plugin_studio_studio__get_project, mcp__plugin_studio_studio__update_preview
---

Update a prototype's team preview with the studio `update_preview` tool. Use the project named in "$ARGUMENTS". If no project is named, use the one whose code this session is in (the slug in `studio.json`); if that doesn't work either, call `list_projects` and ask which project.

1. Call `get_project` to see where the code lives and which prototypes it has.
2. Each prototype has its own team preview, built from its branch on GitHub: `main`, or `prototype/<id>` for a separate one. The prototype is the branch this folder is on (`git branch --show-current`).
   - **Save** the files (local only, nobody else sees them).
   - **Commit** them with a short message that says what changed (still local).
   - **Push** the branch. If the push is rejected because a teammate pushed first, `git pull --rebase`, check the result with the user, and push again. Never force-push.
3. On a hub running on this Mac (the project has a `folder`), the main prototype's preview is the folder as it is now, and separate prototypes have no preview.
4. Call `update_preview` with the prototype (the branch name). It takes about half a minute.

Only the team can open previews, and teammates signed in to the hub open them without a password. Reply with the preview link and the commit it shows. If it fails, show the error.

If the studio tools aren't available, or answer that Claude Code isn't connected, run `/studio:setup`: it connects Claude Code to the Designer Hub through the browser.
