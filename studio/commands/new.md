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
   - If it has a `clone` command (the hosted hub), offer to run it in the current folder. Then give `cd <repository name> && claude` to start working in it. A permission error means the user's GitHub account isn't in the studio's GitHub organisation yet: they should ask an admin.
5. If it failed, show the error and suggest trying again from the hub.

If the studio tools aren't available or answer that a token is missing or invalid, Claude isn't connected to the hub. Ask the user to open their Designer Hub profile, create an API token under API tokens, add the two lines it shows to the `env` section of `~/.claude/settings.json`, and restart Claude.
