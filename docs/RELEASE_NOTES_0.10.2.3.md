# Mugi 0.10.2.3 — Public Beta (hotfix)

Emergency hotfix for **0.10.2.2**. If you installed 0.10.2.2, upgrade immediately — the global Dashboard shortcut is broken in that build.

- Build number **11** (Sparkle compares `CFBundleVersion` for same marketing version).

---

## Highlights

### Global Dashboard shortcut works again

- **Fixed:** in 0.10.2.2, **⇧⌥D** (or your custom Dashboard shortcut) only worked when Mugi was already the frontmost app. From Safari, Mail, or any other app, the shortcut appeared to do nothing.
- **Cause:** `DashboardPanelController` accidentally set `hidesOnDeactivate = true` on the floating panel. Because the Dashboard is a `.nonactivatingPanel` (summoned without activating Mugi), AppKit kept the panel hidden whenever another app was frontmost.
- **Fix:** restored `hidesOnDeactivate = false`, matching the Quick Panel pattern. App-switch dismissal is still handled by the existing resign-key observer — not by hiding the panel on deactivate.

---

## Upgrade notes

- No settings migration. Your Dashboard shortcut preference is unchanged.
- **0.10.2.2 users:** this is the only change vs 0.10.2.2; everything else from that release (TextKit fixes, council Skip, task-plan banner, etc.) is unchanged.

---

## Known limitations

- Unchanged from 0.10.2.2. See `RELEASE_NOTES_0.10.2.2.md` for the full feature list and remaining caveats.

---

Feedback welcome via GitHub issues or your usual channel.
