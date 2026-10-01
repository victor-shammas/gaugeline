# Gaugeline website (GitHub Pages, custom domain)

The static marketing, support and privacy pages for Gaugeline. The site is plain HTML and one stylesheet, with no build step, external fonts, scripts or trackers. Its palette matches the app icon: espresso (`#46321F` → `#1C140E`), amber (`#FFC56A` → `#EE8A25`) and cream (`#FFF1DC`), with a warm off-white (`#F4F1EC`) in light mode.

| File | Published URL |
|---|---|
| `index.html` | https://victorshammas.com/gaugeline/ (Marketing URL) |
| `support.html` | https://victorshammas.com/gaugeline/support.html (Support URL) |
| `privacy.html` | https://victorshammas.com/gaugeline/privacy.html (Privacy Policy URL) |
| `style.css`, `icon.png`, `favicon.png`, `apple-touch-icon.png` | assets |
| `.nojekyll` | tells Pages to serve files as-is |

These URLs are hard-coded in the app (`Links` in `Gaugeline/UI/Support/Theme.swift`, shown in Settings › About), in `metadata.md` and in `review-notes.md` (which links `support.html#remove`). Keep the paths stable.

## How the URL works

Your GitHub Pages **user site** (the `victor-shammas.github.io` repo) already uses the custom domain `victorshammas.com`. GitHub serves every **project site** of the same account under that domain automatically, at `/<repo-name>/`. So a public repo named **`gaugeline`** with Pages turned on is published at `https://victorshammas.com/gaugeline/`. The project repo needs **no `CNAME` file** of its own; don't add one, or it would try to claim a separate domain.

## Deploy

1. On GitHub (account **victor-shammas**), create a **public** repository named exactly **`gaugeline`** (the name becomes the `/gaugeline/` path). Free GitHub Pages needs a public repo.
2. Copy the *contents* of this folder (including `.nojekyll`) to the root of that repo, then commit and push to `main`:
   ```bash
   git clone https://github.com/victor-shammas/gaugeline.git
   cp -R AppStore/site/. ../gaugeline-site/   # a clone of victor-shammas/gaugeline
   (the site repo is already set up; just copy, commit and push)
   cd gaugeline && git add -A && git commit -m "Gaugeline website" && git push
   ```
3. Go to the repo › **Settings › Pages** › Build and deployment › Source: **Deploy from a branch**, Branch: **main**, folder **/ (root)**, then Save. Leave the "Custom domain" field there empty; it's inherited from the user site.
4. After a minute or two, open all three URLs above, plus `support.html#remove`. Check they load over **HTTPS** (Enforce HTTPS is set on the user site). Apple checks that the Support and Privacy URLs load, and the app links to them, so do this **before** submitting for review.
5. If `https://victorshammas.com/gaugeline/` returns 404, check that the user site's custom domain is still set and verified (user site repo › Settings › Pages), and that the repo is named `gaugeline` in lowercase.

## Before or after launch

- **App Store link:** `index.html` contains a placeholder `https://apps.apple.com/app/idAPP_ID`. Once the app record exists, replace `APP_ID` with the numeric Apple ID shown in App Store Connect › App Information. The link works (as "not yet available") before release.
- **Official badge (optional):** to use Apple's "Download on the Mac App Store" badge instead of the text button, download it from https://developer.apple.com/app-store/marketing/guidelines/ and follow Apple's badge rules (unaltered artwork, minimum size, clear space).
- Regenerate the icons after an icon change:
  ```bash
  sips -s format png -z 256 256 ../icon/icon_1024.png --out icon.png
  sips -s format png -z 64 64 ../icon/icon_1024.png --out favicon.png
  sips -s format png -z 180 180 ../icon/icon_1024_opaque.png --out apple-touch-icon.png
  ```
- Changing the privacy policy? Update its effective date, and keep it consistent with the App Privacy answers in `../metadata.md`.
