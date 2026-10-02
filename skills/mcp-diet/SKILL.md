---
name: MCP Diet
description: >-
  Use when the Cursor context is bloated by MCP tools, the user wants a token
  diet, or the task type changes (code, Notion/docs, Figma/design, sheets,
  slides, scrape/research, lean chat). Auto-picks a profile, shows an ON/OFF
  MCP switcher, or runs a schema-tax audit — never silently installs/uninstalls.
---
# MCP Diet

Cut Cursor **MCP schema tax**: enable only the servers the current task needs.

**Do:** recommend a profile + ON/OFF checklist mapped to the user’s real connector names.  
**Don’t:** install/uninstall MCP or plugins without an explicit yes; don’t claim you toggled Cursor UI unless a local profile CLI actually ran.

Keep guidance **stack-agnostic**: map local MCP names into role buckets (forge, docs, design, sheets, browser, research, mail/calendar, docs-API).

## When to use

- MCP diet / profiles / token savings / “what should I turn off”.
- Task type changed (code ↔ docs ↔ design ↔ sheets ↔ slides ↔ research ↔ quick Q&A).
- Context feels bloated; many MCP servers enabled at session start.

## Popup switcher

Treat the profile picker as a **control panel**.

Show it when:
1. User asks to switch diet/profile without naming one.
2. Auto-detect is **ambiguous** (top two scores within 2 points) — mark the recommended option.
3. User says the auto pick was wrong.

Skip the picker when the user already named a profile, or auto-detect is confident.

### Options
- `code` — coding / PR / forge
- `docs` — Notion / knowledge base
- `design` — Figma / UI / motion
- `sheets` — spreadsheets
- `slides` — presentations
- `research` — scrape / actors / live web
- `chat` — lean Q&A
- `full` — rare cross-service (never default)
- `audit` — measure only

After a pick: **ON / OFF** + short toggle hint (Cursor Customize → MCP). Don’t invent UI paths.

Hosts with choice widgets → use them. Plain chat → short numbered list, or proceed if already named.

## Auto-profile (automation)

Score **before** asking. Highest wins; ties / close scores → picker.

| Signal | Bump |
|--------|------|
| PR, branch, CI, commit, refactor, bugfix, TS/JS/Vue/React/Python | `code` +3 |
| cloud agent / forge PR / Origin | `code` +2 |
| Notion, wiki, meeting notes, archive | `docs` +3 |
| Figma, UI kit, design system, motion, GSAP, Refero-like | `design` +3 |
| spreadsheet, matrix, CSV, Sheets | `sheets` +3 |
| deck, slides, presentation | `slides` +3 |
| scrape, Apify, crawl, competitor pages | `research` +3 |
| Playwright / open the page / E2E | browser role ON; +1 to `code` or `research` |
| short factual Q, no tools implied | `chat` +2 |
| spans 3+ fat roles in one ask | `full` +3 |

**Also** (same bumps when obvious): код/ПР/рефакторинг/баг → `code`; фигма/макет/анимация → `design`; таблица/матрица → `sheets`; презентация/слайды → `slides`; скрейп/парсинг → `research`; Notion/заметки/архив → `docs`.

**Confidence:** top ≥ +3 and ≥ +2 clear of runner-up → auto-apply. Else → popup.

After auto-apply, one line only, e.g.  
`MCP Diet → design (auto). ON: Figma, Refero, Shadcn, Context7, GitHub. OFF: Notion, Sheets, Slides, Apify, Gmail, Calendar.`

### Automation limits
- Default = **recommend + checklist**. Cursor MCP toggles are manual unless the user has a local profile CLI and asked you to run it.
- Never silent-uninstall.
- Mixed tasks → prefer picker over a wrong auto.

## Role buckets

