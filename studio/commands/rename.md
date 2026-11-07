---
description: Rename a studio project or change its client
argument-hint: "<project> to <new name>"
allowed-tools: mcp__plugin_studio_studio__update_project
---

Rename a project with the studio `update_project` tool. Read the project and its new name from "$ARGUMENTS", for example "Booking app to Booking". When the user asks to change the client instead, pass `client`. Ask for anything that's missing.

Only the name people see changes; the project's address and links stay the same. Confirm the result in one line.
