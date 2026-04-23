# SalviasApp — Nancy's Gym Tracker

## Quick Nav — Read First

| I'm doing... | Read only... |
|---|---|
| Continuing work / resuming | `STATUS.md` |
| Fixing a bug | `STATUS.md` + Data Shape / Screens sections |
| Adding a feature | `STATUS.md` + Design + Screens |
| Understanding the whole project | This CLAUDE.md in full |

**Do not explore.** If the answer isn't in the files above, ask before searching.

---

## Dev Reference — Symbol Map / Schema / Gotchas

> **Scaffold only — populate on next touch.** When you next edit this project, fill in real line ranges and schema details. Remove the TODO notes as you go.

### Symbol Map

| Feature | File | Lines |
|---|---|---|
| TODO: populate on next touch — one row per major feature with `index.html` line ranges (home screen, workout, rest timer, progress chart, etc.) | | |

### Data Schema

TODO: populate on next touch. Existing doc above already shows the `nancyGym5` localStorage shape — consolidate here so mid-session edits only need to read this section.

### Known Gotchas

TODO: populate on next touch. Candidates from the doc below: `100dvh` iOS fix, `font-size: 16px` weight inputs (iOS zoom prevention), shake animation on empty weight, Chart.js `spanGaps: true` with time-tab grouping.

---

## What It Is

A single-file PWA workout tracker built for Nancy (also known as Salvia Lion). Push/Pull/Glutes & Legs sessions with per-set weight logging, rest timer, progress chart, and a progress screen. Personal app — no login, no accounts.

## Stack

| Layer | Tech |
|---|---|
| UI | Single HTML file — HTML + CSS + Vanilla JS |
| Fonts | Playfair Display (headlines), Nunito (body) — Google Fonts |
| Storage | localStorage key: `nancyGym5` |
| Charts | Chart.js 4.4.0 via CDN |
| Hosting | GitHub Pages — `https://cal-zentara.github.io/nancys-gym/` |
| Repo | `https://github.com/Cal-Zentara/nancys-gym` (Cal-Zentara account) |

## Files

| File | Purpose |
|---|---|
| `index.html` | Entire app — all screens, styles, and logic |
| `manifest.json` | Android PWA manifest — pickleball SVG icon, standalone display |
| `.impeccable.md` | Design context for audit/design skills |

## Screens

1. **Home** — 3 session cards (Push/Pull/Legs) + streak counter + "See My Progress" button. Shows "Continue" + "Start over" if session in progress.
2. **Workout** — Exercise cards with per-set weight inputs (16px, no iOS zoom) and set buttons. Shake animation if set tapped without weight. Progress bar at top. "How to do this" tip toggle per exercise.
3. **Rest Timer** — Full-screen circular countdown (60s). Pickleball-themed messages. Skip button.
4. **Complete** — Session complete screen + pickleball confetti animation (38 balls, canvas, auto-cleans). Saves to history.
5. **Progress** — Featured chart (3 lines: Push/Pull/Legs) + day/time filters + per-exercise session history with weight pills and delta indicators.

## Progress Chart

- Chart.js line chart, 3 datasets — teal (Push), amethyst (Pull), mauve (Legs)
- Time tab controls X-axis grouping:
  - **This Week** → daily dots (last 7 days)
  - **This Month** → weekly slots (Week 1–4)
  - **All Time** → monthly buckets
- Y-axis: average weight across all sets for that session type
- Glow plugin per dataset. Gradient fill under each line. `spanGaps: true`.

## Data Shape (localStorage)

```js
{
  history: [ { date: timestamp, dayKey: 'push'|'pull'|'legs', data: [[{done, weight},...]] } ],
  done_push: timestamp,
  done_pull: timestamp,
  done_legs: timestamp,
  push: [[{done, weight},...]]  // only present mid-session
}
```

## Design

- Background: `#080808`, cards `#111111`, `#0C0C0C`
- Tokens: `--amethyst: #A78BFA`, `--teal: #2DD4BF`, `--mauve: #C8A4C0`, `--green: #4ADE80`, `--red: #F87171`
- Push = teal, Pull = amethyst, Legs = mauve (consistent across cards, chart, progress tabs)
- Fonts: Playfair Display (headlines, italic for progress screen), Nunito (body, buttons)
- Pickleball: SVG ball in header (yellow-green `#C8E040` with holes), "Train hard. Play harder." subtitle

## Mobile / PWA

- `100dvh` — iOS Safari layout jump fixed
- `env(safe-area-inset-top/bottom)` — notch + home bar respected
- `font-size: 16px` on weight inputs — iOS zoom prevented
- `touch-action: manipulation` globally — Android 300ms delay removed
- `overscroll-behavior: none` — rubber-band scroll prevented
- Android: `manifest.json` linked, "Add to Home Screen" installs with pickleball icon
- iPhone: apple-mobile-web-app meta tags present

## Key Decisions

| Decision | Why |
|---|---|
| Single HTML file | Nancy receives it via link/WhatsApp — no install, no app store |
| localStorage only | No backend needed for a personal 1-user app |
| Force weight before set completes | Silent empty logs broke progress chart — shake animation instead |
| "Continue / Start over" on home | Partially done sessions used to linger forever |
| Chart grouped by time tab | Cal wanted Day/Week/Month on X-axis, not fixed monthly |
| Hosted on GitHub Pages | So updates push automatically without re-sending file |

## Audit Results (v2 — post-fixes)

Ran `/audit` — scored 13/20 before fixes. All flagged items resolved:
- `:focus-visible` added globally
- `border-left` side-stripes replaced with background tints (welcome card + tip box)
- Set button padding raised to `13px` (44px touch target)
- `#F87171` moved to `--red` token
- `transition: all` replaced with specific properties
- Weight inputs have `aria-label` (screen reader support)
- Workout screen uses `<h2>` / `<p>` semantic elements

## Status — 2026-04-18

- **LIVE** at `https://cal-zentara.github.io/nancys-gym/`
- Nancy uses Android, Cal tests on iPhone — both platforms covered
- File also synced to `C:\Users\Aesth\Desktop\Nancys_Gym_App.html` for local reference

## Next Steps (optional)

- Bodyweight exercise support — some exercises (Hip Thrust, Walking Lunges) don't need weight; currently blocks completion without a number
- Auto-clear stale in-progress sessions after 24h
- Offline fallback if Chart.js CDN fails
