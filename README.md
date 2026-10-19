# HOF Games

Browser games by Home of Fight. Each folder is one self-contained game (static HTML/JS, no build step). Every game is black-and-gold HOF branding and designed to fit a phone screen.

| Folder | Game | Live now | What it is |
|---|---|---|---|
| `perfect-mma-fighter` | Build the Perfect MMA Fighter | https://buildaperfectfighter.netlify.app | Draft game: one random UFC fighter per round, lock him into one of 8 skill slots (Striking, Power, Wrestling, Jiu Jitsu, Cardio, Fight IQ, Chin, Speed); stats hidden until the end; one respin per game; scored out of 800 with tier badges and a shareable result image. ~1.3M plays/month. |
| `mma-casual-test` | MMA Casual Test ("How casual are you?") | https://mmacasualtest.netlify.app | 30 Agree/Disagree statements → a casual-to-hardcore fan score. |
| `mma-location-test` | MMA Location Test | https://mmalocationtest.netlify.app | 3D globe geography game: guess the location of fights/events. |
| `mma-survivor` | MMA Survivor | https://hofsurvivor.netlify.app | NFL-style survivor: pick one UFC winner every week, build a streak, lose once and you're out; profiles, leaderboard, streak prizes. Planned address: homeoffight.com/survivor |

## How the games fit into the HOF platform

- **The games stay in this repo** and are hosted from it on their own subdomain (to be set, e.g. `games.homeoffight.com/<folder>`). Pushes to `main` auto-deploy.
- **The website and the HOF App embed each game from that URL** (iframe / webview). Game code is never copied into the site or app codebase. HOF updates the games; the site and app pick up updates automatically.
- **Two things each game needs from the HOF platform:**
  1. **HOF Account API** — current logged-in user, submit result/score, award HOF XP. Players' best results persist on their profile.
  2. **Game content from the HOF database**, edited in the dashboard by the "Games operator" role (no code changes): fighters (name, photo, division, per-skill stats), test questions and answers, locations, MMA Survivor's weekly card and results, scoring thresholds. Fighters should be one shared table used by the games and by the site's Stats & Rankings section.

## Current state of the data (what moves to the dashboard)

Today all content is baked into each game's files:

- `perfect-mma-fighter`: fighter roster and stats live in the HTML (maintained from a spreadsheet); fighter photos are WebP files in `images/`, filenames slugged from fighter names.
- `mma-casual-test`: questions are in the HTML.
- `mma-location-test`: locations are in the HTML.
- `mma-survivor`: weekly card and results are entered manually.

Once the dashboard and API exist, each game will be switched to load this content from the HOF database.

**Division of work:** the dev team builds the database tables, the dashboard screens and the API (and imports the current data once). HOF then updates each game to read from the API instead of its built-in data.

## Notes

- Promo offers inside the web versions (sponsor banners, bonus links) are stripped in the app versions.
- Games must work full-screen on a phone with no scrolling.
