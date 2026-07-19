# MoveWell — Brand & Scope Bundle (load into Claude Design)

Everything Claude Design needs to prototype the MoveWell platform with the correct brand. The visual system is copied directly from the earlier Wayflo brand; only the wordmark word changed.

## What's in here

```
movewell-brand/
├── README.md                     ← this file
├── brand-tokens.css              ← drop-in CSS variables (colours, gradients, radius, font)
├── logo/
│   ├── svg/                      ← scalable, editable — prefer these
│   │   ├── movewell-primary-gradient.svg      (marketing / mixed audience)
│   │   ├── movewell-client-coral.svg          (Client App)
│   │   ├── movewell-driver-purple.svg         (Driver App / Operator Portal)
│   │   ├── movewell-admin-purplegrad.svg      (Admin Portal)
│   │   ├── movewell-inverted-white.svg        (dark backgrounds)
│   │   ├── movewell-icon-*.svg                (app-icon / favicon marks)
│   │   └── movewell-wordmark-*.svg            (wordmark only, dark/white)
│   └── png/                      ← raster exports incl. 16/32/180/512/1024 icon sizes
└── movewell-platform-scope.md    ← the platform scope (users, surfaces, IA, per-portal intent)
```

## Which logo where

| Surface | Use |
|---------|-----|
| Client App (participant/family/coordinator) | `movewell-client-coral` + coral icon |
| Driver App | `movewell-driver-purple` + purple icon |
| Admin Portal (incl. Fleet/Asset module) | `movewell-admin-purplegrad` + admin-grad icon |
| Marketing / Driver Recruitment site | `movewell-primary-gradient` (full coral→purple) |
| Any dark section | `movewell-inverted-white` |

## Logo construction (so Design can extend it)

- **Mark:** rounded square, corner radius ≈ 23.5% of side (reads as 0.75rem at UI scale), solid or gradient fill, **no internal artwork**.
- **Wordmark:** lowercase `movewell`, Inter ExtraBold (≈800). Black `#2D3748` on light, white on dark. Never colour-on-colour.
- **Hero gradient:** `linear-gradient(135deg, #FF6B6B → #6C5CE7)`.
- Don't stretch, skew, rotate, or recolour outside the published variants.

## How to load into Claude Design

1. Add `brand-tokens.css` as the project's base styles / design tokens.
2. Upload the SVGs from `logo/svg/` as brand assets.
3. Give Design `movewell-platform-scope.md` as the build brief.
4. Point Design at the surface→logo table above so each app uses its correct variant.

## Note on font

The wordmark is outlined (vector paths) so it renders identically without the font installed. For **UI text**, load **Inter** (open source) — it's the working brand typeface. Atkinson Hyperlegible is the accessibility-first alternative and a good choice for the Client App.
