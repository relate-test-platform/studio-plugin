---
description: Export a published version as a ZIP for developers
argument-hint: "[project name] [version]"
allowed-tools: mcp__plugin_studio_studio__list_projects, mcp__plugin_studio_studio__get_project, mcp__plugin_studio_studio__export_handoff
---

Export a developer handoff of a published version.

1. Read the project and an optional version number from "$ARGUMENTS", for example "Booking app v3". If no project is named, use the one whose code this session is in, or call `list_projects` and ask. Without a version, use the latest live one from `get_project`.
2. If the project has a `folder` (the hub runs on this Mac), call `export_handoff`. The first export of a version installs, builds and tests it, which takes about 15 seconds. Reply with the ZIP's path.
3. On the hosted hub, build it in this session from the project's code instead:
   - Work in a clone of the project (offer to clone it first). Run `git fetch --tags`.
   - Copy the version out of git into a new empty folder outside the clone: `git archive v<number> | tar -x -C <folder>`.
   - In that folder, run `node scripts/handoff.mjs <output folder>`. In the output folder, run `npm ci`, `npm test` and `npm run build`. Stop and show the error if one fails.
   - Delete `node_modules` and `dist` from the output folder. Check that no file contains a password, token or key, then zip the folder as `<project slug>-v<number>-handoff.zip`.
4. Reply with the ZIP's path and what's inside: the product prototype without the review tool, `HANDOFF.md` with how to run it, and an empty `.env.example`.

If the studio tools aren't available, or answer that Claude Code isn't connected, run `/studio:setup`: it connects Claude Code to the Designer Hub through the browser.
