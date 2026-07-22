# Installing RyMac Skills

These are [Claude Code](https://docs.claude.com/en/docs/claude-code) skills.
Installing one is just **copying a folder** into the right place. No package
manager, no build step, no API keys.

## Requirements

- [Claude Code](https://docs.claude.com/en/docs/claude-code) installed and working.

That's it. Some individual skills use tools Claude Code already has (web search,
file writing); none require anything you install separately.

## Where skills live

Claude Code loads skills from a `skills/` folder in one of two places:

| Scope | Path | Use it when |
|---|---|---|
| **Global** | `~/.claude/skills/` <br> Windows: `C:\Users\<you>\.claude\skills\` | You want the skill in **every** project. Best for craft skills like these. |
| **Project** | `<your-project>/.claude/skills/` | You want the skill in **one** repo only. |

Inside that `skills/` folder, each skill is its own subfolder containing a
`SKILL.md`. That's the whole contract.

## Install one skill

1. Copy the skill folder — e.g. `rymac-headline-copywriting` — into your skills
   directory. The **folder name must stay exactly as-is** (Claude uses it as the
   skill's name).
   - Global: `~/.claude/skills/rymac-headline-copywriting/`
   - Project: `<your-project>/.claude/skills/rymac-headline-copywriting/`
2. Start a new Claude Code session (skills load at startup).
3. Verify: run `/help` or check your skills list — the skill should appear. Or
   just ask for what it does and watch it fire.

## Install the whole pack

**macOS / Linux:**
```bash
git clone https://github.com/oathdriven/rymac-skills.git
mkdir -p ~/.claude/skills
cp -r rymac-skills/skills/* ~/.claude/skills/
```

**Windows (PowerShell):**
```powershell
git clone https://github.com/oathdriven/rymac-skills.git
New-Item -ItemType Directory -Force "$env:USERPROFILE\.claude\skills" | Out-Null
Copy-Item rymac-skills\skills\* "$env:USERPROFILE\.claude\skills\" -Recurse
```

Restart Claude Code. All fourteen skills should be listed.

## Updating

Skills don't auto-update. To pull new versions, `git pull` the repo and copy the
folders over again (overwrite). Your own edits to a skill will be overwritten, so
if you customize one, keep a copy.

## Uninstall

Delete the skill's folder from `~/.claude/skills/` (or your project's
`.claude/skills/`) and restart Claude Code.

## Troubleshooting

- **Skill doesn't show up:** confirm the folder is directly inside `skills/`
  (not nested one level too deep, e.g. `skills/rymac-headline-copywriting/rymac-headline-copywriting/`),
  that it contains a `SKILL.md`, and that you started a **new** session.
- **Skill won't trigger:** it fires on matching requests. Open the skill's
  `README.md` for its trigger phrases, or force it with its slash command
  (`/rymac-<name>`).
- **Wrong scope:** a project-scoped skill only works inside that project. Move
  it to `~/.claude/skills/` to use it everywhere.

More on how skills work: <https://docs.claude.com/en/docs/claude-code/skills>
