# superhuman website

The site for superhuman, the open-source Claude Code plugin: https://superhuman-oss.com. Two static pages and
their assets. No build step, no dependencies.

- `index.html`: the home page, self-contained (styles and script inline).
- `merged/`: the Merge Wall, every merged pull request with its link. Served at `/merged`.

The look is the superhuman "Workbench" brand, kept in the `superhuman-growth` repo (`brand/README.md` for the
rules, `brand/theme.css` for the tokens): a stone ruled page, white panels, ink type, one small yellow,
Host Grotesk with DM Mono, two public-domain paintings from The Met (saved in `assets/`), and the product on screen.

## Preview locally

```bash
python3 -m http.server 8000
```

Then open http://localhost:8000. Opening `index.html` as a file also works, but the totals are then the ones
written in the page, because it cannot fetch `/merged/data.json`.

## Numbers

The totals on the home page (merged pull requests and projects) are written into `index.html` as a
fallback and replaced on load from `merged/data.json`. Refresh the Merge Wall and the numbers follow.

## Refresh the Merge Wall

The Merge Wall is built in `superhuman-growth` (`python3 scripts/merge_wall.py` writes `site/merged/`). Copy it
here and commit:

```bash
cp ../superhuman-growth/site/merged/{index.html,data.json,og.png} merged/
```

The generator writes the totals and every row into `merged/index.html`, so the page reads the same with JavaScript off.

## Deploy

Vercel serves the repo root from `main`. `vercel.json` adds clean URLs, security headers (a Content-Security-Policy that allows only this site and Google Fonts) and a one-day cache for `assets/`. `.vercelignore` keeps `docs/` and this README off the site. If you add a script, style or image from another host, add it to the policy in `vercel.json` or the browser will block it.
A push to any other branch gets a preview deployment.

## Assets

- `assets/mark.svg`: the logo mark, ink brackets and a yellow slash (header, footer).
- `assets/favicon.svg`: the same mark, with white brackets in dark browser themes.
- `assets/apple-touch-icon.png`: the avatar, 180x180.
- `assets/og.jpg`: link preview, 1200x630 (`og:image`, `twitter:image`).
- `assets/evidence-*.jpg`: evidence cards of real merged pull requests (ClickHouse, Deno), made by `superhuman-growth/scripts/make_media.py evidence` and resized to 720x900.
- `assets/painting-day.jpg`, `assets/painting-night.jpg`: John Frederick Kensett, "Lake George", 1869, and Johan Christian Dahl, "Copenhagen Harbor by Moonlight", 1846. The Metropolitan Museum of Art, Open Access, public domain. Resized to 2000px wide.
- `assets/mascot-hero.jpg`: the mascot, from `superhuman-growth/brand/mascot/hero.png` (closing band).
- `assets/mascot-scene.png`, `assets/mascot.png`: the old mascot, kept because old links and previews point at them.

