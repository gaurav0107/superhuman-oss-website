# superhuman website

Static landing page for the superhuman harness. One self-contained `index.html` plus two image assets — no build step, no dependencies.

Implemented from the Claude Design project "Superhuman Landing - Options" (option 1a, Orbit): the hero is a live demo window where one unattended run — issue-selector → repo-profiler → planner → builder → scorer — converges to **Merged** around the mascot, on a 16-second loop.

## Preview locally

```bash
open index.html
# or, to serve it:
python3 -m http.server 8000
```

## Deploy

### Vercel

This is a zero-config static site — `index.html` and `assets/` live at the repo
root, and `vercel.json` adds clean URLs plus long-lived caching for assets.
Import the repo into Vercel and deploy (leave every setting at its default), or
from the CLI:

```bash
vercel        # preview deploy
vercel --prod # production deploy
```

### Any static host

Any static host works — just serve the repo root. For GitHub Pages, enable
Settings → Pages → Deploy from a branch (`main` / `/root`).

## Assets

- `assets/mascot-scene.png` — transparent cutout of the mascot at its desk (hero centerpiece)
- `assets/mascot.png` — square face crop on cream (nav avatar / OG image)

Both are crops of the source character art (`ChatGPT Image Jul 5, 2026, 05_43_27 PM.png`). Fonts load from Google Fonts (Instrument Sans, IBM Plex Mono); everything else is local.
