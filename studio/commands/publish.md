---
description: Publish the next version of a project for the client
argument-hint: "[project name]: <what changed>"
allowed-tools: mcp__plugin_studio_studio__list_projects, mcp__plugin_studio_studio__get_project, mcp__plugin_studio_studio__publish_version
---

Publish a client version with the studio `publish_version` tool.

1. Read the project and the note from "$ARGUMENTS": "Booking app: new checkout step" means the project "Booking app" and the note "New checkout step". If no project is named, use the one whose code this session is in (the slug in `studio.json`), or call `list_projects` and ask. If there's no note, ask what changed and stop.
2. The note is shown to the client. Keep it to one plain sentence under 200 characters.
3. Call `get_project`. On the hosted hub (no `folder`), the version is built from the latest commit on GitHub `main`: commit uncommitted changes, push to `main`, and ask before merging another branch. On a hub running on this Mac, `publish_version` commits and pushes the folder itself.
4. Call `publish_version`. It publishes in the background for about a minute.
5. Call `get_project` every 15 seconds until the new version is `live` or `failed`. Don't report every check.
6. When it's live, reply with the version number, the version's own link and the client link, which now opens this version. Clients see it in the Client Hub once someone approves it in the hub: the project's Client access, then Prototype, then Approve. They open it there with their own Client Hub login.
7. If it failed, show the error and suggest trying again from the hub or with this command.

If the studio tools aren't available or answer that a token is missing or invalid, Claude isn't connected to the hub. Ask the user to open their Designer Hub profile, create an API token under API tokens, add the two lines it shows to the `env` section of `~/.claude/settings.json`, and restart Claude.
