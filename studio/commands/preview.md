---
description: Update a project's team preview from its folder
argument-hint: "[project name]"
allowed-tools: mcp__plugin_studio_studio__list_projects, mcp__plugin_studio_studio__update_preview
---

Update the team preview of the project named in "$ARGUMENTS" with the studio `update_preview` tool. If no project is named, call `list_projects` and use the one whose folder is the current working directory; if none matches, ask which project.

It deploys the folder as it is now and takes about half a minute. Only the team signs in on the preview; clients never see it. When it's done, reply with the preview link. If it fails, show the error.

If the studio tools aren't available, the hub isn't running. Ask the user to start it with `npm run dev` in their `relate-studio/hub` folder, then try again.
