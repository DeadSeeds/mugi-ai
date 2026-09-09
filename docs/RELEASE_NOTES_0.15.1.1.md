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

### “Remember this” and “never note that” actually land

A forget or a save could be answered with “Done — that’s scrubbed” and nothing
written. Asking to remember, save, or forget now has to call the tool. A
casual mention (“Jim has a dog named Nelly”) stays off the write path — that
is picked up afterwards, the way it always was.

### Chat knows which note or page you have open

Opening a Vault note or a Results page and talking in the same window now
carries that focus into the turn, so “change the heading” or “add a line
here” is about the thing on screen.

### Originals in Knowledge can be zoomed

PDF and image originals in the Library have zoom controls. The page no longer
sits at whatever size happened to fit.

### Staged Library edits can be reviewed and exported

Asking to change a Word, Excel, PDF, or deck that is already in the Library
now stages a copy instead of spinning. When a document has a proposed change,
you can look at that copy and export it without guessing which file is the
staged one.

### Follow-up turns stay fast

The tool list no longer grows mid-thread when a new tool is found or first
used. That list is the head of the prompt cache; growing it used to make the
next round re-read the whole conversation. On Apple Silicon with more than
32 GB, the prompt cache also keeps more whole-prompt snapshots, so a title
or capture request between two rounds of your chat does not throw the thread
away.

---

## Upgrade notes

- Sparkle will offer this build to anyone on **0.15.1** or earlier (build 24 → 25).
- Everything in the [0.15.1 notes](RELEASE_NOTES_0.15.1.md) still applies.

---

## Known limitations

- Mugi requires **Apple Silicon** (M-series); Intel Macs are not supported.

---

Feedback welcome via GitHub issues.
