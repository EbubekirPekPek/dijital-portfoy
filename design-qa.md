# Design QA

## Evidence

- Reference: `C:\Users\ebube\Downloads\ChatGPT Image 15 Ağu 2026 13_58_38.png`
- Prototype captures: `design-qa-mobile-v5-top.png`, `design-qa-mobile-v5-case.png`
- Viewport: 393 × 852 CSS pixels

## Comparison

- Preserved the reference direction: near-black editorial canvas, hot-orange accent system, green positive KPI treatment, compact uppercase labels, and a continuous vertical story.
- Adapted the reference's phone presentation to the existing portfolio product by using the verified portrait and case-study logo assets already present in the project. This keeps the mobile view a real scrollable page instead of a static mockup.
- Expanded the sequence to nine data-rich beats: Hero, Kimim/Kariyer, Trendyol, Hepsiburada, Shopify, Meta Ads, Konsolide Özet, Yetkinlikler, and İletişim / CTA.
- Restored desktop-backed values: 10 career milestones, 6 Trendyol KPIs, 6 Hepsiburada KPIs, 6 Shopify KPIs, 8 Meta Ads KPIs, 6 consolidated KPIs, 12 certificates, and 26 tools.
- Replaced the prior placeholder KPI treatment with the existing portfolio data and period/source labels.
- Added sticky case-study stages, beat-based reveals, active timeline states, KPI count-up, data bars, image parallax, and a self-contained reduced-motion/performance-safe scrub controller.
- Reworked mobile scrolling so `html/body` and the mobile root no longer create an intermediate `auto` scroll context; sticky stages now pin to the viewport in both directions.
- Replaced threshold-only case beat activation with a viewport reading-line sync, preventing fast swipes and upward reversals from leaving the last beat active or skipping state updates.
- Increased case beat dwell to `62svh` and clipped the case glow/media overflow; measured document, body, root, and case widths now match the 393px viewport content width.

## Functional checks

- `#mpp-hero` CTA anchors to `#mpp-trendyol`.
- Contact links expose the existing phone, email, web, location, LinkedIn, and Instagram destinations.
- Existing desktop deck remains active at the default viewport; `#mobile-portfolio` is hidden above 768px.
- At 393px width, the page becomes vertically scrollable (`body.scrollHeight` 14174px after the readability spacing update), all five mobile image targets receive source images, and no horizontal overflow is introduced (`body`, `html`, mobile root, and case widths all 378px content width).
- Sticky case stages were verified inside each active section range; the mobile root remains visible/clip-safe without creating a competing scroll container.
- Trendyol beat order was verified down and back up: `01 → 02 → 03 → 04` and `04 → 03 → 02 → 01`, with the stage pinned at `top: 0` while its section is active.
- Motion no longer depends on a third-party runtime bundle; scroll parallax runs through a passive scroll listener and a single `requestAnimationFrame` loop.
- Regression root causes fixed: `overflow:auto` on `html/body` was creating an intermediate scroll context, the mobile root had competing overflow behavior, and threshold-only beat observers could leave stale active content during fast/upward scroll.
- Browser console check returned no warnings or errors during the mobile and desktop passes.

## Result

final result: passed
