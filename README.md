# Foldable Guide

A framework-free **PWA boilerplate for foldable devices**, with a live demo: the **Posture Inspector**.

It uses the [Device Posture API](https://www.w3.org/TR/device-posture/) and the [Vie API](https://drafts.csswg.org/mediaqueries

Plain HTML, CSS and JavaScript. No framework, no build step.

## Run it

```sh
npm install      # dev tools only (static server + tests)
npm start        # http://localhost:8080
```

Any static server works. Service workers need `localhost` or HTTPS.

**No foldable?** In Chrome DevTools, open device emulation and pick a foldable  or use **More tools → Sensors** to change the device posture.

## Test it

```sh
npm test
```

Playwright on Chromium. Foldable postures and segments (book, tabletop, Surface Duo hinge) are emulated through the Chrome DevTools Protocol, see [`tests/helpers.js`](tests/helpers.js). Accessibility and contrast are checked with axe in light and dark mode.

## Project layout

| Path | What it is |
| --- | --- |
| `index.html` | The Posture Inspector page. |
| `404.html` | Offline fallback and GitHub Pages 404. |
| `manifest.webmanifest`, `icons/` | PWA manifest and icons (`npm run icons` re-renders the PNGs from the SVGs). |
| `sw.js` | Service worker: precaches the app, serves `404.html` for uncached pages offline. |
| `css/token.css` | Colors, type, spacing. Rebrand here. |
| `css/base.css` | Reset, base responsive layout, Window Controls Overlay title bar. |
| `css/foldable.css` | **Scaffold**: empty, commented blocks for every posture and segment configuration. |
| `css/inspector.css` | The demo's layouts, a worked example of `foldable.css`. |
| `js/features.js` | Feature detection. |
| `js/foldable.js` | Current posture + segments, with a single change subscription. |
| `js/components/` | The Inspector's Web Components. |
| `specs/` | Mission, tech stack, roadmap and feature specs. |

## Fork it and build your own app

1. Replace the content of `index(keep the header, the `<main>`, and the two `.pane` wrappers if you want one pane per segment).
2. Delete `css/inspector.css` and `js/components/`, and remove them from `index.html`, `js/app.js` and the `PRECACHE` list in `sw.js`.
3. Add your foldable styles to the matching blocks in `css/foldable.css`. Each block says which posture and devices it targets.
4. Need posture or segment data in JavaScript? Use `onFoldableChange()` from `js/foldable.js`.
5. Update the name, colors and icons in `manifest.webmanifest`, `css/tokens.css` and `icons/`.
6. Bump `VERSION` in `sw.js` whenever you change a precached file.

## Deploy

The app is fully static. GitHub Pages works as-is: serve the repository root.
