# Design — Rangka

Warm Scandinavian world. Paper background, ink text, gold / sage / clay accents.
Honest-fiction: all visuals are illustrations, never presented as real photos.

## Tokens (`src/styles/global.css`)

- Base: `paper #faf5f2`, `cream-deep #f3ebe1`, `card #ffffff`, `ink #1c1917`, `ink-soft #44403c`, `muted-ink #57534e`
- Lines: `line #e7e0d9`, `line-strong #d6cdbf`
- Gold: `gold #92400e`, `gold-deep #7c360b`, `gold-soft #f7e8d3`, `gold-line #e3c99b`, `gold-wash #fbf1e2`
- Sage: `sage #4f5d46`, `sage-deep #3d4837`, `sage-soft #e8ebe0`, `sage-line #c8cfb8`, `sage-wash #f0f2e9`
- Clay: `clay #9a3f1f`, `clay-deep #7f3319`, `clay-soft #fbe7d6`, `clay-line #eabd97`, `clay-wash #fdf0e3`
- Night (kontak): `night #1c1917`, `night-soft #292524`, `night-line #57534e`, `night-ink #faf5f2`, `night-muted #e9e2d8`, `night-faint #c9c2b8`

### Illustration palette

SVG artwork uses raw hex (exempted with `illustration-palette` comments in `index.astro`).
Mapping to tokens:

| Hex | Token | Use |
|-----|-------|-----|
| `#d9b98f` | `--color-oak` | floors, swatches |
| `#b68f5e` | `--color-oak-line` | floor grain stroke |
| `#8a6a3e` | `--color-oak-deep` | wood grain on tables |
| `#8b9a7b` | `--color-sage-mid` | plants, soft shapes |
| `#f4efe8` | `--color-kapur` | sofa / textile light |
| `#fffdfb` | `--color-paper-bright` | window / furniture bright |
| `#f3ebe1` | `--color-cream-deep` (existing) | wall wash |
| `#f7e8d3` | `--color-gold-soft` (existing) | lamp shade |
| `#fbe7d6` | `--color-clay-soft` (existing) | cushions |
| `#e8ebe0` | `--color-sage-soft` (existing) | cushions alt |

Swatches in UI use `bg-oak / bg-sage-mid / bg-kapur` classes. SVG keeps literals for portability.

## Typography

- Display: `Bitter` (600/700), tight tracking `-0.015em` to `-0.02em`
- Body: `Public Sans` 400/500/600/700, base 15–16px, leading 7–8
- Metadata labels: 13px semibold uppercase `tracking-wide`, `text-muted-ink` (min 13px for mobile legibility)
- Tabular numerals: `.tnum` for process numbers, measurements, timestamps

## Surfaces & washes

- `wash-hero`: gold-wash radial top-right + sage-wash left, on paper
- `wash-proses` (used on `#gaya`): sage-wash top-right + gold-wash bottom-left, on card
- `glow-kontak`: oak 22% + sage 20% radials on night — dark closing panel
- `spine-rail`: `line → sage-line` gradient; `spine-fill`: `sage → clay 52% → gold`, `scaleY` by scroll (rAF-throttled, reduced-motion = full)
- `reveal`: single system, `opacity 0 + translateY(14px) → is-in`, 0.7s `cubic-bezier(0.16,1,0.3,1)`, `--reveal-delay` stagger, `IntersectionObserver threshold 0.12`

## Components

- Header: sticky, `bg-paper/95 backdrop-blur`, 64px, logo R + gold dot, desktop nav pills + `Konsultasi` ink pill
- Mobile nav: `<details>` + `aria-expanded/controls` sync, Escape + outside-click + link-click close, focus return
- Layanan: `dl > div > dt+dd` rows, 56px icon tile (gold/sage/clay washes), side card with palet/denah/list visual
- Gaya: large material moment + 2 cards (Kamar/Dapur `ILUSTRASI`) + `CATATAN DENAH` diagram
- Proses: 3 cards with numbered clay/gold/sage dots + sage-wash checklist pills
- Umpan-balik: 3 `SITUASI` example cards, explicit “bukan ulasan klien nyata”
- Kontak: night panel, `fieldset/legend` cakupan radios (pill, `peer-checked`), template group + `Salin template chat` button + `role=status` feedback, `sessionStorage: rangka-cakupan` sync from `data-layanan` links
- Focus: 3px gold outline (gold-soft on dark), offset 3px, native radius preserved — no forced 4px so pills stay pill-shaped
- Targets: all interactive `min-h-11` (44px)

## Accessibility notes

- Contrast AA+ measured: ink/paper 16.16, muted 7.05, gold-deep/white 8.79, night-muted/night 13.60, paper/clay 6.25, paper/gold 6.55, paper/sage 6.50
- Skip link, landmarks, `h1→h2→h3`, decorative SVG `aria-hidden`, informative SVG `role=img + title/desc`
- Reduced motion: JS `reduce` path + CSS media query kills `reveal`/`spine-fill` transition, preserves final state
