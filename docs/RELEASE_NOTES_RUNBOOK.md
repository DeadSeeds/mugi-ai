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

One checker owns this list: `scripts/check_release_site.py`. It runs in
`make release-gate-static`, **and** in the deploy job before Netlify (against
the tree being published), **and** against the live site after the deploy. If
you edit a claim, run it:

```bash
~/.mugi/venv/bin/python scripts/check_release_site.py
```

- **Version currency.** The same release version must appear in: the
  "What's new in X" callout and the newest "What's working well" row on
  `index.html`; the "Latest Release" badge, "Highlights in X" heading and
  newest changelog heading on `releases.html`; the intro and newest "Version
  X" paragraph on `preview.html`; and `website/releases.json`. They must all
  agree. A release tag may be created *after* the local gate (that is why a
  draft may lead the newest tag locally), but the deploy job passes the real
  release version, so nothing may lead or trail it there.
- **Floor.** The requirements line is a claim about the build. `download.js`
  fills `[data-mugi-requirements]` from `releases.json`; the static HTML is
  only the no-JS fallback, and the checker validates both (plus
  `website/manual/**`). Update them in the same commit as any
  `LSMinimumSystemVersion` change — that plist value is the floor's source of
  truth. `scripts/publish_release.sh` and the appcast workflow derive the same
  string into `website/releases.json` from the plist; neither may spell it.
- **Downloads.** Every `data-mugi-download` href and every hard-coded
  `Mugi-<version>.zip` must name a version that exists as a tag. The static
  fallbacks are what a person with JavaScript off downloads.
- **Notes.** `docs/RELEASE_NOTES_<version>.md` must exist for the release and
  name it in its first line; its short version is the newest changelog block on
  `releases.html`, which must have bullets.
- **Unrecognised claims fail loudly.** A version-shaped sentence the checker
  cannot place errors out. Add its shape to the matching `_scan_*` function in
  `scripts/check_release_site.py` (and classify it current/historical) — do not
  delete the claim, and do not widen the sweep.
- The "PUBLIC PREVIEW — <MONTH YEAR>" badges say the current month (not checked
  mechanically; it is presentation, not a release claim).

## The weekly loop

1. **Engineer**: ships the beta (gate → build → publish per
   `scripts/publish_release.sh`), with the user note as the release notes file.
2. **Growth**: reviews the note against the template above before publish;
   writes the changelog entry and any site copy updates in the same pass.
3. **Deploy**: the Publish Sparkle Appcast workflow (or
   `publish_release.sh --netlify-only`) pushes `website/` to Netlify — it
   regenerates `website/releases.json` and `website/_redirects` from the
   release and the app's Info.plist, runs `scripts/check_release_site.py`
   **before** deploying, and fails the job if the site does not describe the
   release.
4. **Verify**: https://mugi-ai.com/releases shows the new entry at the top, the
   download card shows the right version and macOS floor, and the download
   link points at the new zip. The workflow's last step asserts the live
   `releases.json` and home page say this release (bounded retries for the CDN),
   so a stale deploy is red in CI, not discovered by a person.
