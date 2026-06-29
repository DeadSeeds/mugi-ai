# Mugi 0.10.2.1 — Public Beta

Point release following 0.10.2. Focus: **Dashboard shortcut reliability**, **warm reopen polish**, and fixes discovered during the 0.10.2 soak.

- Build number **9** (Sparkle compares `CFBundleVersion` for same marketing version).

---

## Highlights

### Dashboard shortcut actually works (and stays customizable)

- **Fixed:** changing the Dashboard shortcut in **Settings → Dashboard** had no effect — the pane was wired to the **Quick Panel** hotkey manager (`@EnvironmentObject` type collision). Dashboard edits now apply to the real manager.
- **Default is now ⇧⌥D** (shift+option+D). We avoid **⌃⌥D** because `control+option` is the VoiceOver modifier and is commonly claimed by global-hotkey tools (**BetterTouchTool**, **Alfred**, window managers). On those Macs ⌃⌥D can't register and silently does nothing — the classic “works on her Mac, not mine” failure.
- If your combo can't register, Settings shows an orange **“couldn't be registered”** banner and names the usual culprits. Pick a different shortcut; ⇧⌥-based combos are usually free.
- Legacy **⇧⌘D** Dashboard shortcuts still auto-migrate to the new default on first launch.

### Dashboard reopen — no more re-settling

- Closing the Dashboard and immediately reopening no longer rebuilds the whole tile grid or re-grows the window from scratch. The first open still loads data once; warm reopens snap back to the rendered state while live values keep refreshing in place.

### News feeds editor z-order

- **Modify feeds…** on the News tile opens the editor **in front of** the floating Dashboard panel (it previously landed behind it).

### Calendar clarity for Google-only users

- Clearer copy when EventKit has no calendars: browser-only Google Calendar isn't visible until the account is added under **System Settings → Internet Accounts**. **Open Internet Accounts…** in Settings → Access.

---

## Also in this release line (0.10.2)

- Global Quick Panel (**⌃⇧Space**) and Dashboard shortcuts use Carbon `RegisterEventHotKey` — system-wide, no Input Monitoring permission.
- In-app key-code monitor backs up Carbon so shortcuts work when Mugi is focused.
- **View → Dashboard** menu wired to the same shortcut as the global hotkey.
- Sidebar width persists across restarts.
- Appcast publish workflow hardened (quoted release notes, broken gitlink removed).

---

## Upgrade notes

- Dashboard default shortcut is **⇧⌥D**. Custom shortcuts you already set are preserved.
- If the Dashboard shortcut does nothing, open **Settings → Dashboard** — look for the orange conflict banner and choose a combo that registers (especially if you run BetterTouchTool or Alfred).
- Google Calendar in a browser only: add the account under **System Settings → Internet Accounts** once.

---

## Known limitations

- Mugi reads calendars through macOS **EventKit** — not a direct Google Calendar API. Browser-only Google Calendar requires Internet Accounts sync on the Mac.
- Some global shortcuts may still be owned by third-party tools; pick another combo in Settings if registration fails.

---

Feedback welcome via GitHub issues or your usual channel.
