# Mugi 0.10.2.2 — Public Beta

Point release following 0.10.2.1. Focus: **chat rendering reliability**, **Dashboard layout polish**, and **quieter council / task-plan UX** on long or busy runs.

- Build number **10** (Sparkle compares `CFBundleVersion` for same marketing version).

---

## Highlights

### Chat input text visible again (macOS 15.7+)

- **Fixed:** on some Macs the main chat composer and Quick Panel input bar accepted keystrokes but showed **no glyphs** — not even after Select All. Root cause was TextKit 2 vs TextKit 1 layout mismatch in the `NSTextView` wrappers.
- Both composers now use an explicit TextKit 1 stack so typed text, the caret, and selection render deterministically across macOS versions.

### Assistant bubble text no longer floats below empty space

- **Fixed:** assistant messages sometimes showed a **large blank gap above the text** inside the bubble; scrolling could make the text “slide” into the correct position. Same TextKit class of bug — markdown bubbles now use a matching TextKit 1 display path so the first paint is aligned with the measured height.

### Dashboard chat fills the panel and renders markdown

- Dashboard agent replies now render **markdown** (bold, lists, code, links) instead of raw `#` / `*` source.
- The chat column **expands to match** the tile column height (news capped at five stories sets the window size; chat follows).
- **Fixed:** a follow-up message in Dashboard could **freeze the entire app** — geometry feedback loop between panel resize and chat height measurement is broken.
- Tiles no longer stretch awkwardly when the window grows; only the chat column fills extra vertical space.

### Council “Skip” stays out of the transcript

- Tapping **Skip** on the council offer banner no longer posts *“Answer directly; skip council for this question.”* as a user bubble. Skip dismisses the offer and the agent answers directly — nothing extra enters chat history.

### Task plan keeps showing steps when refresh fails

- If a background **GET /task_plan** times out while the agent is busy, the card no longer replaces your step list with a full-screen error. It keeps the **last known plan** and shows a small **“couldn’t refresh”** banner with Retry.

---

## Also in this release

- **EULA / legal sheets:** dedicated `LegalMarkdownScrollView` for smoother scrolling legal copy in onboarding and Settings.
- **Stalled runs:** empty assistant placeholder bubbles from interrupted runs collapse instead of leaving a tall blank box (the activity row still shows work in progress).
- **Release pipeline:** codesign staging hardened for iCloud-synced `dist/` paths (maintainer-facing; no user-facing change).

---

## Upgrade notes

- No settings migration required. Custom Dashboard and Quick Panel shortcuts are preserved.
- If you skipped council offers in 0.10.2.1, older threads may still show the old skip-line bubble in history — new skips are silent.

---

## Known limitations

- Council **Approve** still convenes the full pipeline; only **Skip** is transcript-silent.
- Task plan refresh can still time out under heavy load; the banner means you are reading cached steps, not a live snapshot.
- Mugi requires **Apple Silicon** (M-series); Intel Macs are not supported.

---

Feedback welcome via GitHub issues or your usual channel.
