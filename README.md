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

## License

MIT
