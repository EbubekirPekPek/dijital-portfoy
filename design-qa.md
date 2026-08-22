# Design QA — Trendyol mobile cover

## Source and implementation

- Source visual truth: `C:\Users\ebube\Downloads\ChatGPT Image 22 Ağu 2026 16_16_57.png` (941 × 1672 px).
- Secondary mood references: `C:\Users\ebube\Downloads\ChatGPT Image 22 Ağu 2026 16_19_14.png` and `C:\Users\ebube\Downloads\ChatGPT Image 22 Ağu 2026 16_19_07.png` (941 × 1672 px each).
- Implementation screenshot: `C:\Users\ebube\Documents\Codex\2026-08-22\proje-devi-r-notu-di-ji\outputs\trendyol-cover-final-390x844.png` (375 × 812 px capture, 390 × 844 CSS viewport).
- Comparison composite: `C:\Users\ebube\Documents\Codex\2026-08-22\proje-devi-r-notu-di-ji\outputs\trendyol-design-qa-comparison-final.png`.
- Density normalization: source was resized to 812 px high for the full-view comparison; implementation was captured at device scale 1 from the 390 × 844 CSS viewport. The browser capture excludes the 15 px scrollbar content width and 32 px browser surface height, so the rendered capture is 375 × 812 px.
- State: settled mobile Trendyol Page 1 cover, pinned at the cover reading position after the initial reveal; no downstream beat is active over the cover.

## Comparison

- Full view: black/charcoal poster field, orange technical grid, directional warm glow, right-edge luminous arc, editorial title stack, KPI card, three evidence blocks, and footer rhythm all match the supplied direction.
- Focused regions: title/lede, KPI logo + `₺786K` card, evidence row, and arc edge were checked against the source composite. The verified cover data is limited to `₺786K` total gross revenue and `6 dönem toplam`; no invented percentage, chart, order count, or secondary KPI appears in the cover.
- Real asset fidelity: the existing `assets/logos/trendyol.webp` asset is used directly. No reference screenshot is pasted into the page and no fake brand mark is generated.

## Findings

- No actionable P0, P1, or P2 findings remain.
- P3 follow-up only: the reference uses pictograms in the three evidence cards; the implementation uses restrained numbered evidence markers to keep the cover data-led without introducing substitute icon artwork.

## Comparison history

1. Initial local comparison identified a smaller-than-reference title scale and an arc that entered too centrally. The title was switched to a taller condensed treatment, the vertical rhythm was expanded, and the arc was moved to the right edge.
2. The enlarged pass exposed a 390 px right-edge title overflow. Font scale was reduced one step while preserving the condensed tracking.
3. Final 390 × 844 capture above was rechecked together with the source composite; title, KPI, evidence row, and footer remain inside the viewport with no horizontal overflow.

## Functional and regression checks

- Responsive cover matrix passed at 375 × 812, 390 × 844, and 430 × 932 CSS viewports. Each settled stage fills the viewport, title scroll width equals its client width, all cover blocks stay inside the viewport, and the logo reports a non-zero natural width.
- Trendyol cover data check passed: required copy is present; the cover contains `₺786K`, `6 DÖNEM`, `VERİ ODAKLI OKUMA`, and `GRAFİK GÖRÜNÜRLÜĞÜ`, with no unverified secondary KPI or percentage.
- Trendyol motion matrix passed at 0/25/50/75/100% section progress; beat activation advanced through `01 → 02 → 03 → 04` and the stage pinned at `top: 0` until the section handoff.
- Reverse scroll restored the cover and the first beat state.
- Hero initial, corridor transition, Career stage, all 12 career cards, and reverse scroll were rechecked after the cover change; no regression observed.
- Desktop regression passed at 1280 × 900: the existing desktop deck remains visible, `#mobile-portfolio` remains hidden, and document/client widths match.
- Browser console returned zero errors and zero warnings in the final local pass. The known out-of-scope certificate 404 was not modified.

## Final result

final result: passed

## Static cover refinement — 2026-08-22

- Source visual truth: `C:\Users\ebube\Downloads\ChatGPT Image 22 Ağu 2026 18_23_05.png` (941 × 1672 px).
- Implementation screenshot: `C:\Users\ebube\Documents\Codex\2026-08-22\proje-devi-r-notu-di-ji\outputs\trendyol-static-refine-local-390x844.png` (375 × 812 px capture, 390 × 844 CSS viewport).
- Comparison composite: `C:\Users\ebube\Documents\Codex\2026-08-22\proje-devi-r-notu-di-ji\outputs\trendyol-static-cover-qa-comparison.png`.
- State: settled mobile Trendyol static cover, cover stage pinned at the top; no downstream beat interaction was exercised in this quick QA.
- Fidelity surfaces checked: condensed title hierarchy and wrapping, right-edge arc placement, charcoal/orange tokens, KPI card proportions, real Trendyol logo asset, warm-ivory `₺786K`, evidence-card spacing, and required copy.
- Responsive evidence: 375 × 812, 390 × 844, and 430 × 932 all had zero horizontal overflow and all cover blocks inside the viewport; logo loaded and verified KPI copy remained present.
- Regression smoke: Hero visible, Career visible with 12 cards and active card 01; local console errors 0.
- Scope evidence: current diff contains only `index.html` Trendyol cover CSS plus this QA record; no GSAP, scroll-timeline, Hero, Career, or Page 2+ source changes.
- P3 follow-up only: source pictograms remain represented by restrained numbered markers because no matching local icon asset exists; no P0/P1/P2 issue remains.

final result: passed
