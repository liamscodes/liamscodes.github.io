# liamscodes.github.io

Liam's personal GitHub Pages site. The thing that gets worked on here is the
**Gym App** (workout tracker) in `workout/`. Everything else at the root is
static site pages; leave them alone unless asked.

## Gym App: where things live

- `workout/index.html` is the whole app: a single-file PWA (vanilla JS, no
  build step). `sw.js` and `manifest.webmanifest` make it installable.
- `workout/netlify/functions/data.mjs` is the sync API (`/api/data`), a
  Netlify Function backed by Netlify Blobs. GET reads, POST merges. The sync
  code is the only credential; it works as `Authorization: Bearer <code>` or,
  for GET only, `?code=<code>`. Data is keyed by the SHA-256 of the code.
- `workout/README.md` has the full feature list, data shape, and API notes.
- `workout/.claude/skills/workout-progress/` is a skill for fetching Liam's
  real data from the API and analyzing progress.

## Deploys

- **Netlify** site `liams-workout-log` (https://liams-workout-log.netlify.app)
  deploys automatically from `main`, base directory `workout/`. Pushing to
  `main` is a production deploy of the app and the sync function.
- **GitHub Pages** serves this repo too, so the same app is also reachable at
  https://liamscodes.github.io/workout/ and talks to the Netlify API
  cross-origin. Liam's phone may be installed from either URL, so keep both
  working and never remove `workout/`.
- There is no separate source of truth. `liamscodes/workout-log` on GitHub is
  an older standalone copy and is not deployed; do not sync to or from it.

## Working here

- Liam works from Claude Code on the web and wants changes committed and
  pushed to `main` directly, not via pull requests, unless he says otherwise.
- Never print, log, or commit Liam's sync code. If a task needs it, read
  `WORKOUT_SYNC_CODE` from the environment or ask once and do not echo it.
- Local dev: `cd workout && npm i && node dev-server.mjs`, then open
  http://localhost:8888. It runs the real function against a local Blobs
  server.
- `node --check` the `.mjs` files before pushing; there is no test suite.
- Keep `index.html` a single file with no build step. Match the existing
  style (2-space indent, plain JS, mobile-first CSS).
