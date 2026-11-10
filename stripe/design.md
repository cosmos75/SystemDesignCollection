# Stripe — Design System (design.md)

> Source: https://stripe.com (payments infrastructure, marketing website)
> Captured: 2026-11-10
> Style keywords: light · editorial · airy · precise · light-weight Söhne · indigo accent · blue-tinted shadows · gradient hero

**数据来源说明 / Provenance:** stripe.com 在本环境中无法直接抓取（代理拦截），下列数值综合自多份第三方样式提取的交叉比对：
designlang（2026-05 从线上 CSS 抽取的 token）、refero.design、webdesignhot.com。
注意：Stripe 在 2025 年前后把品牌紫从经典的 `#635BFF` 调整为更深更饱和的 `#533AFD`，旧值目前主要剩在 focus ring 等少数地方。
Values marked **(✓)** agree across sources; **(≈)** are approximate / sources differ. Verify in DevTools before pixel-exact work.

---

## 1. Brand essence / 品牌调性

- **Quiet confidence, engineered precision.** The UI looks like well-set editorial typography: thin (300) Söhne headlines, tight tracking, lots of white space, almost no bold.
- **One accent colour.** Indigo `#533AFD` is the *only* interactive colour (CTAs, links, focus, selected states). Everything else is navy ink and cool blue-greys.
- **Colour lives in the hero, not the UI.** The famous animated mesh gradient (violet → magenta → orange/yellow, now also a blue radial "glow") gives the brand energy; chrome around it stays calm and neutral.
- **Product as illustration.** Real UI fragments (payment forms, dashboards, charts, code) floating on white cards with soft blue-tinted shadows are the main visuals.
- **Small radii, layered depth.** 4–8px corners, hairline borders, and multi-layer cool shadows — crisp rather than soft and bubbly.

## 2. Color / 颜色

### Brand (indigo)
| Token | Hex | Use |
|---|---|---|
| `indigo` (primary) | `#533AFD` (✓) | Primary CTA fill, links, icon strokes, selected nav, focus |
| `indigo-hover` | `#4434D4` / `#4032C8` (≈) | Hover / pressed on primary |
| `indigo-deep` | `#2E2B8C` | Icon hover, deep emphasis |
| `indigo-400` | `#665EFD` | Range/inputs highlight, illustrations |
| `indigo-legacy` | `#635BFF` | Classic "Blurple" — still used as focus ring (≈) |
| `lavender` | `#B9B9F9` (✓) | Ghost button border, focus ring on dark |
| `lilac` | `#D6D9FC` | Soft purple borders / dividers |
| `periwinkle` | `#E8E9FF` (≈ `#E2E4FF`) | Tinted card / tag / info backgrounds |
| `indigo-50` | `#F5F5FF` | Faintest brand wash |

### Ink & text (navy, never pure black)
| Token | Hex | Use |
|---|---|---|
| `ink` | `#061B31` (✓) | Headings, body, nav, strong text |
| `ink-label` | `#273951` | Form labels |
| `steel` | `#50617A` (✓) | Supporting copy, footer links |
| `slate` | `#64748D` (✓) | Subdued text, captions |
| `quiet` | `#7D8BA4` | Placeholders |
| `disabled` | `#95A4BA` | Inactive / disabled |

### Surfaces & borders
| Token | Hex | Use |
|---|---|---|
| `white` | `#FFFFFF` | Canvas, cards |
| `mist` | `#F8FAFD` (✓) | Alternate section band, footer |
| `soft` | `#F6F9FC` | Soft surface (legacy Stripe grey) |
| `frost` | `#E5EDF5` (✓) | Default border / divider, hover bg, quiet card fill |
| `border-strong` | `#D4DEE9` | Stronger neutral border, input border (at 75% alpha) |
| `border-heavy` | `#BAC8DA` | Heaviest neutral border |
| `night` | `#0D1738` / `#1C1E54` (≈) | Dark bands (developer / enterprise sections) |

### Accents (decorative only — gradients, illustrations, product tags; never buttons)
| Token | Hex |
|---|---|
| `orange` | `#FF6118` (tint `#FFD8C6`, peach `#FFE0D1`) |
| `ruby` | `#EA2261` |
| `magenta` | `#F44BCC` / `#F96BEE` |
| `lemon` | `#E8A30B` |
| `blue` | `#7389FF` / `#486FFD` |
| `green` | `#00D66F` |

### Semantic
| Token | Hex |
|---|---|
| `success` | `#00B261` / `#15BE53`; text `#108C3D` (≈) |
| `warning` | `#9B6829` (≈) |
| `danger` | `#D8351E` (≈; some sources use ruby `#EA2261`) |
| `info` | `#2874AD` |

