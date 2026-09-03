# Mugi 0.15.0 — Public Beta

Following **0.14.1**. The new thing you can do: **ask Mugi to sort out your Mac**. Why is the camera not working in video calls. Make the pointer faster. Read this command-line tool's manual and get the file converted. It asks before changing anything, shows you the change in words rather than in settings-file jargon, and keeps a list you can undo one row at a time.

Underneath that is the change that made it possible, and it applies to everything else too: Mugi now **works from a map of a document instead of memorising the document**. A manual, a scanned PDF, a long page, a big command's output — the whole thing goes to disk and Mugi queries the part it needs. That is how a person researches, and it is why this release can read a manual at all without ruining the conversation it is having with you.

The other half of that sentence: **it looks things up instead of performing a recollection**. A question you would not want to get wrong used to come back fluent and unchecked. The magnifying glass that used to mean "now do a good job" is gone, because that is just the job.

---

## Highlights

### Sort out my Mac

Ask in ordinary language. Mugi works out which setting is involved, tells you what it is about to change, and waits.

> Make the trackpad pointer faster.

> Show the full path at the bottom of Finder windows.

> Why isn't my camera working in video calls?

- **It asks first, every time.** The approval card leads with the change in plain words — "Finder: Show path bar" — not with the command it is about to run. The command is still there if you want to read it.
- **Some things it will not touch at all.** Your firewall, FileVault, Gatekeeper and the rest of that family are refused outright, no matter how the request is phrased.
- **There is a list of what it changed, and an Undo on each row.** New pane: **Settings → This Mac**. Each row is one setting still different from how you had it — what it is, what it was, what it is now, how long ago.
- **Undo means back to how *you* had it.** If Mugi adjusted the same setting three times while you were tuning it, one Undo returns the value you started with, not the previous step. A tuning session is one thing you did, so it comes back as one thing.
- **It can look at about fifty parts of your Mac now** — camera, firewall, Wi‑Fi, USB, login items, installed apps, install history — instead of the eight categories it used to know. macOS keeps that list; Mugi reads it rather than us guessing which problems you would have.
- **When it finds a repair, it offers you that repair.** Not a shell command for you to vet.

### Learn a command-line tool from its own manual

If a tool is installed and Mugi has not used it before, it can read the tool's own documentation, work out the right invocation, and ask you before running anything that changes a file.

- **It keeps the conclusion, not the manual.** The command that worked gets offered up as a saved skill — the exact command and why — so the next time is instant. The manual stays on disk as a cache; it does not move into the conversation.
- **Your saved skills come back to it.** Procedures you saved on this machine are surfaced to Mugi automatically, so it stops re-deriving something you already taught it.
- **It offers to remember a preference.** If you say you like the pointer fast, it offers to write that down, so a new machine can be set up the way you like it.

### It stops telling you it knows things it does not

Most of this release's remaining work was finding places where Mugi quietly dropped information and then spoke as if it had all of it. Those are the answers that feel confidently wrong.

- **Recollection is not a source.** Before asserting something you would not want to be wrong about, Mugi asks whether the answer could have moved since it was trained — and looks it up rather than recalling it. Answering from memory is fine when it says that is what it is doing.
- **A long page, PDF, scan or command output comes back as a map.** Mugi sees an opening excerpt, the sections, and how to ask for any part. Before, the beginning was pasted in and the rest was thrown away — so an answer that lived on page nine simply did not exist.
- **A big result is never silently shortened.** Whatever the size, the full text is kept and Mugi is told plainly that what it is looking at is a window, and how to reach the rest.
- **"You declined that" is no longer recorded as success.** Turning down a change used to show a green check, and anything reasoning about it afterwards believed it had happened.
- **Questions find their answer.** Searching a captured document for a real question — "what does the -gps flag do" — used to return nothing at all unless you happened to phrase it as the exact words on the page.
- **What Mugi knows about you says when there is more.** The block it reads each turn is a slice of your record, and it now says so, instead of letting "not in this slice" pass as "you never told me".
- **A plan step can be finished.** Steps whose description said "implement", "render" or "deploy" could not be marked done at all, however much work was actually completed — so plans stalled at the point of success.
- **A decision gets treated as a decision.** "I'm choosing between two job offers" now reaches the deliberation flow, which previously needed you to use one of a short list of approved words.

### Research is not a mode you switch on

The magnifying glass in the composer is gone. It read as a quality dial — tell Mugi in advance to do a good job — and that is the wrong shape. Looking things up is the job; a long investigation that will not fit in the turn is a destination you can agree to.

- **In the conversation, it searches.** A question that could have moved gets sources in the reply, without you flipping anything.
- **A job that will take a while can leave the chat.** Mugi asks, then sends it to a background research worker and comes back when it is done. You can still send one yourself with **`/research <question>`**.
- **The limits that used to bound "Research mode"** are now **Settings → LLMs → Background research**. They bound the worker, not a mode.

### Also in this release

- Telling Mugi something is wrong is understood even when you phrase it uncertainly — "it's not a house, it's a condo?" used to be ignored entirely because of the question mark.
- Themes in your studied material are no longer discarded for being longer than six words.
- Searching your own memory and your studied material together no longer loses the studied half when the memory half is large.
- Watchlist changes say *which* wording caught their attention, so "urgent" is something you can judge rather than take on faith.
- The update check no longer opens behind the splash. Mugi waits until the window is up before looking for a new build; **Mugi → Check for Updates…** still works immediately.

---

## Upgrade notes

- Restart Mugi once after updating.
- Sparkle will offer this build to anyone on **0.14.1** (build 21 → 22).
- **The Research mode toggle is gone.** One tap used to send the next message — and every message after it, until you noticed — to a background worker. That is no longer how research starts. Lookups happen in the conversation; a long job is something Mugi offers, or you send **`/research …`**. The settings section is now **Background research**.
- **There is no master switch for changing settings, because every change asks you first.** The protection is the approval card, the list of settings Mugi will never touch, and the fact that only you — in a normal conversation — can trigger one. Background work, board workers and scheduled runs are refused.
- **Settings → This Mac has a "Remember what changes on this Mac" toggle, on by default.** That is what keeps the list you can undo from. Turning it off means changes still ask, but nothing is recorded, so there is nothing to undo afterwards.
- **Reading a tool's manual and running scripts** stays behind its existing switch in Settings → Advanced.
- Anything Mugi changed before this release will not appear in the This Mac list — the list starts from the first change it records with this build.

---

## Known limitations

- Mugi requires **Apple Silicon** (M-series); Intel Macs are not supported.
- The This Mac list does not refresh while the pane is open. Close and reopen it after a change made in chat.
- Settings that an app owns can be overwritten by that app when it next quits. Mugi restarts the app for the settings it knows about; for others, quit the app first.
- After a repair, Mugi cannot re-diagnose in the same turn to confirm it worked. Ask again.
- One Undo restores the value you started with, but only for changes Mugi itself made. It will not undo something you changed by hand.

---

Feedback welcome via GitHub issues.
