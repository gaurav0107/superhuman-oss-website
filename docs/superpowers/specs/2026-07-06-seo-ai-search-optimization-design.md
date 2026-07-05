# superhuman website — SEO & AI-search optimization

**Date:** 2026-07-06
**Origin:** https://superhuman-oss.com
**Scope:** Technical SEO + one FAQ section. Hero and existing sections' visuals unchanged. Single static `index.html` + root files. No build step.

## Goal

Rank on page 1 for **B (platform)** and **C (use-case)** keyword clusters, and be citable by AI answer engines (ChatGPT, Claude, Perplexity, Google AI Overviews).

Target terms: `Claude Code plugin`, `Codex skill` / `Codex agent`, `contribute to open source with AI`, `AI agent for GitHub issues`, `autonomous open-source contributions`, `AI pull requests`, `merge-ready AI PRs`.

## Strategy notes / constraints

- **Brand-collision reality:** the bare word "superhuman" is dominated by Superhuman (email client) and is not a target. We win on descriptive B+C long-tail; `superhuman-oss.com` + entity markup disambiguate.
- **Timely wedge:** ~17M AI PRs hit GitHub in early 2026 and GitHub shipped PR caps/kill-switches over "AI slop." superhuman's self-scoring, merge-ready-before-submit loop is the direct answer — lean into it in copy, FAQ, and llms.txt.
- **Hero untouched.** All keyword work lives in `<head>`, structured data, the new FAQ, and root files.

## Deliverables

### 1. `<head>` — keyword + technical tags
- **`<title>`**: `superhuman — autonomous open-source contributions for Claude Code & Codex`
- **meta description**: `An open-source AI agent for Claude Code & Codex that finds a GitHub issue, writes the fix, and scores its own pull request until it's merge-ready. Free, MIT.`
- **canonical**: `https://superhuman-oss.com/`
- **robots**: `index, follow, max-image-preview:large, max-snippet:-1`
- **Open Graph** (upgrade): absolute `og:image` (`https://superhuman-oss.com/assets/mascot.png` until the OG-image add-on lands), `og:url`, `og:type=website`, `og:site_name`, `og:image:alt`, `og:image:width/height`, keep title/description.
- **Twitter**: `summary_large_image` + title/description/image/image:alt.
- **misc**: `theme-color` (#F0B429), `author`.

### 2. Structured data — three JSON-LD blocks
- **SoftwareApplication**: name, keyword-rich description, `applicationCategory: DeveloperApplication`, `operatingSystem: "Claude Code, OpenAI Codex, macOS, Linux"`, `offers` price 0 USD, MIT license, `softwareVersion: 0.8.0`, `downloadUrl` = repo, `keywords`.
- **WebSite** (with publisher Organization: name, url, logo).
- **FAQPage**: the six Q&As below.

### 3. FAQ section (new; matches existing `.section` rhythm, sits before Install or after Loop)
Kicker `FAQ`, `<h2>`, six `<details>`/semantic Q&A pairs. Copy (also mirrored into FAQPage JSON-LD):

1. **What is superhuman?** — Free, open-source (MIT) plugin for Claude Code and OpenAI Codex that autonomously contributes to open-source projects. An agent team picks a GitHub issue, learns the repo's conventions from its merged PRs, writes the fix with tests, and scores its own pull request on a 10-dimension rubric — iterating until ~95% merge-probability. Already merged into Hugging Face Transformers, Apache Airflow, and Ant Design.
2. **How is it different from Copilot, Cursor, Devin, or SWE-agent?** — Most AI coding tools are open-loop: generate once and hope. superhuman is closed-loop — it grades its own PR against a maintainer-style rubric and fixes the single weakest dimension until the PR would actually merge. That self-scoring gate is why its PRs are built to be accepted, not added to the pile of unreviewed "AI slop."
3. **Is it safe — won't it spam maintainers with low-quality PRs?** — Safety is the core design goal. It only opens a PR after the scorer estimates ~95% merge-probability twice in a row, works on forks only, pushes with `--force-with-lease`, runs only allowlisted CI commands, and is MIT-licensed and auditable. It's built to be the opposite of the automated PR spam that pushed GitHub to add PR limits in 2026.
4. **Does it work with OpenAI Codex, or only Claude Code?** — Both. In Claude Code it installs as a plugin (`/plugin install superhuman@superhuman`). In Codex you symlink the skill into `~/.codex/skills` and tell Codex to "use the superhuman skill to contribute." Same workflow on either harness.
5. **Is it free? What does it cost to run?** — superhuman is free and open-source under MIT. You pay only for your own model usage through Claude Code or Codex — no separate subscription, seat, or API.
6. **What do I need to get started?** — The `gh` CLI (authenticated), `git`, and `jq`. In Claude Code, install the `superpowers` plugin first (prerequisite), then add the superhuman marketplace and install — two commands, then it runs unattended.

### 4. Root files
- **`robots.txt`** — `Allow: /` for all, explicit allow for `GPTBot`, `ClaudeBot`, `anthropic-ai`, `PerplexityBot`, `Google-Extended`, `CCBot`, `Applebot-Extended`; `Sitemap:` line.
- **`sitemap.xml`** — single URL `https://superhuman-oss.com/`, `lastmod 2026-07-06`, weekly, priority 1.0.
- **`llms.txt`** — condensed markdown brief: what it is, the loop, why-different, proven merges, install (Claude Code + Codex), requirements, links.

### 5. `vercel.json`
- Keep `cleanUrls`/asset cache. Ensure `robots.txt`, `sitemap.xml`, `llms.txt` served at root with correct content types (Vercel infers; no rewrite needed). Add a short cache header for `llms.txt`/`sitemap.xml` if convenient (optional).

## Explicitly out of scope (YAGNI)
No blog/docs system, no framework/build, no hero redesign, no `keywords` meta tag (dead signal for Google).

## Deferred add-ons (remind user after SEO work)
- **A) 1200×630 OG image** — replace square `mascot.png` as the social/LLM link card; swap `og:image`/`twitter:image` to `og.png` once generated.
- **B) GitHub repo SEO copy** — repo description + ~15 topics + README front-matter tuned to the same B+C keywords, for `gaurav0107/superhuman` (can't push from here; hand off as copy-paste).

## Verification
- Each JSON-LD block parses as valid JSON.
- `robots.txt`, `sitemap.xml`, `llms.txt` reachable at root when served.
- Single `<h1>`; FAQ renders; no console errors; page still fits one viewport (hero unchanged).
