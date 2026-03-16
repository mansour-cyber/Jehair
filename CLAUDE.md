# CLAUDE.md — Jehair Repository Guide

## Project Overview

**Jehair** is a static single-page e-commerce website for a natural barley coffee product sold in Saudi Arabia. The site is entirely Arabic-language (RTL), mobile-responsive, and conversion-focused via WhatsApp integration.

- **Technology:** Pure HTML5 + embedded CSS3 (no JavaScript frameworks, no build tools)
- **Deployment:** Static file serving — no server-side processing required
- **Language:** Arabic (Right-to-Left)
- **Primary sales channel:** WhatsApp (+966555200445)

---

## Repository Structure

```
/Jehair/
├── index.html          # Entire website (HTML + embedded CSS, ~824 lines)
├── README.md           # Minimal project description
├── jehair-logo.svg     # Primary brand logo (SVG)
├── logo.png            # Legacy brand logo (PNG)
├── IMG_0495.jpeg       # Hero background image (OG image)
├── IMG_0496.jpeg       # Problem section — bulk barley vs sachet contrast
├── IMG_0497.jpeg       # Product showcase image
├── IMG_0498.jpeg       # Lifestyle/benefits section image
├── IMG_0494.jpeg       # How-to preparation section image
├── IMG_0486.jpeg       # Additional product image
├── IMG_0461.png        # Additional image
├── IMG_0457.png        # Additional image
├── ing.jpg             # Ingredients display image
├── how.jpg             # Legacy preparation/how-to image
├── hero.jpg            # Legacy hero background image
├── hero2.jpg           # Legacy secondary hero image
├── box1b.jpg           # Legacy product box 1 image
├── box2.jpg            # Legacy product box 2 image
└── .github/
    └── workflows/
        └── auto-merge.yml  # Auto-merges claude/* branches into main
```

Everything lives in `index.html`. There are no subdirectories beyond `.git/` and `.github/`, no build output folders, and no configuration files.

---

## index.html Architecture

The file (~824 lines) is divided into two main parts:

### 1. `<head>` — Metadata & Styles

- **Meta tags:** charset, viewport, SEO title/description
- **OpenGraph tags:** For social sharing previews (OG image: `IMG_0495.jpeg`)
- **Fonts:** System font stack — `SF Arabic`, `SF Pro Display`, `Helvetica Neue`, Arial (no external CDN)
- **Embedded CSS:** ~310 lines of custom styles using CSS variables, Grid, and Flexbox
- **Inline script:** Scroll restoration reset (`history.scrollRestoration = 'manual'`)

### 2. `<body>` — Page Sections (top to bottom)

| Section | CSS Class(es) | Purpose |
|---|---|---|
| Announcement Bar | `.announce`, `.announce-txt` | Top banner: free shipping threshold, box price |
| Navigation | `.nav`, `.nav-brand`, `.nav-links`, `.nav-wa` | Sticky RTL nav with WhatsApp CTA; uses `jehair-logo.svg` with text fallback |
| Hero | `.hero`, `.hero-bg`, `.hero-overlay`, `.hero-inner` | Full-height image (`IMG_0495.jpeg`) with zoom animation and CTA buttons |
| Trust Bar | `.trust`, `.trust-row`, `.trust-item` | 6 trust signals in pill-shaped items (2×3 grid) |
| Problem Section | `.prob-layout`, `.prob-cards-col`, `.prob-card-v`, `.prob-answer` | Pain-point cards + product image (`IMG_0496.jpeg`) |
| Solution Section | `.sol-cards`, `.sol-card` | 3-step solution cards (numbered) |
| Product Showcase | `.showcase`, `.showcase-img-wrap`, `.showcase-content` | Full-bleed 2-col product display with specs + price + CTA |
| Comparison Table | `.compare-wrap`, `.compare` | Jehair vs traditional bulk barley vs regular coffee |
| Ingredients | `.ing-layout`, `.ing-rows`, `.ing-row` | 6 ingredients with icons + descriptions |
| Benefits / Lifestyle | `.lifestyle-layout`, `.bens-in-layout`, `.ben` | 2-col: benefit cards + lifestyle photo (`IMG_0498.jpeg`) |
| Mid-page CTA | `.mid-cta`, `.mid-cta-inner` | Inline WhatsApp order prompt |
| Quote | `.quote-sec`, `.quote-txt` | Brand quote block |
| How-to | `.how-layout`, `.how-steps`, `.how-step` | 4-step numbered preparation guide + photo (`IMG_0494.jpeg`) |
| Shipping & Policy | `.policy-grid`, `.policy-card` | 3 policy cards (shipping, returns, support) |
| Guarantee | `.guarantee` | Full-width satisfaction guarantee block |
| Testimonials | `.reviews-grid`, `.review-card` | 3 customer review cards with star ratings |
| FAQ | `.faq-list`, `.faq-item` | 8 native HTML `<details>` accordion Q&A items |
| CTA | `.cta-sec`, `.cta-price-box`, `.btn-whatsapp` | Final order section with single product price |
| Footer | `.footer-left`, `.footer-links` | Branding, WhatsApp + phone links, copyright |
| Mobile WhatsApp Button | `.mobile-wa` | Fixed bottom sticky button (mobile only) |

