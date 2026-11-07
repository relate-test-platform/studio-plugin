---
description: Open a studio project to work on it
argument-hint: "<project name>"
allowed-tools: mcp__plugin_studio_studio__get_project, mcp__plugin_studio_studio__list_projects
---

Find the project named in "$ARGUMENTS" with the studio `get_project` tool. If no name was given, call `list_projects` and ask which one.

- If this session is already working in the project's folder, read its `CLAUDE.md` and `studio.json`, sum up the flows and screens in `src/proto/flows.ts` in a few lines, and ask what to work on.
- Otherwise, show the preview link and the folder, and the command that starts Claude there: `cd "<folder>" && claude`. Offer to carry on from this session with full paths instead.

If the studio tools aren't available, the hub isn't running. Ask the user to start it with `npm run dev` in their `relate-studio/hub` folder, then try again.
