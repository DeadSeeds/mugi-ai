# Mugi 0.18.0 — Public Beta

This one is about Mugi remembering you properly. The old **About You** page is
gone, replaced by a memory you can read, correct, and forget — and Mugi now
keeps only what you actually said.

## What's new

- **Mugi remembers you, and you can see it.** A new **You** page in Settings
  shows what Mugi has kept, in your own words. Anything it only half-knows is
  shown as something to confirm, not stated as fact.
- **Only what you said gets kept.** Mugi no longer files facts about you from
  background guesswork. Anything it merely assumed before comes back to you as a
  question you can answer or drop.
- **Secrets stay out of the model.** Tell Mugi a number to keep — an account, a
  code — and it goes straight to your Mac's Keychain. Mugi can use it when you
  ask, each time with one Touch ID confirmation, but never sees the value and
  never writes it down.
- **Forget means forget.** Forgetting something now also hides it when it comes
  back in different words. Mugi used to keep showing the same fact rephrased.
- **One place to choose your engine.** **Settings → LLMs** lists the engines
  plainly — **mlx-serve**, **oMLX** as a second on-device engine, plus
  **Exo** and **External API** — and says up front what each one can load,
  instead of failing later.
- **Your work can share the model.** **Model slots** in **Settings → LLMs**
  lets a background task run alongside your conversation. Each reply takes a
  little longer and the local model uses more memory; **Restart Model** applies
  a change in about 15 seconds, and Diagnostics shows the width the engine is
  actually serving.
- **The task board tells the truth.** A cancelled card is no longer reported as
  finished, a card you park for later stays parked instead of looking blocked,
  and newly filed cards appear on the board right away. Running cards also keep
  the Mac awake, down to 30% on battery.
- **The model's window no longer collapses.** On some larger local models the
  automatic context setting resolved to a few hundred tokens, so ordinary
  prompts were refused; Mugi now checks the window before calling the engine
  ready and starts at a usable size.
- **Editing a Results page works the first time.** A save whose text was already
  in place is no longer reported as an error, and an edit sent as page content
  is accepted instead of being refused for a missing field.
- **Mugi has one engine story, not three.** The old bundled "Splash" engine and
  adapter training are gone; the manual now says so rather than hedging.
- **Your chats come back.** Relaunching Mugi returns you to the conversation you
  left, **Stop** keeps the reply you already watched arrive, and a slash command
  no longer disappears when the view reloads.
- **First-run install is fixed.** The three failures from the Mac Studio report
  are fixed — one step that cancelled every step after it, a directory error on
  setup, and an error that swallowed its own reason — and setup failures now
  explain themselves in plain words with a way forward.

## After you update

- **Nothing to do.** The first time Mugi starts, your existing notes are carried
  into the new memory, once. Anything the old system recorded without you ever
  saying it comes back as a question you can confirm or dismiss, rather than
  being kept as fact.
- Mugi still requires **macOS 26.2 or later** on **Apple Silicon** — Intel Macs
  are not supported.

## Known limitations

- The local search engine runs inside a virtual machine that takes about **10 GB**
  of disk. It works; it is just far heavier than the job it does.
- A one-page HTML deliverable can take a few minutes to appear, and it appears
  when it is finished rather than building up on screen.

Feedback welcome via GitHub issues.
