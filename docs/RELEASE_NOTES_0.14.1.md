# Mugi 0.14.1 — Public Beta

Patch following **0.14.0**. The new thing you can do: **hire someone by name**, give them a charter and a stop-line, and put real work on the board for them. Chat can hire, narrow, and retire; Settings can widen, reinstate, or delete. The rest of this release is the reliability that work needed so a finished agent looks finished, and a denied capability actually stays denied.

---

## Highlights

### Hire someone by name

You used to assign board work to a generic profile (`general`, `research`). That is still there. Now you can also hire a **named role** — “Workspace clerk”, “Brief researcher” — with a short charter and a stop-line for what they must never do.

- **Chat can hire, narrow, and retire.** Ask in ordinary language. Named jobs are on by default. Settings → Kanban is where you widen what a role may do, turn them off, and hard-delete a retired one.
- **Work is durable.** Put a task on the board for them. It survives a restart, shows their title on the card, and completes the way the rest of the board already does — the worker finishes; you do not mark it done by hand.
- **A stop-line is a capability, not a verb.** If they must not write files, denying one write tool closes the rest of that family. A different name will not work around it.
- **Unknown and retired roles are refused.** Filing work for someone who does not exist, or who you already retired, fails closed instead of running with full tools.

In chat, that looks like this:

> Hire a workspace clerk. They own short file notes in the workspace. They must never use the shell or send email.

Then, once they exist:

> Put one durable board task on the clerk: write a short hello note to `notes/hello.md`. File it once — do not create a batch.

Name the person, say what the work is, and say it is one board task. Completions come back in this conversation. To retire them later: “Retire the workspace clerk.”

### Finished work looks finished

A role that did its job used to look unreliable at the edges even when the work itself succeeded. This release closes those:

- When a task completes, chat summarises it. It does not file a second copy of the same work, and it does not spend minutes retrying a create that was already refused.
- If they honestly cannot finish — a denied write, a missing tool — the board keeps **their** summary, not a throwaway “handoff submitted.”
- Writes that guessed the wrong home directory land in yours, and the recorded path matches the file that was actually written.
- Completions still come back to the conversation you are in, even if the assign was phrased as “this thread.”
- When a board completion injects into chat, Results can be saved from that turn instead of being blocked as “background.”

### Also in this release

- Knowledge document counts sit where they belong.

---

## Upgrade notes

- Restart Mugi once after updating so named-job tools and the board pick up the new catalog.
- Sparkle will offer this build to anyone on **0.14.0** (build 19 → 20).
- Named jobs are **on by default**. Turn them off in **Settings → Kanban** if you do not want chat to hire. An existing config with `[jobs].enabled = false` stays off. Existing pre-release hires keep their rows.

---

## Known limitations

- Mugi requires **Apple Silicon** (M-series); Intel Macs are not supported.
- Chat can still claim it filed a board task before it has actually done so — glance at the board if a hire or assign looks too fast.
- Provisional facts, the research-mode URL budget, and markdown table editing are unchanged from 0.14.0.

---

Feedback welcome via GitHub issues.
