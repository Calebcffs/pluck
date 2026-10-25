# Pluck

Reference tones for tuning a guitar by ear. No mic, no pitch detection, just a plucked string you match by ear. Works fully offline once it's loaded.

Plain HTML/CSS/JS. No build step, nothing to install.

## Using it

- Click a string (or press **1-6**, where 1 is high E) to hear it. **S** strums all six.
- Change any string's note with its dropdown. The little number next to it is the octave, picked automatically. Tap it to pin a specific octave (handy for baritone or weird setups).
- **Loop**: the icon at the end of each row keeps that string re-plucking until you turn it off. You can loop several at once, like droning the A while you tune the D. **Shift+1-6** toggles a loop, **Esc** stops them all. Loops also stop if you switch away from the app.
- **Save**: once the strings don't match a known tuning, Save lights up. Your tunings show under "My tunings" in the dropdown.
- **...** menu: rename or delete saved tunings, and export/import them as a JSON file to back up or move between devices.

## Run it locally

Any static file server works. From this folder:

```
python3 -m http.server 8000
```

Then open http://localhost:8000. The offline bit (service worker) only works on `localhost` or HTTPS, not by opening `index.html` straight from disk.

## Put it on your phone

The phone needs to reach it over HTTPS, so the easy route is GitHub Pages:

1. On GitHub: repo **Settings > Pages**, source "Deploy from a branch", branch `main`, folder `/ (root)`. Save.
2. After a minute it's live at `https://calebcffs.github.io/pluck/`.
3. Open that link on the phone once (so it can cache everything), then:
   - **iPhone (Safari)**: Share button > **Add to Home Screen**.
   - **Android (Chrome)**: menu > **Install app** (or "Add to Home screen").
4. Test it: airplane mode on, open Pluck from the home screen, tap a string.

iPhone note: on iOS 17+ it plays even with the silent switch on. On older iOS, flip the switch off or you'll hear nothing.

## Updating

The service worker serves the cached copy first. After changing any file, bump `VERSION` in `sw.js` (e.g. `pluck-v2`) or phones will keep the old version. They pick up the new one on the next launch or two.

## Checking installability

Lighthouse dropped its PWA category in v12, so use Chrome DevTools instead: **Application > Manifest** should show no installability warnings, and **Application > Service workers** should show `sw.js` activated. Chrome's address bar also shows an install icon when it's all good.
