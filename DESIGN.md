# Design

<!-- impeccable:design-schema 1 -->

## Visual World

"Highway sign / atlas" — a dark asphalt surface lit by the accent colors of official road signage (sign-green, amber, violet), with cartographic UI chrome (route-shield badges, monospace coordinates-style labels) standing in for literal national flags or generic SaaS gradients.

## Palette

Two themes share one token system, toggled via `[data-theme]` on `<html>` (persisted to `localStorage`, defaulting to dark):

**Dark** (default, unchanged from the original build) — restrained asphalt ground with three functional accents, each tied to one game mode:

- `--asphalt` `#0A1016` / `--panel` `#121B24` / `--panel2` `#17222C` / `--panel3` `#1D2A35` — surface layers, darkest to lightest.
- `--sign` `#0B6B4F` / `--sign-hi` `#0F8863` — "Finden" mode, the announcement banner.
- `--violet` `#7C6FE8` — "Benennen" mode.
- `--amber` `#F4B233` / `--amber-hi` `#FFC85C` — "Lernen" mode, hints, primary hover/focus accent.
- `--ink` `#F3F7F9` / `--muted` `#8CA0AF` / `--muted-soft` `#5E7383` — text hierarchy.

**Light** (`[data-theme="light"]`) — the same three-accent system reworked as pastels on a soft lavender-white ground, since pastel tone only reads on a light surface:

- `--asphalt` `#F6F4FB` / `--panel` `#FFFFFF` / `--panel2` `#F8F5FC` / `--panel3` `#EFE9FA`.
- `--sign` `#8FE0BE` (pastel mint), `--violet` `#CBBFF9` (pastel lavender), `--amber` `#FFD9A0` (pastel apricot).
- `--ink` `#241F35` / `--muted` `#786F92` / `--muted-soft` `#948AAE`.

Every place an accent sits *under* text (selected tabs, the route-sign banner, the solid button, hint/fact labels, focus rings) has its own ink/label token (`--tab-ink`, `--sign-ink`, `--solid-ink`/`--solid-bg`, `--amber-label`, `--focus-ring`) rather than a hardcoded white — pastel fills are light, so white-on-accent (which the dark theme can get away with) would be unreadable in light mode. `--focus-ring` in particular is a saturated caramel in light mode, not the pale `--amber-hi` fill, because a pastel focus outline on a white page would be nearly invisible for keyboard users.

Map state colors (`--map-solved`, `--map-missed`, `--map-label-ink`/`-outline`, `--map-bg-a`/`-b`), the mode-card selected-state tints and glows (`--mode-*-tint`, `--sign-glow`/`--violet-glow`/`--amber-glow`), the modal backdrop (`--backdrop`), and the ok/bad feedback text (`--feedback-ok`/`-bad`, distinct from the `--ok`/`--bad` map-fill tokens since text needs to stay dark-enough-to-read while fills can go full pastel) are all themed the same way.

Body background is a subtle graticule: two 1px hairline grids plus two low-opacity radial washes in the mode accents, over the base ground gradient — an atlas/map association at near-zero visual weight, themed via `--grid-line`/`--wash-a`/`--wash-b`.

The header shield and every route-shield badge keep one constant navy plate (`#173250→#0E2136`) in **both** themes — it's a fixed brand anchor, not a surface color, and reads fine against either ground.

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

## Theme Toggle

A small icon button (`#themeToggle`, first item in `.headerRight`, sun/moon SVGs swapped via `[data-theme]` CSS) flips `document.documentElement.dataset.theme` between `dark`/`light` and persists the choice to `localStorage` (`staatenkunde-theme`). No stored preference and no `prefers-color-scheme` check → defaults to dark, so the original look is unchanged for anyone who never touches the toggle. A tiny inline script in `<head>` applies the stored theme before first paint to avoid a flash of the wrong theme.
