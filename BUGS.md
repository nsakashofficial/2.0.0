# Bug report — pre-release

Findings from the rebuild and their resolution status.

| # | Area       | Issue found in legacy build                                | Status in 2.0 |
|---|------------|-------------------------------------------------------------|---------------|
| 1 | Admin      | Access broken, buttons dead, half-rendered routes           | ✅ Rewritten `js/modules/admin.js` with 8 working tabs and admin allow-list |
| 2 | Home       | Duplicate settings icon and dead post button                | ✅ Redesigned nav; single `+` in tab bar |
| 3 | Messenger  | No live updates, no unread state                            | ✅ Firestore `onSnapshot` + unread counters |
| 4 | Settings   | Empty sub-pages                                             | ✅ Nine populated sections |
| 5 | Payments   | Missing screen entirely                                     | ✅ New `js/modules/payment.js` |
| 6 | Badges     | Blue/Gold/Diamond broken                                    | ✅ New `js/components/badge.js` with animated diamond |
| 7 | UX         | `alert()` used for feedback                                 | ✅ Global toast service |
| 8 | Offline    | White screen when offline                                   | ✅ Offline page + SW shell cache |
| 9 | Theme      | Dark mode inconsistent                                      | ✅ Tokenised, persisted, system-aware |
| 10| Router     | Broken deep-links / white screen on error                   | ✅ Hash router with skeleton + recovery UI |

## Known limitations (post-launch backlog)
- WebRTC call UI is out of scope for this pass (backend schema preserved).
- Analytics sparklines use derived counts; hook to real events when ready.
- Rate-limiting is currently a client-side UI affordance; enforce with Firebase
  security rules or Cloud Functions server-side.
