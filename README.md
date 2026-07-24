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

No account or backend required — two options:

1. **Auto-sync file (Chrome/Edge desktop only):** click the cloud icon → "Connect a sync file" → save it inside a folder that Dropbox, Google Drive, or iCloud Drive already syncs for you (e.g. `Dropbox/cookbook-data.json`). The app will read/write that file automatically from then on. Do this on each computer, pointing at the same synced file.
2. **Export / Import (works everywhere, including phones):** cloud icon → Export downloads a JSON backup. Drop that file into your synced Dropbox/Drive/iCloud folder, then on your other device use Import to load it. This is manual but works on any browser or platform, since phones don't support the auto-sync file API yet.

Your data always lives locally first (in the browser's storage), so the app works fully offline — sync is optional on top of that.

## Using it

- **Recipes tab:** add a recipe (title, tags, time, servings, ingredients, steps, notes). Click a card to view/edit/delete it, or use "Log cooked today" for a one-tap log.
- **Stats tab:** total recipes and meals logged, a monthly cooking-frequency chart, and your most-cooked recipes ranked.

## Files

- `index.html` — the entire app (UI, logic, and storage)
- `vendor/` — bundled local copies of React, Babel, and Chart.js (no CDN/internet dependency)
- `manifest.json`, `sw.js`, `icons/` — makes it installable and offline-capable
