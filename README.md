# MoveWell — complete prototype

Interactive HTML/CSS/JS prototypes for MoveWell, an NDIS transport platform.
Exported from Claude Design (claude.ai/design) as a handoff bundle.

## Run locally

These are `.dc.html` files rendered by a small runtime (`support.js`) that
resolves `<dc-import>` components via `fetch()`, so they must be served over
HTTP — opening a file directly (`file://`) will not work.

```bash
npx serve .
# or
python3 -m http.server 8080
```

Then open **`MoveWell Complete Prototype.dc.html`** — this is the main entry
point.

## Structure

- **`MoveWell Complete Prototype.dc.html`** — the combined prototype. Shows a
  main menu with two forks, **Web Portals** and **Mobile**. Signing out of
  any app or workspace returns to this menu.
  - **Web Portals** → choose a workspace (Coordinator, Allied Health, Ops
    mission control)
  - **Mobile** → choose a user (Maya · rider, Anna · supporter, Deb ·
    contractor driver, Lena · employed driver), shown in an iOS device frame
- `RiderApp.dc.html`, `SupporterApp.dc.html`, `DriverApp.dc.html`,
  `CoordinatorWorkspace.dc.html`, `AlliedHealthWorkspace.dc.html` — the
  individual app/workspace components, imported by the combined prototype
- `MoveWell Web Demo.dc.html`, `MoveWell Mobile Demo.dc.html` — the original
  standalone Web and Mobile demos (kept for reference; each also still runs
  on its own)
- `MoveWell Admin Portal.dc.html`, `MoveWell Recruitment Portal.dc.html`,
  `MoveWell Rider Flow.dc.html`, `MoveWell Driver App.dc.html`,
  `MoveWell Supporter Network & Ops.dc.html`, `MoveWell Platform.dc.html` —
  design-review canvases with multiple iterations/options, not part of the
  combined prototype's live flow
- `assets/`, `uploads/`, `screenshots/` — images and reference files
- `support.js`, `browser-window.jsx`, `ios-frame.jsx` — the Claude Design
  prototype runtime and device-frame components

## Notes

- Design medium is HTML/CSS/JS — these are prototypes, not production code.
- See `CLAUDE.md` for project-specific writing conventions (no em/en dashes).
