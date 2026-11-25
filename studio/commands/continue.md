---
description: Continue work from one exact version or prototype of a studio project
argument-hint: "<project> <v<number> | prototype> [product|website] [commit]"
allowed-tools: mcp__plugin_studio_studio__get_project, mcp__plugin_studio_studio__list_projects, mcp__plugin_studio_studio__create_prototype, mcp__plugin_studio_studio__whoami, mcp__plugin_studio_studio__get_brand, mcp__plugin_studio_studio__list_files, Bash(gh repo clone:*), Bash(git -C:*), Bash(mkdir -p ~/Studio)
---

Continue work from exactly one version or prototype of a project. The canvas's **Copy command for Claude** button and the hub's Version history write this command for you, for example `/studio:continue rupex v3 website a5c363b`.

Read "$ARGUMENTS" as:

- the project, by slug or name;
- what to continue from: `v3` for published version 3, or a prototype by id or branch, such as `main` or `direction-b`;
- the part of the project: `product` for the app screens in `src/proto`, `website` for the site pages in `src/site`. When it's missing, use the one the project has, or ask when it has both;
- after a version, the first characters of its commit.

If no project is named, call `whoami` and use the project assigned to the user, or ask when there are several. If nothing to continue from is named, call `get_project`, list its live versions newest first (number, note, who published it or who saved it, when, and which one clients see) and its prototypes, then ask which one and stop.

1. **Find it.** Call `get_project`.
   - A version must be in `versions` with status `live` and a commit. When a commit was given, the version's commit must start with it. If the version is missing, failed, still publishing, or has a different commit, say exactly that and stop. Never continue from another version instead, and never fall back to the latest one.
   - A prototype must be in `prototypes` by id or branch. If it isn't, say so and stop.
   - If `get_project` says the project isn't there or you have no access, say so, suggest `/studio:setup`, and stop.
2. **Report the context before changing anything**, in a short list:
   - **Project:** its name and slug.
   - **Part:** Product or Website.
   - **Source:** for a version, `v3 "<note>"`, who published it (`publishedBy`, or "publisher not recorded" with `savedBy`), when, its short commit, and whether clients see it. For a prototype, its name, who started it, its branch and what it started from.
   - **Editing target:** filled in at step 5.
3. **Find the code on this computer**, as `/studio:open` does:
   - If this session is already in the project (`studio.json` has its slug), use it. On a hub running on a Mac with a `folder`, use that folder.
   - Otherwise use `~/Studio/<repository name>`. If it isn't there, run `mkdir -p ~/Studio` and `gh repo clone <owner>/<repository> ~/Studio/<repository name>`. If cloning says the repository doesn't exist, the user doesn't have access yet: tell them to run `/studio:setup` and stop.
4. **Protect unsaved work.** Run `git -C <folder> status --porcelain`. If it lists anything, stop: show the changed files and ask the user to commit them or put them aside themselves. Never reset, stash, discard or overwrite local changes.
5. **Set the editing target.**
   - **From a version:** call `create_prototype` with the project and `from_version` set to the number. The hub starts a new prototype at that version's exact published commit, names it after the version and the user (for example "From v3 · Yury"), and remembers it came from v3. The version itself stays published as it was. Then run `git -C <folder> fetch --quiet origin`, `git -C <folder> switch <new branch>`, and check that `git -C <folder> rev-parse HEAD` is the version's commit. If it isn't, stop and say so.
   - **From a prototype:** run `git -C <folder> fetch --quiet origin`, `git -C <folder> switch <branch>` and `git -C <folder> pull --ff-only`. Say that edits change this prototype for everyone working on it, and that `/studio:continue <project> v<number>` starts a separate one from a version instead.
   - Finish the report: **Editing target:** the prototype's name, its branch, and the commit it starts at.
6. **Get ready to work.** Read the project's `CLAUDE.md` and `studio.json`, and call `get_brand` and `list_files`. For Product, the screens live in `src/proto`. For Website, the pages are listed in `src/site/pages.json`, each page is `src/site/pages/<id>.tsx`, and shared sections are in `src/site/sections.tsx`. If this session isn't running in the project's folder, tell the user to start Claude there for the best results: `cd <folder> && claude`, then run this command again. Otherwise ask what to change.

While working on this branch:

- Commit with short messages that say what changed, and push the branch. If the push is rejected because a teammate pushed to the same branch first, run `git pull --rebase`, show the user what came in, and push again. Never force-push: it would throw away a teammate's work.
- `/studio:preview` updates this prototype's team preview. `/studio:publish <project>: <what changed>` publishes it as the next version. The hub records whoever publishes it, and shows that it came from the source version. It refuses a commit that isn't this prototype's latest save on GitHub, so nothing stale gets published.
- Publishing never changes what clients see. Someone approves a version in the hub for that. The source version stays published and can be reopened from the hub or the canvas at any time.

If the studio tools aren't available, or answer that Claude Code isn't connected, run `/studio:setup`: it connects Claude Code to the Designer Hub through the browser.
