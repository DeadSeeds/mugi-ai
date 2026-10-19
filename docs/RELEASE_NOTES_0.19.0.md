# Mugi 0.19.0 — Public Beta

This one is about letting Mugi do more than one thing at a time, about telling
you which model is answering when you bring your own engine, and about the task
board telling you the truth about what happened.

## What's new

- **Pick the model per conversation on a remote engine.** When you use
  **External API** (an OpenAI-compatible server — LM Studio, Ollama, vLLM, a
  cloud endpoint), a **model menu now sits under the composer**. It lists what
  the server actually offers and answers *this* conversation with the model you
  choose; the top row returns the chat to your Settings default and names which
  model that is. The choice is saved with the conversation, and it never leaks
  onto the built-in or Exo engine. If the server stops offering a model, Mugi
  keeps your pick visible, answers with the server's default for that turn, and
  says so in chat — rather than failing mid-reply or quietly forgetting.
- **Your work can share the model.** **Model slots** in **Settings → LLMs →
  Parameters** lets a background job — a Kanban worker, a research task — run
  alongside your conversation. Each reply takes a little longer and the local
  model uses more memory. **Restart Model** applies a change in about 15
  seconds, and **Diagnostics** shows the width the engine is actually serving,
  so you are never told a number nobody enforced.
- **The task board says what really happened.** A cancelled card is reported as
  cancelled, not finished. A card you asked Mugi to *park for later* shows
  **Parked for later** and waits for you instead of looking like a failure.
  Newly filed cards appear on the board immediately, and a running card keeps
  the Mac awake (down to 30% on battery).
- **Large local models start with a usable window.** On some bigger models the
  automatic context setting resolved to a few hundred tokens, so ordinary
  prompts were refused outright. Mugi now checks the window before calling the
  engine ready, and starts at a size that works.
- **Editing a Results page works the first time.** A save whose text was
  already in place is no longer reported as an error, and an edit sent as page
  content is accepted instead of refused for a missing field.
- **Plans don't get refused as duplicates.** When a Goal re-checked its plan
  after a restart, it could be told the board was still busy and file nothing.
  It now recognises the work it already filed.
- **A forgotten thing stays forgotten.** If you forget something, Mugi also
  hides it when the same fact comes back in different words.
- **The manual covers what's new.** Model slots, the per-conversation model menu
  on an External engine, and the parked-card state are documented, including
  what **Cancel** does.

## After you update

- **Nothing to do.** Your conversations, notes, memory and board are unchanged.
- Mugi still requires **macOS 26.2 or later** on **Apple Silicon** — Intel Macs
  are not supported.

## Known limitations

- More than two model slots is untested; two is what has been measured.
- The local search engine runs inside a virtual machine that takes about **10 GB**
  of disk. It works; it is just far heavier than the job it does.
- A one-page HTML deliverable can take a few minutes to appear, and it appears
  when it is finished rather than building up on screen.

Feedback welcome via GitHub issues.
