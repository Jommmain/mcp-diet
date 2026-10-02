# MCP Diet

Profile-based **MCP diet** for Cursor: turn on only the servers the current task needs so schema tax doesn’t eat the context window.

## Features

- Profiles: `code` · `docs` · `design` · `sheets` · `slides` · `research` · `chat` · `full` · `audit`
- **Auto-pick** from the task (EN + common RU cues); popup when unsure
- **ON/OFF checklists** mapped to *your* connector names
- Stack-agnostic role buckets (forge / docs / design / …)

Recommends toggles. Does **not** flip Cursor MCP switches by itself unless you wire a local profile CLI. Never installs/uninstalls without your OK.

## Quick install

```bash
cp -R skills/mcp-diet ~/.cursor/skills/mcp-diet
```

Reload Agent, then `/MCP Diet` or just describe the task.

## Team / marketplace

- **Team:** Customize → Skills → MCP Diet → Publish (skill must live in `~/.cursor/skills/`).
- **Public:** push this repo → https://cursor.com/marketplace/publish  
  Or Customize → import from GitHub (`.cursor-plugin/marketplace.json`).

## Layout

```
assets/logo.png          # feather + hex (lightness + tech)
skills/mcp-diet/SKILL.md
.cursor-plugin/plugin.json
.cursor-plugin/marketplace.json
docs/popup-ux.md
```

## Honest limits

- Token examples in the skill are illustrative — run `audit` on your stack.
- Automation chooses a **profile**; you (or a local CLI) apply MCP toggles.
- Marketplace review may request manifest nits.

See [CHANGELOG.md](CHANGELOG.md) and [docs/agents-snippet.md](docs/agents-snippet.md) for adopters.


## Credits / provenance

This repository is a **Cursor-oriented rework** of the MCP “diet / profile” idea — not a fork of any one codebase.

**Prior art (thank you):**
- [Rumburak916/mcp-diet](https://github.com/Rumburak916/mcp-diet) — MCP profile / analyze tooling that inspired the profile UX for Cursor.
- [haraldalder-vibemogger/mcp-diet](https://github.com/haraldalder-vibemogger/mcp-diet) — MCP→code SDK skills (Claude-oriented).
- [albererinofigo-droid/mcp-diet](https://github.com/albererinofigo-droid/mcp-diet) — stdio schema proxy (related “diet” idea). / PyPI `mcp-diet` lineage — MCP→code “diet” approaches in the Claude/code-SDK world (different runtime; we adapt the *goal*, not the SDK).

**This project** packages an Agent Skill + Cursor plugin manifests (ON/OFF profiles, auto-pick, audit guidance) maintained for Cursor Agent / marketplace use. Branding and skill text here are original to this repo.

If you are the author of a related project and want a clearer credit line or link fix, open an issue.

## License

MIT
