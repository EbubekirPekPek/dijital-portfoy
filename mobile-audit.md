# Mobil Portföy Baseline Audit

## Evidence

- Local prototype: `http://127.0.0.1:4173/index.html?audit=baseline`
- Mobile viewport: 393 × 852 CSS pixels
- Desktop viewport: 1280 × 720 CSS pixels
- Evidence captures: `audit-baseline-mobile-top.png`, `audit-baseline-trendyol.png`, `audit-baseline-meta.png`, `audit-baseline-desktop.png`

## Baseline health

1. Hero — healthy visual direction, but the mobile hero omits the full personal-name lockup and desktop role rotation; motion is reveal/parallax only.
2. Kimim / career — all 10 timeline milestones exist, but several descriptions are shorter than desktop and there is no relationship infographic connecting performance, strategy, commerce, and growth.
3. Trendyol — all six KPIs and four category shares are present; the full result narrative is shortened, the visual is only the marketplace logo, and there is no scroll-drawn data scene or hero KPI moment.
4. Hepsiburada — all six KPIs and four category shares are present; the desktop result narrative is missing and the case has the same visual grammar as Trendyol.
5. Shopify — all six KPIs and five category shares are present; the before/after store story and full result narrative are missing, leaving the D2C case as a repeated KPI template.
6. Meta Ads — the three account summaries and eight KPIs exist, but desktop-only `6.045 profil ziyareti`, the full budget/funnel narrative, and a creative-led visual scene are missing.
7. Consolidated summary — six KPIs exist, but active channels (including Ozon) and the desktop source/expansion narrative are missing.
8. Skills — 12 certificates exist, but mobile currently exposes 26 tools while the desktop markup lists 29 tool pills (including TradingView, Facebook, and TikTok); category hierarchy is flatter than desktop.
9. Contact — core contact links exist, but the source disclaimer and a stronger closing scene are missing.

## Interaction and motion findings

- Existing motion: reveal observer, timeline observer, sticky case stage, count-up, category bars, image parallax, and a native scrub loop.
- Missing motion: hero line-by-line typography, large transition type, KPI approach/retreat, scene-specific case motion, progressive funnel/creative reveal, cross-section continuity, and a persistent scroll progress cue.
- Existing sticky stages are functional after the prior overflow fix, but cases still read as repeated blocks rather than distinct scroll stories.
- No horizontal overflow was present at the baseline 393px viewport; desktop remains on the original deck engine.

## Limits

- The source portfolio contains logos and certification imagery, but no separate Trendyol/Meta/Shopify dashboard screenshots or time-series datasets beyond the visible KPI/category values. New infographics therefore use only existing values and semantic DOM/CSS primitives; no metrics are invented.

