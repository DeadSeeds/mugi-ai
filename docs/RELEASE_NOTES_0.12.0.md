# Mugi 0.12.0 — Public Beta

Release following **0.11.0**. Where 0.11.0 was about the rooms you keep (Vault, Knowledge), **0.12.0 is about Mugi doing things**: acting on your Mac apps with your confirmation, bringing pages and media into your workspace, and starting up like a real first-party app instead of a blank window.

---

## Highlights

### Act on your Mac apps — only when you ask, and only after you confirm

Mugi can now drive the Mac apps you name and approve, instead of just talking about them.

- **App control with confirmation** — Calendar, Notes, Mail, Finder, and other apps you name, actuated only when you ask and only after you approve each action. Nothing runs silently.
- **Calendar & Mail tools** — create events and draft messages with clearer validation and a confirm step before anything is sent or saved.
- **Access, not folklore** — App control lives under Access alongside the other permissions, next to the refusal it unblocks.



### Bring things in — save, download, convert

- **Save a webpage** — capture an article or page into your workspace from chat or a pasted URL, so you can read, search, and discuss it later.
- **Download & convert media** — download-video and convert-media skills turn "grab this and make it usable" into a real action.
- **Deliverable cards** — results of a task arrive in chat as cards you can act on, not just a wall of text.
- **Auto-subscribe on fetch** — pulling something in can keep it fresh, with the downloads surface reported in Diagnostics.



### A calmer, clearer launch

- **Phase-weighted startup** — an honest progress bar across backend → settings → model → conversations, with plain-language status.
- **Real failure path** — if the backend can't start, you get "Couldn't start Mugi" with **Retry** and **Continue anyway**, not a dead window.



### Chat that stops fighting you

- **Compact Work Panel & reserved status slot** — tool activity no longer shoves the transcript around while Mugi works.
- **Focus & continuity** — composer focus is restored after a turn, streaming and arrival are smoother, and a long-running turn resumes cleanly after an idle gap.
- **Model pin** — `mlx-vlm` 0.6.4 (text chat + native tool calls validated on Qwen3.6 / Gemma 4).



### Skills & capabilities, on your terms

- **Optional capabilities disclosure** — Settings → Advanced groups installers (file transcription, Playwright, OCR, utility MLX, and more) under one **Optional capabilities** section instead of a flat wall of switches; search auto-expands the right group.
- **Clearer capability states** — capability enable markers and honest stubs when something is off, plus improved tool discovery so skills are easier to reach.
- **Local file transcription** — transcribe audio on device via the Advanced install path.
- **Bring-your-own search keys** — add paid search API keys for web search when you want them.



### Trust & diagnostics

- **Trust ledger** — a running record of what the assistant did, surfaced in Diagnostics.
- **Knowledge status honesty** — clearer corpus display status and store-consistency handling so the Library reflects its real state.
- **Downloads reporting** — the downloads surface now shows up in health checks.



### Vault & Knowledge polish

- **Vault insights in plain language** — "Not linked yet" / "Themes" / "Recent activity" instead of graph jargon; media renders in the rich note editor; commit-a-note-to-Results intent.
- **Knowledge vocabulary cleanup** — user-facing "Related passages" became **Related** / **Excerpt** / **Themes**; the chunker no longer leaks into the room.



### Background calm

- **Drive & observation hardening** — fewer JSON parse failures and less redundant background work.
- **Near-duplicate reply guards** — fewer repeated memory searches and duplicate assistant turns under load.

---



## Also in this release

- **Watchlist & feeds** — improved management of watchlists and feeds.
- **Results projects** — rename projects and commit work into them more reliably.
- **Kanban** — board refinements and fallback host configuration for durable work.
- **Global Dashboard** — the shortcut is **⇧⌥D** from anywhere.

---



## Upgrade notes

- No settings migration required.
- **App control (AppleScript) requires your approval** — grant access under Settings → Access, and confirm each action. Nothing is actuated silently.
- **Restart Mugi once** after updating so caches and indexes settle cleanly.
- Your Vault notes, Knowledge corpora, and studied attachments from 0.11.x carry forward unchanged.

---



## Known limitations

- Mugi requires **Apple Silicon** (M-series); **Intel Macs are not supported**.
- **Knowledge readiness** — a corpus can report ready while its semantic index is still warming; Ask/Search may be briefly empty right after a large digest. Give it a minute and retry.
- **Full voice conversation is not a shipped chat mode.** On-device **transcription** and **text-to-speech** are available; a hands-free duplex conversation mode is not enabled in this build.
- **Web research** works best with SearXNG (Docker) or Playwright set up for browser-grade results; a public fallback is used when neither is available.
- Mid-size local models sometimes need a nudge to reach for the right tool (notebook, Results, Study) — bigger or recommended models find the path more often.

---

Feedback welcome via GitHub issues.