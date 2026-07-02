# Open Docket

A single-file, no-build web app that tracks government public comment periods before they close — the legally-required windows that almost nobody knows to check, because there's no consumer-facing tool that surfaces them.

**Live demo of the concept:** open `index.html` in any browser. No install, no server, no build step.

## What it does

- Shows dockets (rules, permits, zoning changes, rate cases) currently open for public comment
- Sorts by days remaining so the most urgent ones surface first
- Lets you star items into a personal watchlist (saved in `localStorage`, stays on your device)
- Exports your watchlist deadlines as a `.ics` file you can drop into Google/Apple/Outlook calendar
- Optionally connects to the real [Regulations.gov API v4](https://open.gsa.gov/api/regulationsgov/) using your own free key, entered client-side and stored only in your browser
- Falls back to realistic example data (with dates computed relative to today) if you don't have a key or the API call fails, so the app is never empty or broken

## Why this one

Bill trackers, budget visualizers, and campaign finance maps already exist in decent form. Public comment periods are federally and often locally *mandated* to be open for input — and participation is usually in the single digits, not because people don't care, but because nothing tells them the window exists. This tool closes an awareness gap, not a UX gap.

## Deploying to GitHub Pages

1. Create a new repo (e.g. `open-docket`) and push this folder's contents to it.
2. In the repo, go to **Settings → Pages**.
3. Under **Build and deployment**, set **Source** to `Deploy from a branch`, branch `main`, folder `/ (root)`.
4. Save — your app will be live at `https://<your-username>.github.io/open-docket/` within a minute or two.

No build step, no dependencies to install, no secrets to configure — it's a static HTML file with embedded CSS/JS.

## Extending it

Good next steps if you want to take this further:
- Add state/local open-data portals (many run on Socrata or CKAN) alongside the federal Regulations.gov feed
- Add a zip-code or topic subscription with email digests (would need a small serverless function, since this is currently 100% client-side)
- Add a "plain-language summary" pass using an LLM API call to translate dense regulatory text
- Persist the watchlist to a shareable link instead of only `localStorage`, so people can send a docket to someone else

## Notes on the live-data mode

Regulations.gov's public API is designed for external consumption and works with the `DEMO_KEY` for light testing, but that key is rate-limited. Get your own free key at the link above for regular use. The key never leaves your browser — it's sent directly to Regulations.gov, not through any server of ours (there is no server).
