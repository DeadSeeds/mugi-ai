# Mugi 0.17.0 — Public Beta

Following **0.16.0**. Local chat on this Mac now runs through **mlx-serve**, a native engine Mugi installs for you. Settings → LLMs calls it **Local (mlx-serve)**. There is no longer a Python install for the model server.

Because of the engine switch, all builds moving forward will need **macOS 26.2** or later. Apple Silicon is required; Intel Macs are not supported.

---

## Highlights

### Local chat without a Python model server

Mugi downloads the **mlx-serve** binary and keeps it running on your Mac. Pick a model and download recommended ones the way you already did. Chat, background summaries, and Library search all use that one engine.

If a model will not load because your Mac is out of memory, the alert is a plain sentence — not a server log.

### Train is gone for now

mlx-serve does not apply chat LoRA adapters. The Train and Adapters controls in Settings → LLMs are hidden. Adapter folders already on disk are left alone so you can delete them later; they are not used.

### Library search uses a new encoder

Library embeddings now use **Qwen3-Embedding-0.6B**. A library built with the old encoder needs a re-index before search feels right. If search setup needs attention, the Library says so.

---

## Also in this release

- First launch installs mlx-serve when the binary is missing.
- The 1-bit Bonsai / Prism utility model is no longer a choice. Background summaries use **Gemma 4 E2B**. If you still had the 1-bit model selected, pick Gemma 4 E2B under Settings → Advanced.
- Voice transcription still uses the separate audio environments. Spoken replies are unchanged.

---

## Upgrade notes

- Restart Mugi once after updating.
- Sparkle will offer this build to anyone on **0.16.0** (build 26 → 27).
- **macOS 26.2** is required. The setup wizard already blocked older systems; this build will not launch below that floor.
- Leftover `~/.mugi/mlx-venv` and `~/.mugi/mlx-utility-venv` directories are unused and are removed on next start. Chat models under `~/.mugi/mlx/` are kept.
- Re-index the Library after this update if search looks empty or off.
- Everything in the [0.16.0 notes](RELEASE_NOTES_0.16.0.md) still applies except the old Python MLX engine description.

---

## Known limitations

- Mugi requires **Apple Silicon** (M-series) and **macOS 26.2** or later. Intel Macs are not supported.
- Adapter / LoRA training is not available in this engine.
- A very large chat model can still fail to load if your Mac does not have enough free memory. Quit other heavy apps and try again.

---

Feedback welcome via GitHub issues.
