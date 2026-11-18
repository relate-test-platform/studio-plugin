---
description: Open a studio project to work on it
argument-hint: "<project name>"
allowed-tools: mcp__plugin_studio_studio__get_project, mcp__plugin_studio_studio__list_projects, mcp__plugin_studio_studio__get_brand, mcp__plugin_studio_studio__list_files
---

Find the project named in "$ARGUMENTS" with the studio `get_project` tool. If no name was given, call `list_projects` and ask which one.

- If this session is already in the project's code (its `studio.json` has the project's slug), run `git pull` when it's a clone, read `CLAUDE.md` and `studio.json`, and call `get_brand` and `list_files` for the project. Sum up in a few lines: the flows and screens in `src/proto/flows.ts`, the brand, and the files the studio keeps. Then ask what to work on.
- If the project has a `folder` (the hub runs on this Mac), show the preview link and the command that starts Claude there: `cd "<folder>" && claude`. Offer to carry on from this session with full paths instead.
- Otherwise, show the preview link and offer to run the project's `clone` command in the current folder, then give `cd <repository name> && claude`. If the code is already cloned nearby, use that copy and `git pull` instead.

If the studio tools aren't available or answer that a token is missing or invalid, Claude isn't connected to the hub. Ask the user to open their Designer Hub profile, create an API token under API tokens, add the two lines it shows to the `env` section of `~/.claude/settings.json`, and restart Claude.
