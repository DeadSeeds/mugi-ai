# Mugi 0.10.2 — Public Beta

Patch release following 0.10.1. Focus: **reliable global shortcuts** (Quick Panel + Dashboard) and **calendar access that actually prompts**.

- Build number **8** (Sparkle compares `CFBundleVersion` for same marketing version).

---

## Highlights

### Global shortcuts now work everywhere — no Input Monitoring needed

The Quick Panel and Dashboard shortcuts are now registered as true system hot keys (Carbon
`RegisterEventHotKey`) instead of a passive event monitor. What this fixes:

- **They fire from any app, on a fresh install, with no permission prompts.** Previously the global
  shortcut quietly depended on the **Input Monitoring** permission being granted to that exact app
  binary — so it could work on one Mac and do nothing on another even with identical builds.
- **Letter-key shortcuts (like the Dashboard's) are reliable.** The old monitor frequently dropped
  the character data for letter keys, so the shortcut silently never matched.
- **Conflicts are visible.** If the combination you chose can't be registered (another app owns it),
  Settings shows a "couldn't be registered — pick another shortcut" banner instead of failing
  silently.
- **Dashboard shortcut works inside Mugi too.** A local key-code monitor backs up Carbon registration
  so ⌃⌥D (or your custom combo) fires even when Mugi is focused. The 0.10.1 path matched letter keys
  via `charactersIgnoringModifiers`, which is often empty — so the shortcut could die *inside the app*
  on some Macs. **View → Dashboard** is now wired to the same shortcut.
- **Legacy ⇧⌘D Dashboard shortcuts auto-migrate to ⌃⌥D** on first launch of this build (⇧⌘D collides with
  Mugi’s shell-deny menu and most browsers).

### Customizable Dashboard shortcut

- The Dashboard shortcut is now **customizable** in **Settings → Dashboard**, just like the Quick Panel.
- The default changed to **⌃⌥D** to avoid clashing with **⇧⌘D**, which many browsers and dev tools
  already use (and which Mugi reserves for **Deny shell command** while a shell-approval alert is open).
- Recordings that stored **⇧⌥D** (shift+option, easy to mistake for the intended control+option) now
  auto-migrate to **⌃⌥D** on first launch.

### Shortcut diagnostics — see exactly why a shortcut isn't firing

- **Settings → Dashboard → Shortcut diagnostics** shows the live health of the Dashboard shortcut:
  whether it registered **system-wide**, whether the **in-app** monitor is active, the **stored combo**,
  and a **Last triggered** line that updates the instant the shortcut fires. Press the keys with the
  panel open and watch it light up — that's end-to-end proof, not a guess.
- If a combo can't register (another app owns it), the panel says so instead of silently doing nothing.
  **Re-register** and **Reset to ⌃⌥D** buttons are right there.

### Calendar access that prompts correctly

- The **Request Calendar Access** button now reliably brings Mugi to the front so macOS can show the
  permission prompt (it previously could be suppressed when the Settings window was focused).
- If access was already denied, Mugi now **opens System Settings → Privacy & Security → Calendars**
  directly, with an **Open Calendar Settings…** button and a clear status line.
- The Dashboard calendar tile's retry now requests permission directly when it's the thing blocking.
- **Fixed: calendars staying blank even with Full Access granted.** If macOS hands the app an empty
  calendar list (the long-lived EventKit connection had loaded before your accounts finished syncing),
  Mugi now resets and re-reads the store, and — if it's still empty — explains why instead of a misleading
  "no events" (including **Google Calendar used only in a browser**: Mugi reads macOS Calendar via
  EventKit, so add Google under **System Settings → Internet Accounts** once; you don't need to switch
  to Calendar.app day to day).
- **Settings → Access → Calendar** adds **Open Internet Accounts…** and copy that browser-only Google
  Calendar isn't visible until the account is connected on the Mac.

### Dashboard polish

- **News feeds editor** — right-click the News tile → **Modify feeds…** now opens the editor **in
  front of** the floating Dashboard panel (it previously landed behind the panel until you closed it).

### Sidebar width persists across restarts

- The left sidebar width is now **reliably remembered between launches**. Previously, as the window
  grew to its restored size during launch, the split view redistributed the extra space *into the
  sidebar* and then saved that inflated width — so a sidebar you'd narrowed quietly widened back on
  the next launch (and only on some Macs, depending on window size). Now only the middle column
  absorbs window resizes, the sidebar keeps the width you set, and the persisted width is the single
  source of truth (AppKit's built-in split autosave is disabled and its accumulated per-window
  entries are purged on launch).

---

## Upgrade notes

- Existing installs: **Mugi → Check for Updates…** after this build is published to Sparkle.
- **You can remove Mugi from System Settings → Privacy & Security → Input Monitoring** — it is no
  longer used for shortcuts.
- The Dashboard shortcut default is now **⌃⌥D**. If you'd set a custom Dashboard shortcut, it is
  preserved. Stored **⇧⌘D** Dashboard shortcuts auto-migrate to **⌃⌥D** on first launch of this build.
  **⇧⌘D** continues to mean **Deny shell command** when a shell-approval alert is open.
- **Google Calendar in a browser only?** Add your Google account under **System Settings → Internet
  Accounts** (or **Settings → Access → Open Internet Accounts…** in Mugi) so events sync to macOS;
  then Retry on the Dashboard calendar tile.

---

## Requirements

| | |
|---|---|
| **OS** | macOS 15.0 (Sequoia) or later |
| **Hardware** | Apple Silicon (M-series) required — Intel Macs are not supported |

---

## Known limitations

- Carbon hot keys don't always report a cross-app conflict as an error, so a shortcut already owned
  by another app may register without a banner yet still not fire. If a shortcut does nothing, pick a
  different combination in Settings.
- EventKit reads **macOS's Calendar database**, not Google Calendar in a browser. Remote calendars
  (Google, Exchange, iCloud) must be added under **Internet Accounts** and may lag until sync completes.

User manual: [Menus & shortcuts](https://mugi-ai.com/manual/chapter.html?f=04-menus-and-shortcuts.md).

Feedback welcome via GitHub issues or your usual channel.
