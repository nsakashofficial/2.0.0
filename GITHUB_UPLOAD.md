# GitHub upload guide

## Option A — Web upload (fastest)
1. Create a new repository on GitHub (public or private).
2. Click **Add file → Upload files**.
3. Drag the *contents* of the extracted ZIP (not the folder) into the drop zone.
4. Scroll down, commit with message "Initial Meetwoyou 2.0 release".
5. **Settings → Pages → Deploy from branch → main / (root)** and save.
6. Wait ~1 minute. Your site is live at `https://<user>.github.io/<repo>/`.

## Option B — CLI
```bash
unzip meetwoyou-2.0.0.zip -d meetwoyou
cd meetwoyou
git init
git remote add origin https://github.com/<you>/<repo>.git
git add .
git commit -m "Initial Meetwoyou 2.0 release"
git branch -M main
git push -u origin main
```

Then enable Pages as described in Option A step 5.

## Post-publish
- Verify `env.js` overrides if hosting under a different Firebase project.
- Confirm the service worker registered: DevTools → Application → Service Workers.
- Test PWA install (Chrome desktop shows install icon in the URL bar).
