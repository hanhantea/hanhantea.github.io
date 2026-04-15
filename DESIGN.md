# Design System: Christine Han Portfolio

## 1. Visual Theme & Atmosphere

**Mood:** Warm, editorial, contemplative — like a hand-bound Korean art book or a quiet gallery catalog. The site evokes hanji paper texture, celadon ceramics, and persimmon ink.

**Density:** Spacious and unhurried. Generous whitespace between sections. Content breathes. The page rewards slow scrolling.

**Aesthetic philosophy:** Korean-American cultural duality expressed through bilingual typography, traditional craft motifs (norigae tassels, silk road metaphors), and a restrained warm palette. Never flashy, always intentional.

**Guardrails:**
- Never use cool blues, pure whites, or saturated neons — stay within the warm earth tone family
- Never use more than two typefaces on a single element
- Avoid drop shadows darker than `rgba(44, 37, 29, 0.2)` — keep elevation subtle
- Custom cursor (mugunghwa flower) is part of the identity on desktop; always hidden on touch devices
- Korean characters are decorative anchors, not translational — they set atmosphere, not provide translation


## 2. Color Palette & Roles

### Primary Surface
- **Hanji** `#F3EBE0` — Primary background. The warm cream of traditional Korean mulberry paper. Used on `body`, page backgrounds, and as the base tone everything else sits on.
- **Hanji Warm** `#EBE0D2` — Slightly deeper parchment. Used for subtle differentiation: decorative Korean characters, section dividers, and card wash backgrounds.

### Text
- **Ink** `#2C251D` — Primary text. Deep walnut brown, not black. Used for headings, hero title, body copy.
- **Ink Soft** `#52493B` — Secondary text. Muted brown for article body content, nav links, and supporting copy.
- **Warm Gray** `#847A6C` — Tertiary text. Used for hero descriptions, about section body paragraphs, and footer copy.
- **Taupe** `#B0A090` — Quaternary text. Used exclusively for dates and the most recessive metadata.

### Accent
- **Persimmon** `#C07A6E` — Primary accent. Warm terracotta. Used for: name highlight in hero, Korean labels, active nav states, hover states, link colors, "current" tags, and the footer Korean text. The signature color of the site.
- **Amber** `#C4A86C` — Secondary accent. Muted gold. Used for: interlude quote highlights, pull-quote left borders. Sparingly applied.
- **Celadon** `#9AAD8C` — Tertiary accent. Sage green inspired by Korean celadon pottery glaze. Used for: article category tags ("learnings", "stories") and select experience card washes.

### Decorative
- **Mauve** `#A08890` — Dusty rose. Used in gradient washes and the photo collage placeholder background.
- **Wood Light** `#AA9868` — Light brown. Used for the silk road path stroke and essay number color.
- **Wood Med** `#8A7650` — Medium brown. Used in decorative elements.

> **⚠ Inconsistency noted:** A stray hex value `#7A9BB5` (cool blue-gray) appears in one experience card wash gradient (`exp-stop-6`). This is outside the palette and should be replaced with an existing palette color like Celadon or Mauve.


## 3. Typography Rules

### Font Stack

| Font | Role | Weights Used |
|------|------|-------------|
| **Playfair Display** | English headings, editorial titles, pull quotes | 400, 500, 600, italic 400/500 |
| **Noto Serif KR** | Korean text only — decorative hangul, Korean labels, Korean subtitles | 200, 300, 400, 500, 600 |
| **Karla** | Body text, UI elements, navigation, dates, buttons | 300, 400, 500 |

### Type Scale

The scale uses two tiers for small text — **label** (0.75rem) and **caption** (0.68rem) — to maintain clear hierarchy without size proliferation. All Karla-set metadata uses one of these two sizes.

