# Mugi 0.15.0.1 — Public Beta

A patch on **0.15.0**. The 0.15.0 build shipped three failures that should never
have reached anyone: a reply that doubled itself in the thread, named jobs that
could not be deleted from Settings, and a job hired to "only report" that
received every tool in the app.

---

## Fixed

### A reply no longer becomes two identical bubbles

A mid-run history reload could land after the server had already saved the
answer that was still streaming. The client appended both. One reply looked
like two.

### Named jobs can be retired and deleted in Settings

Delete only appeared on a retired job, and retiring was a chat-only verb with
no Settings route. Letting a job go meant leaving the pane, asking chat, and
coming back. There is a **Retire** button on live jobs now. Retiring reveals
the retired list so Delete is on the same screen.

### A hire cannot start with every tool in the app

Hiring on `general` compiled to the full registry (264 always-on schemas). The
stop-line was prose in the prompt; it did not close any tools. A hire must now
name a bounded base profile. If the stop-line rules out a whole capability
(writing files, shell, mail, …) and `deny_tools` leaves it open, the hire is
refused. Widening to everything remains a Settings action.


### One finished board task reports into the thread once

A standalone root task had two carriers into its origin thread — a queued
subscription and an inline delivery — and both fired. One task produced two
user bubbles and two parent wakes.

---

## Upgrade notes

- Sparkle will offer this build to anyone on **0.15.0** (build 22 → 23).
- Existing named jobs are unchanged. A job already hired on `general` stays
  that wide until you retire it or narrow it in Settings.
- Everything in the [0.15.0 notes](RELEASE_NOTES_0.15.0.md) still applies.

---

## Known limitations

- Mugi requires **Apple Silicon** (M-series); Intel Macs are not supported.
- A job hired before this patch on the everything base is still that wide.
  Retire it and hire again if you want the new bound.

---

Feedback welcome via GitHub issues.
