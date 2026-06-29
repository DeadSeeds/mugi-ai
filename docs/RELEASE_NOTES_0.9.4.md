# Mugi 0.9.4 — Public Beta

Patch release following 0.9.3. Focus: remove bundled LLMster (LM Studio headless) from Mugi.

---

## Highlights

### LLMster removed
- Mugi no longer installs or manages **LLMster** / LM Studio headless on port `:1234`.
- **Local inference** is **MLX only** (Settings → LLMs). Default backend URL is now `http://127.0.0.1:8000/v1`.
- **External backend** unchanged — point at desktop LM Studio, Ollama, vLLM, or any OpenAI-compatible API.
- On upgrade, existing `use_local_ollama` prefs migrate to MLX (`mlx_enabled`) with backend URL reset to `:8000` when appropriate.

### Setup wizard
- Removed the "Install llmster (GGUF models)" onboarding path. Choices are MLX, external API, or configure later.

### App menu
- Fixed duplicate **About Mugi** entries in the Mugi menu (custom About now replaces the system default).

### Release engineering
- Build number **5** (Sparkle compares `CFBundleVersion` for same marketing version).

---

## Upgrade notes

If you relied on Mugi-managed LLMster:
1. Switch to **MLX** in Settings → LLMs, or
2. Run **desktop LM Studio** (or another server) and enable **Use external backend** with your API URL.

Your `~/.mugi/.lmstudio` data is not deleted automatically.

Existing 0.9.0–0.9.3 installs: **Mugi → Check for Updates…** after this build is published to Sparkle.

Fresh install: download from [mugi-ai.com](https://mugi-ai.com) or use the GitHub release artifact (`Mugi-0.9.4.zip`).

---

## Requirements

| | |
|---|---|
| **OS** | macOS 15.0 (Sequoia) or later |
| **Hardware** | Apple Silicon strongly recommended |

---

## Known limitations

0.9.4 remains a **public beta**. Automated release-gate live batteries may occasionally flake on model-dependent user-trust cases; hard gates still cover storage, kernel boundaries, Kanban workers, and delivery seams.

Feedback welcome via GitHub issues or your usual channel.
