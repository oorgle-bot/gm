# GM Dashboard

## Project Overview
A single-file browser-based GM dashboard for Dungeon World — no build step, no server, no npm.

## Tech Stack
React 18, Babel Standalone, Tailwind CSS — all via CDN.
Entry point: `dungeonworld2tool/gm_dashboard.html` (~1580 lines)

## Key Directories
```
dungeonworld2tool/gm_dashboard.html  — entire application
.claude/docs/                        — supplementary docs for Claude
```

## Running the App
Open `dungeonworld2tool/gm_dashboard.html` directly in any modern browser. No build step needed.

## Code Layout (file:line)
```
Utilities:             gm_dashboard.html:70–77
State templates:       gm_dashboard.html:79–101
loadState / migration: gm_dashboard.html:103–137
Reducer:               gm_dashboard.html:140–190
Static data:           gm_dashboard.html:192–259
Shared UI components:  gm_dashboard.html:270–472
Tab components:        gm_dashboard.html:595–1213
App root:              gm_dashboard.html:1320–1357
```

## State Management
`useReducer` with a centralized reducer. `localStorage` key: `gm_dashboard_v2`.
Auto-save: 2.5s debounce. v1→v2 migration in `loadState()`.
- **Global:** `factions[]`, `npcs[]`
- **Campaign-scoped:** `characters[]`, `sessionNotes`, `xpChecklist`, `randomTables`

## Reducer Action Namespaces
```
Campaign:      ADD_CAMPAIGN, SWITCH_CAMPAIGN, DEL_CAMPAIGN, RENAME_CAMPAIGN
Character:     ADD_CHAR, UPD_CHAR, DEL_CHAR
Faction:       ADD_FAC, UPD_FAC, DEL_FAC
NPC:           ADD_NPC, ADD_NPC_WITH_DATA, UPD_NPC, DEL_NPC
Session:       SET_NOTES, TOGGLE_XP, RESET_XP
Random Tables: ADD_TABLE, UPD_TABLE, DEL_TABLE
```

## Key Design Constraints
- **Single file only** — all code stays in `gm_dashboard.html`
- **No build tooling** — no npm, webpack, vite, or bundler
- **CDN dependencies only** — no local JS/CSS files
- **localStorage is the only persistence** — no backend, no IndexedDB

## Additional Documentation
See `.claude/docs/` when relevant:
- `architectural_patterns.md` — reducer conventions, local state patterns, component reuse, styling
