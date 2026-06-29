# Mugi 0.10.0 — Public Beta

Focus: **a new agent engine**, **durable Results deliverables**, **verify-before-assert grounding**, and **Exo as a connect-only local option** — while **MLX (mlx-vlm) remains the default** managed engine.

- Build number **6** (Sparkle compares `CFBundleVersion` for same marketing version).

---

## Highlights

### New agent engine (kernel path)

- The default chat, subagent, Kanban-worker, Quick Panel, and Dashboard paths now run through the **kernel loop** (`[kernel] enabled = true` by default).
- Tool calling, context trimming, and error recovery are simpler and more predictable than the legacy loop they replace.
- **Show agent thinking** works on the kernel path again: when enabled in Settings → General, model reasoning streams into separate thinking bubbles (not mixed into the main reply).
- **Plugin lifecycle hooks** (`on_agent_start`, tool-call events, `on_agent_done`) fire on foreground kernel runs again, so bundled plugins that listen for agent activity behave as documented.
- **Research mode** (when you turn it on for a chat turn) now spawns a **durable Kanban research worker** bound to your thread. Mugi acknowledges the request immediately and delivers findings when the worker finishes — instead of blocking the UI on a long in-thread harness.
- Foreground chat caps repeated **search** tool calls and steers the model toward synthesis when it would otherwise loop on degraded backends.

### Results workspace

- New **Results** workspace mode in the sidebar rail — a durable home for HTML pages, markdown reports, plain-text contracts, and chart/image deliverables tied to a conversation.
- Agent tools: **`commit_results_deliverable`**, **`read_results_deliverable`**, **`patch_results_deliverable`** (plus project list/rename via the sidebar or `find_tools`).
- Revisions are versioned on disk under `~/Documents/Mugi/Results/`; **Export…** from the Results sidebar is the canonical copy (chat gets a short summary, not the full document).
- **Read → patch → summarize** workflow for iterating on an existing deliverable in the same thread; start a **new chat** for a different content type or a from-scratch rewrite.
- Auto-switch to Results when a deliverable lands (configurable); optional background toast when work completes in another thread.
- Legacy html/markdown/text fenced blocks in chat still auto-commit as a fallback.

### Grounding / verify-before-assert

- Mugi can **check its own checkable claims** instead of stating them as settled truth when uncertain.
- Default mode (**Advisor**): the agent narrates a hunch, dispatches a background fact-check (local SearXNG search), and delivers a short **Confirmed** / **Quick correction** / **Inconclusive** note when the check finishes — without blocking your turn.
- Settings → General → **Grounding / fact-checking**: Off, Advisor (default), or Ask first. Optional toggle to allow the background checker to escalate to the public web.
- Chat bubbles for grounding outcomes use distinct styling (confirmed vs corrected vs inconclusive).
- Open verification holds and recent self-corrections are injected into the agent's context so it does not re-assert superseded facts.

### Exo (connect-only)

- New engine option: **Exo (connect)** in Settings → LLMs and the setup wizard.
- Point Mugi at your running Exo OpenAI API (`http://127.0.0.1:52415/v1` by default).
- **Connect / Test** probes reachability, loaded model state, and native tool calls.
- Mugi does **not** install, bundle, or manage the Exo process.
- Use Qwen / Hermes-template models for reliable native tool calling on Exo.

### Engine selector

- Replaces the old MLX toggle + external toggle with a three-way picker: **MLX / Exo / External API**.
- `inference_engine` pref in `app_prefs.json` (migrated from legacy flags on load).
- **MLX (mlx-vlm)** remains the default and fully managed local engine on `:8000`.
- Embeddings and utility model continue to use the MLX venv regardless of chat engine.
- **Model selection** in Settings → LLMs now saves and loads on the first pick (fixed a race that required selecting twice).
- **Text-only MLX models** (e.g. MiniMax-M2.7): Mugi no longer enables Automatic Prompt Caching (APC) on launch — mlx-vlm's APC path assumes a multimodal model and returned HTTP 500 (`LanguageModel` has no `.config`). Multimodal models still get APC for faster follow-up turns.

### Local search (SearXNG)

