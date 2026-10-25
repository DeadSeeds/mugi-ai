# Mugi 0.20.0 — Public Beta

This one is about the moments when a reply does not arrive the way it should:
a long answer still being written, a reply that stops halfway, a Stop you
pressed on a silent engine, a model that will not fit in this Mac. In each case
Mugi now keeps what you already watched arrive and says plainly what happened.

It is also the release where **Mugi makes pictures and clips on your own
machine** — make an image, change one you already have, or turn a still into a
few seconds of video — and every render finally has a folder, a Settings pane
and a Dashboard tile that show it.

## What's new

### A reply appears as it is written

The answer used to be held back until nearly the end and then appear in one
piece. It now streams into the bubble while the model is still writing, the
same way you watch it think. Nothing is retyped or replayed when the turn
finishes.

### A reply that stops arriving is marked as cut, not passed off as the answer

Quit mid-answer, or an engine that dies mid-stream, used to leave a half
sentence sitting in the thread as if it were the finished reply — or, worse,
replace everything you had already read with one line of internal parser text.

Now the text that streamed stays exactly where it was, followed by a sentence
that says so:

> This answer was cut off before it finished. Send again — or ask me to
> continue — and it will pick up from here.

The detail an operator needs is kept behind that sentence, not shown instead of
your answer, and the row is recorded as a partial reply rather than a finished
one. On reopen the same sentence is there, so a cut answer never looks complete.

### Stop is instant, even when the engine has gone quiet

Pressing **Stop** while the spinner was up did nothing until the engine sent
another token — up to two minutes of a turn you had already cancelled, which
then sometimes generated a second answer you did not ask for. Stop is now
noticed in about a second whether or not anything is arriving, keeps the text
that was already on screen, and does not retry a turn you ended.

### When a model will not fit, Mugi gives you the arithmetic

A model that does not fit this Mac used to fail with "the model server stopped
before it finished loading", which names nothing you can act on. It now says
what it needs and what is available — for example *"needs about 40.5 GB free
(29.0 GB of weights). This Mac has 9.4 GB"* — and the suggestion fits the
failure: a shorter message when the window is the problem, quit-and-reopen when
memory is, instead of a **Restart Model** button that cannot help.

The same care applies to ordinary memory pressure during a turn: you get a
sentence instead of the engine's JSON, and Mugi no longer tells you to retry
something the engine has already said cannot fit.

### The engine's log survives the restart that recovers from an incident

Restarting the engine used to open its log with truncation, so the record of
the crash was erased by the very restart that came after it. Each launch now
keeps the outgoing run as a timestamped generation (the newest three), and a
start-up that launches the engine twice no longer overwrites the run that was
live before you restarted. Diagnostics can be read after the fact.

### Make a picture, change a picture, make a clip — on this Mac

Mugi can now make images and short videos with local models. Nothing is
uploaded, there is no account in the middle, and the media models live in the
same folder as your chat models.

- **Ask for a picture** — *"draw a workshop at night"*, *"make me an image
  of…"* — and it arrives in the conversation, saved to disk instead of pasted
  in as bytes, so a folder full of renders does not make every later turn more
  expensive. It appears inline, so you do not have to go and find it.
- **Ask for a change instead of starting over.** *"Turn this into watercolour"*,
  *"remove the background"*, *"make the sky darker"*. Point it at the picture
  you attached or one Mugi just made, and it keeps that picture's subject and
  composition rather than inventing a new scene.
- **Ask for a clip** — *"a few seconds of the waves moving"* — or **animate a
  still**: a photo you attached, or a picture Mugi just drew. You get an
  ordinary MP4 with a soundtrack of its own; the soundtrack can be switched off,
  and a broadcast frame rate can be asked for and is actually conformed onto the
  finished file rather than quietly ignored.
- **If no picture or clip model is installed, Mugi points at Settings → Media**
  — rather than failing with a decoder error you cannot act on. `~/.mugi/models`
  stays the place the weights live.
- **Get a model without a terminal.** Settings → Media now lists the picture and
  clip models that work with Mugi, tells you before you start whether each one
  fits this Mac's memory, and installs the one you pick with a single button.
  The download shows real progress, keeps going if you leave the pane, and can
  be stopped; what has already been fetched is kept, so pressing Download again
  continues from there instead of starting over.

**Know what it costs in time.** A picture is seconds once the model is loaded.
A four-second clip was measured at just under three minutes on an M4 Max, and
the first render of a session also pays for loading the model. The render keeps
a row with a step count while it works, so you can leave it and come back
instead of watching a spinner.

### Every render has a folder, a pane, and a place on the Dashboard

