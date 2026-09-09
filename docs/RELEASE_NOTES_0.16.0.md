# Mugi 0.16.0 — Public Beta

Following **0.15.1.1**. The new thing you can do: **put the Library in folders, and change a Word, Excel, PowerPoint, or PDF that is already in it.** Asking to add a sentence, fix a figure, or update a date stages a copy. You look at that copy, then one **Change Documents** card writes it — or doesn’t.

The other half of that sentence: **the conversation is about the thing on screen.** An open Vault note, a Results page, a Library document — “add a line here” and “change the heading” mean that object, not a hunt through the disk.

Underneath, follow-up turns stay fast. Finding a new tool no longer grows the list stuffed into every later round, which used to make the next reply re-read the whole thread.

---

## Highlights

### Folders in the Library

Knowledge is a library of documents you keep, not a pile. You can put them in folders without copying, moving, or deleting the files on disk.

- **New Folder, Add to, Remove from Library.** Removing a document leaves the original file where it was.
- **Drag a document onto another folder, or Move to.** The reader follows. Move does not re-extract or re-summarize.
- **Reading order** is yours to set, and it survives a quit.
- **This folder or Whole Library** when you search or ask. A Whole Library hit shows which folder it came from and opens there.
- **Study into a folder.** An attachment or a file you are looking at can be studied into a folder you name, instead of becoming a new pile.

Searching Settings for Knowledge no longer teaches an internal table name.

### Change a document where it lives

Ask in ordinary language. Mugi outlines the file, stages a copy, and waits.

> Update the retention period in this procedure from 7 years to 10 years.

> Add a draft sentence after the membership paragraph.

- **Word, Excel, PowerPoint, and PDF.** Tables, list items, slides, sheets, charts, images, comments, headers — the engines keep the rest of the file.
- **One approval, titled Change Documents.** Approve writes; Don’t change leaves the original. There is no “allow for N minutes.”
- **You can look at the staged copy and export it** before anything is written, so you are not guessing which file is the proposal.
- **A prior version is kept.** Asking to restore brings the snapshot back behind a second approval.
- **A Library document you already have open is enough.** You do not have to paste the path.

### Chat knows which note or page you have open

Opening a Vault note or a Results page and talking in the same window carries that focus into the turn. Changing a Results heading is one ask. Adding a line to the open Vault note appends it there.

### Originals in Knowledge can be zoomed

PDF and image originals in the Library have zoom controls. The page no longer sits at whatever size happened to fit.

### Follow-up turns stay fast

The tool list no longer grows mid-thread when a new tool is found or first used. That list is the head of the prompt cache; growing it used to make the next round re-read the whole conversation. On Apple Silicon with more than 32 GB, the prompt cache also keeps more whole-prompt snapshots, so a title or capture request between two rounds of your chat does not throw the thread away.

### “Remember this” and “never note that” actually land

A forget or a save could be answered with “Done — that’s scrubbed” and nothing written. Asking to remember, save, or forget now has to call the tool. A casual mention stays off the write path — that is picked up afterwards, the way it always was.

### Optional remote reading for scans

**Settings → Knowledge** can take a Firecrawl API key. Off (the default) keeps every file on this Mac. On sends a copy of scanned or image-only pages to Firecrawl so those pages can be read; Office files still convert locally either way.

---

## Also in this release

- Turning off Vault noticing stays off. The Motion switches do what they say.
- A spoken first turn titles the thread, and only one stop fires.
- Asking what panicked or crashed names the process from the report, instead of wandering through folklore and dumps.
- A helper ask runs as a helper, not as a name dropped into the reply. A precise calculation goes to Python, not the shell.
- A parked card can be started from chat instead of sitting blocked. A filed card hands the turn back, and the tail shows that worker.
- A mesh card that needs a write fails on this Mac, not on the other one.
- Reminders and Calendar go through their own doors; AppleScript is refused when those already exist.

---

## Upgrade notes

- Restart Mugi once after updating.
- Sparkle will offer this build to anyone on **0.15.1.1** or earlier (build 25 → 26).
- **Change Documents is a new approval.** Edits to Word, Excel, PowerPoint, or PDF wait on that card. Deny writes nothing.
- **Firecrawl is off unless you turn it on.** Using it sends a copy of scanned or image-only pages off this Mac.
- Folders in the Library are membership, not a move of your files. Remove from Library does not delete the original.
- Everything in the [0.15.1.1 notes](RELEASE_NOTES_0.15.1.1.md) and [0.15.1 notes](RELEASE_NOTES_0.15.1.md) still applies.

---

## Known limitations

- Mugi requires **Apple Silicon** (M-series); Intel Macs are not supported.
- Local models still miss sometimes. Staging a change is the contract; picking the right paragraph is still the model’s job.
- Totals in Excel that depend on new rows stay blank until Excel opens and recalculates.

---

Feedback welcome via GitHub issues.
