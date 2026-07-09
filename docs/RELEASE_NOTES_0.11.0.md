# Mugi 0.11.0 — Public Beta

Release following **0.10.3**. Focus: **Vault as its own notebook**, **Knowledge Library maturity**, and **kernel cutover completion**.

- Build number **13** (Sparkle compares `CFBundleVersion` for same marketing version).

---

## Highlights

### Vault — a dedicated notebook

Vault is no longer a filter inside Activity. It has its own front door, module, and vocabulary: **Vault** holds **Notes** (not "captures").

- **Dedicated Vault workspace** — browse, write, and organize notes without triage-inbox chrome in the way.
- **Rich note editor** — proportional typography, comfortable reading measure, and improved markdown rendering (including tables).
- **Hybrid search** — full-text plus semantic recall so older notes are findable beyond the recent-500 substring scan.
- **Related inspector** — embedding and wikilink neighbors beside the note, in plain language instead of buried graph jargon.
- **Projects sidebar & toolbar** — clearer project navigation and note actions.
- **Wikilinks & recently deleted** — link notes with `[[…]]`; recover mistakes from a recently-deleted list.
- **On my mind stays separate** — the Activity triage queue is its own task; Vault is the library you keep.

### Knowledge Library — workspace, graph, and trust

The Library graduates from a mode-picker into a continuous study surface.

- **Knowledge workspace** — one library with search, reader, and inspector instead of five subsystem tabs.
- **Graph mode & Connections explorer** — see how sources relate; open passages from the graph.
- **Unified field mode** — browse and read without mode-switching context loss.
- **Inspector & reader customization** — typography controls, source editing polish, and clearer loading/error states.
- **Source repair & rename** — fix broken digests and rename corpora without starting over.
- **First-run hero & ingest profiles** — clearer onboarding when you add your first corpus.
- **Ambient knowledge injection** — relevant studied material can inform foreground chat with attribution (when enabled).
- **Hardening gates** — automated eval and golden-path tests guard retrieval and graph consistency.

### Kernel & reliability

- **Kernel cutover complete** — legacy `execute_raw_agent` path removed; chat and workers run on the kernel stack by default.
- **Activity trust summary** — faster, cached health blocks for Knowledge, Vault, and related subsystems.
- **Near-duplicate reply guards** — fewer redundant memory searches and repeated assistant turns under load.

### Kanban & research quality

- **Outcome signals & provenance** — task-plan and Kanban workers record structured outcomes for evaluation.
- **Research report quality gate** — clearer evidence requirements before a report is accepted.
- **Kanban progress thumbnails** — richer worker progress metadata for long-running tasks.

---

## Also in this release

- **Evolution features** enabled by default (text evolution and workspace git evolution where configured).
- **Capability metrics** in Settings → Advanced — live view of what the backend exposes.
- **MLX loading** — improved server verification when switching models.
- **PDF extraction** — better section titles and verse-marker handling for religious/structured texts.
- **Markdown tables** in chat rendering.

---

## Upgrade notes

- No settings migration required.
- **Restart Mugi once** after updating so Vault search indexes and Knowledge graph caches rebuild cleanly.
- If you used Vault heavily inside Activity before, look for **Vault** in the sidebar — your notes are unchanged; only the navigation moved.
- Knowledge corpora and studied attachments from 0.10.x carry forward unchanged.

---

## Known limitations

- **Vault hybrid search** indexes in the background; very large notebooks may take a minute after first launch before semantic recall is fully warm.
- **Ambient knowledge** respects your consent settings — Mugi will not silently quote private corpora without the relevant toggles and attribution path enabled.
- Mugi requires **Apple Silicon** (M-series); Intel Macs are not supported.
- Council **Skip** remains transcript-silent; task plan refresh can still time out under heavy load (cached steps + retry banner).

---

Feedback welcome via GitHub issues or your usual channel.
