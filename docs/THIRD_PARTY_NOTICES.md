# Mugi — Third-Party and Open Source Notices

**Last updated:** June 2026

Mugi (the proprietary macOS application and its bundled local backend) includes
or may download **third-party and open source software** ("Third-Party
Components"). Each component is licensed separately. This document lists the
major components and their licenses.

The Mugi application itself (original SwiftUI UI, orchestration, and
proprietary backend logic) is **not** open source and is governed by the
[End User License Agreement](EULA.md).

Full license texts for common licenses (MIT, Apache 2.0, BSD 3-Clause) are in
**OPEN_SOURCE_LICENSES.txt** in this bundle.

---

## 1. macOS application (shipped in the app bundle)

| Component | Use | License | Copyright / source |
|-----------|-----|---------|-------------------|
| [Sparkle](https://github.com/sparkle-project/Sparkle) | In-app software updates | MIT | Sparkle Project |
| [MarkdownUI](https://github.com/gonzalezreal/swift-markdown-ui) | Markdown rendering in the UI | MIT | González Real |

---

## 2. Python backend (bundled; installed into `~/.mugi/venv` on first run)

The backend is copied into the app bundle (`Contents/Resources/Backend/`) and
bootstrapped into a local virtual environment. Direct dependencies are listed in
`requirements-headless.txt` in that bundle. Representative packages:

| Component | Use | License |
|-----------|-----|---------|
| [FastAPI](https://github.com/tiangolo/fastapi) | HTTP API server | MIT |
| [Uvicorn](https://github.com/encode/uvicorn) | ASGI server | BSD 3-Clause |
| [Starlette](https://github.com/encode/starlette) | Web toolkit | BSD 3-Clause |
| [Pydantic](https://github.com/pydantic/pydantic) | Data validation | MIT |
| [OpenAI Python SDK](https://github.com/openai/openai-python) | LLM client | Apache 2.0 |
| [LangChain Core / Community](https://github.com/langchain-ai/langchain) | Agent tooling | MIT |
| [LangGraph](https://github.com/langchain-ai/langgraph) | Agent graph runtime | MIT |
| [MCP Python SDK](https://github.com/modelcontextprotocol/python-sdk) | Model Context Protocol | MIT |
| [cryptography](https://github.com/pyca/cryptography) | Encryption | Apache 2.0 / BSD |
| [discord.py](https://github.com/Rapptz/discord.py) | Optional messaging bridge | MIT |
| [httpx](https://github.com/encode/httpx) / [requests](https://github.com/psf/requests) | HTTP clients | BSD 3-Clause / Apache 2.0 |
| [NumPy](https://github.com/numpy/numpy) | Numerics | BSD 3-Clause |
| [pandas](https://github.com/pandas-dev/pandas) | Data frames | BSD 3-Clause |
| [matplotlib](https://github.com/matplotlib/matplotlib) | Charts | BSD-style |
| [OpenCV (opencv-python)](https://github.com/opencv/opencv-python) | Image processing | Apache 2.0 |
| [Pillow](https://github.com/python-pillow/Pillow) | Images | HPND (permissive) |
| [pypdf](https://github.com/py-pdf/pypdf) | PDF parsing | BSD 3-Clause |
| [Beautiful Soup](https://www.crummy.com/software/BeautifulSoup/) | HTML parsing | MIT |
| [psutil](https://github.com/giampaolo/psutil) | System metrics | BSD 3-Clause |
| [zeroconf](https://github.com/python-zeroconf/python-zeroconf) | LAN discovery (mesh) | LGPL 2.1+ |
| [sqlite-vec](https://github.com/asg017/sqlite-vec) | Vector search extension | MIT / Apache 2.0 |
| [dulwich](https://www.dulwich.io/) | Pure-Python Git | Apache 2.0 |
| [pytest](https://github.com/pytest-dev/pytest) | Testing (dev/CI; may be present in venv) | MIT |

Additional transitive dependencies are installed by `pip` when the backend
venv is created. Most use MIT, Apache 2.0, or BSD-style licenses.

**Python runtime:** Mugi expects a compatible Python 3 interpreter on the
system or in the managed venv. Python is licensed under the [PSF License
Agreement](https://docs.python.org/3/license.html).

---

## 3. MLX inference stack (optional; installed on demand)

When you enable MLX or install the local model server, Mugi may create
`~/.mugi/mlx-venv` (and optionally `~/.mugi/mlx-utility-venv`) using
`requirements-mlx-pinned.txt`:

| Component | Use | License | Copyright |
|-----------|-----|---------|-----------|
| [MLX](https://github.com/ml-explore/mlx) | Apple Silicon ML framework | MIT | Apple Inc. |
| [mlx-lm](https://github.com/ml-explore/mlx-lm) | Language models | MIT | Apple Inc. |
| [mlx-vlm](https://github.com/Blaizzy/mlx-vlm) | Vision-language server | MIT | Blaizzy et al. |
| [mlx-embeddings](https://github.com/Blaizzy/mlx-embeddings) | Text embeddings | MIT | Blaizzy et al. |
| [transformers](https://github.com/huggingface/transformers) | Model configs/tokenizers | Apache 2.0 | Hugging Face |

**Model weights** (e.g. from Hugging Face `mlx-community`) are separate
downloads with their own licenses (often MIT or Apache 2.0 per model card).
You are responsible for complying with each model's license when you download
it.

---

## 4. Other optional components (installed only when you choose)

| Component | Location | Use | License |
|-----------|----------|-----|---------|
| [Chatterbox TTS](https://github.com/resemble-ai/chatterbox) | `~/.mugi/chatterbox-venv` | Reference-audio voice cloning | MIT |
| [Hyperframes](https://github.com/heygen-com/hyperframes) | `~/.mugi/hyperframes` | HTML-to-video rendering | Apache 2.0 |
| Node.js | `~/.mugi/hyperframes/` (via installer) | Hyperframes runtime | MIT |
| Chromium | `~/.mugi/hyperframes/` (via installer) | Headless browser for Hyperframes | BSD-style |
| FFmpeg / FFprobe | `~/.mugi/hyperframes/` (via installer) | Media encoding | LGPL 2.1+ / GPL (build-dependent) |

Hyperframes installation may download additional npm packages; see the
Hyperframes repository for its dependency tree.

---

## 5. External services (not bundled; user-configured)

If you enable **external LLM backends**, **LM Studio**, **cloud APIs**, or
similar, those services and their client libraries are subject to their own
terms. Mugi does not bundle their server software.

---

## 6. Trademarks

Third-party names (Apple, MLX, Hugging Face, etc.) are trademarks of their
respective owners. Mugi is not affiliated with or endorsed by those parties
unless explicitly stated.

---

## 7. Questions

For questions about these notices, use the feedback channels on
[mugi-ai.com](https://mugi-ai.com) or **Help → About Mugi** in the application.

*This file is bundled in the Mugi app and published at mugi-ai.com/acknowledgements.html.*
