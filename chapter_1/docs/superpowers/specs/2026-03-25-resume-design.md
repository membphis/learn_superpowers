# Personal Resume Page Design Specification

**Date:** 2026-03-25  
**Version:** 1.0  
**Status:** Design Approved

---

## Executive Summary

Design a clean, minimal personal resume website for Ming Wan, Apache APISIX creator and CTO. The page showcases professional identity, key project (APISIX), work experience, technical talks, and contact information. Deliverable is a pure frontend, fully responsive site deployable to GitHub Pages.

---

## Design Principles

1. **Minimalism with Impact** — Dark theme (#0a0a0a), generous whitespace, large typography
2. **Content-First** — Information hierarchy through size and spacing, not decoration
3. **Engineer Aesthetic** — Monospace accents, subtle grid lines, code-like precision
4. **Fully Responsive** — Seamless experience on mobile (< 768px), tablet (768px-1023px), desktop (≥ 1024px)

---

## Visual Style

### Color Palette
```
Background:    #0a0a0a (deep black)
Text Primary:  #ffffff (white)
Text Secondary: #888888 (light gray)
Text Tertiary: #666666 (dark gray)
Border:        #222222 (subtle gray)
Accent:        #00d9ff (cyan) — for links, highlights
```

### Typography
- **Font Family:** System stack (-apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, etc.)
- **Hero Name:** 52px (desktop) / 36px (mobile), weight 700, letter-spacing -2px
- **Section Titles:** 28px (desktop) / 22px (mobile), weight 700, UPPERCASE, letter-spacing 2px
- **Body Text:** 16px (desktop) / 14px (mobile), line-height 1.6

### Spacing & Layout
- **Max Content Width:** 900px
- **Padding:** 40px (desktop) / 24px (mobile)
- **Section Gap:** 80px (desktop) / 60px (mobile)
- **Grid:** Single column (full-width responsive)

---

## Page Structure

### 1. Hero Section
**Purpose:** Immediate identity and role clarity

**Content:**
- Name: "Ming Wan" (large, bold)
- Role: "Apache APISIX Creator & CTO"
- Bio: 1-2 sentence professional summary
- Social Links: GitHub, Twitter/X, LinkedIn, Email

**Styling:**
- Border-bottom separator
- Extra bottom padding for visual closure
- Links: bordered pills with hover state

---

### 2. About Section
**Purpose:** Personal context and values

**Content:**
- 2-3 paragraphs describing background, expertise, and philosophy
- Emphasis on API infrastructure, cloud-native tech, community

**Styling:**
- Max-width 700px for comfortable reading
- Color: secondary gray
- Line-height: 1.8 for readability

---

### 3. Projects Section
**Purpose:** Showcase key work with APISIX as centerpiece

**Layout:**
- **APISIX (Featured):** Large card with gradient background
  - Project name (cyan accent color)
  - Founder/Lead role label
  - 3-4 sentence description
  - Meta grid (Tech Stack, Community, Status)
  - Links: GitHub, Official Website, Documentation

- **Other Projects (Optional):** 2-3 simple cards in grid layout
  - Title and brief description only
  - Hover state: border highlight + subtle background

**Styling:**
- Featured card: border + gradient background, larger font
- Meta items: left border accent, column layout responsive to grid
- Links: cyan with underline on hover

---

### 4. Experience Section
**Purpose:** Professional history with dual focus

**Structure (Dual-Track):**
- **Current Role (Highlighted):**
  - Timeline: "2019 – Present"
  - Title: "Full-time APISIX Maintainer & CTO"
  - Company: "Apache Software Foundation / APISIX Community"
  - Description: Key achievements and responsibilities
  - Visual indicator: colored dot (accent cyan)

- **Previous Experience (Simplified):**
  - Timeline, Title, Company, Brief Description
  - Visual indicator: hollow dot

**Styling:**
- Timeline bar (left border) with dots at each entry
- Responsive: adjust for mobile legibility
- Font: smaller than main content but still readable

---

### 5. Talks & Writing Section
**Purpose:** Direct visitors to distributed content

**Content:**
- Intro paragraph: "Search 'Ming Wan' or 'APISIX' to discover more..."
- Three link cards:
  - GitHub Profile (open-source work)
  - Technical Articles (blog/Medium)
  - Conference Talks (video)

**Styling:**
- Cards: border + hover highlight
- Links in cyan, opening in new tab
- Responsive grid (1-3 columns based on device width)

---

### 6. Contact Section
**Purpose:** Easy reach out

**Content:**
- Repeated social links from Hero section
- Simple layout for mobile thumb-friendly clicking

**Styling:**
- Centered
- Links: bordered pills with padding
- Flex wrap for mobile

---

## Responsive Breakpoints

### Desktop (≥ 1024px)
- Full typography sizes
- Generous padding and spacing
- Hero: single row layout
- Projects: featured card full-width, others in 3-column grid
- Experience: timeline with side-by-side layout

### Tablet (768px - 1023px)
- Typography: scaled down 10-15%
- Padding: 32px
- Projects: featured full-width, others in 2-column grid
- Experience: similar to desktop, slightly compressed

### Mobile (< 768px)
- Typography: base 14px
- Padding: 16px
- All grids: single column
- Projects: featured + stacked cards
- Experience: vertical timeline
- Links: larger touch targets (44px+ height)

---

## Technology Stack

- **Language:** HTML5 + CSS3 (no JavaScript required initially)
- **Framework:** None (vanilla frontend)
- **Hosting:** GitHub Pages (static site)
- **Build Process:** None (direct HTML/CSS deployment)
- **Performance Target:** < 1s first contentful paint

---

## Browser Support

- Modern browsers (Chrome, Firefox, Safari, Edge)
- Minimum ES5 (no polyfills needed for CSS Grid/Flexbox)
- Responsive via viewport meta tag + media queries

---

## Accessibility Considerations

- Semantic HTML (h1, h2, sections, etc.)
- Sufficient color contrast (#fff on #0a0a0a passes WCAG AAA)
- Links have visible focus states
- Responsive design supports zoom (user can scale to 200%)
- No auto-playing media

---

## File Structure

```
resume/
├── index.html           # Main page
├── styles.css          # (optional, can be inline in index.html)
├── README.md           # Deployment instructions
└── .gitignore
```

---

## Success Criteria

✓ Single HTML file (or cleanly separated HTML + CSS)  
✓ Responsive on mobile, tablet, desktop  
✓ Fast load (< 1s on 3G)  
✓ Professional appearance matching "clean, minimal, impactful" brief  
✓ Deployable to GitHub Pages without build step  
✓ All sections (Hero, About, Projects, Experience, Talks, Contact) visible and functional  
✓ APISIX featured prominently in Projects section  
✓ Social links functional  

---

## Next Steps

1. Generate detailed implementation plan (via writing-plans skill)
2. Implement HTML structure with CSS styling
3. Fill in actual content (replace placeholders with real data)
4. Test responsive layout across devices
5. Deploy to GitHub Pages
6. Iterate based on feedback