Generated pictures and clips now land in **`~/Documents/Mugi/Media`** instead of
being mixed in with reports, OCR text and saved results.

- **Settings → Media** shows the newest renders as thumbnails (a clip shows its
  first frame), and sets what a render will be before you ask: picture and clip
  shape and size, clip length and frame rate, silent clips, and a model
  preference per kind. It also says what a render would pick right now,
  including when a saved model has since been removed.
- **Right-click a finished picture or clip** for Open in the right app, Reveal in
  Finder, Save As, and **Make Larger (2×)** / **Make Smaller (½×)**. A picture
  can also be **Redrawn Larger**, which asks the picture model again with the
  prompt that made it, so the extra detail is real.
- A clip can be **rotated** by asking, without enabling developer tools.
- Every render keeps the prompt that made it in a hidden note beside the file,
  so a picture in the folder is never anonymous.
- A render is **a row while it is running**, not only a spinner that leaves with
  the window; if Mugi restarts mid-render the row says it was abandoned instead
  of pulsing forever.
- The **Media Dashboard tile** shows the render in flight with its prompt,
  elapsed time and step count, anything that failed and why, and the newest
  files. Every tile the manifest carries now actually appears on the panel —
  Media and Memory had been registered, enabled and served while being fetched
  by nothing.

### Attachments behave like the file you attached

- A pinned attachment can be read again. Asking for the text of a PDF you
  attached earlier no longer answers that it lives in a "protected or dangerous
  location".
- An iPhone **HEIC** photo now reaches the engine as something it can decode,
  instead of being labelled PNG and refused with a raw error.
- An attached image keeps its identity beside its pixels, so the next turn can
  name it — the same picture can be read *and* used as a picture.

## Fixed

### Personal memory

- **A figure of speech is not a forget.** *"Forget the essay."* used to delete
  unrelated memories: the retry prompt took a value out of the memory block and
  a shared word was enough to match it. A forget now needs the person's own
  wording on the value, or the named slot plus an exact live row — and a
  one-word ask cannot sweep several rows. (Two wrongly-forgotten rows were
  restored.)
- **"What did I have before?"** is answered from the superseded row rather than
  the current one.
- **Rotating a secret** is treated as a correction, so the old pointer is kept
  as history instead of looking like data loss.
- **"Don't bring up X"** now bans the subject, and the ban hides it on read as
  well as refusing the write.
- A cold exclusion judge no longer blanks the whole personal-memory block while
  it is still deciding.

### Everything else

- **The clock line names the weekday**, so "what day is it?" no longer answers
  Thursday on a Friday.
- **Back Up Chats** carries every message, and **Restore Chats** replaces the
  live store safely instead of refusing while it is open.
- **Upgrading** writes the personality sheet before retiring the legacy files,
  so an interrupted upgrade cannot come back to a nameless assistant.
- **Settings → Models** update badge is a control, not a dead end.
- **A failed status read is "unknown"**, never "Not installed" — Chatterbox and
  plugin Disconnect no longer report a wish.
- **A switch in Live View** before the page reloads is no longer silently
  ignored.
- **Vault search** typed past no longer reports an older failure over the newer
  hits.
- **Re-run Setup** and **Full Reset** no longer freeze the window while they
  delete, and the setup wizard's model check no longer freezes while it waits.
- **VoiceOver** labels the composer's attach and send buttons and the message
  actions.
- **Security:** a web page can no longer make Mugi fetch `127.0.0.1` through an
  image link, a localhost page cannot spend Mugi's API cookie, mesh frames have
  a bounded declared size, the Playwright guard covers popups, and a publish
  with no tweet id is a failure rather than "published".

## After you update

- **Nothing to do.** Your conversations, notes, memory and board are unchanged.
- Generated media from earlier versions stays where it was; new renders go to
  `~/Documents/Mugi/Media`.
- Mugi requires **macOS 26.2 or later** on **Apple Silicon** — Intel Macs are
  not supported.

## Known limitations

- A model too large for this Mac still refuses rather than running at a smaller
  size; the message now tells you the numbers.
- More than two model slots is untested; two is what has been measured.
- A turn that asks to run a shell command waits on the approval sheet; after
  five minutes it times out and the model explains the refusal.
- The local search engine runs inside a virtual machine that takes about **10
  GB** of disk.
- Making pictures and clips needs a model that this Mac can actually run. With
  none installed, Mugi points at **Settings → Media** and tells you what each one
  needs before you start the download; a pack that would not fit is refused with
  the arithmetic rather than downloading for twenty minutes and then failing.
- Media downloads are large — a clip model is **tens of gigabytes** — and Mugi
  keeps a margin of free disk space clear instead of filling the volume.

Feedback welcome via GitHub issues.