| Token | Size | Font | Weight | Usage |
|-------|------|------|--------|-------|
| `display-xl` | clamp(2.5rem, 4.4vw, 4.4rem) | Playfair Display | 400 | Hero title |
| `display-lg` | 3rem | Playfair Display | 400 | Footer heading |
| `display-md` | 2.8rem | Playfair Display | 400 | Section heading ("Living") |
| `heading-lg` | 2rem | Playfair Display | 400 | Experience section header |
| `heading-md` | 1.8rem | Playfair Display | 400 | Section header EN ("Writing") |
| `heading-sm` | 1.3rem | Playfair Display | 400 | Experience roles, essay titles |
| `quote` | clamp(1.4rem, 2.4vw, 2rem) | Playfair Display | 400 | Interlude pull quotes |
| `body` | 0.92rem | Karla | 300 | Hero description, about text |
| `body-sm` | 0.85rem | Karla | 400 | Article subtitles, logo EN |
| `tab` | 0.8rem | Karla | 400 | Writing category tabs (lowercase, letter-spaced) |
| `label` | 0.75rem | Karla | 400 | Company names, essay dates, show-more buttons |
| `caption` | 0.68rem | Karla | 400 | Experience dates, exp tags (current/contract), essay category tags |
| `kr-display` | clamp(4rem, 8vw, 8rem) | Noto Serif KR | 200 | Section header Korean characters |
| `kr-hero` | clamp(18rem, 38vw, 40rem) | Noto Serif KR | 200 | Hero background character (韓) |
| `kr-accent` | 1.8rem | Noto Serif KR | 200 | Essay numbering (一, 二, 三...) |
| `kr-label` | 0.9rem | Noto Serif KR | 200–300 | Korean subtitles and labels |
| `kr-body` | 0.82rem | Noto Serif KR | 300 | Korean body labels |

### Letter Spacing
- Tab labels: `0.1em`
- Label text (company, dates): `0.06–0.08em`
- Caption text (exp dates, tags): `0.08–0.14em` (uppercase)
- Korean labels: `0.15–0.18em`

### Hierarchy Rules
- Within any component, only **one** element uses Playfair Display (the headline). All supporting text uses Karla.
- Metadata (dates, company names, tags) must be visually subordinate to the headline — always `label` or `caption` size, always muted color (`--warm-gray` or `--taupe`).
- No inline font styles. All typography is controlled through CSS classes.
- Noto Serif KR is reserved exclusively for Korean-language text and decorative Korean characters.

### Optical Alignment
When Playfair Display headings stack above Karla body text, the serif glyphs have wider left-side bearing than the sans-serif, creating a subtle visual misalignment even though both share the same box-model edge. To compensate:
- Playfair headings at display size (2.5rem+): `text-indent: -0.04em`
- Playfair headings at heading size (1.3rem): `text-indent: -0.03em`
- This is applied to: `.hero-title`, `.exp-role`, `.essay h3`

### Section Header Pattern
All three content sections (Experience, Living, Writing) use the same bilingual header component:

**Bilingual section header**: Korean decorative character + English heading + horizontal rule, in a three-column grid (`auto auto 1fr`), bottom-aligned. Korean character uses `Noto Serif KR` weight 200 at 3.5rem; English heading uses `Playfair Display` at 1.8rem. Grid gap: 1.5rem. On tablet: English drops to 1.3rem. On mobile: collapses to single column, rule hidden, English at 1.3rem.

All three use the same CSS class (`section-head-*`). Experience's parent (`work-section`) has no horizontal padding, so it gets an override: `.work-section .section-head { padding: 0 10vw; }`.

| Section | Korean Character | English Heading |
|---------|-----------------|-----------------|
| Experience | 경험 | Experience |
| Living | 삶 | Living |
| Writing | 글 | Writing |

**Footer header**: Korean label above (`Noto Serif KR` 1.4rem, persimmon) + English heading below (`Playfair Display` 3rem). Centered layout, intentionally distinct from section headers.

