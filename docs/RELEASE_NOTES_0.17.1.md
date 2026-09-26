# Mugi 0.17.1 — Public Beta

A small maintenance beta about setup: Mugi installs its own local AI engine for
you, and we removed an old manual step that could leave some Macs stuck.

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

## After you update

- Nothing to do. If the local engine was already working, it keeps working.

## Known limitations

- Nothing new in this build.

Feedback welcome via GitHub issues.
