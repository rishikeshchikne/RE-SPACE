# RE:SPACE — Backup & Setup Guide

RE:SPACE is a digital museum of the NASA machines left on the Moon and Mars,
built for NASA Space Apps Challenge 2026. It is an independent student project,
not an official NASA website.

This ZIP has two folders:

| Folder | What it is | Use it when |
|---|---|---|
| `1-original-working-project/` | The complete original source code (React + TypeScript + Tailwind CSS). | You want to keep editing or rebuild the website. |
| `2-ready-built-website/` | The finished website, already built and split into `html/`, `css/`, `js/` and `images/`. | You just want to open or host the website as it is. |

---

## Folder 2 — Ready-built website (html / css / js / images)

```
2-ready-built-website/
├── index.html      → opens html/index.html automatically
├── favicon.ico
├── robots.txt
├── html/           → the 10 pages
│   ├── index.html                          (Home)
│   ├── explore.html                        (Archive of Forgotten Machines)
│   ├── map.html                            (3D Ghost Map + Mission Timeline)
│   ├── academy.html                        (Explorer Academy + quiz)
│   ├── about.html                          (About & Sources)
│   ├── artifact-apollo-11-descent-stage.html
│   ├── artifact-lunar-roving-vehicle.html
│   ├── artifact-surveyor-3.html
│   ├── artifact-sojourner.html
│   └── artifact-spirit.html
├── css/            → the full stylesheet
├── js/             → all page scripts (including the 3D Ghost Map)
└── images/         → NASA / USGS planet surface maps used by the 3D globes, favicon
```

### How to open it

The pages use links that start from the folder root (for example `/css/...`),
so **double-clicking an HTML file will NOT work**. Run a small local web server
inside `2-ready-built-website/`:

**Option A — Python (already on most computers)**
```
cd 2-ready-built-website
python -m http.server 8000        (on some computers: python3 -m http.server 8000)
```
Then open **http://localhost:8000/** in your browser.

**Option B — Node.js**
```
cd 2-ready-built-website
npx serve .
```
Then open the address it prints.

### How to put it online

Upload the *contents* of `2-ready-built-website/` to any static host
(Netlify Drop, Cloudflare Pages, Vercel, GitHub Pages with a custom domain, etc.).
It must sit at the **root of the domain** (e.g. `https://example.com/`), not in a sub-folder.

---

## Folder 1 — Original working project

### Requirements
- Node.js 20 or newer (https://nodejs.org) — includes `npm`.

### Run it
```
cd 1-original-working-project
npm install          (first time only, downloads the libraries)
npm run dev          (starts the site — open the address shown in the terminal)
```

Other commands:
```
npm test             (runs the 27 automated checks: artifacts, quiz, links, 3D map maths)
npm run build        (creates a production build in dist/)
```

You can also import this folder into a new GitHub repository and connect it to Lovable.

### Where everything lives (code map)

| Type | Location |
|---|---|
| **Pages** | `src/routes/` — `index.tsx` (Home), `explore.tsx`, `map.tsx`, `academy.tsx`, `about.tsx`, `artifact.$id.tsx` (one template for all 5 machine stories), `__root.tsx` (shared page shell, navigation, footer, fonts) |
| **Styles (CSS)** | `src/styles.css` — colours, fonts, starfield, glass panels, animations (Tailwind CSS v4) |
| **Scripts / components** | `src/components/museum/` — navigation, footer, cards, NASA source cards, page headers; `src/components/museum/space/` — 3D Ghost Map scene, sky, schematic fallback; `src/components/ui/` — buttons and other interface parts |
| **Data (museum content)** | `src/lib/artifacts.ts` — the 5 machines, references, image credits, timeline; `src/lib/quiz.ts` — Academy quiz; `src/lib/resources.ts` — official NASA links; `src/lib/space.ts` — 3D map coordinates, planet sizes, texture credits |
| **Images** | NASA photos load directly from images-assets.nasa.gov. Planet surface maps are in `public/__l5e/assets-v1/…/` (referenced by `src/assets/textures/*.asset.json`). |
| **Tests** | `src/test/` |
| **Settings** | `package.json`, `vite.config.ts`, `tsconfig.json`, `vitest.config.ts` |

### Notes
- No `.env` file is included. The museum is fully public and does not use sign-in
  or a database, so it runs without one. `.env.example` shows the optional
  (unused) template variables.
- `node_modules/` and build output are not included; `npm install` recreates them.

---

## Both folders need internet for
- NASA photographs (loaded from images-assets.nasa.gov)
- The Space Grotesk and Inter fonts (Google Fonts)
- The external NASA reference links

The 3D Ghost Map needs a browser with WebGL (all modern browsers). Devices without
it automatically show the flat schematic map instead.

## Image and data credits
Mission photos: NASA. Moon surface: NASA Scientific Visualization Studio (CGI Moon Kit,
LRO LROC / LOLA). Mars surface: NASA Ames / USGS Astrogeology (Viking MDIM 2.1) and
NASA / JPL / GSFC MGS MOLA. Earth: NASA Goddard / Visible Earth Blue Marble.
Full source links are on each artifact page and in the Ghost Map "Surface map credits".
