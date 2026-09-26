# Release-notes runbook — every weekly beta

Every public beta ships with two written deliverables, written before the
release goes out:

1. **A short, plain-language user note** — `docs/RELEASE_NOTES_<version>.md`.
   It is the GitHub release body, which is what users see in the Sparkle update
   window and on the release pages. Write it for a non-technical Mac user.
2. **A changelog entry** — a new entry at the top of the changelog on
   `website/releases.html`. Short version of the same note, newest first.

The note and the changelog entry are the same story told twice: the note ships
*with* the beta (Sparkle dialog, appcast), the entry lives on the site.

## The user note (`docs/RELEASE_NOTES_<version>.md`)

Shape — keep it short enough to read in an update dialog:

```markdown
# Mugi <version> — Public Beta

<One or two sentences a friend would understand: what this beta is about. If
anything changes what the user must do — a new macOS floor, a re-index, a
setting to re-pick — it goes here or in its own loud line.>

## What's new

- <One line per change, plain language. Three bullets is plenty.>

## After you update

- <Anything the user must do: restart, re-index, re-pick a setting.>
- <Requirements that changed, if any.>

## Known limitations

- <Only what a user might actually hit. Keep it short.>

Feedback welcome via GitHub issues.
```

Writing rules:

- Plain language first; product names and settings paths in bold where they
  help someone find the thing.
- Lead with anything that changes what the user must do (for example a raised
  macOS floor). Do not bury it in Upgrade notes.
- No commit messages, no internal codenames without a plain gloss, no
  engineering detail that does not help the reader.
- Known limitations are honest: what does not work yet, said plainly.

## The changelog entry (`website/releases.html`)

- Add an entry block at the top of the **Changelog** section: version in
  `font-mono text-cyan-400`, the release date, and 1–4 bullets in plain
  language (the "What's new" lines, trimmed).
- Update the **Latest Release** card to match: version badge, highlights,
  download fallback link, and the requirements line when the floor changed.
- When the release is notable, also update `website/index.html` ("What's new"
  callout and the "What's working well" list) and `website/preview.html`
  ("Recent progress").

## Claims checklist (every beta)

- The requirements line shown on the site lives in the page HTML
  (`data-mugi-requirements` in `index.html` / `releases.html`); `download.js`
  deliberately does not overwrite it. Update it in the same commit as any
  `LSMinimumSystemVersion` change — that plist value is the floor's source of
  truth. `scripts/publish_release.sh` (and the appcast workflow) derive the
  same string into `website/releases.json` from the plist.
- The "PUBLIC PREVIEW — <MONTH YEAR>" badges say the current month.
- Version strings on the site come from `website/releases.json` at runtime;
  the hardcoded fallbacks in `index.html` / `releases.html` are updated when
  the version in them changes.

## The weekly loop

1. **Engineer**: ships the beta (gate → build → publish per
   `scripts/publish_release.sh`), with the user note as the release notes file.
2. **Growth**: reviews the note against the template above before publish;
   writes the changelog entry and any site copy updates in the same pass.
3. **Deploy**: the Publish Sparkle Appcast workflow (or
   `publish_release.sh --netlify-only`) pushes `website/` to Netlify — it
   regenerates `website/releases.json` and `website/_redirects` from the
   release and the app's Info.plist.
4. **Verify**: https://mugi-ai.com/releases shows the new entry at the top, the
   download card shows the right version and macOS floor, and the download
   link points at the new zip.
