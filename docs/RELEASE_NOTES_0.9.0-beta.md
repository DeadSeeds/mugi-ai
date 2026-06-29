# Mugi 0.9.0 — Public Beta

**Mugi** is a local AI companion for macOS built around a simple idea: it should *notice* things about you over time — and show you what it noticed so you can accept, edit, or reject it. Nothing important happens silently.

**0.9.0 is a public beta**, not a finished 1.0. It has been through extensive automated testing (release gate, soak, cold-install ladder), but it is early software from a solo project. Kind, specific feedback is very welcome.

---

## Highlights

### A relationship, not just a chat window
- **You** pane (Settings → You) — personal facts arrive as **proposals** with before/after diffs. You review; Mugi doesn’t auto-rewrite who you are.
- **Activity** feed and **On my mind** — background observations surface for approve / discuss / dismiss, not silent execution.
- Protected personality files after onboarding — the agent routes durable personal facts through review surfaces.

### Your notes and knowledge, first-class
- **Vault** — capture notes, voice memos, attachments; open any item in chat with **Discuss this**.
- **Knowledge** — point Mugi at folders or repos; get synthesis, studied sources, and a queryable graph.

### Durable background work
- **Kanban** — cross-session task board with encrypted storage, worker handoffs, and terminal notifications.
- **Council mode** (opt-in) — multi-seat debate pipeline for complex questions when you want extra rigor.

### Local-first on Apple Silicon
- **MLX** recommended for on-device inference; OpenAI-compatible APIs supported if you prefer remote models.
- Bundled Python backend — no Terminal required; first-run wizard handles setup.
- Optional **local web search** via SearXNG + Colima (onboarding path hardened for first install).

### macOS-native app
- SwiftUI interface with sidebar (conversations, Vault, Kanban), Live View, compact panel, global hotkeys.
- **Sparkle** auto-updates — **Mugi → Check for Updates…** after install.

---

## Requirements

| | |
|---|---|
| **OS** | macOS 15.0 (Sequoia) or later |
| **Hardware** | Apple Silicon strongly recommended (MLX, local Docker/Colima path) |
| **Disk** | ~2–8 GB+ depending on models and Knowledge corpora |
| **Network** | Required for first-run setup (Python/runtime download); optional thereafter if fully local |

---

## Getting started

1. Download **Mugi.app.zip**, unzip, and open **Mugi**.
2. Accept the **license agreement**, then follow the **setup wizard** (Recommended path is fine for most people).
3. Complete onboarding — personality files are created; first chat should feel personal.
4. Explore **Settings → You** when proposals appear.

**First launch:** Use the notarized build from this release. If macOS still blocks the app, right-click → Open once.

---

## Safe defaults (beta)

| Feature | Default |
|---------|---------|
| Mesh federation | Off |
| Council mode | Off |
| Web automation scripts | Off |
| Kanban mesh agent creation | Off |
| Background drives | Bounded |

---

## Known limitations (beta)

- **Public beta** — expect rough edges, especially around long MLX sessions and first-time Docker/Colima setup.
- **Apple Silicon focus** — Intel Macs are not a supported target for local search / Colima onboarding.
- **Model quality varies** — smaller local models may need patience; tool-heavy workflows benefit from larger models or a capable API.
- **Auto-updates** — after install, **Check for Updates…** may take a few minutes to work once this release finishes publishing.
- **Not 1.0 yet** — APIs, defaults, and UX may change before a stable release.

---

## Feedback

- **Bugs & ideas:** GitHub Issues (label `preview-feedback` if you like)
- **Especially helpful:** Does the **You** pane feel useful vs. creepy? Did first-run setup complete without confusion?

---

Built with care on a Mac, for Mac people who want an assistant that remembers — with consent.
