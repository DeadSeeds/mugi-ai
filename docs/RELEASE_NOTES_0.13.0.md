# Mugi 0.13.0 — Public Beta

Minor release following **0.12.2**. Two big themes: the **Modern layout** — a full rework of the main window that gets the chrome out of your way — and a **personal-context layer** that actually learns from ordinary conversation and from your corrections, without pretending a fix to your calendar is a fact about you. Alongside those, the **plugin platform** grew from a bridge into a real SDK with per-plugin dashboards and runtime diagnostics, and every major subsystem gained **self-healing** tools.

---

## Highlights

### The Modern layout

The main window has been reworked around one canvas and two columns — the conversation, and an inspector that slides in only when you need it.

- **A layout you choose.** A new layout picker in Settings, with a default that matches the install. The classic layout is still there; nothing is taken away.
- **One surface, two columns.** Panels got real glass, the toolbar moved to the top-right, and the mode rail floats over the canvas instead of owning the window.
- **Branches stay close.** Branches nest in the sidebar and conversation history floats as a working set, instead of a separate pane competing for the same space.
- **A hero composer on empty conversations.** A new conversation gets a proper blank page to start from, not a tiny input box.
- **The inspector is a place, not a popup.** It slides in and out, closed by default with an edge peek — and when it's closed, attention-grabbing cards still get their loud moment.
- **Motion that matches.** The dismissal slides out the way arrival slid in; glyphs sit above the panel; the composer aura, working glint, and transcript edge are toned with Modern's accent tokens.
- Fixes along the way: the Modern transcript is no longer completely unscrollable, and the column stretches instead of drifting.
- **Looks pretty effing cool.** Open to feedback.

### About You — the person, and what Mugi should remember

The personal-context system that had been a thin injection is now a real, user-correctable layer.

- **About You as a first-class store.** Facts Mugi learns about you live in a versioned store you can view and correct — not scattered background notes.  Work in progress.
- **Corrections take.** A corrections ledger in the You pane: Mugi learns from what you correct, and corrections feed the morning brief (including calendar-event corrections).
- **"Never note that about me again"** is honored in the turn you say it.  Hopefully.  WIP,
- **"Just learned" facts.** The morning brief now shows facts Mugi picked up recently, with one-tap correction.
- **Working-knowledge auto-apply.** Facts you confirm and corrections you make apply as working knowledge automatically.
- **Reply style adaptation.** Mugi can learn your reply style from chat feedback.
- **Measured, not guessed.** Attribution and recall are instrumented end-to-end — including offline golden evals and audits over stored real conversations — so we can tell whether personal context actually changes replies. MLX prefix reuse was proven at Mugi's real 16–40k prompt scale, cutting per-turn latency.
- **Open commitments, honestly.** The brief checks in on open commitments; open loops carry honest age labels and are cataloged with mutable-tools guidance.

### The plugin platform grows up

- **A real SDK.** Typed context protocol, per-tool timeouts, an `api_version`, and validation — with fixtures, a CLI, and docs.
- **Approval you can actually read.** Plugin tools, permissions, and source are shown in an approval sheet with a re-approval diff; permission overrides can only tighten.
- **Per-plugin dashboard.** Each plugin gets its own home: stream contract, detail endpoint, a two-pane layout, and a runtime diagnostics sheet with restart and log tail.
- **8-slot tier-0 cap is visible.** The always-visible toggle caption shows the cap, and plugin tools can be promoted by intent with a per-plugin tier-0 override.

### Self-healing — every major surface

Nine subsystems gained `diagnose_` / `repair_` tools: **search, inference, Kanban, Mesh, web unlock, MCP bridge, knowledge corpus, Vault, and Live View / Activity** — plus plugins and the dashboard. When something drifts, you can diagnose it and repair it in place instead of restarting the app.

### Honest web reading

- A blocked page now offers the browser handoff instead of going quiet.
- HTTP status-code walls are handled instead of swallowed.

### Kernel reliability

- **Last-message-wins** reply contract in the foreground tail — stops a raced reply from overwriting a newer one.
- **Prefetch and consistency fixes** across background runs, morning brief, and the composer.
- **Results** "new" dot stays cleared once you've looked.
- Council asks once per question, and only when the stakes warrant it.

---

## Also in this release

- The backend bundle no longer ships smoke demos.
- Relationship facts are no longer silently dropped from People.
- Post-turn personal capture is more reliable under load (coalesced jobs, honest rate limits, distinctive details kept instead of collapsed away).

---

## Upgrade notes

- **Layout:** if you've used the previous layout, you can switch back to it any time via **Settings → General → Layout**. The first-run picker chooses a default that matches your install.
- **About You:** the personal-context layer is user-correctable. Corrections you make in the You pane are what Mugi actually learns from — including facts picked up from ordinary chat.
- **Plugins:** after updating, existing plugins may ask you to re-approve permissions, because the approval surface now shows exactly what each plugin can do.

---

## Known limitations

- Mugi requires **Apple Silicon** (M-series); Intel Macs are not supported.
- The research-mode toggle and its per-run URL budget do not yet reach the kernel that runs the turn; treat those controls as inert for now.
- Duplicate tool calls issued within a *single* model response are not yet de-duplicated — only repeats across turns.
- Nested list indentation in the markdown editor is still off, and tables can be viewed but not edited in edit mode.
- The Modern layout is still the newest surface; a few edge cases (very long titles, tiny window widths) may still show rough corners.
- Personal facts from chat are best-effort: Mugi may miss a turn or need a clearer restatement. Anything wrong stays correctable in **Settings → You**.

---

Feedback welcome via GitHub issues.
