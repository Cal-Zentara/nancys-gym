# STATUS — SalviasApp (Nancy's Gym Tracker)

*Last updated: 2026-04-23*

## What this is
Single-file PWA workout tracker for Nancy (Salvia Lion). Push/Pull/Legs splits, per-set weight logging, rest timer, progress chart. Personal app — no login, no accounts.

## What's live
- Live at https://cal-zentara.github.io/nancys-gym/
- Nancy uses Android, Cal tests on iPhone — both PWA-installable
- v2 (post-audit) — all `/audit` flagged items resolved (13/20 → all fixed)

## What's broken / blocked
- Bodyweight exercises blocked — Hip Thrust, Walking Lunges need weight input, currently blocks completion without a number
- Offline fallback missing — if Chart.js CDN fails, progress chart breaks
- Stale in-progress sessions linger until user hits "Start over"

## What's next
1. Bodyweight exercise support (toggle or "BW" flag per exercise)
2. Auto-clear stale in-progress sessions after 24h
3. Offline fallback for Chart.js

## Key files
- `index.html` — entire app
- `manifest.json` — Android PWA manifest (pickleball icon)
- `CLAUDE.md` — full doc, data shape, design tokens

## Deploy notes
- GitHub: `Cal-Zentara/nancys-gym`
- Hosting: GitHub Pages
- Storage: localStorage key `nancyGym5`
- Local copy synced to `C:\Users\Aesth\Desktop\Nancys_Gym_App.html`
