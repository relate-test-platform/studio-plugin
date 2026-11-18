---
description: Set up this computer for studio work, or check that it still is
allowed-tools: mcp__plugin_studio_studio__whoami, mcp__plugin_studio_studio__link_github, Bash(gh --version), Bash(gh auth status:*), Bash(gh api user --jq .login), Bash(gh api user/repository_invitations:*), Bash(gh api --method PATCH user/repository_invitations/:*)
---

Set this computer up for Relate Studio work. Each step checks what's already done, so this is safe to run again at any time, for example after an interruption or when a new project is assigned.

1. **Designer Hub.** Call the studio `whoami` tool.
   - If the studio tools aren't available or say Claude Code isn't connected, tell the user to type `/mcp`, choose **studio** and **Authenticate**. Their browser opens the Designer Hub; they sign in if asked and click **Connect**. Then stop and ask them to run `/studio:setup` again.
   - If it works, note their name, their GitHub username (if any) and their projects.
2. **GitHub CLI.** Run `gh --version`. If it's missing, tell the user to install it (`brew install gh` on a Mac, or https://cli.github.com), then run `/studio:setup` again. Stop.
3. **GitHub sign-in.** Run `gh auth status`. If they aren't signed in, tell them to type exactly `! gh auth login --web --git-protocol https` here, follow the browser sign-in with their own GitHub account, then run `/studio:setup` again. Stop. Never ask for a GitHub password or token.
4. **Link GitHub.** Run `gh api user --jq .login`. If `whoami` showed no GitHub username, or a different one, call `link_github` with this login. That asks GitHub to invite them to the repositories of their assigned projects.
5. **Accept invitations.** Run `gh api user/repository_invitations --jq '.[] | select(.repository.owner.login == "relate-test-platform") | "\(.id) \(.repository.full_name)"'`. Accept each one with `gh api --method PATCH user/repository_invitations/<id>`. These are the studio's own invitations for their projects; don't accept invitations from other owners.
6. **Check.** Call `whoami` again. For each project, report one line:
   - `ready`: give its open command, the `open` value.
   - `invited`: the invitation is still pending; GitHub can take a minute. Run `/studio:setup` again.
   - `needs-github`: GitHub isn't linked yet; repeat step 4.
   - `failed`: show the error and say an admin can retry it from the project's **Team access** in the Designer Hub.

Finish with what to do next: open a project with `/studio:open <project>`, or paste its open command in Terminal. If they have no projects yet, say that a manager assigns them in the Designer Hub, and that this setup doesn't need repeating after that.
