---
description: Export a published version as a ZIP for developers
argument-hint: "[project name] [version]"
allowed-tools: mcp__plugin_studio_studio__list_projects, mcp__plugin_studio_studio__export_handoff
---

Export a developer handoff with the studio `export_handoff` tool.

1. Read the project and an optional version number from "$ARGUMENTS", for example "Booking app v3". If no project is named, call `list_projects` and use the one whose folder is the current working directory. Without a version, the latest published one is used.
2. Call `export_handoff`. The first export of a version installs, builds and tests it, which takes about 15 seconds.
3. Reply with the ZIP's path and what's inside: the product prototype without the review tool, `HANDOFF.md` with how to run it, and an empty `.env.example`. If it failed, show the error.

If the studio tools aren't available, the hub isn't running. Ask the user to start it with `npm run dev` in their `relate-studio/hub` folder, then try again.
