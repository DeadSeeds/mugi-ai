# Mugi 0.10.1 — Public Beta

Patch release following 0.10.0. Focus: **global Dashboard panel**, **tile polish**, **calendar & news reliability**, and **compact layout fixes**.

- Build number **7** (Sparkle compares `CFBundleVersion` for same marketing version).

---

## Highlights

### Global Dashboard (⇧⌘D)

- Dashboard is now a **floating panel** you can summon from anywhere — same spirit as Quick Panel, not a full-window overlay.
- **⇧⌘D** toggles it globally (View → Dashboard in the menu). Esc dismisses.
- **Three-column layout:** system vitals · calendar · reminders | weather · markets · news | agent chat with composer.
- Draggable title bar, greeting inside the glass, close button top-left (Apple style).
- Panel height **hugs content** — no dead space at the bottom, rounded corners on all four edges.
- Chat column **fills the full height** of the panel; transcript grows above the composer.

### Dashboard tiles & visuals

- Redesigned **vitals strip** (compute, RAM, disk, network) and **weather hero** with richer gradients and gauges.
- **Kanban tile removed** from the bundled dashboard (board stays in the sidebar / Settings).
- **News feeds editor** — right-click the News tile → Modify feeds… to add or remove RSS/Atom URLs.
- Reconnect banner when the backend drops; clearer empty/error states on tiles.
- Dashboard **arrival highlight** motion disabled (less visual noise on open).

### Calendar

- **Click an event** to open it in your **default calendar app** — not hardcoded to Apple Calendar. Supports Outlook, Fantastical, BusyCal, and generic `.ics` fallback.
- Fetches **shared and subscribed calendars** (Google, Exchange, iCloud shared): refreshes remote sources before querying and searches every calendar Mugi has access to.
- **48-hour** lookahead (was 24h); events sorted by start time before display.
- Event rows show the **calendar name** so you can see which feed an item came from.
- If shared events are missing: **System Settings → Privacy & Security → Calendars → Mugi → Options…** — enable the shared calendars there.

### News & backend

- `POST /dashboard/news_feeds` for persisting feed URLs from the dashboard editor.
- Markets/news feed plumbing and tests tightened.

---

## Upgrade notes

- Existing **0.10.0** installs: **Mugi → Check for Updates…** after this build is published to Sparkle.
- Fresh install: download from [mugi-ai.com](https://mugi-ai.com) or use the GitHub release artifact (`Mugi-0.10.1.zip`).
- Dashboard global shortcut changed from **⌥⇧⌘D** to **⇧⌘D** (documented in the shortcut cheat sheet). When a shell-approval alert is open, **⇧⌘D** still means “deny” — Dashboard is deferred in that moment.

---

## Requirements

| | |
|---|---|
| **OS** | macOS 15.0 (Sequoia) or later |
| **Hardware** | Apple Silicon (M-series) required — Intel Macs are not supported |

---

## Known limitations

- Dashboard panel height is computed from SwiftUI layout; very long calendar lists may approach the max panel height (~72% of screen) before clipping — open Calendar.app for the full month view.
- EventKit still depends on macOS calendar sync; remote calendars may lag until Calendar.app or `refreshSourcesIfNecessary` has pulled updates.
- Kernel legacy-loop deletion (Slice 6) remains **deferred** — this release does not remove the `[kernel] enabled = false` revert valve.

User manual: [Dashboard panel](https://mugi-ai.com/manual/chapter.html?f=08-right-panels.md#dashboard-panel) (also in `website/manual/docs/08-right-panels.md`).

Feedback welcome via GitHub issues or your usual channel.