| Role | Typical servers | Diet note |
|------|-----------------|-----------|
| docs-api | Context7-like | lean — keep |
| ui-kit | shadcn-like | lean — keep |
| canvas | tldraw-like | lean |
| calendar | Calendar-like | lean/medium |
| forge | GitHub-like | fat — `code` |
| origin | Origin-like | fat — `code` when shipping |
| browser | Playwright-like | on demand |
| design | Figma-like | fat — `design` |
| design-ref | Refero-like | few tools, long schemas |
| docs | Notion-like | often fattest — off outside docs/sheets/slides |
| sheets | Sheets-like | fat — `sheets` |
| slides | Slides-like | medium/fat |
| mail | Gmail-like | medium |
| research | Apify-like | `research` |

Diet effort pays off from ~6+ tools/server. Prefer toggling fat HTTP MCP (docs/design/forge/sheets) before proxy hacks.

## Profiles

### `code`
ON: docs-api, forge, origin, browser, ui-kit (+ lean SAST only while scanning)  
OFF: design, design-ref, canvas, slides, sheets, mail, calendar, research, docs

### `docs`
ON: docs, docs-api, forge (light); optional mail, calendar  
OFF: design, browser, ui-kit, research, slides, sheets, canvas

### `sheets`
ON: sheets, docs-api; docs if linked  
OFF: design, browser, research, slides, design-ref, canvas, ui-kit

### `design`
ON: design, design-ref, ui-kit, docs-api, forge; optional canvas; browser only for live UI check  
OFF: sheets, slides, research, mail, calendar

### `slides`
ON: slides, docs; design if mockups  
OFF: browser, research, sheets, ui-kit, design-ref, canvas

### `research`
ON: research, docs-api; browser if live DOM  
OFF: design, sheets, slides, design-ref, ui-kit, canvas

### `chat`
ON: docs-api (+ non-MCP skills)  
OFF: everything else

### `full`
Only true cross-service threads.

## Cost intuition (illustrative)

Re-audit per user (`audit` mode):
- Full ~300+ tools can burn ~80%+ of a 200k window on schemas alone.
- Notion-class MCP can be ~half the tax.
- Clean `code` often ~−80% vs full; `chat` ~−99%.

Method hint: `sum(len(name+description+schema))/4` (±~20%).

## `audit` mode

1. List ready MCP + tool counts.
2. Flag fat vs lean.
3. Recommend a profile for the *current* ask (+ picker if unclear).

## How users toggle

1. Cursor **Customize → MCP**: disable the OFF list.
2. Optional: local profile CLI if they keep `mcp.json` on disk.
3. Stdio schema proxies = last resort (mostly stdio, not hosted HTTP MCP).

## Example replies

**Auto (confident):**  
`MCP Diet → code (auto). ON: Context7, GitHub, Origin, Playwright, Shadcn. OFF: Notion, Figma, Sheets, Slides, Gmail, Calendar, Apify, Refero, Tldraw.`  
Then stop unless they ask why.

**Ambiguous:** show picker with e.g. design recommended; don’t dump the scoring table.

**Audit:** short table (server / tools / fat|lean) + one recommended profile.

## After the user toggles

If they confirm MCP were switched, acknowledge in one short line and continue the original task — don’t re-litigate the diet unless the stack still looks wrong.

## Session checklist

- [ ] Profile matches the task
- [ ] Fat servers outside the profile are OFF (especially docs-MCP)
- [ ] Browser MCP only if needed now
- [ ] Sheets MCP only for spreadsheet work

## Known limits

- Cannot remotely flip Cursor MCP UI; checklist / optional local CLI only.
- Token figures are order-of-magnitude; prefer live `audit`.
- Auto-scoring can misfire on mixed tasks → popup when close.
- Icons/branding don’t change MCP behavior.

## Publication notes

- Keep this file generic; personal stack numbers belong in local `AGENTS.md` / memory.
- Ship: `skills/mcp-diet/SKILL.md` + `.cursor-plugin/plugin.json` + `assets/logo.png`.
- Team: `~/.cursor/skills/mcp-diet/` → Customize → Skills → Publish.
- Public: GitHub → https://cursor.com/marketplace/publish
