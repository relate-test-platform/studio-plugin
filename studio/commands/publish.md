---
description: Publish the next version of one prototype of a project
argument-hint: "[project name]: <what changed>"
allowed-tools: mcp__plugin_studio_studio__list_projects, mcp__plugin_studio_studio__get_project, mcp__plugin_studio_studio__publish_version
---

Publish one prototype of a project, at one exact commit, with the studio `publish_version` tool.

1. Read the project and the note from "$ARGUMENTS": "Booking app: new checkout step" means the project "Booking app" and the note "New checkout step". If no project is named, use the one whose code this session is in (the slug in `studio.json`), or call `list_projects` and ask. If there's no note, ask what changed and stop.
2. The note is shown to the client. Keep it to one plain sentence under 200 characters.
3. Work out which prototype this is. It's the branch this folder is on (`git branch --show-current`): `main` is the project's first prototype, and `prototype/<id>` is a separate one someone started. `get_project` lists the prototypes by name. If the branch isn't one of them, stop and ask.
4. Make sure GitHub has exactly what should be published. Commit the changes that belong in this version, then `git push`. If the push is rejected because a teammate pushed first, run `git pull --rebase`, check the result with the user, and push again. Never force-push: it would throw away a teammate's work.
5. Read the commit with `git rev-parse HEAD`, and call `publish_version` with the prototype (the branch name) and that commit. The hub refuses a commit that isn't on GitHub, or that isn't the prototype's latest save, and says which save it has. Sort that out and try again; never publish another prototype or commit instead.
6. Call `get_project` every 15 seconds until the new version is `live` or `failed`. Don't report every check.
7. When it's live, reply with the version number, the prototype's name, the short commit and the version's own link. Publishing doesn't change what clients see: they get a version once someone approves it in the hub (the project's Client access, then Prototype, then Approve), and the client link then opens it.
8. If it failed, show the error. Trying again from the hub's Version history publishes the same commit.

If the studio tools aren't available, or answer that Claude Code isn't connected, run `/studio:setup`: it connects Claude Code to the Designer Hub through the browser.
