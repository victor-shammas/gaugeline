# Gaugeline website

The public website for Gaugeline, a paid Mac App Store menu bar app that shows
Claude Code and OpenAI Codex usage limits. Plain HTML and one stylesheet; no
build step, external fonts, scripts or trackers. The app's source is in the
private repo `victor-shammas/gaugeline-app`.

This repo is public and every file in it is served, including this one and
`README.md`. Keep anything private out of it.

## Files

- `index.html` — landing page (the App Store "Marketing URL")
- `support.html` — setup, FAQ and contact (the "Support URL"); anchors
  `#start`, `#claude`, `#remove`, `#remove-manual`, `#codex`, `#numbers`,
  `#demo`, `#contact`
- `privacy.html` — privacy policy (the "Privacy Policy URL"), with an
  effective date
- `style.css` — the only stylesheet; light and dark via
  `prefers-color-scheme`
- `icon.png`, `favicon.png`, `apple-touch-icon.png` — made from the app icon
  (commands in `README.md`)
- `.nojekyll` — serve files as-is
- `README.md` — how the site is deployed

## How it's served

GitHub Pages, deploy from branch `main`, folder `/` (root). The custom domain is
inherited from the user site `victor-shammas.github.io` (`victorshammas.com`),
so this repo appears at https://victorshammas.com/gaugeline/. Don't add a
`CNAME` file. A push to `main` is live in a minute or two.

## Things that must stay stable

- The app links to `/gaugeline/`, `support.html` and `privacy.html` (Settings ›
  About), the App Store listing uses the same three URLs, and the App Review
  notes link `support.html#remove`. Don't rename these pages or that anchor.
- `privacy.html` must match the app: no network access, no accounts, no data
  collected ("Data Not Collected" in App Store Connect). If the policy changes,
  update the effective date.

## App Store link

The app is not live yet, so `index.html` shows a disabled "Coming soon to the
Mac App Store $1.99" button. The HTML comment right above it holds the
replacement link (`https://apps.apple.com/app/idAPP_ID`). Once the app is
approved and released, swap the span for that link with the app's numeric
Apple ID; the steps are in `RELEASING.md` in `gaugeline-app`.

## Copy in the app repo

`gaugeline-app` has a copy of this site in `AppStore/site/`, which was used to
create this repo. It is behind: the Staple tile in the app bar (2026-10-09)
exists only here. Don't overwrite this repo from that folder without bringing
those changes across first.

## Conventions

- Shared design with the sister sites Plainview, Quoth and Staple
  (https://victorshammas.com/plainview/, /quoth/, /staple/). Every page ends
  with the same app bar (`<section class="app-bar">`): one tile per app with
  icon, name and a one-line description, the current app marked
  `class="app-tile current"` with "You’re here". When an app is added or a
  tagline changes, update the app bar on all three pages here and on every
  sister site, and adjust `.app-tiles` columns in `style.css` (now 4, with
  breakpoints at 900 px and 560 px).
- Palette from the app icon: espresso, amber and cream, with a warm off-white
  in light mode (values in `README.md` and `:root` in `style.css`).
- Plain, concrete, unhyped prose; no emoji. Trademark names (Claude, Codex,
  OpenAI, Anthropic) only as "works with" statements and in the footer
  disclaimer; no logos.
- Contact: contact+gaugeline@victorshammas.com (footer and support page).
- Commits: short subject naming the change ("App bar: add Staple"), no
  trailing period.
