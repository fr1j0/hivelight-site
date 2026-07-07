# Hive Light Landing Page — Design

**Date:** 2026-07-07
**Status:** Draft for review

## Goal

A single, polished marketing page at **hivelight.app** that serves as the canonical
link for promoting Hive Light. It must read as a real product to non-engineers
while giving engineers an immediate path to the source and the install command.

The GitHub repo remains the link for Show HN; this page is the canonical link for
Reddit, X, Product Hunt, the repo README, and anywhere else.

## Audience

Claude Code users — a mix of engineers and non-engineers. Everyone in the audience
already uses a terminal (Claude Code is a CLI), so `brew install` is an acceptable
install path for all of them.

## Scope

One static page. No docs site, no changelog page, no blog, no App Store link.
These can be added later if the product grows.

## Architecture

- **Stack:** hand-written `index.html` + `styles.css`. No framework, no build step.
  Minimal vanilla JS for copy-to-clipboard on the install command only.
- **Hosting:** GitHub Pages from this repo (public), custom domain `hivelight.app`,
  HTTPS enforced (required by the `.app` TLD; GitHub Pages provisions the cert).
- **Repo layout:**
  - `index.html`, `styles.css` at the root (GitHub Pages serves from root)
  - `assets/` — panel GIF, screenshots, app icon, OG image
  - `CNAME` — `hivelight.app`
- **DNS (manual step, owner):** register `hivelight.app`; A/AAAA records to GitHub
  Pages, `www` CNAME optional. Optionally register `hive-light.app` as a redirect.

## Page content (top to bottom)

1. **Hero** — app icon, name "Hive Light", tagline
   *"A native macOS menu-bar traffic light for your Claude Code sessions."*
   Panel GIF as the centerpiece. Two calls to action side by side:
   a copyable install block (`brew tap` + `brew install --cask`) and a
   "View on GitHub" button.
2. **Feature grid** — the differentiators, one card each: live session panel,
   context gauge, model chip, branch labels, subagent rows, notification detail,
   done-state, question detection, one-click terminal focus (iTerm / Terminal /
   Warp / VS Code).
3. **How it works** — short section: hook-driven (no polling daemon), pure
   Swift/SwiftUI (no Electron), works with any terminal.
4. **Trust** — signing status (Developer ID; notarization wording updates when the
   Apple gate clears), privacy: everything stays local, the app phones nothing home.
5. **Footer** — GitHub, license, credit link to loopwayz.com.

## Visual design

- Hive/hex/amber decorative language is available for backgrounds and accents
  (decorative surfaces only — any depiction of lamp states must mirror the real
  lamp geometry, per the established design rule).
- Light and dark mode via `prefers-color-scheme`.
- Wide-gamut-safe colors; the page must look right on both a MacBook display and
  a cheap external monitor.

## Metadata & measurement

- OpenGraph + Twitter-card tags with a purpose-built OG image (1200x630).
- Favicon derived from the app icon.
- Analytics: GoatCounter (free, privacy-friendly, no cookie banner needed).
  Plausible is the fallback if GoatCounter is unsatisfying.

## Success criteria

- Page loads fast: no framework, assets optimized (GIF poster/lazy-load if heavy).
- Link previews render correctly when pasted into X, Reddit, Slack, iMessage.
- Install command copies with one click and works verbatim.
- Reads as a product page to a non-engineer; source is one click away for an engineer.

## Open items (not blockers for building the page)

- Domain registration (owner action).
- Panel GIF and screenshots do not exist yet — the page ships with placeholder
  frames until the asset pass happens.
- Notarization wording depends on the Apple gate; ship with the current honest
  wording and update after.
