---
description: List the studio's prototype projects
argument-hint: "[archived | deleted | all]"
allowed-tools: mcp__plugin_studio_studio__list_projects
---

List Relate Studio projects with the studio `list_projects` tool. Use the shelf named in "$ARGUMENTS" (archived, deleted or all); otherwise list active projects.

Reply with a compact table: name, client, status and preview link. Mention a local folder only for the project this session is working in.

If the studio tools aren't available, the hub isn't running. Ask the user to start it with `npm run dev` in their `relate-studio/hub` folder, then try again.
