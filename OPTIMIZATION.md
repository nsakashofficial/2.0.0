# Optimization report

## Startup budget
- **HTML shell:** ~1.6 kB gzip
- **Critical CSS (tokens+base+components):** ~5 kB gzip
- **Entry JS `main.js`:** ~1.2 kB gzip; further modules lazy-loaded on demand.
- **Firebase SDK:** deferred until a service consumer imports it.

## Techniques applied
- Route-level code splitting via dynamic `import()` in `js/main.js`.
- Skeleton loaders on every route (no white screens).
- Preconnect hints to `gstatic.com`, `firestore.googleapis.com`, `res.cloudinary.com`.
- Service worker: stale-while-revalidate for same-origin, cache-first for
  Cloudinary media, network-first for Google APIs.
- Feed cached in `localStorage` for 60 s (`cache.wrap`).
- `loading="lazy"` on post images.
- `will-change`-free transitions using `transform/opacity` only.
- `Intl` for number/date/currency (no bundled date lib).

## Prevented failure modes
- Router `try/catch` renders a recovery UI on module errors.
- Toast messages replace every `alert()` and provide user-visible feedback.
- Firestore failures degrade gracefully (empty feed / cached list).

## Possible future wins
- Ship a build step that minifies JS/CSS and inlines critical CSS (~-30 %).
- Move Firebase to a self-hosted bundle (`firebase/app` + `firebase/auth`).
- Split analytics sparkline into its own micro-module.
