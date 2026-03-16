# CLAUDE.md — Jehair Repository Guide

## Project Overview

**Jehair** is a static single-page e-commerce website for a natural barley coffee product sold in Saudi Arabia. The site is entirely Arabic-language (RTL), mobile-responsive, and conversion-focused via WhatsApp integration.

- **Technology:** Pure HTML5 + embedded CSS3 (no JavaScript frameworks, no build tools)
- **Deployment:** Static file serving — no server-side processing required
- **Language:** Arabic (Right-to-Left)
- **Primary sales channel:** WhatsApp (+966555200444)

---

## Repository Structure

```
/Jehair/
├── index.html      # Entire website (HTML + embedded CSS, ~477 lines)
├── README.md       # Minimal project description
├── logo.png        # Brand logo
├── hero.jpg        # Main hero background image
├── hero2.jpg       # Secondary hero image
├── box1b.jpg       # Product box 1 image (Thermos Box)
├── box2.jpg        # Product box 2 image (Daily Cup Box)
├── ing.jpg         # Ingredients display image
└── how.jpg         # Preparation/how-to image
```

Everything lives in `index.html`. There are no subdirectories, no build output folders, and no configuration files beyond `.git/`.

---

## index.html Architecture

The file is divided into two main parts:

### 1. `<head>` — Metadata & Styles

- **Meta tags:** charset, viewport, SEO title/description
- **OpenGraph tags:** For social sharing previews
- **Google Fonts:** `Tajawal` (body) and `Amiri` (display) — both Arabic-optimized fonts
- **Embedded CSS:** ~160 lines of custom styles using CSS variables, Grid, and Flexbox

### 2. `<body>` — Page Sections (top to bottom)

| Section | CSS Class(es) | Purpose |
|---|---|---|
| Navigation | `.nav`, `.nav-brand`, `.nav-links` | Sticky RTL nav with WhatsApp CTA |
| Hero | `.hero`, `.hero-overlay`, `.hero-inner` | Full-height image with CTA buttons |
| Trust Badges | `.badges` | Icons + short trust signals |
| Mosaic Gallery | `.mosaic` | 3-column image grid |
| Products | `.pcard` | 2 product cards (Thermos Box, Daily Cup Box) |
| Ingredients | `.ing-layout`, `.ing-rows` | 6 ingredients with icons + descriptions |
| Benefits | `.bens`, `.ben` | 6-item responsive benefit grid |
| Quote | `.quote-sec` | Brand quote block |
| How-to | `.how-layout`, `.how-steps` | 4-step numbered preparation guide |
| Testimonials | Inline grid styles | 3 customer review cards with ratings |
| FAQ | `<details>` elements | 5 native HTML accordion Q&A items |
| CTA | `.cta-sec`, `.cta-prices` | Final order section with pricing |
| Footer | `.footer-left`, `.footer-links` | Branding, contact links, copyright |
| Mobile WhatsApp Button | `.mobile-wa` | Fixed bottom button (mobile only) |

---

## CSS Conventions

### CSS Variables (defined in `:root`)

```css
--ink:   /* primary dark text color */
--ink2:  /* secondary text color */
--gold:  /* primary brand accent (golden) */
--gold2: /* secondary gold variant */
--cream: /* light background tone */
--sand:  /* warm neutral background */
--pale:  /* very light background */
--white: /* pure white */
--r:     16px   /* standard border-radius */
--w:     1040px /* max content width */
```

Always use these variables rather than hardcoded color values to maintain brand consistency.

### Responsive Breakpoints

- `max-width: 860px` — Tablet: collapse multi-column grids to 2 columns
- `max-width: 520px` — Mobile: collapse to single column, show `.mobile-wa` button

### Layout Patterns

- **CSS Grid** for multi-column sections (products, benefits, gallery)
- **Flexbox** for navigation and inline groupings
- **`clamp()`** for fluid typography scaling
- **RTL-aware layout** — all text-align, flex direction, and grid ordering account for Arabic right-to-left reading

---

## Product Catalog

| Product | Price | Sachets | Per Sachet | Use Case |
|---|---|---|---|---|
| Thermos Box (Box 1) | 89 SAR | 12 | 7.4 SAR | Makes 1 full liter; family/trips |
| Daily Cup Box (Box 2) | 115 SAR | 30 | 3.8 SAR | Makes 200ml; daily 1-month supply |

Box 2 is marked as the featured/most popular product.

### Ingredients (6 total)

1. Barley (Beta-glucan)
2. Turmeric (Curcumin)
3. Saffron (Mood & memory)
4. Cardamom (Digestion)
5. Ginger (Circulation)
6. Safflower (Antioxidant)

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
- Referenced as relative paths: `src="hero.jpg"`, `src="logo.png"`, etc.
- Recommended formats: JPEG for photos, PNG for logos/graphics with transparency
- Keep images optimized for web (compress before adding)

### Editing Content

All visible text is inside `index.html` and written in Arabic. When editing:
- Maintain RTL text direction (`dir="rtl"` on the `<html>` element)
- Use existing font variables (Tajawal/Amiri) for any new text
- Do not add `dir="ltr"` blocks unless displaying a URL or numeric code

### WhatsApp Links

WhatsApp CTA links follow this format:
```html
<a href="https://wa.me/966555200444?text=...">
```
The `text` parameter is URL-encoded Arabic. When updating the message, encode the Arabic text properly.

---

## Git Conventions

### Branch Strategy

- `main` / `master` — production-ready code
- `claude/<task-description>-<ID>` — AI-generated feature/task branches

### Commit Messages

Use clear, descriptive English commit messages:
```
Add CLAUDE.md documentation
Update hero section copy
Replace box1b.jpg with optimized version
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

1. **Do not introduce JavaScript** unless explicitly requested. The site is intentionally JS-free.
2. **Preserve RTL layout.** All CSS changes must be tested against Arabic text direction.
3. **Use existing CSS variables** for all colors and spacing — never hardcode hex values.
4. **Keep the single-file structure.** Do not split into separate CSS/JS files unless asked.
5. **Image references are relative paths** — do not convert to absolute URLs.
6. **Arabic text must remain Arabic** — do not translate or alter product copy without explicit instruction.
7. **WhatsApp is the primary CTA** — preserve all `.nav-wa`, `.pcard-btn`, and `.mobile-wa` WhatsApp links when editing structure.
8. **Test at both 860px and 520px breakpoints** after any layout changes.
9. **No new dependencies** — no npm, no CDN scripts beyond the existing Google Fonts link.
10. **Do not add a backend** — this is intentionally a static site with no server-side logic.
