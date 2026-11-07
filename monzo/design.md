# Monzo — Design System (design.md)

> Source: https://monzo.com (UK challenger bank, marketing website)
> Captured: 2026-11-07
> Style keywords: light · bold · rounded · friendly fintech · Hot Coral accent · deep navy

**数据来源说明 / Provenance:** monzo.com 的首页由 JS 渲染，本次无法直接抓取其 CSS。下列数值综合自 Monzo 官方博客
（[Reimagining monzo.com](https://monzo.com/blog/reimagining-monzo-com-building-a-modular-high-fidelity-web-design-system-that-scales)）、
页面 meta（`theme-color: #112231`）以及多份第三方样式提取（refero.design、shadcn.io、webdesignhot.com）的交叉比对。
Values marked **(✓)** agree across all sources; **(≈)** are approximate / sources differ. Verify in DevTools before pixel-exact work.

---

## 1. Brand essence / 品牌调性

- **Confident, warm, plain-spoken.** Big bold headlines, short sentences, second person ("Your money, doing what it should").
- **Hot Coral is a moment of delight, not a UI state.** Monzo explicitly avoids using coral for errors/alerts, because red-ish reads as danger. Use it for brand objects (the card, illustrated tiles, wordmark, category links), not for every button.
- **Card silhouette as a motif.** Content blocks borrow the soft-rounded shape of the Monzo card: large radii, flat fills, no gradients, almost no shadows.
- **Full-bleed bands.** Pages alternate light (white / mint) and dark (navy) bands with hard edges.
- **Modular.** Pages are assembled from ~7 templates and reusable blocks: hero, feature highlight, UI spotlight, card carousel, link list, FAQ, footer.

## 2. Color / 颜色

### Brand
| Token | Hex | Use |
|---|---|---|
| `coral` (Hot Coral) | `#FF4F40` (✓) | Wordmark, card mockups, illustrated product tiles, large category links, highlight moments |
| `coral-hover` | `#FF6557` (≈) | Hover on coral surfaces |
| `coral-pressed` | `#E83B2D` (≈) | Pressed |
| `coral-ink` | `#C42D22` (≈) | Coral-coloured **small text** on white (Hot Coral is only ~3:1 on white — OK for ≥24px bold, not body) |

### Navy / Ink
| Token | Hex | Use |
|---|---|---|
| `ink` (Midnight Ink) | `#091723` (✓) | Primary text, primary CTA fill, dark bands, footer |
| `navy` (Deep Navy) | `#112231` (✓) | Cards layered on ink bands; browser `theme-color` |
| `slate` | `#3B4C54` (≈) | Secondary dark button / hover on dark |

### Neutrals & surfaces
| Token | Hex | Use |
|---|---|---|
| `white` | `#FFFFFF` | Default canvas, cards on mint |
| `mist` (Page Mist) | `#F2F8F3` | Alternate page canvas, active pill segment |
| `mint` (Soft Mint) | `#E3EBE4` | Feature cards, secondary button fill, dividers |
| `fog` | `#B5B9BD` | Disabled, inactive indicators, strong dividers on light |
| `steel` | `#6B747B` | Muted text, placeholders |
| `ash` | `#75817E` | Captions, meta text |
| `black` | `#000000` | Occasional headline text |

### Semantic (product-style, use sparingly on marketing pages)
| Token | Hex |
|---|---|
| `success` | `#1F8A4C` (≈) |
| `warning` | `#C77700` (≈) |
| `danger` | `#D23B2E` (≈) — keep visually distinct from Hot Coral; pair with an icon |

### Pairing rules
- Text on white/mint/mist → `ink`. Text on `ink`/`navy`/`coral` → `white`.
- Never put coral text on navy at small sizes; never place coral next to `danger` without icons/labels.
- Mostly 2 colours per band: one surface + `ink` or `white` text, with coral as the single accent.

```css
:root {
  --mz-coral: #ff4f40;  --mz-coral-hover: #ff6557;  --mz-coral-pressed: #e83b2d;  --mz-coral-ink: #c42d22;
  --mz-ink: #091723;    --mz-navy: #112231;         --mz-slate: #3b4c54;
  --mz-white: #ffffff;  --mz-mist: #f2f8f3;         --mz-mint: #e3ebe4;
  --mz-fog: #b5b9bd;    --mz-steel: #6b747b;        --mz-ash: #75817e;
  --mz-success: #1f8a4c; --mz-warning: #c77700;     --mz-danger: #d23b2e;
}
```

## 3. Typography / 字体

Monzo uses proprietary families:
- **MonzoSansDisplay** — headlines, big numbers, category links. Weights 600 / 700 / 800. Fallback: `"Manrope", "Inter", system-ui, sans-serif`.
- **MonzoSansText** — body, UI, buttons. Weights 400 / 600 / 700. Fallback: `"Inter", "DM Sans", system-ui, sans-serif`.

Headlines are heavy (700–800) with tight line-height (1.0–1.2). Body is generous (1.4–1.5). Money amounts use tabular numerals (`font-variant-numeric: tabular-nums`).

| Role | Family | Size (desktop → mobile) | Weight | Line height | Tracking |
|---|---|---|---|---|---|
| display | Display | 61px → 40px | 800 | 1.0 | -0.01em |
| h1 | Display | 49px → 36px | 800 | 1.1 | -0.01em |
| h2 | Display | 39–44px → 32px | 700 | 1.2 | normal |
| h3 | Display | 31px → 24px | 700 | 1.2 | normal |
| h4 / menu label | Display | 25px → 20px | 700 | 1.3 | normal |
| body-lg | Text | 20px | 400 | 1.4 | normal |
| body | Text | 16px | 400 | 1.5 | normal |
| button / label | Text | 16px | 600 | 1.0 | normal |
| caption | Text | 13px | 400–600 | 1.38 | normal |

Scale ratio ≈ 1.25 (16 → 20 → 25 → 31 → 39 → 49 → 61).

```css
--mz-font-display: "MonzoSansDisplay", "Manrope", "Inter", system-ui, sans-serif;
--mz-font-text: "MonzoSansText", "Inter", "DM Sans", system-ui, sans-serif;
```

## 4. Spacing & layout / 间距与布局

- **Base unit:** 8px (4px allowed for fine adjustments).
- **Scale:** `4, 8, 12, 16, 24, 32, 48, 64, 80, 128`.
- **Content max width:** ~1200px (≈); prose ≤ 720px.
- **Grid:** 12 columns desktop, 24px gutters; 4 columns mobile, 16px gutters, 16–20px side padding.
- **Section padding:** 64–80px vertical desktop, 48px mobile.
- **Card padding:** 32px desktop, 24px mobile. **Element gap:** 24px.
- **Header:** sticky, 64–80px tall.
- **Breakpoints (suggested):** 600 / 900 / 1200 / 1440px.

## 5. Shape / 圆角

| Token | Value | Use |
|---|---|---|
| `radius-xs` | 4px | Badges, tags, FSCS logo plate |
| `radius-sm` | 8px | Small inputs, tooltips |
| `radius-md` | 24px | Product tiles, feature cards, text inputs (≈) |
| `radius-lg` | 32px | Containers, menu panels |
| `radius-xl` | 64px | Hero / carousel cards, large dark card |
| `radius-pill` | 500px | **All** buttons, nav pills, segment toggles, search bar |

The large radius on big cards is a signature — don't shrink it to 12–16px.

## 6. Elevation / 阴影

Monzo's marketing UI is essentially **flat**: separation comes from colour bands and surface contrast, not shadows.
- `shadow-none` — default for cards and tiles.
- `shadow-float`: `0 0 10px rgba(0,0,0,0.10)` — only floating elements (bottom search bar, sticky menus).
- Optional `shadow-overlay`: `0 12px 32px rgba(9,23,35,0.18)` for modals.

## 7. Motion / 动效

Subtle, guiding attention, never showy.
- Durations: 150ms (hover), 240ms (state), 320–400ms (carousel / reveal).
- Easing: `cubic-bezier(0.2, 0, 0, 1)`.
- Respect `prefers-reduced-motion`: disable parallax, auto-advancing carousels, number count-ups.

## 8. Components / 组件

### Buttons (all pill-shaped, 500px radius)
| Variant | Fill | Text | Border | Notes |
|---|---|---|---|---|
| Primary | `ink` | white | — | "Sign up", main CTA. Hover → `slate` |
| Inverse | white | `ink` | — | On photos / dark bands |
| Secondary | `mint` | `ink` | — | Lower emphasis |
| Outline | transparent | `ink` | 1–1.5px `ink` | Hover: fill `ink`, text white |
| Brand (rare) | `coral` | white | — | Only for a single featured moment |

Size: height 48–52px, padding 12–16px × 24–32px, MonzoSansText 16/600. Small: 40px, 8×16px.

### Navigation
- Sticky top bar, white (or transparent over hero), coral wordmark left, **Personal / Business segment toggle** (pill; active segment `mist` fill, 16/600), primary "Sign up" CTA right. 1px `mint` bottom border appears on scroll.
- Mobile: full-screen menu with large **category link list** — MonzoSansDisplay 32–36px/700 in coral, 60–72px rows, 1px `mint` dividers.

### Cards
- **Hero / carousel card:** radius 64px, full-bleed photo or coral/navy fill, white display text 44–61px/700 overlay, CTA button, dot indicators (8px white dots, inactive 40% opacity), 40px circular arrow controls with 1.5px stroke.
- **Product tile:** coral or mint fill, radius 24px, 32px padding, illustration/card render + short headline + link.
- **Dark feature card:** `navy` on an `ink` band, radius 32–64px, white text.
- No borders and no shadows on cards by default.

### Inputs
- Height 48–56px, radius 24px (pill-ish) or 8px for dense forms, 1px `fog` border, placeholder `steel`, focus: 2px `ink` (or coral accent) border + 3px ring.

### Badges
- Trust badges (e.g. FSCS, awards): white plate, 4px radius, small text 11–13px.
- Circular award badge ~100–120px on hero corner.

### Lists & FAQ
- Rows with 1px `mint` dividers, 20–24px vertical padding, plus/chevron icon right, question in Text 20/600.

### Footer
- `ink` background, white/`fog` links in Text 16, multi-column link groups, legal small print 13px in `fog`.

## 9. Imagery & iconography / 图像与图标

- Real-life lifestyle photography, warm and candid; product shots of the coral card and app screens.
- Illustrations are flat, chunky, rounded, using coral + navy + mint.
- Icons: simple rounded line icons, 24px, 1.5–2px stroke, `ink` or white.

## 10. Voice & tone / 文案

- Friendly, direct, jargon-free; short headlines ("Banking made easy"), benefit-led subcopy.
- Sentence case everywhere, including buttons ("Sign up", "Find out more").
- Address the reader as "you"; numbers are concrete ("Get paid up to a day early").

## 11. Accessibility / 无障碍

- Primary text `ink` on white ≈ 18:1 (AAA). Coral on white ≈ 3.1:1 → large/bold text only; use `coral-ink` for small coral text.
- Focus ring: 3px `ink` ring with 2px offset (white ring on dark bands).
- Minimum touch target 44×44px.
- Don't convey state by coral alone.

## 12. Do / Don't

**Do**
- Use big, heavy headlines with lots of whitespace.
- Keep buttons pills; keep big cards very round (24–64px).
- Alternate white/mint and navy bands; let coral appear once or twice per screen.

**Don't**
- Don't use gradients, heavy shadows, or thin/light headline weights.
- Don't use coral for errors or as the default button colour everywhere.
- Don't use small corner radii (≤12px) on marketing cards.

## 13. Quick prompt for AI tools / AI 提示词

> Build in the style of Monzo: white and pale-mint (#F2F8F3 / #E3EBE4) canvas alternating with deep navy (#091723) bands; Hot Coral (#FF4F40) as a sparing brand accent for hero objects and big links; heavy rounded sans headlines (MonzoSansDisplay → Manrope/Inter 800, tight line-height), Inter body 16–20px; pill buttons (radius 500px) — primary navy with white text, secondary mint; cards with very large radii (24–64px), flat, no shadows; 8px spacing grid, 1200px max width, generous 64–80px section padding; friendly, direct sentence-case copy.

## Sources
- Monzo blog: [Reimagining monzo.com](https://monzo.com/blog/reimagining-monzo-com-building-a-modular-high-fidelity-web-design-system-that-scales)
- [Refero style extraction](https://styles.refero.design/style/e8a1d114-6924-4f03-acd2-996dd30f15a6)
- [shadcn.io Monzo DESIGN.md](https://www.shadcn.io/design/monzo)
- [webdesignhot Monzo design.md](https://www.webdesignhot.com/design.md/monzo/)
