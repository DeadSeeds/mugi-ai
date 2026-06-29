# Mugi 0.9.3 — Public Beta

Patch release following 0.9.2. Focus: open source licensing compliance, legal notices in the app and on the website, and About / Help access to license documents.

---

## Highlights

### Licensing & legal
- **EULA v0.9.3** — third-party and open source software section; proprietary-only restrictions; OSS carve-out.
- **THIRD_PARTY_NOTICES.md** — bundled acknowledgements for Sparkle, MarkdownUI, Python backend, MLX stack, Chatterbox, Hyperframes, and optional runtimes.
- **OPEN_SOURCE_LICENSES.txt** — MIT, Apache 2.0, and BSD 3-Clause full texts in the app bundle.
- **Help → About Mugi** and **Mugi menu → About Mugi…** — view License Agreement and Open Source Acknowledgements.
- **mugi-ai.com/acknowledgements.html** — public acknowledgements page linked from the EULA and site footer.

### Release engineering
- Build number **4** (Sparkle compares `CFBundleVersion` for same marketing version).
- EULA acceptance version bumped — existing installs re-accept on first launch after update.

---

## Requirements

| | |
|---|---|
| **OS** | macOS 15.0 (Sequoia) or later |
| **Hardware** | Apple Silicon strongly recommended |

---

## Upgrade

Existing 0.9.0 / 0.9.1 / 0.9.2 installs: **Mugi → Check for Updates…** after this build is published to Sparkle.

Fresh install: download from [mugi-ai.com](https://mugi-ai.com) or use the GitHub release artifact (`Mugi-0.9.3.zip`).

---

## Known limitations

0.9.3 remains a **public beta**. Automated release-gate live batteries may occasionally flake on model-dependent user-trust cases; hard gates still cover storage, kernel boundaries, Kanban workers, and delivery seams.

Feedback welcome via GitHub issues or your usual channel.
