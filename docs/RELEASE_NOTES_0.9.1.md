# Mugi 0.9.1 — Public Beta

Patch release following 0.9.0 public beta. Focus: chat reliability, tool-round visibility in the thread, activity feed parsing, and documentation.

---

## Highlights

### Chat & tools
- Tool rounds surface as readable rows in the chat thread (not buried in raw message payloads).
- Chat view performance and scrolling refinements.
- Shell command handling and approval flow clarity improvements.

### Activity feed
- More reliable parsing of activity events and tool-runtime emissions.

### Documentation
- Expanded user manual (slash commands, Kanban, background jobs, privacy, Profile vs You).
- Website manual navigation and download wiring updates.

### Release engineering
- Appcast workflow handles private-repo release assets and pre-releases.
- Release bundle verification (`verify_release_bundle.sh`) for Sparkle codesign checks.

---

## Requirements

| | |
|---|---|
| **OS** | macOS 15.0 (Sequoia) or later |
| **Hardware** | Apple Silicon strongly recommended |

---

## Upgrade

Existing 0.9.0 installs: **Mugi → Check for Updates…** after this build is published to Sparkle.

Fresh install: download from [mugi-ai.com](https://mugi-ai.com) or use the GitHub release artifact.

---

## Known limitations

0.9.1 remains a **public beta**. Automated release-gate live batteries may occasionally flake on model-dependent user-trust cases; hard gates still cover storage, kernel boundaries, Kanban workers, and delivery seams.

Feedback welcome via GitHub issues or your usual channel.
