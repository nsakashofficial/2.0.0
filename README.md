# Meetwoyou documentation

- [README](../README.md)
- [Changelog](CHANGELOG.md)
- [Backend compatibility](BACKEND_COMPATIBILITY.md)
- [Deployment guide](DEPLOYMENT.md)
- [Bug report](BUGS.md)
- [Optimization report](OPTIMIZATION.md)
- [GitHub upload guide](GITHUB_UPLOAD.md)

## Architecture at a glance

```
index.html
 └─ js/main.js  (entry, chrome, router)
     ├─ utils/*         DOM, router, theme, i18n
     ├─ services/*      config, firebase, cloudinary, storage, auth, notifications
     ├─ components/*    navbar, tabbar, cards, modal, badge, buttons
     └─ modules/*       home, search, messenger, create, profile,
                        settings, payment, admin, creator, auth
```

## Data flow
```
UI module ──► service (firebase / cloudinary / storage)
      ▲              │
      │              ▼
    router      Firestore / Auth / Storage
```

## Adding a new route
```js
// js/main.js
route('/marketplace', () => import('./modules/marketplace.js'));
```
```js
// js/modules/marketplace.js
import { h } from '../utils/dom.js';
export default async function view({ params }) {
  return h('section', { class: 'mw-view' }, h('div', { class: 'mw-container' }, h('h1', {}, 'Marketplace')));
}
```

The router will lazy-load the module, show a skeleton, then swap in the view.
