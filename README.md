# First Measure Studios

Independent game development studio site for First Measure Studios, based in Harrison, Arkansas. Built as a static site and deployed via GitHub Pages.

**Live site:** https://firstmeasurestudio.store

## Structure

```
/
├── index.html          Main site — hero, projects grid, studio info, contact
├── privacy.html         Privacy page
├── show.html             Sessions page — actual play showcase/episode archive
├── favicon.ico           Multi-resolution favicon
├── site.webmanifest      Android/PWA icon manifest
├── CNAME                 Custom domain config for GitHub Pages
├── assets/               Favicon sizes, apple-touch-icon, and OG social preview image
└── tools/                DM Toolkit — see below
    ├── index.html               Tools landing page
    ├── shared.css               Shared nav/footer/layout styles for all tool pages
    ├── dice-calculator.html      Dice probability calculator
    ├── hit-chance.html           Hit-chance curve visualizer
    ├── initiative-tracker.html   Initiative tracker
    ├── loot-tables.html          Encounter & loot table generator
    ├── battle-map.html           Battle map grid
    ├── name-generator.html       Name generator
    ├── npc-quest-generator.html  NPC & quest hook generator
    ├── hex-map.html              Procedural hex map generator
    ├── logic-puzzles.html        Logic puzzle generator (mystery deduction + knights & knaves)
    └── session-recorder.html     Browser-based mic/camera backup recorder
```

No build step, no dependencies, no backend. Every page is plain HTML/CSS/JS and can be opened directly or served as static files.

## Main Site

Single-page layout covering:
- **Projects** — current game dev, tabletop, and writing projects
- **Studio** — design philosophy, craft/medium, and narrative approach
- **Contact** — links out

Visual identity: dark editorial aesthetic (`--ink` background, `--amber` accent), Cormorant Garamond (serif/display), Barlow Condensed (body/UI), and DM Mono (labels/data), with a subtle grain overlay and hairline rules throughout.

## Sessions (`show.html`)

Showcase/archive page for actual play recordings from the tabletop table (multitrack in-person audio, edited before posting). Two sections:

- **Episodes** — data-driven from an `EPISODES` array at the bottom of `show.html`. Empty by default (shows an honest "in production" state). To publish an episode, add an entry to that array — fully documented inline with an example. Supports two hosting paths: a YouTube embed (`type: 'youtube'`, give it a `youtubeId`) or a self-hosted file (`type: 'audio'`/`'video'`, give it a `mediaUrl` pointing into `/media`). Newest entries go at the top; there's no backend, so "publishing" just means editing this array and pushing.
- **Shows** — a repeatable list of the shows themselves (currently the Issylra campaign and Pilated Pals, plus the upcoming public series), each its own `.show-entry` block with a system tag, status badge, and fact list. Copy an existing block to add a new show.

Deliberately avoids referencing Dungeons & Dragons by name or branding in the public copy — the planned public series uses an original FFG Star Wars-based setting instead, to sidestep WotC's IP enforcement stance.

## DM Toolkit (`/tools`)

A set of small, client-side utilities for running and building tabletop games, linked from the "Tools" tab in the main nav. All 10 are live:

| Tool | What it does |
|---|---|
| Dice Probability Calculator | Parses dice formulas (`3d6+2`, `1d20+1d4`, etc.) and computes the *exact* outcome distribution — mean, range, std. dev., full bar chart, and chance to hit a target number. |
| Hit-Chance Curve Visualizer | Editable distance → hit-chance breakpoints, rendered as a piecewise-linear falloff curve, with a distance probe. |
| Initiative Tracker | Add combatants, auto-sort by initiative, track HP/conditions, step through rounds. Persisted to `localStorage`. |
| Encounter & Loot Tables | Build your own weighted tables and roll on demand. Saved to `localStorage`, and **shareable by link** — a table's data is encoded into the URL and auto-imports into whoever opens it. |
| Battle Map Grid | Pan/zoom SVG tactical grid with colored, draggable, labeled tokens. |
| Name Generator | Syllable-based name generation across 4 styles (High Fantasy, Grim/Northern, Sci-Fi, Settlement). Click a name to copy it. |
| NPC & Quest Hook Generator | Tabbed roller for a quick NPC (role/trait/want/secret) or a quest hook with a built-in twist. |
| Procedural Hex Map | Clustered-terrain hex grid generation with adjustable radius and reroll. |
| Logic Puzzles | Mystery deduction grids and knights & knaves riddles — each puzzle is run through a backtracking solver before being shown, guaranteeing a unique, deducible solution rather than randomly-scattered clues. |
| Session Recorder | Browser-based mic/camera backup recorder using MediaRecorder — live input level meter, device selection, audio-only or audio+video modes. Records and downloads entirely client-side; nothing is uploaded. |

Shared styling for all tool pages lives in `tools/shared.css` (nav, footer, page-header, section, status-badge, and fade-up scroll-reveal styles) so individual tool pages only need to define their own page-specific CSS.

### Adding a new tool

1. Copy the `<head>` / nav / footer / fade-up scaffolding from an existing tool page (e.g. `dice-calculator.html`) and link `shared.css`.
2. Build the tool in a single self-contained HTML file — no external JS dependencies beyond Google Fonts.
3. Add a card for it to `tools/index.html`'s grid (bordered individual cards with real gaps — any tool count works cleanly now, no column-math needed).
4. Link it from the Projects section on the main site if it's substantial enough to stand on its own.

## Deployment

Pushes to `main` deploy automatically via GitHub Pages. No CI/build step — whatever's committed is what's served.
