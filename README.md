# Relate Studio plugin for Claude Code

The `studio` plugin connects Claude Code to the Relate Designer Hub, so you can open the projects you're assigned to, design with their brand and files, and update their team previews.

## Set up (once per computer)

You need [Claude Code](https://claude.ai/download) and the [GitHub CLI](https://cli.github.com) (`brew install gh` on a Mac). Then paste this in Terminal:

```bash
claude plugin marketplace add relate-test-platform/studio-plugin; claude plugin install studio@relate-studio; claude "/studio:setup"
```

`/studio:setup` walks you through the rest and skips what's already done:

1. **Designer Hub.** If Claude Code isn't connected yet, type `/mcp`, choose **studio** and **Authenticate**. Your browser opens the hub; click **Connect**. No tokens to copy.
2. **GitHub.** If you aren't signed in, type `! gh auth login --web --git-protocol https` and sign in with your own GitHub account in the browser.
3. **Access.** It links your GitHub account to the hub, and accepts the studio's invitations to the repositories of the projects you're assigned to. Access covers those projects only.

Run `/studio:setup` again whenever something seems off or a new project is assigned. It's safe to repeat.

## Work on a project

- `/studio:open <project>` finds or clones the code into `~/Studio/<repository>`. It updates it only when you have no local changes, and never overwrites your work. The project page in the hub has the same thing as **Open in Claude Code**.
- `/studio:continue <project> v<number> [product|website]` continues from one published version, including a teammate's. It reports the project, part, source version and its publisher, then starts a separate prototype at that version's exact commit, so the original stays as it was. In the canvas or the hub's Version history, **Copy command for Claude** writes this command for the version you're looking at; paste it into Claude Code.
- Ask Claude for screens and flows in plain words. It designs with the project's brand (`get_brand`) and the files the studio keeps (`list_files`).

| Step | What it does | Who sees it |
|---|---|---|
| Save | Files change on your computer | Only you |
| Commit | Records the change locally with a short message | Only you |
| Send back (`git push`) | Uploads your commits to the project's repository | The team, in the code |
| `/studio:preview` | The hub rebuilds the team preview from the latest pushed code | The team, behind Designer Hub sign-in |
| `/studio:publish` | Publishes a numbered version for the client | Clients, once it's approved in the hub |

Team previews open from the hub with your Designer Hub sign-in; there's no separate preview password. You never need your own Vercel account: the hub builds previews.

## Commands

| Command | What it does |
|---|---|
| `/studio:setup` | Connects this computer to the hub and GitHub, and checks your project access |
| `/studio:open <project>` | Opens a project from its checkout in `~/Studio` |
| `/studio:continue <project> <v<number> \| prototype> [product\|website]` | Continues from one exact version (in a separate prototype) or prototype |
| `/studio:preview [project]` | Sends your committed changes and updates the team preview |
| `/studio:publish [project]: <what changed>` | Publishes the next client version |
| `/studio:new <name> [for <client>]` | Starts a new prototype project |
| `/studio:handoff [project] [version]` | Packages a published version for developers |
| `/studio:list`, `/studio:rename`, `/studio:archive`, `/studio:restore` | Lists, renames, archives and restores projects |

To work against a hub running on your Mac, install the plugin from a local checkout and change the address in `studio/.mcp.json`.
