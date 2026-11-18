---
description: Start a new prototype project from the studio template
argument-hint: "<project name> [for <client>]"
allowed-tools: mcp__plugin_studio_studio__create_project, mcp__plugin_studio_studio__get_project
---

Start a new Relate Studio project with the studio `create_project` tool.

1. Read the name and client from "$ARGUMENTS": "Booking app for Acme" means the name "Booking app" and the client "Acme". If there's no name, ask for one and stop.
2. Call `create_project`. It returns at once; setup carries on for about a minute.
3. Call `get_project` every few seconds until the status is `active` or `failed`. Tell the user how it's going now and then, not on every check.
4. When it's active, reply with the team preview link and the GitHub repository. Teammates signed in to the hub open the preview without a password.
   - If the project has a `folder` (the hub runs on this Mac), give the command that starts Claude there: `cd "<folder>" && claude`.
   - On the hosted hub, offer to open it with `/studio:open <name>`: it clones the code into `~/Studio` and checks access. A repository the user can't see means their setup isn't finished: run `/studio:setup`.
5. If it failed, show the error and suggest trying again from the hub.

If the studio tools aren't available, or answer that Claude Code isn't connected, run `/studio:setup`: it connects Claude Code to the Designer Hub through the browser.
