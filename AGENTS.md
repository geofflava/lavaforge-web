# AGENTS.md — lavaforge-web

Personal site of Geoff "Lava" Lavagnino (lavaforge.dev). Hand-written static HTML/CSS on
Firebase Hosting. There is no framework, no build step, and no JavaScript — that is a
product decision (the site of an agent-safety product provably ships zero script), not
an omission.

Pages: `public/index.html`, `public/receipts/001.html`,
`public/receipts/001-research-cascade.html`, `public/404.html`. Each page carries its own
inline `<style>`; a shared rule must be added to every page it applies to.

## Hard rules

- Zero JavaScript. CSP is `default-src 'none'` with inline styles. Never add `<script>`,
  external fonts, CDN links, images from other hosts, or new CSP directives.
- Design tokens in `:root` are locked (basalt / ink / ash / ember / go / wip). Button ink
  is `#1a0d05`. Ember stays scarce — it is the accent, not a theme.
- Copy is pre-approved and arrives verbatim in the work package. Do not write, rewrite,
  or "improve" prose, titles, or metadata. Banned everywhere: bare "agent readiness",
  "AOSF", "Senior", "built in public" as a written claim. Headings are sentence case.
- Motion is opt-in. Every `transform`/`animation` lives inside
  `@media (prefers-reduced-motion: no-preference)` or has a `reduce` fallback that lands
  on the fully visible end state. Never put `opacity: 0` in base styles. Animate
  compositor properties only (`transform`, `opacity`); name transitioned properties,
  never `all`. Scroll-driven rules additionally sit inside
  `@supports (animation-timeline: view())`.
- Lighthouse (mobile) stays 100/100/100/100 — the known exception is index a11y 95 from a
  pre-existing nav target-size finding. Contrast stays AA (≥4.5:1 text). CLS stays 0.

## Verify loop (run before reporting, every task)

1. Serve `public/` (e.g. `python -m http.server 8080`) and check changed pages at 1440px
   and 375px viewports.
2. Hover and focus every link, button, card, and row you touched; Tab from the top (skip
   link must be first).
3. Re-run with reduced motion emulated: no transforms fire, nothing is hidden or stuck
   mid-animation.
4. Console: zero errors. Network panel: zero external requests.

## Git

- Commit locally with clear messages, one logical change per commit. Never push, never
  deploy, never touch remotes or `firebase.json` — a human gates both.
- Don't touch `favicon.*`, `og.png`, `robots.txt`, `sitemap.xml`, or `assets-src/` unless
  the package says so.
- If the package conflicts with what you find in the files, stop and report the conflict
  instead of improvising.
