# Product

<!-- impeccable:product-schema 1 -->

## Platform

web

## Users

Lucas (the maintainer) and the friends/family he shares the link with informally. It's a casual, self-directed learning game played solo in short sessions to memorize geography (states, cantons, provinces, countries) rather than a classroom or institutional tool.

## Product Purpose

Staatenkunde is a browser-based geography learning game. The player picks a region (USA, Switzerland, Germany, Austria, Canada, Australia, Italy, Sweden, Japan, Thailand, Europe, or the World) and one of three modes, then practices identifying its subdivisions/countries on an interactive SVG map until all are solved.

## Positioning

A single self-contained `index.html` with no backend, no build step, no accounts — open it and play immediately. Unlike quiz-app templates, the core mechanic is direct map interaction (click a shape / type a name / flip through fact cards), not multiple-choice trivia.

## Operating Context

- Static single-page site, deployed on Vercel with no framework/build config (`vercel.json` only).
- All game data (region metadata, per-subdivision facts) and SVG map geometry are inlined directly in `index.html`.
- Played casually on both desktop and mobile in a browser tab, short sessions (a few minutes to a full region).

## Capabilities and Constraints

- Twelve selectable regions, each a menu card in the region picker.
- Three game modes, switchable via header tabs or the mode picker in the start menu:
  - **Finden** — a subdivision name is announced; click the matching shape on the map.
  - **Benennen** — a shape is highlighted; type its name.
  - **Lernen** — flip through fact cards (location, shape/appearance, capital, notable fact, mnemonic) per subdivision.
- Per-session stats: solved count, elapsed time, streak, progress bar; a hint system (3 hints/session, 15s time penalty each); skip/solve/restart controls.
- A completion celebration (confetti canvas) when all subdivisions in a region are solved.
- Country map outlines are sourced from the `@svg-maps` project (CC-BY-4.0) plus user-provided SVGs for Switzerland/Germany; this attribution and the underlying map data must be preserved.
- Game mechanics, modes, scoring/hint logic, and region content are out of scope for this redesign — visual/UI only.
- No stated requirement to support future regions/features beyond what exists today.

## Brand Commitments

Name "Staatenkunde" is not binding — open to a rename or restyled wordmark if the redesign calls for it (no constraint was set).

## Evidence on Hand

Current implementation is the only evidence on hand: an existing dark "asphalt/road-sign" visual system (CSS custom properties for asphalt/panel/sign-green/amber/violet tones, Archivo + JetBrains Mono type), plus a country picker whose menu cards currently render each nation's flag colors as a background gradient. No user research, analytics, or external brand references exist beyond the live site and README.

## Product Principles

- Zero-friction play: no login, no loading state beyond opening the file — must stay instant.
- The map is the interface: mechanics stay map-first (click/type directly on the SVG), never buried behind menus.
- Casual, replayable, low-stakes: short sessions, forgiving hints, a small celebratory payoff on completion — not a formal test.
- Self-contained and portable: single-file architecture with no backend is a deliberate constraint to preserve, not incidental debt.