### Gradients
```css
/* signature spectrum (hero mesh, highlight strokes) */
--st-gradient-spectrum: linear-gradient(90deg, #7232F1 3%, #FB76FA 50%, #FFCF5E 100%);
/* brand glow behind product shots */
--st-gradient-glow: radial-gradient(50% 50% at 50% 50%, rgba(83,58,253,.8) 62.5%, rgba(83,58,253,0) 100%);
/* blue hero wash fading to mist */
--st-gradient-hero: radial-gradient(103% 103% at 50% 103%, #486FFD 0%, #F8FAFD 100%);
```

### Pairing rules
- Text on white/mist → `ink` (headings) / `steel` (supporting). Text on `night` → white, muted `rgba(255,255,255,.7)`.
- Indigo is reserved for things you can click. Don't use it for large fills.
- Accent colours (orange, ruby, magenta, lemon) only in gradients and illustrations.

```css
:root {
  --st-indigo: #533afd;   --st-indigo-hover: #4434d4; --st-indigo-deep: #2e2b8c; --st-indigo-legacy: #635bff;
  --st-lavender: #b9b9f9; --st-lilac: #d6d9fc;        --st-periwinkle: #e8e9ff;
  --st-ink: #061b31;      --st-ink-label: #273951;    --st-steel: #50617a; --st-slate: #64748d;
  --st-quiet: #7d8ba4;    --st-disabled: #95a4ba;
  --st-white: #ffffff;    --st-mist: #f8fafd;         --st-frost: #e5edf5; --st-border: #d4dee9; --st-night: #0d1738;
  --st-orange: #ff6118;   --st-ruby: #ea2261;         --st-magenta: #f44bcc; --st-lemon: #e8a30b;
  --st-success: #00b261;  --st-warning: #9b6829;      --st-danger: #d8351e;  --st-info: #2874ad;
}
```

## 3. Typography / 字体

- **Söhne** (Klim Type Foundry), served as `sohne-var` (variable). Single family for everything. Fallback: `"Inter Tight", "Inter", "SF Pro Display", -apple-system, system-ui, sans-serif`.
- **Mono:** `SourceCodePro` → `SFMono-Regular, ui-monospace, Menlo, monospace` (code samples).
- **Weights:** **300 for headings and body** (signature), 400 for buttons / nav / links / labels, 500 rare. Never 600–700 on headlines.
- **OpenType:** `font-feature-settings: "ss01"` on Söhne text; `"tnum"` on figures, prices, tables.
- **Tracking tightens with size:** ≈ -0.01em ≤26px, -0.02em at 32–48px, -0.025em at 56px+.

| Role | Size (desktop → mobile) | Weight | Line height | Tracking |
|---|---|---|---|---|
| display | 56px → 40px | 300 | 1.03 | -1.4px |
| h1 | 48px → 36px | 300 | 1.10–1.15 | -0.96px |
| h2 | 32px → 28px | 300 | 1.10 | -0.64px |
| h3-lg | 26px | 300 | 1.12 | -0.26px |
| h3 | 22px | 300 | 1.10 | -0.22px |
| lead | 20px | 300 | 1.40 | -0.2px |
| body-lg | 18px | 300 | 1.40 | normal |
| body | 16px | 300 (400 for emphasis) | 1.40–1.55 | normal |
| button / nav | 14–16px | 400 | 1.0 | normal |
| caption | 12–13px | 300–400 | 1.33–1.45 | normal |
| micro / badge | 10px | 300 | 1.15–1.5 | 0.1px |
| code | 12–14px | 500 | 1.6–2.0 | normal |

A common hero pattern: headline in `ink` where the first phrase is ink and the rest is `slate`/`steel` (two-tone headline), all at weight 300.

```css
--st-font: "sohne-var", "Inter Tight", "Inter", "SF Pro Display", -apple-system, system-ui, sans-serif;
--st-font-mono: "SourceCodePro", "SFMono-Regular", ui-monospace, Menlo, monospace;
body { font-family: var(--st-font); font-weight: 300; font-feature-settings: "ss01"; color: var(--st-ink); }
```

## 4. Spacing & layout / 间距与布局

- **Base unit:** 8px (2/4px steps for fine tuning).
- **Scale:** `4, 8, 12, 16, 24, 32, 40, 48, 64, 80, 96, 128`.
- **Content max width:** ~1264px (≈; sources give 1080–1320). Prose ≤ 720px.
- **Grid:** 12 columns, 16–24px gutters; side margin 16px on mobile. Stripe's layout is famous for visible vertical **guide lines** (hairline 1px dashed/solid `frost` column lines) in some sections.
- **Section padding:** 96px vertical desktop (✓), 64px mobile.
- **Card padding:** 24–32px. **Stack gaps:** 16 / 48 / 64px.
- **Header:** ~72–76px tall.
- **Breakpoints (suggested):** 640 / 1024 / 1280 / 1536px.

