# Typography Ledger

## Current State

| Property | Value |
|----------|-------|
| Body font | Inter (400/500/600/700) |
| Data font | JetBrains Mono (400/700) |
| Reading font | Source Serif 4 (300/400) |
| Display font | Playfair Display (400/700) |
| Body size | `clamp(16px, 1.1vw + 14px, 18px)` |
| Size scale | 12 / 13 / 15 / 17 / 20 / 24 / 28 (6 steps, ~1.25 ratio) |
| Line height (body) | 1.5 |
| Line height (headings) | 1.1 |
| Content max-width | `min(90vw, 65ch)` |
| Dark bg | `#0a0e18` |
| Body text | `#d1d5e0` on `#0a0e18` (~13:1 contrast) |
| Secondary text | `#6b7280` on `#0a0e18` (~5.2:1 contrast) |
| Touch targets | `min-height: 44px` on buttons and range inputs |
| Padding (buttons) | `10px 16px` minimum |
| Responsive padding | `clamp(16px, 4vw, 32px)` on content container |

## Session Log

### 2026-04-06 — Typography review and overhaul

**Changes made:**
- Added Inter as body/UI font (was JetBrains Mono everywhere)
- JetBrains Mono now reserved for data readouts, stats, monospace contexts
- Consolidated 13 distinct font sizes down to 6-step scale (S.xs through S.xxl)
- Raised minimum font size from 8px to 12px (skill section 1.2)
- Added `clamp()` for responsive body font sizing
- Set `line-height: 1.5` on body (was unset)
- Increased button padding for 44px touch targets (skill section 1.8)
- Changed content max-width from `1000px` to `min(90vw, 65ch)` (skill section 1.1)
- Adjusted dark background from `#070b14` to `#0a0e18` (warmer, less pure-black)
- Bumped muted text from `#475569` to `#6b7280` for better contrast (~5.2:1 vs ~3.8:1)
