# Linear — Design System (design.md)

> Source: https://linear.app (issue tracking / product development tool, marketing website + app)
> Captured: 2026-11-10
> Style keywords: dark-first · near-black canvas · indigo accent · hairline borders · dense · precise · Inter Display · quiet

**数据来源说明 / Provenance:** linear.app 本次无法直接抓取（沙箱代理拦截）。下列数值综合自 Linear 官方博客
（[How we redesigned the Linear UI](https://linear.app/now/how-we-redesigned-the-linear-ui)、
[Behind the latest design refresh](https://linear.app/blog/behind-the-latest-design-refresh)）
以及多份第三方样式提取（shadcn.io、oh-my-opencode design reference 等）的交叉比对。
Values marked **(✓)** agree across sources; **(≈)** are approximate / sources differ. Verify in DevTools before pixel-exact work.

---

## 1. Brand essence / 品牌调性

- **Built for focus.** Calm, precise, engineered. The UI should feel like a native app: fast, dense, keyboard-first.
- **"Don't compete for attention you haven't earned."** Content is prominent; navigation and chrome recede (dimmed sidebar, muted inactive text).
- **"Structure should be felt, not seen."** Few, soft, low-contrast borders and dividers; elevation comes from stepping surface luminance, not from shadows.
- **Dark-first.** The marketing site lives on a near-black canvas with product screenshots glowing out of it. Light mode exists in the app and uses the same generated system.
- **One accent.** Linear indigo (`#5E6AD2`) is reserved for CTAs, focus and interactive accents. Everything else is grayscale.
- **Themes are generated, not hand-picked.** The app derives every color from three inputs in LCH space: **base color, accent color, contrast** (replacing ~98 hand-tuned variables per theme). Recent refresh moved neutrals from cool blue-gray toward a slightly **warmer, less saturated gray**.

## 2. Color / 颜色

### Canvas & surfaces (dark)
| Token | Hex | Use |
|---|---|---|
| `bg-canvas` | `#08090A` (✓) | Marketing page background (some extractions report `#010102`) |
| `bg-panel` | `#0F1011` (✓) | Panels, sidebar, section blocks |
| `bg-surface-1` | `#141516` (≈) | Subtle rows, dividers |
| `bg-surface-2` | `#18191A` (≈) | Hover rows |
| `bg-elevated` | `#191A1B` (✓) | Cards, menus, popovers |
| `bg-secondary` | `#28282C` (≈) | Secondary fills, selected items |

### Text
| Token | Hex | Use |
|---|---|---|
| `text-primary` | `#F7F8F8` (✓) | Headlines, primary text (never pure `#FFF`) |
| `text-secondary` | `#D0D6E0` (✓) | Body copy, sub-headlines |
| `text-tertiary` | `#8A8F98` (✓) | Meta, captions, inactive nav |
| `text-quaternary` | `#62666D` (✓) | Placeholders, disabled |

### Brand / accent
| Token | Hex | Use |
|---|---|---|
| `brand` (Linear indigo) | `#5E6AD2` (✓) | Primary CTA fill, focus ring, logo tint |
| `brand-hover` | `#828FFF` (✓) | Hover on brand surfaces |
| `brand-accent` | `#7170FF` (≈) | Links / accent text on dark |
| `brand-muted` | `#7A7FAD` (≈) | Security / secondary brand moments |

### Borders
| Token | Value | Use |
|---|---|---|
| `border-subtle` | `rgba(255,255,255,0.05)` (✓) | Default hairline on cards |
| `border` | `rgba(255,255,255,0.08)` (✓) | Stronger hairline, inputs, icon buttons |
| `border-solid-1/2/3` | `#23252A` / `#34343A` / `#3E3E44` (✓) | Solid equivalents when transparency isn't possible |

### Semantic & status
| Token | Hex |
|---|---|
| `success` | `#27A644` (✓) · emerald variant `#10B981` |
| `warning` | `#F2994A` (≈) |
| `danger` | `#EB5757` (≈) |
| Issue status (app) | Backlog gray `#BEC2C8`(≈), Todo gray, In Progress yellow `#F2C94C`(≈), Done indigo `#5E6AD2`, Canceled gray |

### Light mode neutrals (app)
`#FFFFFF` canvas, `#F7F8F8` / `#F5F6F7` panels, `#E6E6E6` borders, `#D0D6E0` strong dividers, text from `#1F2023` (≈) down to `#8A8F98`.

### Pairing rules
- Text on the dark canvas uses the 4-step ladder (`primary → quaternary`), not opacity on white.
- Indigo only on interactive things; never as a large background band.
- Prefer translucent white fills/borders (0.02–0.08) so surfaces work on any underlying gray.
- Marketing sections sometimes add a very faint radial indigo/gray glow behind product shots — keep it subtle (≤10% opacity).

```css
:root {
  --ln-bg: #08090a;        --ln-panel: #0f1011;     --ln-surface-1: #141516;  --ln-surface-2: #18191a;
  --ln-elevated: #191a1b;  --ln-secondary: #28282c;
  --ln-text-1: #f7f8f8;    --ln-text-2: #d0d6e0;    --ln-text-3: #8a8f98;     --ln-text-4: #62666d;
  --ln-brand: #5e6ad2;     --ln-brand-hover: #828fff; --ln-brand-accent: #7170ff; --ln-brand-muted: #7a7fad;
  --ln-border-subtle: rgba(255,255,255,0.05);  --ln-border: rgba(255,255,255,0.08);
  --ln-border-solid: #23252a;  --ln-border-solid-2: #34343a;  --ln-border-solid-3: #3e3e44;
  --ln-success: #27a644;   --ln-warning: #f2994a;   --ln-danger: #eb5757;
  --ln-overlay: rgba(0,0,0,0.85);
}
```

## 3. Typography / 字体

- **Inter Variable** for UI and body; **Inter Display** for headings (adds expression while staying readable — per Linear's redesign post). Fallback: `"Inter", "SF Pro Display", -apple-system, system-ui, "Segoe UI", Roboto, sans-serif`.
- **Berkeley Mono** for code / keyboard shortcuts. Fallback: `ui-monospace, "SF Mono", Menlo, monospace`.
- OpenType features on globally: `font-feature-settings: "cv01", "ss03";` (≈).
- **Variable weights, not the usual steps:** 400 (regular), **510** (default emphasis / medium), **590** (strong). Avoid 700.
- Display text uses tight line-height (1.0–1.1) and **negative tracking** (≈ -0.022em at large sizes). Small text stays near 0.

| Role | Family | Size (desktop → mobile) | Weight | Line height | Tracking |
|---|---|---|---|---|---|
| display-xl | Inter Display | 72px → 44px | 510 | 1.00 | -1.584px (-0.022em) |
| display | Inter Display | 64px → 40px | 510 | 1.00 | -1.408px |
| h1 | Inter Display | 48px → 36px | 510 | 1.00 | -1.056px |
| h2 | Inter Display | 32px → 28px | 400 | 1.13 | -0.704px |
| h3 | Inter Display | 24px → 20px | 400 | 1.33 | -0.288px |
| h4 | Inter | 20px | 590 | 1.33 | -0.24px |
| body-lg | Inter | 18px | 400 | 1.60 | -0.165px |
| body | Inter | 16px / 15px | 400 | 1.50–1.60 | normal / -0.165px |
| ui / button | Inter | 14px | 510 | 1.50 | -0.182px |
| small | Inter | 13px | 400–510 | 1.50 | -0.13px |
| caption / eyebrow | Inter | 12px | 510 | 1.40 | normal (eyebrow +0.4px, ≈) |
| micro / badge | Inter | 11px / 10px | 510 | 1.40 | normal |
| mono | Berkeley Mono | 12–14px | 400 | 1.50 | normal |

Hero headlines are typically 2 lines, `text-primary`, followed by a `text-tertiary` 18px subline. In the app, base UI text is 13–14px (dense).

## 4. Spacing & layout / 间距与布局

- Base unit **4px**, core rhythm **8px**: `4, 8, 12, 16, 24, 32, 48, 64, 96`.
- Max content width **≈1200px** (marketing), 24px gutters; hero product shots may bleed wider (~1400px).
- Section padding: 96–160px desktop, 48–64px mobile.
- Top nav height **56px** (≈64px on some pages).
- Breakpoints: 600, 640, 768 (nav → hamburger), 1024, 1280px.
- App layout: inverted-L chrome (left sidebar ~220–244px + top header), compact rows 32–36px tall, alignment of icons/labels on a strict grid.

## 5. Shape / 圆角

| Token | Value | Use |
|---|---|---|
| `r-xs` | 2px | Keyboard-shortcut keys, tiny badges, toolbar buttons |
| `r-sm` | 4px | Tags, small chips |
| `r-md` | 6px (✓) | **Buttons, inputs, menu items** (the workhorse) |
| `r-lg` | 8px | Cards, popovers |
| `r-xl` | 12px | Large feature cards, dialogs |
| `r-2xl` | 16–22px (≈) | Big product-screenshot frames, hero panels |
| `r-pill` | 9999px | Pills, announcement chips |
| `r-full` | 50% | Avatars, icon buttons |

Corners are modest — precise, not bubbly.

## 6. Elevation / 阴影

Elevation = **lighter surface + hairline border**, not drop shadow. Shadows on dark are barely visible.

| Token | Value | Use |
|---|---|---|
| `shadow-hairline` | `0 0 0 1px rgba(255,255,255,0.08)` | Ring around cards on dark |
| `shadow-ring-dark` | `0 0 0 1px rgba(0,0,0,0.2)` | Ring on light mode |
| `shadow-sm` | `0 1.2px 0 rgba(0,0,0,0.03)` | Toolbars |
| `shadow-md` | `0 2px 4px rgba(0,0,0,0.4)` | Menus, popovers |
| `shadow-inset` | `inset 0 0 12px rgba(0,0,0,0.2)` | Recessed panels |
| `shadow-dialog` | `0 4px 24px rgba(0,0,0,0.2), 0 2px 8px rgba(0,0,0,0.12), 0 0 0 1px rgba(255,255,255,0.08)` (≈) | Modals, command menu |

Product screenshots often get a 1px top highlight (`inset 0 1px 0 rgba(255,255,255,0.06)`) to read as glass.

## 7. Motion / 动效

Fast and functional — the product should feel instant.
- Durations: 100–150ms (hover, menu open), 200–250ms (panels, dialogs), 400–800ms (marketing reveals).
- Easing: `cubic-bezier(0.25, 0.46, 0.45, 0.94)` (ease-out) for UI; `cubic-bezier(0.16, 1, 0.3, 1)` (≈) for marketing entrances.
- Marketing: text and screenshots fade + rise 8–16px on scroll; subtle glow/beam effects; no bounce.
- Respect `prefers-reduced-motion`: remove rise/blur reveals and animated gradients.

## 8. Components / 组件

### Buttons (radius 6px, 14px / 510)
| Variant | Fill | Text | Border | Notes |
|---|---|---|---|---|
| Primary | `#5E6AD2` | `#FFFFFF` | — | Hover `#828FFF`. "Start building", "Sign up" |
| Inverse | `#F7F8F8` / white | `#08090A` | — | Big marketing CTA on dark (rare, high-impact) |
| Secondary / ghost | `rgba(255,255,255,0.02)` | `#E2E4E7` | 1px `#24282C` | Default secondary |
| Subtle | `rgba(255,255,255,0.04)` | `#D0D6E0` | — | Toolbars, low emphasis |
| Icon | `rgba(255,255,255,0.03–0.05)` | `text-secondary` | 1px `rgba(255,255,255,0.08)` | Circular or 6px |

Size: height 32px (app) / 40px (marketing), padding 8×16px. Small: 28px, 12px/510. Optional trailing `→` or shortcut key hint.

### Navigation
- Sticky top bar, 56px, translucent canvas with `backdrop-filter: blur(12–20px)` and a 1px `border-subtle` bottom line.
- Logo left, text links center (14px/510, `text-secondary` → `text-primary` on hover), "Log in" ghost + "Sign up" primary on right.
- Mobile ≤768px: hamburger → full-screen dark sheet.

### Cards
- Fill `rgba(255,255,255,0.02–0.05)` or `bg-elevated`, 1px `border` hairline, radius 8–12px, 24–32px padding.
- Feature cards: small icon / illustration top, 16–20px/590 title, 15px `text-tertiary` description.
- Product-screenshot cards: radius 16–22px, hairline border, faint top highlight, sit on canvas with soft radial glow.

### Inputs
- Height 32–40px, fill `rgba(255,255,255,0.02)`, 1px `border`, radius 6px, padding 8×12px (textarea 12×14px), placeholder `text-quaternary`.
- Focus: border → `brand`, plus `0 0 0 3px rgba(94,106,210,0.25)` ring (≈).

### Badges & pills
- Announcement pill (hero top): radius 9999px, 1px `#23252A` border, 13px `text-secondary`, trailing chevron.
- Subtle badge: `rgba(255,255,255,0.05)`, radius 2–4px, 10–11px/510.
- Status pill: semantic color dot + label.
- Keyboard shortcut `kbd`: 2–4px radius, 1px border, 11–12px mono, `text-tertiary`.

### Command menu (⌘K)
- Centered dialog ~640px wide, `bg-elevated`, radius 12px, `shadow-dialog`; search input 48px tall without border; rows 36–40px with icon + label + right-aligned shortcut; selected row `rgba(255,255,255,0.05)`.

### Lists (app)
- Dense issue rows 36px, columns: priority icon · ID (mono-ish, `text-tertiary`) · status icon · title (`text-primary`, 13–14px) · labels · assignee avatar (20px) · date.
- Hover `bg-surface-2`, selected adds left 2px `brand` indicator (≈).

### Footer
- Canvas background, 1px top `border-subtle`, 4–5 link columns (13–14px `text-tertiary`, hover `text-primary`), small logo + legal 12px.

## 9. Imagery & iconography / 图像与图标

- **Product UI is the hero image**: large, crisp, dark-mode screenshots of the app, often tilted/perspective or cropped, with soft glows.
- Abstract 3D / light-beam renders and minimal monochrome illustrations; no stock photography.
- Icons: custom, 16px (app) / 20–24px (marketing), 1.5px stroke or solid glyphs, `text-tertiary`; status/priority icons are compact geometric shapes (circles, partial pies, bars). Recent refresh shrank icons and removed colored team-icon backgrounds.

## 10. Voice & tone / 文案

- Confident, concise, craft-focused: "Linear is a purpose-built tool for planning and building products."
- Short declarative headlines, sentence case; emphasize speed, focus and quality.
- Precise product language (issues, cycles, projects, triage); no exclamation marks or hype.

## 11. Accessibility / 无障碍

- `#F7F8F8` on `#08090A` ≈ 18:1; `#8A8F98` on `#08090A` ≈ 6:1 (AA body); `#62666D` ≈ 3.4:1 → only placeholders/disabled or ≥18px.
- White on `#5E6AD2` ≈ 4.6:1 (AA for 14px/510 button text).
- App's theme generator exposes a **contrast** input to generate high-contrast themes.
- Full keyboard operability with visible focus (`brand` ring); every action reachable via ⌘K and shortcuts.

## 12. Do / Don't

**Do**
- Start from a near-black canvas and a 4-step gray text ladder.
- Use hairline translucent borders and luminance steps for depth.
- Keep indigo for interactive elements; use Inter Display with negative tracking for headlines.
- Be dense and aligned; let product screenshots carry the visual weight.

**Don't**
- Don't use pure white text, heavy drop shadows, or weight 700+.
- Don't use large colorful bands, gradients everywhere, or bubbly radii (>12px on controls).
- Don't add borders/dividers where spacing alone works; don't let navigation outshine content.
- Don't use positive letter-spacing on display text.

## 13. Quick prompt for AI tools / AI 提示词

> Build in the style of Linear: dark-first near-black canvas (#08090A) with panels #0F1011 and elevated #191A1B; text ladder #F7F8F8 / #D0D6E0 / #8A8F98 / #62666D; a single indigo accent #5E6AD2 (hover #828FFF) for primary buttons, links and focus rings only; Inter Display headlines at weight 510 with tight line-height (1.0) and negative tracking (-0.022em), Inter body 15–16px, Berkeley Mono for code; translucent white fills (2–5%) and 1px rgba(255,255,255,0.08) hairline borders instead of shadows; radius 6px on buttons/inputs, 8–12px on cards; 8px grid, ~1200px max width, generous section spacing; large glowing dark product screenshots; calm, precise, sentence-case copy.

## Sources
- Linear blog: [How we redesigned the Linear UI](https://linear.app/now/how-we-redesigned-the-linear-ui)
- Linear blog: [Behind the latest design refresh](https://linear.app/blog/behind-the-latest-design-refresh)
- [shadcn.io Linear DESIGN.md](https://www.shadcn.io/design/linear)
- [oh-my-opencode Linear design reference](https://cdn.jsdelivr.net/npm/oh-my-opencode@4.18.2/dist/skills/frontend/references/design/linear.app.md)
- [The Linear Aesthetic, Decoded](https://www.buildmvpfast.com/blog/linear-aesthetic-tokens-density-keyboard-first-ux-2026)
