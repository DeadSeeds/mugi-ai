# Mugi 0.17.1 — Public Beta

This update is about getting set up and getting out of your way: Mugi installs
its own local AI engine for you, you come back to the conversation you left,
and a handful of everyday screens now tell the truth.

## What's new

- **Setup has one path — the app's.** We removed the leftover "install it
  yourself" instructions and code that pointed at a manual command. On some
  Macs (for example, ones with Homebrew's copy of Python) that command always
  failed, and it could never repair anything. If the local engine ever needs
  installing or reinstalling, the **first-run setup** or **Settings → LLMs**
  does it for you.
- **Recovery buttons do the same thing they promise.** **Reinstall** and
  **Revert to stable** in **Settings → LLMs** now simply re-download the local
  engine — no hidden package steps, nothing to type.
- **Come back to your conversation.** Relaunching Mugi no longer opens a
  brand-new empty chat; you're back where you left off.
- **One place to choose your local engine.** **Settings → LLMs** has a single,
  simple engine picker (it replaces the old scattered controls). The optional
  Python MLX engine is available again — pick it and Mugi installs it for you,
  with the download size shown up front.

## Also in this update

- **Your downloaded-models list tells the truth.** If it can't load, Mugi says
  so instead of showing an empty list.
- **Plainer error messages.** First-run setup and Diagnostics failures explain
  themselves in plain words and offer a way forward.
- **Open Software Update works.** The button now lands on the Software Update
  pane, where it promised to.
- **Snappier after actions.** A reply that ended by using a tool could add a
  few seconds of delay to your next message; that's fixed.
- **Under the hood.** A long list of reliability fixes too small to list.

## After you update

- Nothing to do. If the local engine was already working, it keeps working.

## Known limitations

- Nothing new in this build.

Feedback welcome via GitHub issues.
