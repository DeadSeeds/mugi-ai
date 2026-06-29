# Mugi 0.9.2 — Public Beta

Patch release following 0.9.1. Focus: X (Twitter) marketing integration with Activity approval, proactive inbox polish, website and manual updates, and Docker/Colima setup UX.

---

## Highlights

### X API (marketing posts)
- Bundled **X API** plugin: connect via OAuth in **Settings → Plugins → X API**.
- Agent can research mentions and metrics, then **`x_propose_post`** drafts copy for your review.
- **Activity → On my mind** is the approval surface — nothing publishes until you tap **Post**.
- Diagnostics report connection status and pending draft count.
- Kanban workers with `deliverable_type: x_post` can propose drafts; publish stays human-gated.

### Proactive & Activity
- Observation tiers and inbox actions handle X post drafts alongside existing observation types.
- Dismiss and publish flows wired through the backend with idempotency guards.

### Network & local search (Docker / Colima)
- **Settings → Network → Docker Controls**: clearer setup expectations (~500 MB+, several minutes).
- Long-running setup/start actions stream status in the pane instead of failing silently.
- Lima virtualization entitlements bundled for Colima on Apple Silicon.

### Website & documentation
- Homepage and preview copy reframed around Mugi as a **local personal assistant**.
- User manual expanded (Makefile targets, navigation, clarity pass).
- Releases page and download metadata point at `Mugi-0.9.2.zip` on R2.

### Release engineering
- Appcast workflow Netlify deploy configuration refinements.
- Build number **3** (Sparkle compares `CFBundleVersion` for same marketing version).

---

## Requirements

| | |
|---|---|
| **OS** | macOS 15.0 (Sequoia) or later |
| **Hardware** | Apple Silicon strongly recommended |

---

## Upgrade

Existing 0.9.0 / 0.9.1 installs: **Mugi → Check for Updates…** after this build is published to Sparkle.

Fresh install: download from [mugi-ai.com](https://mugi-ai.com) or use the GitHub release artifact (`Mugi-0.9.2.zip`).

---

## Known limitations

0.9.2 remains a **public beta**. Automated release-gate live batteries may occasionally flake on model-dependent user-trust cases; hard gates still cover storage, kernel boundaries, Kanban workers, and delivery seams.

X API requires your own X developer app credentials and explicit OAuth connect; posting always requires Activity approval.

Feedback welcome via GitHub issues or your usual channel.
