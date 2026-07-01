# Deployment guide

## 1 — Local preview
```bash
python3 -m http.server 8080
open http://localhost:8080
```

## 2 — GitHub Pages
1. Create a new GitHub repository (e.g. `meetwoyou-web`).
2. Copy the contents of the ZIP (or this folder) into the repo root.
3. Commit and push to `main`.
4. **Settings → Pages → Deploy from branch → main / (root) → Save.**
5. GitHub gives you a URL like `https://<user>.github.io/meetwoyou-web/`.

> The router is hash-based (`#/route`) so no 404 rewrite rules are required.

## 3 — Firebase Hosting (recommended)
```bash
npm i -g firebase-tools
firebase login
firebase init hosting
# public directory: .
# single-page app: N (we use hash routes)
# service worker: N (we ship our own)
firebase deploy --only hosting
```

## 4 — Custom domain
Add a `CNAME` file at the repo root containing your domain and update the
DNS provider with the target CNAME provided by Pages / Firebase.

## 5 — Config overrides
Set values in `env.js` before publishing to override the defaults in
`js/services/config.js` — never commit real secrets to a public repo.

## 6 — Post-deploy checklist
- [ ] `/` loads the home feed within 2.5 s
- [ ] `#/auth` allows login/register
- [ ] `#/admin` shows the dashboard for admin emails
- [ ] `#/payments` allows adding a payout method
- [ ] Install prompt appears (Chrome desktop / Android)
- [ ] Offline: reload while disconnected → offline shell renders