### Accent Color Rule
**Persimmon** (`--persimmon`, #C07A6E) is the single accent/highlight color. It is used for: link hover states, name highlights ("Christine"), interlude emphasis ("works"), pull-quote borders, date labels, active tabs, Korean labels, and the footer. There is no secondary accent color for emphasis — amber (`--amber`) is reserved exclusively for decorative wash gradients at low opacity and should never be used for text or interactive elements.

### Content Grid
All content sections share a horizontal margin of `10vw` on desktop, `6vw` on tablet, `5vw` on phone. The hero section's `padding-left: 10vw` aligns its text with section headers below. The norigae is positioned at `left: calc(10vw - 14px)` to sit at the content edge.

### Metadata Colors
All metadata text (dates, company names, tags) uses a consistent muted palette:
- Dates: `var(--warm-gray)` across all sections
- Company/org names: `var(--warm-gray)`
- Tags (current/contract): `var(--warm-gray)`, italic
- Category tags: `var(--celadon)`, uppercase
- Experience date labels: `var(--persimmon)` (the only metadata that uses an accent color, because it serves as a section-level timestamp)


## 4. Component Stylings

### Navigation Bar
- Fixed to top, full width
- Background: Hanji at 94% opacity with 4px backdrop blur (frosted glass)
- Border bottom: 1px solid `rgba(200, 188, 168, 0.25)`
- Padding: `2rem 5vw` (desktop), `1rem 4vw` (mobile)
- Logo: Korean name (Noto Serif KR 400) + English name (Playfair Display 400, Ink Soft)
- Link hover: Persimmon underline slides in from left, `width .5s cubic-bezier(.25,.1,.25,1)`

### Hero Section
- Full viewport height, flexbox centered
- Welcome label: Karla 0.75rem, Persimmon, letter-spaced — uses Karla (not Noto Serif KR) because this is English text
- Title: Playfair Display with `text-indent: -0.04em` for optical alignment
- Profile photo: circular with `clip-path: inset(0 0 18% 0)` for flat base crop, heavy shadow (`0 12px 28px`)
- Background character (韓): absolutely positioned, Noto Serif KR weight 200, Hanji Warm color, purely decorative
- Staggered fade-in animations: label → title → description → photo, delays 0.1s–0.45s

### Experience Cards (Silk Road)
- Absolutely positioned along a winding SVG path
- Alternating left/right alignment with text-alignment flip
- Marker dot: 10px circle, Persimmon fill, Hanji border, rgba halo
- Card max-width: 340px
- Color wash: 0.2 opacity gradient behind each card (alternating palette colors)
- No hover transform (intentionally disabled to avoid suggesting clickability)

### Essay List Items
- Three-column grid: `auto 1fr auto` (number, title, date)
- Bottom border: 1px solid Hanji Warm
- Hover: left padding shifts 1.2rem, title color shifts to Persimmon
- "Show more" toggle reveals hidden items with `hidden-essay` class

### Photo Collage
- Container: `aspect-ratio: 3/4`, relative positioning
- 10 images absolutely positioned with rotation transforms (-3° to +3°)
- Images overlap at varied z-index levels (2–11)
- Hover: `scale(1.04)` with elevated shadow, z-index jumps to 20
- Fallback placeholder: gradient from Hanji Warm to Mauve with centered Korean character (삶)

### Writing Category Tabs
- Horizontal flex row with `2rem` gap
- Active state: Persimmon text color, underline slides in (same animation as nav)
- Inactive: Taupe color

### Buttons
- Text-only style (no background, no fill)
- Font: Karla, 0.78rem, letter-spaced, lowercase
- Color: Persimmon
- Hover: opacity 0.7
- Password page buttons: 1px Ink Soft border, 4px radius, hover fills with Ink background

### Links
- Inline links: Persimmon color, transparent bottom border that appears on hover
- Nav links: Ink Soft color, Persimmon underline grows on hover
- Footer links: Warm Gray, shift to Persimmon on hover

### Cards/Containers
- No visible card borders
- Elevation through subtle box-shadow only
- Border radius: 3–4px for practical corners, 50% for circular elements
- Background differentiation through opacity washes rather than border/fill


## 5. Layout Principles

### Grid System
- No formal column grid. Layout is section-based with generous horizontal padding.
- Desktop horizontal padding: `10vw` → tablet `6vw` → phone `5vw`
- Content max-width: `min(1120px, 90vw)` on hero
- About section: asymmetric two-column grid `0.9fr 1.1fr` with `4rem` gap. **Note:** Because grid `gap` already provides spacing between items, `.about-section > .section-head` uses `margin-bottom: 0` to avoid compounding with the grid gap. The `4rem` margin-bottom on `.section-head` only applies in non-grid parent contexts (Writing, Experience).
- All section headers: `auto auto 1fr` grid (Korean, English, decorative line)

### Spacing Scale

All spacing values in the site are drawn from this scale. No ad-hoc values.

| Token | Value | Usage |
|-------|-------|-------|
| `space-xs` | 0.25rem (4px) | Micro: exp-company margin-top |
| `space-sm` | 0.5rem (8px) | Tight: date margins, tag margins |
| `space-md` | 1rem (16px) | Standard: label margins, paragraph gaps, adjacent element spacing |
| `space-lg` | 1.5rem (24px) | Component internal: card padding, heading gaps, section-head grid gap |
| `space-xl` | 2rem (32px) | Nav padding, essay row padding, writing-tabs gap |
| `space-2xl` | 3rem (48px) | Section padding, nav-link gap, footer-links gap |
| `space-3xl` | 4rem (64px) | Section internal: section-head margin-bottom (non-grid contexts), about-section grid gap |
| `space-4xl` | 8rem (128px) | Section external: footer top padding |

### Vertical Section Rhythm
All content sections use fixed `3rem` (48px) vertical padding — never viewport-relative units like `vh`, which produce unpredictable gaps across screen sizes. Sections flow directly into one another, yielding a consistent ~96px section-to-section gap (48px bottom pad + 48px top pad).

**Why fixed rem, not vh:** Reference design systems (Apple HIG, Figma, Notion, Spotify) all use fixed spacing units (8px base). Viewport-relative vertical spacing causes the same layout to feel cramped on short screens and oversized on tall ones.

- Hero: `min-height: 100vh`, `padding-top: 9.5rem` (accounts for fixed nav), `padding-bottom: 3rem`
- Experience: `padding: 3rem 0` (no horizontal padding — silk road needs full width)
- Interlude: `padding: 3rem 0`
- Living: `padding: 3rem 10vw`
- Writing: `padding: 3rem 10vw`
- Footer: `padding: 8rem 10vw 3rem`

**Responsive overrides** (tablet ≤1200px, phone ≤600px): section padding reduces to `2rem`.

### Responsive Breakpoints
- **1200px** (tablet): single-column about, linearized experience, `6vw` padding
- **600px** (phone): stacked hero, compact nav, single-column headers, `5vw` padding
- **380px** (small phone): further font size and gap reductions


## 6. Depth & Elevation

Shadows use exclusively warm-toned `rgba(44, 37, 29, ...)` (the Ink color) rather than black. Five levels:

| Level | Shadow | Usage |
|-------|--------|-------|
| `elevation-0` | none | Most elements, flat design default |
| `elevation-1` | `0 2px 12px rgba(44,37,29,0.12)` | Collage images at rest |
| `elevation-2` | `0 6px 24px rgba(44,37,29,0.2)` | Collage images on hover |
| `elevation-3` | `0 12px 28px rgba(44,37,29,0.18)` | Hero profile photo |
| `glow` | `0 0 0 4px rgba(192,122,110,0.15)` | Experience marker dot halo (Persimmon-based) |

### Texture Overlays
- Hanji paper texture: SVG fractal noise filter at 7% opacity, fixed position, full viewport
- Warm radial gradients: two overlapping at 6–8% opacity for subtle color variation


## 7. Animation & Motion

### Entrance Animations
All entrance animations use `forwards` fill mode (element stays at final state).

| Element | Animation | Duration | Delay | Easing |
|---------|-----------|----------|-------|--------|
| Hero hangul (韓) | fadeIn | 1.2s | 0.2s | ease |
| Norigae | fadeIn | 1s | 0.4s | ease |
| Hero label | fadeUp | 0.6s | 0.1s | ease |
| Hero title | fadeUp | 0.7s | 0.25s | ease |
| Hero description | fadeUp | 0.7s | 0.45s | ease |
| Hero photo | fadeUp | 0.7s | 0.35s | ease |

### Scroll Reveals
- All `.reveal` elements: `opacity 0 → 1`, `translateY(22px) → 0`
- Duration: 1s, easing: `cubic-bezier(.25,.1,.25,1)`
- Triggered by IntersectionObserver at 6% threshold

### Scroll-Driven Animations
- Silk road path: draws along stroke-dashoffset as user scrolls through experience section

### Hover Transitions
- Standard color transitions: `0.3s ease`
- Nav/essay underline growth: `0.4–0.5s cubic-bezier(.25,.1,.25,1)`
- Collage image scale: `0.4s ease`
- Essay padding shift: `0.4s ease`

### Guardrails
- Never use bounce or elastic easing — motion should feel smooth and restrained
- Entrance delays should never exceed 0.5s total — the hero should feel snappy
- Scroll animations should be subtle and not block content visibility


## 8. Decorative Elements

### Norigae (노리개)
SVG tassel ornament hanging from the nav area on the left side. Uses Persimmon and Amber tones with gradient fills. Hidden on mobile (below 600px).

### Silk Road Path
Winding SVG bezier curve connecting experience stops. Stroke: Wood Light at 0.5 opacity. Glow layer: Persimmon at 0.2 opacity. Draws progressively as user scrolls.

### Custom Cursor (무궁화)
Rose of Sharon (mugunghwa, Korea's national flower) SVG replaces the default cursor on desktop. Scales up and rotates 15° on hoverable elements. Hidden on touch devices.
