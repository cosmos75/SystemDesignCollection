# SystemDesignCollection

收集各个网站的设计系统，每个站点一个文件夹，内含一份 `design.md`，方便日后给设计师、开发者或 AI 工具直接使用。

A collection of website design systems. Each site lives in its own folder with a `design.md` describing colors, typography, spacing, radius, elevation, motion, components, imagery and voice.

## Index / 目录

| Site | Style | File | Captured |
|---|---|---|---|
| [Monzo](https://monzo.com) | light · bold · rounded fintech · Hot Coral + navy | [monzo/design.md](monzo/design.md) | 2026-11-07 |
| [Stripe](https://stripe.com) | light · editorial · Söhne 300 · indigo accent · gradient hero | [stripe/design.md](stripe/design.md) | 2026-11-10 |

## Structure / 结构

```
SystemDesignCollection/
├── README.md          # this index
├── _template/design.md  # blank template for new sites
└── <site>/design.md   # one folder per site (lowercase, kebab-case)
```

## Adding a site / 新增站点

1. Copy `_template/design.md` to `<site>/design.md`.
2. Fill in each section; mark uncertain values with (≈).
3. Add a row to the index table above.
