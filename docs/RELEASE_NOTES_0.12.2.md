# Mugi 0.12.2 — Public Beta

Patch release following **0.12.1**. Focus: **doing the boring, hard work honestly** — reading whole documents instead of the first few pages, handing back a real Word file you can edit, reaching you over iMessage, and being much clearer about what Mugi may read and where an answer is allowed to go.

---

## Highlights

### Documents you can actually work with

- **Structure-preserving PDF ingest** — headings, numbered lists, and tables survive extraction instead of collapsing into a wall of text. A procedures document keeps its numbering.
- **Word (.docx) export** — ask for a document and get one back, not homework. Deliverables in Results export to DOCX with real headings, lists, and tables.
- **Edit in Results** — a document Mugi wrote is now editable in place, with a live-formatting editor rather than a raw markdown box. Bold looks bold while you type; the file underneath stays clean markdown.
- **Tables render as tables** — in chat and in Results. Header row, cell borders, and text that wraps inside cells instead of being flattened into a pile of bullets.

### Reading the whole thing, or saying exactly what was missed

Several read paths were quietly capped at numbers chosen when initial development of the app began, and the model would summarize the first few pages as though it had read everything. That class of bug is now gone across the board.

- **File reads size themselves from the model's context budget** rather than a hardcoded window, and no longer elide the middle of a document.
- **Web pages paginate** — long pages can be read through to the end instead of being truncated with an apology.
- **Attachments** derive their limit the same way, and dropped files no longer point you at a tool that isn't available.
- Where something genuinely *was* cut short, Mugi now says which part it read.

### Reach Mugi from your phone — iMessage

- **iMessage inbound** joins Discord as a way to reach Mugi while you're away. Only **you** can trigger it, by design.
- **Your messages are told apart from Mugi's** — replies are marked, so a thread with yourself doesn't read as one confusing monologue.
- Outage logging no longer repeats the same failure every three seconds.

### Who is asking, and where the answer goes

Personal context and remote messaging surfaces needed a real boundary rather than one blurry notion of "trust".

- **Caller and destination are now separate questions.** Reading your private life and sending an answer to a room you don't own are governed independently.
- **Tools that would be refused are no longer offered** — the model doesn't see a capability it cannot use from that surface.
- **A refusal explains itself in plain words** meant for you, instead of an internal policy code.
- **An untrusted caller gets conversation and nothing else** — no file reads, writes, or deletes.

### Undo, outside the Vault

- **The previous version of every file Mugi touches is kept**, so an edit it made can be walked back — not just Vault notes.
- Copies and moves that quietly replace an existing file are covered too.

### Folder access you can grant in the moment

- When Mugi needs a folder it isn't allowed to read, it **asks in a dialog** and waits for your answer, the way shell commands already work.
- **A declined folder is respected** — it isn't asked about again, and no leftover buttons pile up in the chat.
- Shell `find` commands that are really file searches are routed to the proper search tool, so the dialog can't be sidestepped.

### Screen awareness, Contacts, and the morning brief

- **Ask what's on your screen** via a hotkey — and when capture fails, Mugi says why instead of guessing.
- **Watch-this actually watches**, and reported snapshots carry their date.
- **Contacts** support, with permission handling.
- **Morning brief** — an opt-in start-of-day summary, with four defects found in live smoke testing already fixed.

---

## Also in this release

- **Conversation traces are no longer kept forever.** Trace logs had no retention policy and grew unbounded; they now prune. Old files are cleaned on upgrade.
- `background.log` rotates by copy-truncate and is **no longer world-readable**.
- "No" means no — dismissing a suggestion stops it being re-proposed.
- Research synthesis compares claims rather than digits, and a timed-out prefetch is salvaged instead of discarded.
- Background durations are measured on a clock that ignores system sleep.
- Counters now record what actually happens across recall, denials, and tool use, so future tuning stops being guesswork.
- Assorted test-isolation fixes so the suite stops writing to real `~/.mugi` state.

---

## Upgrade notes

- Restart Mugi once after updating.
- **iMessage** is opt-in and requires Full Disk Access plus your own number under **Settings → Messaging**. Only your number can trigger it.
- **Contacts** and **screen capture** prompt for macOS permission the first time they're used.
- Old conversation trace files are pruned on first launch after upgrade. This is expected and frees disk space.
- If a folder search refuses, Mugi will now ask for access directly — granting in that dialog is enough; you don't need to visit Settings.

---

## Known limitations

- Mugi requires **Apple Silicon** (M-series); Intel Macs are not supported.
- The research-mode toggle and its per-run URL budget do not yet reach the kernel that runs the turn; treat those controls as inert for now.
- Duplicate tool calls issued within a *single* model response are not yet de-duplicated — only repeats across turns.
- Nested list indentation in the markdown editor is still off, and tables can be viewed but not edited in edit mode.
- Preferences / Advanced IA cleanup remains deferred to a dedicated prefs program.

---

Feedback welcome via GitHub issues.
