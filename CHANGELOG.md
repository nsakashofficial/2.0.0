# Changelog — Meetwoyou 2.0.0

## Rebuild highlights
- Full rebuild as pure HTML + CSS + vanilla JS (no build step).
- Modular directory layout under `js/{utils,services,components,modules}`.
- New lazy-loading hash router with skeleton fallbacks & error recovery.
- Design tokens for consistent light/dark theming; system-aware.
- Installable PWA with offline shell, stale-while-revalidate, and push scaffold.

## Home
- Centred logo, right-aligned actions (messenger, theme, avatar).
- Removed active-status pill, removed duplicate settings, removed post button.
- Single `+` create action lives in the mobile tab bar.

## Admin panel (full rebuild)
- Overview, Users, Moderation, Verification, Analytics, Finance, Payments, Settings.
- Live metrics from Firestore (`users`, `activity`, `chats`) with fallback.
- User search, ban/unban, force logout (writes `banned` / `forceLogoutAt`).
- Verification approve/reject queue with badge preview.
- Growth + engagement sparklines.
- Global admin roster editable in-app (persisted).

## Payments
- Add Bank / Visa / Mastercard / Wallet payout methods (nothing hardcoded).
- Withdraw flow with pending balance tracking.
- Transaction history with CSV export.

## Messenger
- Firestore realtime chat pane, unread counters, sent/received bubbles.

## Settings
- Nine populated sections: Account, Privacy, Security, Notifications,
  Appearance, Messenger, Monetization, Storage, Language.

## Security
- Session list + revoke, login logs, 2FA UI toggle.

## Notifications
- Toast system replacing every `alert()`. Push permission flow.

## Storage
- Cache clear, keys count, IndexedDB scaffold for outbox/background sync.

## Performance
- Lazy-loaded route modules; feed cache (60 s); preconnect to Firestore/Cloudinary.
- No global JS blob — smallest module is < 2 kB gzipped.

## Compatibility
- Legacy Firebase project (`meetwoyou-436a2`) preserved.
- Legacy Cloudinary (`dpgawb5sl` / `Meetwoyou`) preserved.
- Firestore collections unchanged: `users`, `chats`, `activity`, `calls`,
  `offerCands`, `ansCands`.
