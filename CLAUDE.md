# CLAUDE.md — attesto-website

Project context for Claude (and humans). Read before editing. This repo is the **marketing/landing
site for Attesto** — "the consent layer for AI agents."

## What this is

A single, **self-contained** static landing page (`index.html`) — inline CSS + vanilla JS, **zero
runtime dependencies**, no framework, no bundler, no build step. It renders identically opened
directly from `file://`.

- **Live:** https://openmobilehub.github.io/attesto-website/ (GitHub Pages, **GitHub Actions** source).
- **Deploy:** `.github/workflows/pages.yml` deploys on every push to `main`. Pages is already enabled
  (Settings → Pages → Source: GitHub Actions). A merge to `main` auto-redeploys.
- **Local dev:** open `index.html` in a browser, or `python3 -m http.server` and visit it.

## The product it markets (so the copy stays accurate)

Attesto: an AI agent proves a verifiable credential from the user's wallet **before** a consequential
action completes. **Identity leads; payments is one application.** An OpenMobileHub / OpenWallet
Foundation project, heading to the Global Digital Collaboration Conference (Sept 1–2) co-presented with
Multipaz. Two npm packages, both live at `0.1.0`: `@openmobilehub/attesto-gate` (the Gate —
`new Attesto()`, `attesto.mount(app)`, policy of `required()`/`optional()` credentials) and
`@openmobilehub/attesto-storefront`.

## Design

- **Direction:** bold & dark — teal-on-near-black. Palette tokens live in `index.html` `:root`
  (`--bg`, `--teal`, `--line`, etc.).
- **Hero:** the animated **"Watch the agent ask"** consent-handshake (Treatment A): a user prompt types
  out → an agent pauses → a 🔒 gate pulses → a 📱 wallet proves a credential → the action completes →
  loops (~8s). It **honors `prefers-reduced-motion`** (renders the final state statically, no motion).
- **Sections (top→bottom):** sticky nav → animated hero → problem band → how-it-works (3 cards) →
  quickstart (the gate policy as a ladder) → gate-any-credential → **Honest by design** (the trust
  table) → built-on-open-standards → for-developers → footer.
- **Full rationale:** `docs/2026-06-28-attesto-website-design.md` (a synced copy; the canonical version
  lives in the demo repo — see Links).

## Conventions — do not regress

- **Self-contained:** no external `<script src>` / `<link rel="stylesheet">` / `<img src="http…">` /
  `url(http…)`. Everything inline. Verify before committing:
  ```bash
  grep -ioE '<script[^>]+src=|<link[^>]+rel="stylesheet"|<img[^>]+src=|url\(\s*https?:' index.html | grep -i http | wc -l   # must be 0
  ```
- **No framework / bundler / build step.** A single hand-authored page is the right size — YAGNI on tooling.
- **Accessibility:** keep the `@media (prefers-reduced-motion: reduce)` guard and the responsive
  breakpoints (`@media (max-width:880px)` and `…520px`).
- **DCO:** sign off every commit with `git commit -s` (the OpenWallet Foundation org enforces it).
- **Workflow:** make changes on a branch and open a PR to `main`; merging auto-deploys via Pages. Don't
  push straight to `main` without sign-off.
- **Honesty rule (load-bearing):** the **"Honest by design"** trust table mirrors the SDK's
  `trust_level`. The site must **never** claim a stronger guarantee than the library actually provides.
  Canonical source: `docs/reference/trust-model.md` in https://github.com/openmobilehub/attesto. When the
  SDK's `trust_level` advances (e.g. to issuer-verified), update the table here — **the site follows the
  SDK, never the reverse.** Presence-only rails are labeled presence-only and are never presented as a
  real safety control.

## Current state (2026-06-29)

- The site is **LIVE and current**.
- **`openmobilehub/attesto` is now PUBLIC** — so the nav/hero **Docs** and **GitHub** links resolve for
  everyone, and the **npm** package links resolve (`0.1.0` shipped). *(The earlier caveat that those
  links 404'd for logged-out visitors is RESOLVED.)*
- Open ideas for "continue updating the website" (not yet done): an OG/social image; a docs/blog; a
  custom domain (`CNAME`); splitting `index.html` into `styles.css` + `app.js` if it grows.

## Links

- **Library (public):** https://github.com/openmobilehub/attesto
- **npm:** https://www.npmjs.com/package/@openmobilehub/attesto-gate ·
  https://www.npmjs.com/package/@openmobilehub/attesto-storefront
- **Reference demo + project dashboard (the cross-project hub, with `STATUS.md` + the design specs/plans):**
  https://github.com/openmobilehub/mcp-apps-shopping-demo
