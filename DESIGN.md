# Design

<!-- impeccable:design-schema 1 -->

## Visual World

"Highway sign / atlas" — a dark asphalt surface lit by the accent colors of official road signage (sign-green, amber, violet), with cartographic UI chrome (route-shield badges, monospace coordinates-style labels) standing in for literal national flags or generic SaaS gradients.

## Palette

Restrained dark ground with three functional accents, each tied to one game mode:

- `--asphalt` `#0A1016` / `--panel` `#121B24` / `--panel2` `#17222C` / `--panel3` `#1D2A35` — surface layers, darkest to lightest.
- `--sign` `#0B6B4F` / `--sign-hi` `#0F8863` — "Finden" mode, the announcement banner.
- `--violet` `#7C6FE8` — "Benennen" mode.
- `--amber` `#F4B233` / `--amber-hi` `#FFC85C` — "Lernen" mode, hints, primary hover/focus accent.
- `--ink` `#F3F7F9` / `--muted` `#8CA0AF` / `--muted-soft` `#5E7383` — text hierarchy.

Body background is a subtle graticule: two 1px hairline grids (`rgba(255,255,255,.014)`, 72px pitch) plus two very low-opacity radial washes in sign-green and violet, over the base asphalt gradient — an atlas/map association at near-zero visual weight, never competing with content.

## Type

`Archivo` (sans, weight 500-700) for all UI text; `JetBrains Mono` for labels, stats, codes, and anything that reads as data (map labels, kickers, region badges, quality-bar-style eyebrows).

## Country / Region Identity

Countries are represented by their own **route-shield badge** — a small rounded-square plate in the header's navy gradient (`linear-gradient(160deg,#173250,#0E2136)`), bearing a 3-letter code in JetBrains Mono (USA, CHE, DEU, AUT, CAN, AUS, ITA, SWE, JPN, THA, EUR, WLD) — not national flag colors. This reuses the same visual device as the header's state-count shield, so every region reads as part of one system rather than a UN flag wall. On hover/focus the badge border and glow switch to amber, matching the app's single interactive accent.

The in-game completion celebration for Switzerland/Germany still renders those two national flags (`.flag-ch`, `.flag-de`) as a one-off reward animation on finishing that specific region — this is a deliberate, scoped exception (out of the menu, tied to an actual accomplishment) and was left untouched by the flag-color removal, which was scoped to the region-picker menu only.

## Components

- **Menu card** (`.menu-card`): panel2 surface, route-shield badge top-left, title + monospace subtitle, amber border/lift on hover, arrow affordance fades in. Grid: `repeat(auto-fill, minmax(216px,1fr))`, staggered fade/rise-in via `--i` custom property per card.
- **Mode card** (`.mode-card`): same shell, but its selected state borrows that mode's own accent (sign-green / violet / amber) rather than the shared amber — this is the app's own coding system, distinct from and unrelated to national flags.
- **Route sign** (`.sign`): the primary announcement banner, styled as an actual highway guide sign (green gradient, white rule, uppercase display type).
- **Buttons** (`.btn`, `.btn-solid`, `.btn-amber`): panel-toned by default; solid/amber variants for primary actions.

## Motion

Menu/mode cards fade + rise in on open (`cardIn`, 400-450ms, staggered ~35-45ms per card via `--i`). Hover lifts (`translateY(-2/-3px)`) plus shadow escalation. Respects `prefers-reduced-motion`.

## Layout

Both overlay grids (`.mode-grid`, `.menu-grid`) and their shared `.celebrate-inner` container are explicitly `width:100%` (with `box-sizing:border-box` on the container) so percentage/wrap sizing resolves against the actual viewport rather than shrink-to-fit — required because both sit inside `align-items:center` flex ancestors, which otherwise silently overflow narrow viewports.
