---
description: Open a studio project to work on it
argument-hint: "<project name> [prototype]"
allowed-tools: mcp__plugin_studio_studio__get_project, mcp__plugin_studio_studio__list_projects, mcp__plugin_studio_studio__create_prototype, mcp__plugin_studio_studio__whoami, mcp__plugin_studio_studio__get_brand, mcp__plugin_studio_studio__list_files, Bash(gh repo clone:*), Bash(git -C:*), Bash(mkdir -p ~/Studio)
---

Open the project named in "$ARGUMENTS". If no name was given, call `whoami` and use the project assigned to the user, or ask which one when there are several.

1. Call `get_project` for its repository (`code`) and, on a hub running on a Mac, its `folder`.
2. Find the code on this computer.
   - If this session is already in the project (`studio.json` has its slug), use it.
   - On a Mac hub with a `folder`, use that folder.
   - Otherwise use `~/Studio/<repository name>`. If it isn't there, run `mkdir -p ~/Studio` and `gh repo clone <owner>/<repository> ~/Studio/<repository name>`. If cloning says the repository doesn't exist, the user doesn't have access yet: tell them to run `/studio:setup`.
3. Bring it up to date safely. Run `git -C <folder> status --porcelain`. Only when it's empty, run `git -C <folder> fetch --quiet origin` and `git -C <folder> pull --ff-only`. Never reset, stash, discard or overwrite local changes. If there are changes, leave them and say so.
4. Pick the prototype. `get_project` lists them with their names, branches and who started them. If "$ARGUMENTS" names one, or the user asks for a teammate's prototype, switch to its branch with `git -C <folder> switch <branch>` (only when there are no local changes). Say which prototype the session is on.
   - Editing a prototype changes it for everyone who works on it, and teammates' pushes arrive with `git pull`.
   - To try an alternative without changing it, call `create_prototype` with a name and the prototype to copy, then `git -C <folder> fetch --quiet origin` and `git -C <folder> switch <new branch>`.
5. Read the project's `CLAUDE.md` and `studio.json`. Call `get_brand` and `list_files`. In a few lines, sum up its screens and flows, its brand and the files the studio keeps.
6. If this session isn't running in the project's folder, tell the user to start Claude there for the best results: `cd <folder> && claude`. Otherwise ask what to work on.

If the studio tools aren't available, or answer that Claude Code isn't connected, run `/studio:setup`: it connects Claude Code to the Designer Hub through the browser.
