# Design QA

## Evidence

- Reference: `C:\Users\ebube\Downloads\ChatGPT Image 15 Ağu 2026 13_58_38.png`
- Prototype capture: `design-qa-mobile.png`
- Viewport: 393 × 852 CSS pixels

## Comparison

- Preserved the reference direction: near-black editorial canvas, hot-orange accent system, green positive KPI treatment, compact uppercase labels, and a continuous vertical story.
- Adapted the reference's phone presentation to the existing portfolio product by using the verified portrait and case-study logo assets already present in the project. This keeps the mobile view a real scrollable page instead of a static mockup.
- The long-scroll sequence contains all seven requested beats: Hero, Kimim, Trendyol, Meta Ads, Shopify, Yetkinlikler, and İletişim / CTA.
- KPI examples are explicitly marked as design examples and are not presented as verified achievements.

## Functional checks

- `#mpp-hero` CTA anchors to `#mpp-trendyol`.
- Contact links use the existing email and LinkedIn destinations, with Instagram added as a direct social CTA.
- Existing desktop deck remains active at the default viewport; `#mobile-portfolio` is hidden above 768px.
- At 393px width, the page becomes vertically scrollable (`body.scrollHeight` 4928px) and all mobile asset targets receive source images.

## Result

final result: passed