---

## CSS Conventions

### CSS Variables (defined in `:root`)

```css
--ink:   #3C2210   /* primary dark text color */
--ink2:  #7A5C35   /* secondary text color */
--gold:  #B8902A   /* primary brand accent (golden) */
--gold2: #C8A028   /* secondary gold variant */
--cream: #FEFAF5   /* light background tone */
--sand:  #F5E8D2   /* warm neutral background */
--pale:  #EDD8BC   /* slightly darker warm background */
--latte: #D8C4A0   /* mid-warm neutral */
--box:   #C4AE8A   /* box/border accent */
--warm:  #F0E2CC   /* warm tinted background */
--white: #FFFFFF   /* pure white */
--bdr:   rgba(60,34,16,.09)  /* standard border color */
--r:     16px      /* standard border-radius */
--w:     1040px    /* max content width */
--font:  -apple-system, BlinkMacSystemFont, 'SF Arabic', 'SF Pro Display', 'Helvetica Neue', Arial, sans-serif
--font-display: -apple-system, BlinkMacSystemFont, 'SF Arabic Rounded', 'SF Pro Rounded', 'SF Pro Display', 'Helvetica Neue', Arial, sans-serif
```

Always use these variables rather than hardcoded color/size values to maintain brand consistency.

### Section Background Modifiers

```css
.sec           /* base section: white background, 84px vertical padding */
.sec.tinted    /* gradient: white → var(--sand) → white */
.sec.ltinted   /* gradient: white → var(--pale) → white */
.sec.dark      /* dark ink background with white text overrides */
```

### Responsive Breakpoints

- `max-width: 860px` — Tablet: collapse multi-column grids, hide nav links, show mobile WA button
- `max-width: 520px` — Mobile: single-column layouts, smaller hero heading

### Layout Patterns

- **CSS Grid** for multi-column sections (products, benefits, gallery, policy)
- **Flexbox** for navigation and inline groupings
- **`clamp()`** for fluid typography scaling
- **RTL-aware layout** — all text-align, flex direction, and grid ordering account for Arabic right-to-left reading
- **RTL grid note:** In 2-column `.prob-layout` and `.lifestyle-layout`, the first child renders on the **right** side in RTL — the cards/content column is always first in HTML

---

## Product Catalog

**Single Product** (current site version):

| Product | Price | Units | Per Unit | Use Case |
|---|---|---|---|---|
| بوكس جهيّر (Jehair Box) | 45 SAR | 10 individual sachets | 4.5 SAR | 1 sachet = 1 cup (200ml); daily use |

Free shipping threshold: orders over 200 SAR.

### Ingredients (6 total)

1. **الشعير البلدي** — Barley (warm authentic base)
2. **الكركم** — Turmeric (golden color and flavor depth)
3. **الزعفران** — Saffron (luxury touch and aroma)
4. **الهيل** — Cardamom (Gulf authentic spirit)
5. **الزنجبيل** — Ginger (warmth and balance)
6. **العصفر** — Safflower (vibrant color and distinctive character)

