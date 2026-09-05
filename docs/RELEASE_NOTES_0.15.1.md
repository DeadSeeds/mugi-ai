# Mugi 0.15.1 — Public Beta

A patch on **0.15.0.1**. The new thing you should notice: **asking about your Mac, your notes, or a long recording no longer goes to a blank shell — and the rest of a long answer is not thrown away**. The menu of tools for a turn is now the tools that answer that turn. A result that used to be sliced off in the middle is kept.

---

## Fixed

### The turn arrives with the tool that answers it

A question like "why is my disk full" or "how's the network" used to sit next to a general shell command on every turn, and local models reached for the shell. The shell is now offered only when the request really is a command. Specialized tools are added for the turn from what you asked; a tool that was merely suggested is not pinned into the rest of the conversation.

### Leftover startup items have a real inventory

Asking what is still launching after an uninstall used to wander through application folders. There is a host-diagnostics pass for leftover LaunchAgents now, and leftover-Mac questions are pointed at it instead of at a tool that does not exist.

### A long result keeps its ending

A long transcription was cut at 100k characters before anyone saw the rest. Knowledge search sliced hits so a later match vanished. A graph dump lost its tail. Combined memory-and-library search could look as if the library had never been searched. Those bodies are kept now, and Mugi is told how to reach the part that did not fit in the turn.

### A fat folder listing does not swallow the conversation

Listing a large directory used to paste every name into the turn. The listing is budgeted; unreadably-permissioned folders are reported as unlistable rather than empty.

### Always-visible scroll bars no longer sit on your messages

On a Mac set to **Show scroll bars: Always**, the bar was drawn over the trailing edge of chat bubbles and clipped the timestamp. The transcript now reserves a gutter for that bar. Overlay scrollers (the ones that only appear while you scroll) are unchanged.

### An image that leaves the conversation says so

When an attached image ages out of context to make room, the history records that it left instead of going silent about it.

---

## Upgrade notes

- Sparkle will offer this build to anyone on **0.15.0** or **0.15.0.1** (build 23 → 24).
- Existing named jobs are unchanged.
- Everything in the [0.15.0.1 notes](RELEASE_NOTES_0.15.0.1.md) still applies.

---

## Known limitations

- Mugi requires **Apple Silicon** (M-series); Intel Macs are not supported.
- Local models still miss sometimes. The change is the menu they are choosing from, not a guarantee they pick perfectly.

---

Feedback welcome via GitHub issues.