## 5. Shape / 圆角

| Token | Value | Use |
|---|---|---|
| `radius-xs` | 2px | Small buttons, chips |
| `radius-sm` | 4px (✓) | **Buttons, inputs**, badges, switches |
| `radius-md` | 6px | Cards, dropdowns, dark-section inner cards |
| `radius-lg` | 8px | Larger cards, product UI frames |
| `radius-xl` | 16px | Big media / screenshot containers (rare) |
| `radius-pill` | 9999px | Avatars, a few status badges only |

Keep it crisp: no pill buttons, nothing ≥12px on buttons or regular cards.

## 6. Elevation / 阴影

Shadows are **blue-tinted and multi-layered** (never neutral grey/black). Used on product-UI cards floating over the page; plain content cards often have none.

```css
--st-shadow-xs: 0 2px 10px rgba(0,55,112,.06), 0 1px 4px rgba(0,59,137,.04);
--st-shadow-sm: 0 5px 14px rgba(0,55,112,.08), 0 2px 8px rgba(0,59,137,.05);
--st-shadow-md: 0 6px 22px rgba(0,55,112,.10), 0 4px 8px rgba(0,59,137,.02);
--st-shadow-lg: 0 15px 40px -2px rgba(0,55,112,.10), 0 5px 20px -2px rgba(0,59,137,.04);
--st-shadow-xl: 0 20px 80px -16px rgba(0,55,112,.14), 0 10px 60px -16px rgba(0,59,137,.06);
/* classic Stripe "elevated" card & nav dropdown */
--st-shadow-card: 0 30px 45px -30px rgba(50,50,93,.25), 0 18px 36px -18px rgba(0,0,0,.10);
--st-shadow-nav:  0 30px 60px -10px rgba(50,50,93,.25), 0 30px 60px -50px rgba(0,0,0,.10);
```

## 7. Motion / 动效

Smooth, responsive, often scroll-linked (sections reveal and product UIs "assemble" as you scroll; the hero gradient animates continuously on WebGL).
- Durations: 100ms (xs), 150–200ms (hover), 240–300ms (nav, state), 500ms (reveal), 800ms+ (hero / showcase).
- Easing: `cubic-bezier(0.25, 1, 0.5, 1)` (main ease-out); nav `cubic-bezier(0.45, 0.05, 0.55, 0.95)`; standard `cubic-bezier(0.4, 0, 0.2, 1)`.
- Button hover: colour shift (+ optional `translateY(-1px)`); arrow icon in link/CTA nudges right ~3px.
- Card hover: shadow `md` → `lg`/`card`.
- Mega-menu dropdown: morphing panel that resizes/slides between menu items (~240ms).
- `prefers-reduced-motion`: stop the gradient animation, keep opacity-only transitions.

## 8. Components / 组件

### Buttons (radius 4px)
| Variant | Fill | Text | Border | Notes |
|---|---|---|---|---|
| Primary | `indigo` | white | — | "Get started", main CTA. Hover `indigo-hover` |
| Ghost / secondary | transparent or `rgba(255,255,255,.65)` | `indigo` | 1px `lavender` | Paired next to primary ("Contact sales"). Hover fill `rgba(83,58,253,.05)` |
| Tertiary outline | transparent | `indigo` | 1px `lilac` | Smaller, lower emphasis |
| Text link | transparent | `indigo` | — | Trailing chevron/arrow "›" that slides on hover |
| On dark | white | `ink` | — | In `night` bands |

Size: height ~40–48px, padding 8–12px × 16–24px, Söhne 14–16px / 400. Hero CTA pair: primary + ghost, 8–16px gap.

### Navigation
- Sticky white header (~72–76px), optionally `rgba(255,255,255,.7)` + `backdrop-filter: blur(12px)`; 1px `frost` bottom border on scroll.
- Wordmark left, menu items (Products / Solutions / Developers / Resources / Pricing) 14–16px/400 `ink`; "Sign in" text link + primary "Contact sales"/"Get started" on the right.
- **Mega-menu:** white panel, radius 6–8px, `shadow-nav`, multi-column with small coloured product icons + title (400) + one-line description (`slate`).

### Cards
- **Product UI card:** white, radius 6–8px, `shadow-card` or `shadow-md`, contains real UI (payment form, charts).
- **Feature card / tile:** white or `mist`, no shadow, 1px `frost` border optional, small eyebrow label (indigo or accent colour, 14px/400), 22–32px/300 headline, `steel` body, 24–32px padding.
- **Dark section card:** on `night`, `rgba(255,255,255,.1)` 1px border, radius 6px, white text.

### Stats
- Big numbers 48–56px / 300 with `tnum`, label below in `slate` 14–16px. No container.

