# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## What this repo is

Static legal/support site for the GainTrack fitness app, served as GitHub Pages at
`gaintrack.app` (custom domain via `CNAME`). There is no build step, no dependencies, and no
framework — three self-contained HTML files, each with its styles inlined in a `<style>` block
in the `<head>`. Edits are made directly to the HTML and take effect on push (GitHub Pages
serves the repo directly).

## Files

| File | Purpose |
|---|---|
| `index.html` | Privacy Policy (site root) |
| `terms.html` | Terms of Service |
| `delete-account.html` | Account deletion instructions (linked from Google Play data-safety / account-deletion requirements) |
| `CNAME` | GitHub Pages custom domain (`gaintrack.app`) |

These three pages are cross-linked to each other via a shared `<nav>` (Privacy / Terms / Delete
Account) and a matching `<footer>`, and share one color/typography system (CSS custom properties
defined per-page: `--bg`, `--accent` (`#c8ff00`), `--text`, `--body`, `--muted`, etc., DM Sans +
DM Mono via Google Fonts). There is no shared CSS/JS file — the styling is intentionally
duplicated per page. If you change the visual design, update the `:root` variables and repeated
component rules (`.nav-link`, `.intro`/`.warning-box`, `section`/`h2`, `.contact-box`,
`.footer-inner`, etc.) in **all three files** to keep them in sync.

## Editing conventions

- Each page has a `Effective:` / `Last updated:` date line under its `<h1>` (or a one-line
  `.meta` subtitle on `delete-account.html`) — bump the "Last updated" date when content changes.
  - `terms.html`'s sections are numbered (`1. Acceptance of Terms` … `17. Contact`); if you
    insert or remove a section, renumber the following ones.
- Support/contact email throughout all three pages is `support@gaintrack.app` — do not
  reintroduce the old Gmail address in visible text.
- This site is the canonical source for legal claims that must stay in sync with what the app
  actually does — e.g. `index.html`'s "AI Coach Feature" section and `terms.html`'s "5. AI
  Features" section describe exactly what GainTrack's Gemini-powered features (AI coaching,
  meal-photo analysis, workout-video analysis) do with user data (processed transiently, not
  retained, not used for model training). If the app's AI/data-handling behavior changes, these
  sections need a matching update — check with the `gaintrack` repo (the main app) for current
  behavior before editing.
- `delete-account.html`'s in-app steps (Profile tab → Account section → Delete Account) must
  match the app's actual navigation — verify against the `gaintrack` repo if the profile screen
  is restructured.
- Third-party services listed in `index.html` ("Third-Party Services" section: Firebase,
  RevenueCat, Gemini API, Expo/EAS, MongoDB Atlas, Apple Health/Google Fit) should track the
  app's real infrastructure — see the `gaintrack` repo's `CLAUDE.md` for the current
  infrastructure list if unsure whether a service is still in use.

## Deploy

No build/deploy command — push to `main` and GitHub Pages serves the updated HTML directly at
`gaintrack.app` (typically live within a minute or two).
