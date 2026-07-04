# Mugi 0.10.3 — Public Beta

Release following **0.10.2.3**. Focus: **chat attachments → durable Knowledge**, **richer document extraction in chat**, and **Knowledge Library reliability** (health, consistency, export).

- Build number **12** (Sparkle compares `CFBundleVersion` for same marketing version).

---

## Highlights

### Study chat attachments in Knowledge

Attachments are great for one-off work in a thread; **Knowledge** is how Mugi remembers a document across future conversations. This release closes that gap — always with your consent, never auto-ingest on upload.

- **Study in Knowledge…** on attachment chips (composer and message bubbles): pick a corpus label, optional update-if-exists, then digest runs in the background.
- **Agent tool `digest_chat_attachment`:** ask in chat — e.g. *“Keep this contract in my knowledge base as Acme – contract”* — and Mugi proposes a label; after you confirm, it stages the file and runs the same digest pipeline as the Library.
- **Post-turn nudge:** after a long attachment-only analysis, a subtle inline hint offers **Study in Knowledge** without blocking the thread.
- **Prompt guidance** distinguishes quick in-thread work (`extract_document_text`, prefetch) from durable study (Knowledge corpora).

Staging copies live under `{workspace}/knowledge/.ingest_staging/` with a 7-day maintenance sweep; the studied corpus keeps human-readable sources under `{slug}/sources/`.

### Document attachments in chat

- **`extract_document_text`** for PDF, plain text, Word, Excel, PowerPoint, and OpenDocument — paginated, size-capped, with OCR fallback where configured.
- **Thread-scoped access:** attachments resolve only in the conversation that uploaded them; cross-thread reads are refused.
- Clearer upload errors (size limits, partial failures) and supported-format hints in the composer.

### Knowledge Library — trust, consistency, and admin

- **Activity trust summary** now includes a **Knowledge** block: manifest health, search/graph drift, connections status, and cap-hit signals when indexes are under pressure.
- **Detect + reconcile** when the search index and chunk graph diverge (`POST /knowledge/{slug}/reconcile`; surfaced in Preferences and the Library).
- **Export and remove corpora** from the Library admin UI.
- **Honester digest status** — fewer “complete but not searchable yet” surprises; improved graph refresh messaging.
- **Citation deep links** open the correct corpus row in the Library.
- **Topic confidence / gap tracking** backend for future “what Mugi doesn’t know yet” surfacing (foundations; not a full UI product yet).

### Install MLX models from Hugging Face

*(Shipped after 0.10.2.3 tag; first included in this build for most updaters.)*

- **Settings → LLMs:** paste a Hugging Face link or `org/name`, run a compatibility check, then download. Progress shows bytes downloaded; the model is pre-selected in the picker — tap **Load model** when ready (download does not switch the active model automatically).
- **Chat:** ask Mugi to install a model from a link; it uses `preflight_mlx_model` then `install_mlx_model` (foreground chat only). Gated repos need `HF_TOKEN` in the backend environment.
- **Third-party pre-converted Qwen3.5 MoE checkpoints** (e.g. some community MLX exports) now load and generate correctly through Mugi's mlx-vlm server. Catalog **`mlx-community/Qwen3.6-*`** models remain the best-tested path.

---

## Also in this release

- **Timer routing** — improved reminder delivery documentation and routing behavior.
- **Chat tab strip** — layout and integration polish.
- **Dashboard & Activity feed** — more responsive data handling and UI updates.
- **Network setup** — clearer error handling during first-run / mesh status checks in Preferences.
- **Kanban coordinator** — better handling when you explicitly ask for a new batch while an old coordinator board is still winding down (operator edge case).
- **EULA / project config** — acceptance and versioning hardening.

---

## Upgrade notes

- No settings migration required.
- After updating, **restart Mugi once** (or reload the MLX model) so bundled mlx-vlm compatibility patches apply — especially if you use non-catalog Hugging Face MLX downloads.
- Knowledge corpora you already studied are unchanged; new **Study in Knowledge** flows reuse the same digest pipeline.

---

## Known limitations

- **Study in Knowledge** requires a confirmed corpus label — Mugi will not silently ingest uploads.
- Large digests remain **async**; the Library shows job status and trust health, but very large PDFs can take minutes.
- **Custom Hugging Face models** are best-effort: preflight catches common blockers (gated repos, OptiQ MTP sidecars, embedding-only checkpoints), but third-party quant layouts vary. Prefer **`mlx-community`** catalog entries when possible.
- Mugi requires **Apple Silicon** (M-series); Intel Macs are not supported.
- Unchanged from 0.10.2.x: council **Skip** is transcript-silent; task plan refresh can still time out under heavy load (cached steps + retry banner).

---

Feedback welcome via GitHub issues or your usual channel.
