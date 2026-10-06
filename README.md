# Handoff: Yurt Quote – Talia (הצעת מחיר יורט קוטר 6 מ׳)

## Overview
A one-page, Hebrew (RTL) personal price quote for a 6 m yurt from Alternative Dream, prepared for a customer named Talia. The customer can choose a package, add an extra door, pick wall/roof/liner colors, and confirm the order through a prefilled WhatsApp message.

## About the Design Files
`yurt-quote-talia.html` is a **design reference built in HTML**. It already runs as a static page (no build step), so it can go to GitHub Pages as-is. If it's moving into an existing codebase (React, Next, etc.), rebuild it there with that codebase's patterns and keep the look and behavior described below.

**Fastest path to GitHub:** upload the whole folder to the repo (`femmeacademy1-code/alternative`, branch `main`), keeping the relative paths. To make it the homepage, rename it `index.html`. Otherwise it will be at `/yurt-quote-talia.html`.

## Fidelity
High-fidelity. Final copy, colors, type, spacing and interactions.

## Layout (single screen, max-width 880px, centered)
Page padding `0 clamp(18px,5vw,48px) 120px` (the bottom padding leaves room for the fixed bar). Each section has `padding:36px 0` and a `1px dashed` top divider. Every section starts with a small orange kicker (14px/700, `#a4531c`) and then an H2 (`clamp(26px,3.4vw,34px)`).

1. **Header**: the Alternative Dream logo (84px tall, Wix CDN URL) on one side, "הצעת מחיר עבור **טליה**" and the date 06.10.2026 on the other.
2. **Hero**: a 2-column grid. Text column: kicker, H1 "יורט קוטר 6 מטר" (`clamp(34px,5vw,52px)`), a 19px paragraph, and pill chips (28 מ״ר / גובה מרכזי 3.70 מ׳ / 4 עונות). Image column: `assets/yurt-b.jpeg` in an arch shape (3:4, `border-radius:200px 200px 24px 24px`).
3. **Specs** (נתונים טכניים): a `<dl>` auto-fit grid (min 150px) of 10 tiles. Tile background `#e8dfd1`, radius 20px; 13px orange label over a 19px/700 brown value.
4. **Packages** (מה כלול): two selectable cards (`<button aria-pressed>`). Card: background `#fbf7f1`, radius 28px, padding 24px, 2px border (green when selected), radio dot, ✓ list (excluded items marked "–" at 55% opacity). Price row shows a struck-through old price, the price in 32px orange, and "פטור ממע״מ".
   - Full ("יורט מלא – הכל כלול"): ₪28,000 (was ₪32,000)
   - Fabric only ("בד חיצוני ופנימי בלבד"): ₪13,000 (was ₪15,500), plus a note that the customer must supply exact door and window measurements.
   - Add-on row (shown only when Full is selected): checkbox "תוספת דלת", +₪1,500.
5. **Color picker** (בחירת צבעים): left side is a simple SVG yurt preview whose roof, wall and door-liner fills update live. Right side has 3 swatch rows (40px circles; the selected one gets a double green ring): wall (20 colors), roof (same 20), liner (9). The selected color's name is shown next to each label.
6. **Materials** (תפריט חומרים): a 3-band layer stack (outer `#5d6b4f`, felt `#bfae95`, canvas `#ece3d3`), then 10 material rows in a grid `96px 150px 1fr` (thumbnail from `assets/yurt-parts/`, title + tagline, description + small specs).
7. **Terms** (פרטים נוספים): an auto-fit list with orange dot bullets. ⚠️ "אחריות יצרן 12 חודשים" currently appears twice. The client should confirm whether to remove one or replace it with something else.
8. **Gallery**: a 2-column grid of 4 photos (4:3, radius 24px), then 2 vertical videos (9:16, max height 520px).
9. **Fixed bottom bar**: translucent cream background with blur. Shows the selected package label and the total in 28px, plus a primary button "אישור הזמנה בוואטסאפ".

Mobile (≤640px): single column, the hero image moves above the text, material rows switch to `76px 1fr`.

## Interactions & State
State: `pkg` ('full' | 'fabric'), `door` (checkbox), `sel = {wall, roof, liner}` (swatch indices; defaults are 1, 1, 0).
- Every change runs `update()`, which refreshes `aria-pressed`, the color names, the SVG fills, add-on visibility, the total, the bar label, and the WhatsApp link.
- Total = `PRICES[pkg] + (pkg==='full' && door ? 1500 : 0)`.
- WhatsApp: `https://wa.me/972515490099?text=` + an encoded Hebrew confirmation listing the package, the add-on, and the wall/roof/liner color names with codes.
- Prices are in the `PRICES` constant at the top of the script.
- Print: the bar becomes static, the button is hidden, shadows are swapped for borders.

## Design Tokens
- Background `#f3ece2` · surface `#e8dfd1` · card `#fbf7f1`
- Text `#4a342c` · headings brown `#72544b`
- Orange `#c46a2f` / deep `#a4531c` (prices, kickers)
- Green `#52725a` / deep `#3f5a46` (selection, primary button, links)
- Divider: `color-mix(in srgb,#4a342c 16%,transparent)`
- Fonts: headings "Ploni" (local) falling back to **Assistant** 700; body Assistant 17px/1.6 (Google Fonts)
- Radii: 20px tiles, 24px media, 28px cards, 999px pills/buttons
- Shadows: `--shadow-sm` / `--shadow-md` from the Organic stylesheet (`_ds/.../styles.css`), which also provides `.btn .btn-primary`

## Assets
- `assets/yurt-a.jpeg`, `yurt-b.jpeg`, `yurt-frame.jpeg`, `yurt-aerial.jpeg`: photos
- `assets/yurt-video-1.mp4`, `yurt-video-2.mp4`: vertical videos
- `assets/yurt-parts/*.png`: material thumbnails
- Logo: loaded remotely from static.wixstatic.com

## Files
- `yurt-quote-talia.html`: the complete page (HTML + CSS + JS in one file)
- `_ds/organic-a559c2d1-44e1-47d3-b89e-0be943f0461b/styles.css`: base tokens and button styles
- `assets/`: images and videos
