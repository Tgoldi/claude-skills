# Claude Skills

A snapshot of custom Claude Code skills + the plugins that ship the rest.

## What's in this repo

114 user-authored / hand-installed skills, each as a folder containing a `SKILL.md`
(and any helper scripts). They're meant to be loaded by Claude Code from
`~/.claude/skills/`.

## Setup (coworker, one-time)

### 1. Clone the user skills

```bash
git clone <this-repo-url> ~/.claude/skills
```

That's it for the file-based skills. Claude Code auto-discovers any folder
under `~/.claude/skills/` that contains a `SKILL.md`.

> If you already have a `~/.claude/skills/` directory, either back it up
> (`mv ~/.claude/skills ~/.claude/skills.bak`) or clone elsewhere and merge
> the folders manually.

### 2. Install the plugins

These skills are maintained by their authors and updated through Claude Code's
plugin system — not stored in this repo. Run inside Claude Code:

```text
/plugin marketplace add thedotmack@github:thedotmack/claude-mem

/plugin install frontend-design@claude-plugins-official
/plugin install figma@claude-plugins-official
/plugin install supabase@claude-plugins-official
/plugin install superpowers@claude-plugins-official
/plugin install code-review@claude-plugins-official
/plugin install semgrep@claude-plugins-official
/plugin install github@claude-plugins-official
/plugin install claude-code-setup@claude-plugins-official
/plugin install skill-creator@claude-plugins-official
/plugin install claude-md-management@claude-plugins-official
/plugin install learning-output-style@claude-plugins-official
/plugin install pr-review-toolkit@claude-plugins-official
/plugin install claude-mem@thedotmack
```

The official marketplace (`claude-plugins-official`) is built in — no `add` needed.

## Caveats

- **MCP-server auth**: Several plugins (`figma`, `supabase`, `github`, etc.)
  call MCP servers that need per-user authentication. You'll be prompted on
  first use — there's no way to share auth tokens.
- **Don't copy** `~/.claude/.credentials.json` or `~/.claude/settings.json`
  wholesale from another machine — they contain personal state.
- **Skills evolve**: This repo is a point-in-time snapshot. To keep it in
  sync, occasionally `git pull` here and re-run the `/plugin install`
  commands (or use `/plugin` UI to update).

## Updating this repo (owner)

```bash
cd ~/.agents/skills
git add -A
git commit -m "sync skills"
git push
```

(`~/.claude/skills/` on the owner's machine is a symlink farm pointing into
this folder, which is why the source of truth lives at `~/.agents/skills/`.)
