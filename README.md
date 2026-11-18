# Relate Studio plugin for Claude

The `studio` plugin connects Claude Code to the Relate Designer Hub. With it, Claude can:

- start a prototype project from the studio template, open it and clone its code;
- design with the project's brand and the files the studio keeps, and save new files back to the hub;
- update the team preview, publish client versions and package handoffs for developers;
- add screens, dialogs, flows and scenarios the way the template expects.

## Install

```bash
claude plugin marketplace add <this repository>
claude plugin install studio@relate-studio
```

## Connect it to the hub

1. Open your profile in the Designer Hub and create a token under API tokens.
2. Add the two lines the hub shows to the `env` section of `~/.claude/settings.json`:

   ```json
   {
     "env": {
       "STUDIO_HUB_URL": "https://relate-designer-hub.vercel.app",
       "STUDIO_HUB_TOKEN": "<your token>"
     }
   }
   ```

3. Restart Claude. `/studio:list` shows the studio's projects when it's connected.

The token acts as you, with your hub level, until you revoke it on your profile. To use a hub running on your Mac, set `STUDIO_HUB_URL` to its address, for example `http://127.0.0.1:4310`.

## Commands

| Command | What it does |
|---|---|
| `/studio:new <name> [for <client>]` | Starts a project: a private GitHub repository and a team preview |
| `/studio:open <name>` | Opens a project: clones it if needed and sums up its flows, brand and files |
| `/studio:preview [name]` | Pushes the latest changes and updates the team preview |
| `/studio:publish [name]: <what changed>` | Publishes the next client version |
| `/studio:handoff [name] [version]` | Packages a published version as a ZIP for developers |
| `/studio:list` | Lists projects |
| `/studio:rename`, `/studio:archive`, `/studio:restore` | Renames, archives and restores a project |
