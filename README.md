# lavaforge.dev

Source for [lavaforge.dev](https://lavaforge.dev) — Geoff "Lava" Lavagnino's workshop: Runworthy, Agent Flight Rules, and the rest of the work.

Static site, no build step. One page of hand-written HTML and CSS in `public/`, zero JavaScript, deployed to Firebase Hosting.

## Layout

```
public/
  index.html          the site
  404.html            not-found page
  favicon.svg         primary icon (ember prompt on basalt)
  favicon.ico         32px fallback
  apple-touch-icon.png 180px icon for iOS
  og.png              1200x630 social card
  site.webmanifest    PWA manifest
  robots.txt
  sitemap.xml
firebase.json         hosting config + security headers
.firebaserc           Firebase project alias (lavalab-dev)
```

## Deploy

Prerequisite: `firebase login` as the account with access to the `lavalab-dev` project.

Preview on a temporary URL (safe — does not touch the live site):

```
firebase hosting:channel:deploy qa --project lavalab-dev --expires 7d
```

Publish to lavaforge.dev:

```
firebase deploy --only hosting --project lavalab-dev
```

## Notes

- The `public/index.html` copy is final and matches `design/copy-deck.md` in the handoff kit. Changing site text means changing the copy deck first.
- Security headers (a strict `Content-Security-Policy` with no script sources, HSTS, `nosniff`, frame denial) live in `firebase.json`.
- The social card `og.png` is rendered from `assets-src/og.html`.

Code is MIT (`LICENSE`). Site copy © Geoff Lavagnino.
