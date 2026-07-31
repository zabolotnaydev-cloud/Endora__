# ENDO — Premium Client Space (static version)

A version of the same app with **no backend at all** — one HTML file plus
two bundled libraries. Built specifically so you can push it to GitHub and
get a live link via **GitHub Pages**, with nothing to install, run, or keep
running on your computer.

Chart.js and Leaflet are bundled locally under `vendor/` — nothing is
loaded from an external CDN, so it can't silently break because a CDN is
blocked on someone's network.

## Get a live link (GitHub Pages)

1. Create a new repo on GitHub (or use an existing one) and push this
   folder's contents to it:
   ```bash
   git init
   git add .
   git commit -m "ENDO static site"
   git branch -M main
   git remote add origin https://github.com/<your-username>/<repo-name>.git
   git push -u origin main
   ```
2. On GitHub: **Settings → Pages → Source → Deploy from a branch**, pick
   `main` and `/ (root)`, save.
3. Wait ~1 minute. Your link is:
   ```
   https://<your-username>.github.io/<repo-name>/
   ```

That's it — no build step, no server, nothing to configure.

## Try it locally first

No install needed — just open `index.html` directly in a browser
(double-click it, or drag it into a browser window). Everything works
identically to the deployed version.

## How it works without a backend

Every place the full-stack version called a REST API (`/api/profile`,
`/api/journal`, etc.), this version intercepts those same calls in the
browser and answers them from data built into the page — same shape,
same behavior, same generated analysis results for every exam type and
month. You wouldn't be able to tell the difference from the UI.

**Writes work too** — logging a journal entry, posting to the community
feed, liking a post, editing your profile — they're saved to
`localStorage`, so they're still there next time you open the same link
in the same browser.

**The one real trade-off, stated plainly:** `localStorage` is per-browser,
per-device. If you open the link on your phone, or a friend opens the
same link, they get their own separate copy of the data — nothing is
shared between visitors, because there's no server to share it through.
For a live demo, portfolio link, or trying the product yourself, that's
invisible. For a real multi-user product, you'd need the full-stack
version (`endo-fullstack-app.zip`) with an actual database behind it.

## Resetting the demo data

Open the browser console on the page and run:
```js
localStorage.clear(); location.reload();
```
This wipes anything you've added and restores the original seed data.

## Files

```
index.html      # everything — markup, styles, app logic, seed data, local "API"
vendor/          # Chart.js + Leaflet, bundled (no external CDN dependency)
```
