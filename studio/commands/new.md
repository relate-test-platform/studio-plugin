---
description: Start a new prototype project from the studio template
argument-hint: "<project name> [for <client>]"
allowed-tools: mcp__plugin_studio_studio__create_project, mcp__plugin_studio_studio__get_project
---

Start a new Relate Studio project with the studio `create_project` tool.

1. Read the name and client from "$ARGUMENTS": "Booking app for Acme" means the name "Booking app" and the client "Acme". If there's no name, ask for one and stop.
2. Call `create_project`. It returns at once; setup carries on for about a minute.
3. Call `get_project` every few seconds until the status is `active` or `failed`. Tell the user how it's going now and then, not on every check.
4. When it's active, reply with the preview link, the GitHub repository, the local folder and the command that starts Claude in it: `cd "<folder>" && claude`.
5. If it failed, show the error and suggest retrying from the dashboard.

If the studio tools aren't available, the hub isn't running. Ask the user to start it with `npm run dev` in their `relate-studio/hub` folder, then try again.
