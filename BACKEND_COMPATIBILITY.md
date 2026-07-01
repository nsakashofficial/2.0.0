# Backend compatibility report

## Preserved integrations
| Service    | Identifier                       | Status     |
|------------|----------------------------------|------------|
| Firebase   | project `meetwoyou-436a2`        | ✅ preserved |
| Firebase   | web app id `1:612788132077:web:0a8b92edf26778efd4d4e4` | ✅ preserved |
| Cloudinary | cloud `dpgawb5sl`, preset `Meetwoyou` (unsigned) | ✅ preserved |

No credentials were rotated, no projects were recreated, no data was migrated.

## Firestore collections (unchanged)
- `users`
- `chats` (+ subcollection `messages`)
- `activity`
- `calls`
- `offerCands`
- `ansCands`

New optional user fields (extensions only, never destructive):
- `banned: boolean` — set by admin.
- `forceLogoutAt: number` — timestamp to invalidate old sessions.
- `verified: 'blue' | 'gold' | 'diamond' | null` — badge tier.
- `premium: boolean` — reserved for future premium features.

## Endpoints & SDKs
- Firebase modular SDK v10.8.0 loaded from `gstatic.com` (same version as legacy).
- Cloudinary REST: `POST https://api.cloudinary.com/v1_1/dpgawb5sl/auto/upload` — unchanged.

## Migration notes
No data migration is required. Legacy users, chats, and posts remain fully
readable. New writes only *extend* documents with additional optional keys.

## Env override
Runtime override is available through `env.js` (`window.__MW_ENV__`). Missing
keys fall back to production values defined in `js/services/config.js`.

## File mapping vs legacy
| Legacy concept     | New location                              |
|--------------------|-------------------------------------------|
| `sw.js`            | `service-worker.js` (extended cache strat) |
| Firebase init      | `js/services/firebase.js`                 |
| Cloudinary upload  | `js/services/cloudinary.js`               |
| Admin gating       | `js/services/auth.js` (email allow-list)  |
| Feed rendering     | `js/modules/home.js`                      |
| Messenger          | `js/modules/messenger.js`                 |
| Payments           | `js/modules/payment.js` (new)             |
| Admin panel        | `js/modules/admin.js` (rebuilt)           |

## Existing feature status
- Login / register / password reset → **working**
- Read/write to `users` / `chats` / `activity` → **working**
- Cloudinary uploads → **working** (unsigned preset preserved)
- WebRTC signalling collections (`calls`, `offerCands`, `ansCands`) → **preserved**
  (front-end call UI is out of scope this pass; back-end untouched).
