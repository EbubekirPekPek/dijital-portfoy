# Design QA

## Evidence

- Reference: `C:\Users\ebube\Downloads\ChatGPT Image 15 Ağu 2026 13_58_38.png`
- Prototype capture: `design-qa-mobile-v2.png`
- Viewport: 393 × 852 CSS pixels

## Comparison

- Preserved the reference direction: near-black editorial canvas, hot-orange accent system, green positive KPI treatment, compact uppercase labels, and a continuous vertical story.
- Adapted the reference's phone presentation to the existing portfolio product by using the verified portrait and case-study logo assets already present in the project. This keeps the mobile view a real scrollable page instead of a static mockup.
- Expanded the sequence to nine data-rich beats: Hero, Kimim/Kariyer, Trendyol, Hepsiburada, Shopify, Meta Ads, Konsolide Özet, Yetkinlikler, and İletişim / CTA.
- Restored desktop-backed values: 10 career milestones, 6 Trendyol KPIs, 6 Hepsiburada KPIs, 6 Shopify KPIs, 8 Meta Ads KPIs, 6 consolidated KPIs, 12 certificates, and 26 tools.
- Replaced the prior placeholder KPI treatment with the existing portfolio data and period/source labels.
- Added sticky case-study stages, beat-based reveals, active timeline states, KPI count-up, data bars, image parallax, and a native reduced-motion/offline fallback.

## Functional checks

- `#mpp-hero` CTA anchors to `#mpp-trendyol`.
- Contact links expose the existing phone, email, web, location, LinkedIn, and Instagram destinations.
- Existing desktop deck remains active at the default viewport; `#mobile-portfolio` is hidden above 768px.
- At 393px width, the page becomes vertically scrollable (`body.scrollHeight` 13748px), all five mobile image targets receive source images, and no horizontal overflow is introduced.
- Browser console check returned no warnings or errors during the mobile and desktop passes.

## Result

final result: passed