---

## Development Workflow

### Making Changes

There is no build step. Edit `index.html` directly and open it in a browser to preview.

```bash
# Preview locally
open index.html         # macOS
xdg-open index.html     # Linux
```

### Adding or Replacing Images

- All images are in the root directory alongside `index.html`
- Referenced as relative paths: `src="IMG_0495.jpeg"`, `src="jehair-logo.svg"`, etc.
- New product photos follow the `IMG_XXXX.jpeg` naming pattern
- Recommended formats: JPEG for photos, SVG/PNG for logos and graphics
- Keep images optimized for web (compress before adding)

### Logo

The nav uses `jehair-logo.svg` as the primary logo with an `onerror` fallback to inline text (`.nav-logo-text`). Both must be kept in sync when updating brand copy.

### Editing Content

All visible text is inside `index.html` and written in Arabic. When editing:
- Maintain RTL text direction (`dir="rtl"` on the `<html>` element)
- Use `var(--font)` and `var(--font-display)` for any new text — no Google Fonts
- Do not add `dir="ltr"` blocks unless displaying a URL, phone number, or numeric code

### WhatsApp Links

WhatsApp CTA links follow this format:
```html
<a href="https://wa.me/+966555200445?text=...">
```
The `text` parameter contains Arabic pre-fill text. The phone number is `+966555200445`.
Modern browsers handle Arabic encoding automatically — no manual URL encoding needed.

---

## CI/CD — GitHub Actions

`.github/workflows/auto-merge.yml` automatically merges any `claude/**` branch into `main` on push:
- All AI-generated branches named `claude/<task>-<ID>` are automatically promoted to production
- No manual PR merge required for `claude/*` branches
- The workflow uses `github-actions[bot]` with a `--no-ff` merge commit

---

## Git Conventions

### Branch Strategy

- `main` — production-ready code (auto-merged from claude/* branches via CI)
- `master` — legacy local branch
- `claude/<task-description>-<ID>` — AI-generated feature/task branches

### Commit Messages

Use clear, descriptive English commit messages:
```
Update CLAUDE.md to reflect current site structure
Replace hero image with IMG_0495.jpeg
Add comparison table section
Fix mobile nav overflow on 320px screens
```

### Push

```bash
git push -u origin <branch-name>
```

---

## Deployment

The site is a static HTML file — deploy by copying files to any web host:

- Upload `index.html` + all image files to the web root
- No build step, no server configuration needed
- HTTPS is recommended (WhatsApp links require it in some browsers)
- Suitable for: GitHub Pages, Netlify, Vercel (static), any shared hosting, Nginx/Apache

---

## Key Conventions for AI Assistants

1. **Do not introduce JavaScript** beyond the existing single-line scroll-restoration script. The site is intentionally minimal-JS.
2. **Preserve RTL layout.** All CSS changes must account for Arabic right-to-left rendering. In 2-column grids, first child = right column in RTL.
3. **Use existing CSS variables** for all colors and spacing — never hardcode hex values.
4. **Keep the single-file structure.** Do not split into separate CSS/JS files unless explicitly asked.
5. **Image references are relative paths** — do not convert to absolute URLs.
6. **Arabic text must remain Arabic** — do not translate or alter product copy without explicit instruction.
7. **WhatsApp is the primary CTA** — preserve all `.nav-wa`, `.showcase-btn`, `.mid-cta-btn`, `.btn-whatsapp`, and `.mobile-wa` WhatsApp links when editing structure. Current number: `+966555200445`.
8. **Test at both 860px and 520px breakpoints** after any layout changes.
9. **No new dependencies** — no npm, no CDN scripts. The font stack is system fonts only (no Google Fonts).
10. **Do not add a backend** — this is intentionally a static site with no server-side logic.
11. **Single product** — the site sells one product (10-sachet box, 45 SAR). Do not reintroduce the old 2-product structure (Thermos Box / Daily Cup Box) unless explicitly requested.
12. **Section modifiers** — use `.sec.tinted`, `.sec.ltinted`, or `.sec.dark` to alternate section backgrounds; do not hardcode background colors on `<section>` elements.
