# Mugi 0.14.0 — Public Beta

Minor release following **0.13.0**. One theme runs through it: **being known accurately, and being able to check.**

0.13.0 gave Mugi a personal layer that learned from ordinary conversation. Using it revealed the harder half of the problem — a system that writes things down about you has to be honest about *what* it recorded, *where* it came from, and *how sure* it is, and it has to let you see and undo any of it. So About You now has its own window, marks what it worked out as distinct from what you told it, keeps a fact that lapsed instead of deleting it, and asks before it guesses.

Alongside that: **Abilities**, so Mugi asks for a capability in chat instead of quietly lacking one; **Knowledge that reads by page**, so a citation opens the actual page of the actual PDF; and per-model **response settings** you can see and take over.

---

## Highlights

### About You is a place you can open

- **Its own window.** Open About You from the menu bar (or from Settings) and read everything Mugi has written down about you, in plain sentences.
- **Every fact carries its own record.** When it was first noticed, who wrote it, and whether it came from you or was worked out. Provenance is per-fact now, not per-document.
- **Told apart from worked out.** A fact Mugi inferred is marked as provisional and stays that way until you confirm it. It will check in passing when the conversation is already on the subject — not read you a queue.
- **It asks instead of guessing.** Mugi can look a personal fact up and quote what is actually recorded. If nothing is recorded, "I don't know" is the answer rather than an inference.
- **A lapsed thread becomes past, not deleted.** A trip whose dates have passed stays on the page so Mugi can ask how it went. Previously it vanished on the very day it became worth mentioning.
- **A correction retires what it contradicts.** Putting Mugi right removes the thing it replaces, instead of leaving both on the page.
- **The conversation outranks the record.** What you say in the turn wins over what was written down last month.

### What reaches the prompt is chosen, not sliced

The personal context Mugi carries into a reply used to be the first few lines of each section — which meant most of what it knew was unreachable, and three threads about the thing being actively worked on never appeared at all.

- Facts are now **ranked against the conversation** and selected by relevance, then recency.
- The ranking query is built from the **whole conversation**, not just your last message.
- Irrelevant facts no longer spend the block's budget.

### Background noticing got boundaries

- **Goals, identity, and values are off-limits to background.** Those say who you are and what you are committed to, so a wrong entry is both hard to spot and costly to leave standing. Only you set them now; anything a noticer infers is set aside for review instead of written in.
- **The stores are bounded.** The follow-up backlog was full and had started refusing *you* in favour of month-old guesses; it now evicts by rank and keeps the person's entries.
- **Background runs can see what they write to.** They were reading the oldest 1.6% of memory and writing on that basis.
- **Corrections honour their setting.** `auto_apply = false` is actually respected.

### Abilities — Mugi asks, you grant

- **An Abilities pane** in Settings listing what Mugi can do on your behalf, and what it is asking for.
- **Grant offers in chat.** When a turn needs a capability that has not been granted, Mugi offers a card you can accept in one tap rather than failing quietly or asking you to go hunting in Settings.
- **Email watch.** Opt-in, with its own section in Access, chat tools, and a standing grant for sending that skips the per-message confirm once you have allowed it.
- **Visible in Activity.** Anything done under a grant is attributable after the fact.

### Knowledge reads by page

- **PDFs open in the app** under an Original tab, in a real PDF reader.
- **Citations land on the page they cite** — from chat, and from search hits.
- **Your place is kept.** Reading is locked to the current page and restored where you left it.
- **Related links connect pages**, not fragments, so the connections are ones a person recognises.
- Original copies are **bounded and reclaimable**, so the library does not grow without limit.

### Response settings you can see

- **Sampling resolves per model, not per model family** — the previous behaviour assumed every local model wanted Qwen's settings.
- **Thinking and sampling follow the running model**, and foreground chat defaults to bounded thinking rather than none.
- **Reasoning effort** is exposed in Preferences.
- The **resolved settings are shown**, and you can take them over.

### Durable work finishes cleanly

- A worker that already submitted is no longer re-driven, and a handoff mangled by escaping is recovered rather than lost.
- Run rows abandoned by a killed process are closed; staging files from a killed index rebuild are swept.
- A capacity refusal no longer erases the previous attempt's findings or spends the task's retry budget.
- Tasks get the tools they declared, and chat-planner verbs are no longer advertised to workers.

---

## Also in this release

- **Word export works** The markdown dependency was declared in the wrong requirements file, so Results → *Word Document (.docx)* returned an error for everyone who had not installed it by hand.
- **MLX startup failures are on the boot screen** with the real reason, instead of a spinner that polls forever. Model downloads can be cancelled and report status honestly.
- **Councils convene when asked.** The tool was registered but never harvested into the catalog, so the model was told the seats existed and could not reach them.
- **Local delegation no longer starves chat.** A fan-out sharing one local model server is capped to one worker so the foreground turn is not queued behind its own subagents.
- **A plugin can no longer narrow Mugi's own view of a tool.** A plugin manifest can only describe filesystem, network, and shell access, but registering a tool used to replace its classification wholesale — so the bundled yt-dlp plugin quietly removed the marker that stops an unverified requester from pointing a download at a URL of their choosing. Manifest permissions now add to the built-in classification instead of overwriting it.
- **`backend.jsonl` rotates.** It had no rotation.  Fixed.
- Unclosed XML tool-call blocks parse; digest pools no longer crash on Python 3.14; Colima shutdown cleans up after itself.

---

## Upgrade notes

- **About You migrates on first launch.** Your existing personal document is converted to the per-fact record format. It is worth taking a backup of your workspace before updating — this release changes how that document is stored.
- **Background noticers can no longer write goals, identity, or values.** If you relied on that, those entries are now yours to set in the About You window; anything inferred is set aside instead.
- **Check your response settings.** Sampling now resolves per model, so a local model that was silently being given another family's settings will behave differently — better, but differently. Settings → LLMs shows what is actually in effect.
- **Plugins** may ask to re-approve permissions, as in 0.13.0.

---

## Known limitations

- Mugi requires **Apple Silicon** (M-series); Intel Macs are not supported.
- Provisional facts are only raised when the conversation is already on the subject. A wrong one can sit unconfirmed for a while — the About You window is the place to catch it.
- The research-mode toggle and its per-run URL budget still do not reach the kernel that runs the turn; treat those controls as inert.
- Duplicate tool calls issued within a *single* model response are still not de-duplicated — only repeats across turns.
- Nested list indentation in the markdown editor is still off, and tables can be viewed but not edited in edit mode.
- Personal facts from chat remain best-effort: Mugi may miss a turn or need a clearer restatement. Anything wrong stays correctable in the About You window.

---

Feedback welcome via GitHub issues.
