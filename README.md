# MoveWell: complete prototype

Interactive HTML/CSS/JS prototypes for MoveWell, an NDIS transport platform.
Exported from Claude Design (claude.ai/design) as a handoff bundle.

Live demo: https://ericvan88.github.io/movewell-prototype/

## Run locally

These are `.dc.html` files rendered by a small runtime (`support.js`) that
resolves `<dc-import>` components via `fetch()`, so they must be served over
HTTP. Opening a file directly (`file://`) will not work.

```bash
npx serve .
# or
python3 -m http.server 8080
```

Then open **`MoveWell Complete Prototype.dc.html`** (or just the root URL,
which redirects there).

## Structure

- **`MoveWell Complete Prototype.dc.html`**: the combined prototype and
  main entry point. The menu lists all Web Portal workspaces (Coordinator,
  Allied Health, Ops mission control) and all Mobile users (Maya · rider,
  Anna · supporter, Deb · contractor driver, Lena · employed driver) on one
  page. Any option is one click away, and signing out of any app or
  workspace returns to this same menu.
- `RiderApp.dc.html`, `SupporterApp.dc.html`, `DriverApp.dc.html`,
  `CoordinatorWorkspace.dc.html`, `AlliedHealthWorkspace.dc.html`: the
  individual app/workspace components, imported by the combined prototype.
- `MoveWell Web Demo.dc.html`, `MoveWell Mobile Demo.dc.html`: the original
  standalone Web and Mobile demos, kept for reference. Each still runs on
  its own.
- `MoveWell Admin Portal.dc.html`, `MoveWell Recruitment Portal.dc.html`,
  `MoveWell Rider Flow.dc.html`, `MoveWell Driver App.dc.html`,
  `MoveWell Supporter Network & Ops.dc.html`, `MoveWell Platform.dc.html`:
  design-review canvases with multiple iterations/options, not part of the
  combined prototype's live flow.
- `assets/`, `uploads/`, `screenshots/`: images and reference files.
- `support.js`, `browser-window.jsx`, `ios-frame.jsx`: the Claude Design
  prototype runtime and device-frame components.

## Notes

- Design medium is HTML/CSS/JS. These are prototypes, not production code.
- See `CLAUDE.md` for project-specific writing conventions (no em/en dashes).
