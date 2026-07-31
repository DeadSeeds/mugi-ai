# Mugi 0.12.1 — Public Beta

Patch release following **0.12.0**. Focus: **reliability of work that already ships** — Kanban boards that stay honest under load, study and research that route without scavenger hunts, and filesystem search that stops escalating into home-wide shell greps.


---

## Highlights

### Kanban — durable work you can trust mid-flight

- **Dispatcher health honesty** — status distinguishes a live loop from storage that still has in-flight work, and when a Nudge can reclaim an unowned dispatcher without false “restart” on a foreign owner.
- **Softer wakes & reclaim** — create/patch and nudge paths reclaim carefully so helpers don’t double-claim; mid-flight boards recover instead of looking permanently dead.
- **Retry, backoff, and notifications** — clearer eligibility, subscription targeting, and operator-facing failure modes when a worker gives up or needs a follow-up.
- **Worker cwd & shell gates** — kanban workers keep a coherent working directory and refuse shell patterns that don’t belong on the board path.

### Study, research, and skills — less scavenger hunting

- **Library-first study routing** — “study this in my library” promotes the right Knowledge tools instead of asking for a re-upload by habit.
- **Research-brief skill bind** — research-mode and “write a brief” stamp and prefer the web-research path so the first moves are search and synthesis, not tool archaeology.
- **Heartbeat allowlist honesty** — background heartbeats stop advertising tools they can’t run (less WARN noise, fewer dead ends).

### Search & shell — calm misses, clear confirms

- **Filesystem search calm-stop** — after an empty or Access-scoped `search_filesystem` result, search-shaped `shell_execute` (home `grep`/`rg`/`find|grep`) gets an instructional soft-stop: invite Access or a narrower root, don’t escalate over `~`.
- **Stale confirm harden** — shell / HTTP / Swift confirm paths fail louder and recover cleaner when a dialog is already gone.
- **find-in-files skill** — anti-patterns match the calm-stop: no home-shell bypass after Access deny.

### Chat & kernel hygiene

- **Idle / no-progress persistence** — ephemeral retry tails don’t pollute durable history the wrong way; `check-idle-calm` stays green.
- **Kernel diet & budget** — wiring extracts keep always-on tool count at **12** and freeze/budget gates green after the Pass 10/11 work.
- **Council handoffs** — researcher → verifier evidence and delivery wakes behave more predictably when seats finish.

---

## Also in this release

- Auto-checkpoint and chat-storage extracts for clearer kernel foreground lifecycle.
- Proactive observation / trust severity polish on subscription edges.
- Broader Kanban CLI and argument-normalization hardening.

---

## Upgrade notes

- Restart Mugi once after updating so the dispatcher and any in-flight board health refresh cleanly.
- Kanban storage may apply small on-disk migrations on first launch after upgrade (next-eligible / subscription hashing) — automatic; no settings migration required.
- If Documents search still refuses, add the folder under **Settings → Access → Allowed Directories** — that is intentional, not a bug.

---

## Known limitations

- Mugi requires **Apple Silicon** (M-series); Intel Macs are not supported.
- Prose-only offers to “just grep home” (without a tool call) are steered by notices and the find-in-files skill; the soft-stop covers the tool-call path.
- Preferences / Advanced IA cleanup remains deferred to a dedicated prefs program.

---

Feedback welcome via GitHub issues or your usual channel.