- **Fixed a fatal default:** early builds shipped a hardcoded **dev-machine LAN address** (`192.168.1.111:8888`) as the SearXNG `base_url`. On every other Mac, “local search” pointed at a host that does not exist — `search_web` silently timed out and the app felt broken.
- **All shipped defaults are now loopback:** `http://127.0.0.1:8888` in config templates, fallbacks, and runtime resolution.
- **Settings → Network:** when **Use local SearXNG (Docker)** is on, the base URL is shown as a fixed read-only `http://127.0.0.1:<port>` (derived from your port) so there is no stale LAN field to mis-edit.
- **Upgrade migration:** installs that still have the exact old dev default are rewritten to loopback on first load. A URL you deliberately set to another LAN host is left alone.

### Kanban & task reliability

- Kanban workers can complete via an in-band **`kanban_post_summary`** even when the trailing `kanban-result` fence is missing — real work is not discarded for a formatting slip.
- **`task_id`** is optional on several Kanban tools when the worker already holds an active claim.
- Priority validation and board UI handling are tightened.
- Generation-phase status signaling during kernel runs (clearer “working” feedback while the model is thinking).

### Other polish

- Shell command approval modal state is more reliable (fewer stuck or duplicate prompts).
- Clearer file-read error messages when a path does not exist or is out of scope.
- Task-plan seeding and history-trim callbacks on the kernel path.
- Chat storage schema **v11**: per-message display kind for richer bubble rendering.

---

## Upgrade notes

- Existing **0.9.x** installs: **Mugi → Check for Updates…** after this build is published to Sparkle.
- Mugi no longer installs or manages LLMster on `:1234`. Local inference is MLX on `:8000`, or point **External API** at desktop LM Studio / Ollama / vLLM.
- Fresh install: download from [mugi-ai.com](https://mugi-ai.com) or use the GitHub release artifact (`Mugi-0.10.0.zip`).
- Existing MLX users: no change — migration sets `inference_engine=mlx`.
- Existing external backend users: stay `external` even if URL contains `:52415`.
- To use Exo: install and run Exo separately, then select **Exo (connect)** in Settings → LLMs.
- **SearXNG:** if local search never worked on your machine, update and confirm Settings → Network shows `127.0.0.1` (migration runs automatically). Use **Refresh** / **Start** if Docker + Colima are not running yet.
- **Revert the kernel** (support/debug only): set `[kernel] enabled = false` in `mugi_config.toml`. Every surface returns to the legacy loop immediately.

---

## Behavior changes (intentional — not regressions)

These differ from 0.9.x because the kernel path is now default. See [kernel_dropped_resilience_decision.md](kernel_dropped_resilience_decision.md) for the full decision record.

| Area | 0.9.x (legacy loop) | 0.10.0 (kernel default) |
|------|---------------------|-------------------------|
| Long-run context pressure | Gradual token-pressure trim + optional mid-run summarization | Hard char cap; oldest messages dropped; working-buffer digest preserves discoveries |
| Crash mid tool-round | Could resume the interrupted round | Next run starts from persisted history (no mid-round resume) |
| Live multi-tool turn | New chat bubble per tool round | One growing assistant bubble while streaming; reload shows the correct multi-bubble history |
| XML-in-content tool calls | Salvaged on legacy path | Salvaged on kernel path (Hermes + Gemma channel formats); native tool calls still preferred |

---

## Requirements

| | |
|---|---|
| **OS** | macOS 15.0 (Sequoia) or later |
| **Hardware** | Apple Silicon (M-series) required — Intel Macs are not supported |

---

## Known limitations

- **Exo preset** is experimental until validated end-to-end on capable models (Qwen2.5-7B+). Exo vision requires `EXO_ENABLE_IMAGE_MODELS` in Exo; Mugi assumes no vision on stock Exo. Llama-style models on Exo may not surface native tool calls.
- **Grounding advisor** uses local SearXNG by default; weak evidence resolves to *inconclusive*, not a fabricated answer. Public-web escalation is opt-in.
- **Results**: the first commit on a thread locks `content_type` (html vs markdown vs text). A different type requires a new conversation.
- Automated release-gate live batteries may occasionally flake on model-dependent user-trust cases; hard gates still cover storage, kernel boundaries, Kanban workers, and delivery seams.

Feedback welcome via GitHub issues or your usual channel.
