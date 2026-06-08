# ⚔️ HERE — Alliance Duel Portal

A single-file web portal that turns your weekly **Alliance Duel** Excel export into a clean dashboard: weekly charts, daily breakdowns, underperformer tracking, and an all-time leaderboard that builds up over time.

Everything runs in your browser. No server, no install, no accounts.

---

## What it does

You upload one `.xlsx` file each week. The portal reads **only the `Historical` sheet** and computes everything else automatically:

| Tab | What it shows |
|-----|---------------|
| **📊 Graphic** | Weekly KPIs, stacked points-by-theme chart, top 10 by weekly total, alliance points per day, bottom 10 needing improvement, and a per-day breakdown table. |
| **📅 Current Week** | All 6 days side by side (Raven, Building, Scroll, Hero, Speedup, Raid), color-coded, ranked, with the chest tier earned for each score. |
| **⚠️ Underperformers** | Every player who scored **0 on any day**, with a column per day (0-cells highlighted in that day's color) and notes listing which days they missed. |
| **🏆 Overall** | All-time leaderboard. Grows each week as you archive — totals and weeks-played accumulate. |
| **🎁 Chest Tiers** | Reference for chest thresholds and the day/theme color legend. |

---

## How to use it

### 1. Open the portal
- **Easiest:** double-click `index.html` to open it in your browser.
- It needs an internet connection the first time (it loads the chart + spreadsheet libraries from a CDN).

### 2. Upload the week
- Click **Upload week (.xlsx)** (top right) or drag your file onto the drop zone.
- The file **must contain a sheet named `Historical`** with the 6 days laid out in the standard column blocks. The portal ignores every other sheet.

### 3. Review the tabs
- Graphic / Current Week / Underperformers populate instantly.

### 4. Archive the week (optional but recommended)
- Click **📊 Archive → Overall** to add this week's numbers to the all-time leaderboard.
- Do this **once per week**. Archiving the same week twice will double-count it — if that happens, use **Reset history** and re-archive.

---

## What gets saved (and where)

The portal uses your browser's **localStorage**:

- **The uploaded week** is saved automatically — refresh or reopen the page and it's still there, no need to re-upload.
- **The Overall leaderboard** persists across weeks as you archive.

| Button | Effect |
|--------|--------|
| **Archive → Overall** | Adds the current week to the all-time totals. |
| **Reset history** | Clears the all-time Overall only. Your loaded week stays. |

### ⚠️ Important limitations of browser storage
- **Per-device, per-browser.** Data saved on your PC is *not* visible on your phone, and vice versa.
- **Incognito / private windows wipe everything on close** — don't use them.
- If you want a **shared** Overall that the whole alliance sees from one URL, localStorage can't do that. That requires a small backend (can be added later).

---


## The `Historical` sheet format

The parser auto-detects where data starts (it skips title and header rows). It expects the standard 6-block layout — each day occupying 4 columns:

| Day | Columns | Theme |
|-----|---------|-------|
| 1 | A–D | 🐦 Raven |
| 2 | E–H | 🏗 Building |
| 3 | I–L | 📜 Scroll/Open |
| 4 | M–P | ⚔ Hero |
| 5 | Q–T | ⚡ Speedup |
| 6 | U–X | 💥 Raid |

Within each block the columns are: **date · rank · player · points**.

As long as you keep this layout each week, it parses cleanly. If you restructure the columns, the parser needs updating.

---

## Chest tiers (points in a single day)

| Tier | Minimum points |
|------|-----------------|
| C9 ⭐ | 7,190,000 |
| C8 | 3,620,000 |
| C7 | 2,630,000 |
| C6 | 2,280,000 |
| C5 | 1,020,000 |
| C4 | 650,000 |
| C3 | 550,000 |
| C2 | 145,000 |
| C1 | 38,000 |

---

## Troubleshooting

| Problem | Fix |
|---------|-----|
| "Could not find the Historical sheet" | The sheet must be named `Historical` (any capitalization). |
| Charts don't appear | You opened it with no internet on first load. Reconnect and refresh. |
| Data disappears on refresh | You're in a private/incognito window, or viewing inside a sandboxed preview. Open the actual file in a normal browser window. |
| Overall double-counted a week | Click **Reset history**, then re-archive each week once. |
| Looks broken / shows old text | Hard-refresh with **Ctrl+Shift+R** (Cmd+Shift+R on Mac) to clear the cache. |

---

*HERE Alliance Duel Portal — computed entirely in your browser.*
