# DraftBoard

A single-page fantasy football draft tracker for 12-team snake drafts. No backend or account. Runs entirely in the browser with state persisted to localStorage.

![Draft Board](https://img.shields.io/badge/zero--dependency-single%20HTML%20file-blue)

## Features

- **Live player pool**: auto-loads all active NFL players from the [Sleeper API](https://docs.sleeper.com/) on first visit, ranked by popularity
- **Snake draft board**: 12 teams × configurable rounds (1-40), with snaking
- **Drag to reorder**: rearrange picks on the board or re-rank players in the pool by dragging
- **Target & DND flags**: star players you want to target (green) or mark do-not-draft (red); flags carry through to the board
- **Right-click context menu**: draft, flag, return to pool, or remove a player without leaving the board
- **Click to black out**: click any drafted cell to grey it out (for tracking picks you don't care about)
- **Import a custom list**: paste a ranked list or upload a CSV; missing position/team/bye week data is auto-filled from Sleeper
- **Editable team names**: click any column header to rename a team
- **Persistent state**: everything survives a page refresh via localStorage

## Usage

Open `index.html` in a browser. That's it!

On first load the app fetches the Sleeper player list (cached for 24 hours). You can also bring your own list at any time without losing your draft state.

## Importing players

### Paste list

Click **Paste list** and enter one player per line in rank order:

```
Ja'Marr Chase, WR, CIN, 6
Bijan Robinson, RB, ATL, 11
Justin Jefferson, WR, MIN, 6, 1, 0
```

Columns: `Name, Position, Team, Bye, Target (1/0), DND (1/0)`

Everything after Name is optional. Missing position, team, and bye week are looked up from Sleeper automatically.

### CSV

Click **Import CSV** and select a file with the same column format. A header row (`Name,Position,...`) is detected and skipped automatically.

## Keyboard / mouse shortcuts

| Action | How |
|---|---|
| Draft a player | Click a pool tile |
| Draft via menu | Right-click a pool tile → Draft player |
| Return a pick to pool | Right-click a board cell → Return to pool |
| Black out a cell | Click a filled board cell |
| Reorder picks | Drag a board cell to a new position |
| Re-rank pool | Drag a pool tile up or down |
| Undo last pick | Right-click board cell → Return to pool (or use Reset draft to clear all) |
| Filter by position | Click a position tab (QB / RB / WR …) |
| Search | Type in the search box |

## Tech

Single HTML file — vanilla JS, no build step, no dependencies beyond two Google Fonts. State lives in `localStorage` under the key `fftracker_state_v1`. Sleeper data is cached separately under `fftracker_sleeper_v2` with a 24-hour TTL.
