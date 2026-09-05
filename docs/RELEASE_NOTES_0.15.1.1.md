# Mugi 0.15.1.1 — Public Beta

A patch on **0.15.1**. Automatic updates actually run after the chat window is
on screen. 0.15.0 said this was fixed; it was not. The check either never ran,
or it ran under the launch card and you never saw it.

---

## Fixed

### The update check runs after the launch card is gone

Sparkle used to start on the first boot frame, while the chat window was still
ordered out. That consumed the one start the updater gets. A later 60-second
safety net then fired while a slow boot was still showing the splash, so the
dialog sat behind the launch card. The check now waits until chat is the thing
on screen. A last-resort start still exists for a boot that never reveals chat;
it no longer steals the start from a launch that is merely slow.

---

## Upgrade notes

- Sparkle will offer this build to anyone on **0.15.1** or earlier (build 24 → 25).
- Everything in the [0.15.1 notes](RELEASE_NOTES_0.15.1.md) still applies.

---

## Known limitations

- Mugi requires **Apple Silicon** (M-series); Intel Macs are not supported.

---

Feedback welcome via GitHub issues.
