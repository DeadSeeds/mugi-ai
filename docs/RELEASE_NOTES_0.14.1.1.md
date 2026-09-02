# Mugi 0.14.1.1 — Public Beta

A single-fix patch on top of **0.14.1**. Nothing else changed; if 0.14.1 is working for you, the only thing you gain here is a Results page you can actually use.

---

## Fixed

### Results buttons no longer sit on top of the toolbar

In the Modern layout, the **Edit / Copy / Export** buttons on the Results page were drawn in the same band as the floating toolbar buttons in the top-right corner — On my mind, Activity, Plugins, Kanban — so the two rows overlapped and neither was reliable to click.

The Results header now starts on the same line as the inspector panel and the first message in a conversation, which is where the rest of the app already begins. Vault, chat, and Knowledge were checked and were never affected.

---

## Upgrade notes

- Sparkle will offer this build to anyone on **0.14.1** (build 20 → 21).
- No settings, data, or board state change. Named jobs, hires, and durable tasks carry over untouched.
- Everything in the [0.14.1 notes](RELEASE_NOTES_0.14.1.md) still applies — hiring by name, durable board work, and the reliability fixes that shipped with it.

---

## Known limitations

- Mugi requires **Apple Silicon** (M-series); Intel Macs are not supported.
- Unchanged from 0.14.1: chat can still claim it filed a board task before it has actually done so — glance at the board if a hire or assign looks too fast.

---

Feedback welcome via GitHub issues.
