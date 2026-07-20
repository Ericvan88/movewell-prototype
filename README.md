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
  main entry point. The menu lists all Web Portals (Coordinator, Allied
  Health, Admin Portal) and all Mobile options (Maya · rider, Anna ·
  supporter, Deb · contractor driver, Lena · employed driver, plus New
  participant · self sign-up) on one page. Any option is one click away, and
  signing out of any app or workspace returns to this same menu.
- `AdminPortal.dc.html`: the internal ops portal (live ops with the Adelaide
  map, dispatch and rostering, participant register plus intake queue,
  drivers, driver onboarding, fleet assignment, claims, incidents,
  compliance). Ops mission control lives here as the Live Ops section.
- `CoordinatorWorkspace.dc.html`: coordinator caseload, plus an Add-participant
  onboarding wizard (identity, plan management, Supporter linking,
  accessibility, refer for allied-health assessment) and an Assessments view
  tracking those referrals.
- `AlliedHealthWorkspace.dc.html`: allied-health (OT) workspace with an
  incoming Referrals tab. Accepting a coordinator referral opens the
  assessment; saving returns the vehicle requirements and closes the loop.
- `ParticipantOnboarding.dc.html`: mobile self-service sign-up. A participant
  path (mobile, NDIS plan, address, accessibility, consent, into the app) and
  a Supporter path (look up a participant by mobile, send a consent-gated
  access request).
- `RiderApp.dc.html`, `SupporterApp.dc.html`, `DriverApp.dc.html`: the
  individual mobile app components, imported by the combined prototype.
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