### Inputs
- Height 40–48px, radius 4px, 1px `frost`/`border-strong` border, label `ink-label` 14px/400 with 8px gap, placeholder `quiet`.
- Focus: `indigo` border + 3–4px `rgba(83,58,253,.2)` ring. Error: `danger` border + text.

### Code blocks
- `night` or very dark navy background, radius 6–8px, SourceCodePro 13–14px, syntax colours from the accent palette; tab strip on top for languages.

### Badges / tags
- 10–12px, radius 4px, tinted background (e.g. success `rgba(21,190,83,.2)` with `#108C3D` text; info `periwinkle` with indigo text).

### Footer
- `mist` or white, `steel` links 14–16px, multi-column groups, small print 12–13px in `slate`, country/language selector.

## 9. Imagery & iconography / 图像与图标

- **Hero gradient:** animated, flowing mesh of violet, magenta, orange, yellow and blue, often cut at an angle (skewed band ~ -6°) behind the hero.
- **Product screenshots** recreated as crisp vector UI, floating with shadows, sometimes overlapping devices.
- Customer logos in a monochrome logo rail.
- Icons: small (16–24px), geometric, 1.5px stroke or duotone, using `indigo` or per-product accent colours.
- Occasional 3D/isometric illustrations; no lifestyle stock photography in core pages.

## 10. Voice & tone / 文案

- Calm, authoritative, outcome-led: "Financial infrastructure to grow your revenue."
- Sentence case for headlines and buttons ("Get started", "Contact sales", "Start with Payments").
- Concrete numbers as proof ("135+ currencies", "99.999% uptime").
- Speaks to both business and developers — product names plus plain-English benefit lines; developer pages show code early.

## 11. Accessibility / 无障碍

- `ink` on white ≈ 17:1 (AAA). `steel` on white ≈ 6.4:1 (AA). `slate` on white ≈ 4.7:1 (AA, borderline at 300 weight — keep ≥16px).
- White on `indigo` ≈ 6.2:1 (AA). `#635BFF` on white ≈ 4.7:1.
- Weight 300 is thin — avoid it below 14px and on tinted backgrounds; switch to 400.
- Focus: 2px `indigo` outline with 2px offset (or 4px soft indigo ring); `lavender` ring on dark bands.
- Min touch target 44×44px; animated gradient must pause under reduced motion.

## 12. Do / Don't

**Do**
- Use one sans (Söhne → Inter Tight) at weight 300 for headlines and body, with negative tracking at large sizes.
- Keep indigo for interactive elements only; pair the primary button with a lavender ghost button.
- Use navy `#061B31` instead of black; use cool blue-grey neutrals.
- Use 4px radius on buttons/inputs, 6–8px on cards; blue-tinted layered shadows.
- Put the colour energy in one gradient hero / glow per page; keep 96px between sections.

**Don't**
- Don't use bold (600–700) headlines or pure black text.
- Don't use pill buttons or large (≥12px) radii on cards.
- Don't use neutral grey/black shadows.
- Don't use orange / ruby / magenta / yellow for buttons or links.
- Don't fill large areas with indigo or add gradient overlays to UI components.

## 13. Quick prompt for AI tools / AI 提示词

> Build in the style of Stripe: white (#FFFFFF) and very pale blue-grey (#F8FAFD) canvas, navy ink text (#061B31) with blue-grey supporting copy (#50617A / #64748D), and a single indigo accent (#533AFD, hover #4434D4) reserved for buttons, links and focus. Typography: one sans (Söhne → "Inter Tight"/Inter), weight 300 for headlines and body, 400 for buttons/nav; headlines 48–56px with tight negative tracking (-0.02em), line-height ~1.05; ss01 + tabular numbers for figures. Buttons have 4px radius — filled indigo primary paired with a transparent ghost button with 1px #B9B9F9 border. Cards 6–8px radius, white, with layered blue-tinted shadows (0 30px 45px -30px rgba(50,50,93,.25), 0 18px 36px -18px rgba(0,0,0,.1)). One animated violet→magenta→orange mesh gradient or indigo glow in the hero; real product UI mockups as illustrations; 8px grid, ~1264px max width, 96px section spacing; calm, confident sentence-case copy with concrete numbers.

## Sources
- [designlang — Stripe design language (extracted 2026-05)](https://designlang.vercel.app/gallery/stripe-com/stripe-design-language.md)
- [Refero style reference — Stripe](https://styles.refero.design/style/48e5de76-05d5-4c4e-a269-c7c245b291ec)
- [webdesignhot — Stripe design.md](https://www.webdesignhot.com/design.md/stripe/)
- [shadcn.io — Stripe Inspired DESIGN.md](https://www.shadcn.io/design/stripe)
