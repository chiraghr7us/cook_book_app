# Cookbook

A minimal, installable recipe app. Store recipes, log what you cooked, and see stats on your most-made meals.

## Running it

This is a static web app — no build step, no install required. All of its code libraries are bundled locally in the `vendor` folder, so it needs no internet connection to run.

**Quickest way:** double-click `index.html` to open it in your browser. Everything works, including recipes, logging, and stats. (The one exception: the "auto-sync file" option needs the page served over http rather than opened as a local file — see below. Export/Import sync works fine either way.) If something still goes wrong, the page will now show an actual error message instead of staying blank — open DevTools (F12 → Console) for details if so.

**For full functionality, including auto-sync (optional):** serve the folder over local http:
```
cd cookbook-app
python3 -m http.server 8000
```
Then open `http://localhost:8000` in Chrome or Edge.

For real use, host this folder anywhere that serves static files (GitHub Pages, Netlify, Vercel, or a simple always-on server) so you can reach the same URL from your phone and PC.

## Installing as an app

Once it's served over http/https:
- **Desktop (Chrome/Edge):** click the install icon in the address bar, or menu → "Install Cookbook."
- **Phone (Android Chrome):** menu → "Add to Home screen."
- **iPhone (Safari):** Share → "Add to Home Screen."

It'll then open full-screen like a native app, and works offline once loaded.

## Syncing across devices

Your data always lives locally first (in the browser's storage), so the app works fully offline — sync is optional on top of that. Three options, from the cloud icon menu:

1. **GitHub sync (recommended — works on any device, including phones).** Reads/writes a JSON file directly in a GitHub repo you own via the GitHub API, so it works in any browser with no special features required. Setup:
   - Host this app's files in a GitHub repo (e.g. via GitHub Pages — you need a repo either way for this to point at).
   - Create a token at [github.com/settings/tokens?type=beta](https://github.com/settings/tokens?type=beta) → "Generate new token" → Fine-grained token → under **Repository access**, select only this repo → under **Permissions → Repository permissions**, set **Contents** to "Read and write" → Generate, then copy the token (starts with `github_pat_`).
   - In the app, cloud icon → enter `owner/repo-name` (e.g. `chirag/cookbook-app`) and paste the token → Connect. Leave branch as `main` unless your repo's default branch is different (e.g. `master`).
   - Repeat on your other devices (PC and phone), pointing at the same repo — you'll need to generate a token again for each device, or reuse the same one.
   - From then on, opening the app pulls the latest data, and any change pushes it back automatically — no manual steps.
   - The token is stored only in that browser's local storage and is scoped to just this one repo, so keep it private the same way you'd treat a password.
2. **Auto-sync file (Chrome/Edge desktop only — not supported in Brave without an experimental flag).** Cloud icon → "Connect a sync file" → save it inside a folder that Dropbox, Google Drive, or iCloud Drive already syncs for you. Do this on each computer, pointing at the same synced file.
3. **Export / Import (manual, works everywhere).** Cloud icon → Export downloads a JSON backup; Import loads one back in. Useful as a one-off migration or a backup, even if you're using one of the options above.

## Using it

- **Recipes tab:** add a recipe (title, tags, time, servings, ingredients, steps, notes). Click a card to view/edit/delete it, or use "Log cooked today" for a one-tap log (has a few seconds to Undo right after). "Surprise me" picks a recipe you haven't cooked in the last 14 days (or, if everything qualifies, whichever's gone longest). A recipe's "Cook history" lets you edit or delete any past log entry, not just the most recent one.
- **Voice input:** the mic icon next to Title, Tags, Ingredients, Instructions, and Notes lets you dictate instead of typing — for Ingredients/Instructions, pause between each item and it'll drop each one on its own line. Uses your browser's built-in speech recognition, so it needs mic permission and (for most browsers) an internet connection; it won't appear in browsers that don't support it (e.g. Firefox).
- **Stats tab:** total recipes and meals logged, a monthly cooking-frequency chart, and your most-cooked recipes ranked.

## Files

- `index.html` — the entire app (UI, logic, and storage)
- `vendor/` — bundled local copies of React, Babel, and Chart.js (no CDN/internet dependency)
- `manifest.json`, `sw.js`, `icons/` — makes it installable and offline-capable
