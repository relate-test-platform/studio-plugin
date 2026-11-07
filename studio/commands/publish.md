---
description: Publish the next version of a project for the client
argument-hint: "[project name]: <what changed>"
allowed-tools: mcp__plugin_studio_studio__list_projects, mcp__plugin_studio_studio__get_project
---

Publish a client version with the studio `publish_version` tool.

1. Read the project and the note from "$ARGUMENTS": "Booking app: new checkout step" means the project "Booking app" and the note "New checkout step". If no project is named, call `list_projects` and use the one whose folder is the current working directory. If there's no note, ask what changed and stop.
2. The note is shown to the client. Keep it to one plain sentence under 200 characters.
3. Call `publish_version`. It commits and pushes the folder, then publishes in the background for about a minute.
4. Call `get_project` every 15 seconds until the new version is `live` or `failed`. Don't report every check.
5. When it's live, reply with the version number, the client link (it now opens this version) and the version's own link. Clients sign in with the login `client` and the client password shown in the dashboard.
6. If it failed, show the error and suggest trying again from the dashboard or with this command.

If the studio tools aren't available, the hub isn't running. Ask the user to start it with `npm run dev` in their `relate-studio/hub` folder, then try again.
