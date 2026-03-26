# Personal Resume Page Implementation Plan

> **For agentic workers:** REQUIRED SUB-SKILL: Use superpowers:subagent-driven-development (recommended) or superpowers:executing-plans to implement this plan task-by-task. Steps use checkbox (`- [ ]`) syntax for tracking.

**Goal:** Build a clean, fully responsive personal resume website for Ming Wan showcasing Apache APISIX, deployable to GitHub Pages.

**Architecture:** Single HTML file with embedded CSS (no build process required). Semantic HTML structure with flexbox/grid layout. Pure CSS media queries for responsiveness. No JavaScript initially; enhanced with vanilla JS for future interactivity if needed.

**Tech Stack:** HTML5, CSS3 (Flexbox, CSS Grid, Media Queries), pure frontend, GitHub Pages deployment.

---

## File Structure

**Files to Create:**
- `resume/index.html` — Main page (HTML + embedded CSS)
- `resume/README.md` — Deployment and customization guide
- `resume/.gitignore` — Standard GitHub ignore

**Deliverable Location:** 
```
/home/rain/learn_ai/superpowers/chapter_1/resume/
```

---

## Task Breakdown

### Task 1: Clean Up Prototype and Create Production Index

**Files:**
- Modify: `resume/index.html` (finalize from prototype)

The prototype at `resume-prototype/index.html` is a good starting point. This task makes it production-ready by:
- Replacing placeholder content with real information
- Adding actual GitHub/social links
- Adding APISIX project details accurately
- Verifying semantic HTML structure

- [ ] **Step 1: Review current prototype**

Run: `cat /home/rain/learn_ai/superpowers/chapter_1/resume-prototype/index.html | head -50`

Verify it has all sections and proper structure.

- [ ] **Step 2: Update hero section with real content**

In `index.html`, replace placeholder social links with actual ones:

```html
<div class="social-links">
  <a href="https://github.com/wingsxdu" target="_blank">GitHub</a>
  <a href="https://twitter.com/wingsxdu" target="_blank">Twitter/X</a>
  <a href="https://www.linkedin.com/in/mingwan/" target="_blank">LinkedIn</a>
  <a href="mailto:mingwan@example.com">Email</a>
</div>
```

Also update bio if needed:
```html
<p class="hero-bio">Open source contributor dedicated to building high-performance API infrastructure and advancing cloud-native technologies through community-driven innovation.</p>
```

- [ ] **Step 3: Update about section**

Replace placeholder with real summary (2-3 sentences about Ming Wan's background, expertise in API infrastructure, open-source contributions).

- [ ] **Step 4: Verify APISIX project details**

Ensure the featured project has correct information:
- GitHub link: `https://github.com/apache/apisix`
- Official website: `https://apisix.apache.org/`
- Tech stack accurate: Lua, Go, OpenResty
- Star count: ~10,000+ (update if higher)

- [ ] **Step 5: Update experience section**

Fill in accurate dates, titles, descriptions for:
- Current: Full-time APISIX Maintainer & CTO (2019-Present)
- Previous roles as needed

- [ ] **Step 6: Add talks/writing links**

Update the Talks section cards with real links:
- GitHub profile
- Medium or personal blog
- YouTube or conference video platform

- [ ] **Step 7: Verify all links open correctly**

Open `index.html` in browser and manually click each link (GitHub, Twitter, LinkedIn, Email, GitHub profile in Talks, etc.)

Expected: All links open in correct tab/app without errors

- [ ] **Step 8: Commit**

```bash
cd /home/rain/learn_ai/superpowers/chapter_1/resume
git add index.html
git commit -m "feat: create production resume index with real content"
```

---

### Task 2: Refactor CSS for Maintainability (Optional: Extract to Separate File)

**Files:**
- Create: `resume/styles.css` (optional, for cleaner separation)
- Modify: `resume/index.html` (link to external stylesheet)

**Decision:** For simplicity and GitHub Pages deployment, keep CSS inline in HTML. Skip this task unless CSS grows beyond 500 lines.

- [ ] **Step 1: Verify CSS is not bloated**

Run: `grep -c "^\s*\." /home/rain/learn_ai/superpowers/chapter_1/resume/index.html`

If count < 100 CSS rules, skip extraction. Otherwise proceed.

- [ ] **Step 2: If extraction needed, create styles.css**

Move all CSS from `<style>` block in HTML to `resume/styles.css`.

```html
<!-- In index.html -->
<link rel="stylesheet" href="styles.css">
```

- [ ] **Step 3: Test in browser**

Open `resume/index.html` in browser, verify styling intact.

Expected: Page looks identical to inline CSS version, no layout breaks.

- [ ] **Step 4: Commit**

```bash
git add resume/index.html resume/styles.css
git commit -m "refactor: extract CSS to separate stylesheet for maintainability"
```

---

### Task 3: Test Responsive Design Across Breakpoints

**Files:**
- No new files (testing existing index.html)

Browser DevTools will be used to simulate devices.

- [ ] **Step 1: Test desktop view (≥ 1024px)**

Open `http://localhost:8888` in browser.
Window width: 1440px (or full screen on large monitor)

Check:
- Hero name size is large (52px)
- Sections have proper spacing (80px gaps)
- APISIX project is featured prominently
- All sections readable with comfortable margins

Expected: Professional appearance, good use of space.

- [ ] **Step 2: Test tablet view (768px - 1023px)**

DevTools: Simulate iPad (768px width)

Check:
- Font sizes scaled down appropriately
- Padding adjusted (32px)
- Projects grid shows 2 columns (if applicable)
- All text still readable

Expected: No horizontal scroll, proper line-wrapping.

- [ ] **Step 3: Test mobile view (< 768px)**

DevTools: Simulate iPhone (375px width)

Check:
- Single column layout enforced
- Font sizes readable (14px base)
- Links have sufficient touch target (44px+)
- Spacing still comfortable
- Hero name wraps if needed (no truncation)
- Experience timeline readable on small screen

Expected: No horizontal scroll, all text readable, links tappable.

- [ ] **Step 4: Test actual phones (if available)**

Open resume on real iPhone/Android device.

Expected: Matches DevTools simulation, no browser quirks.

- [ ] **Step 5: Test zoom functionality**

On mobile, pinch-zoom to 200%, then zoom out to 50%.

Expected: Page remains usable at all zoom levels, no broken layout.

- [ ] **Step 6: Test landscape orientation**

Rotate mobile to landscape.

Expected: Layout adapts smoothly, readable at landscape width.

- [ ] **Step 7: Document findings**

No code change needed. If issues found, log them for next iteration.

---

### Task 4: Performance Check and Optimization

**Files:**
- Verify: `resume/index.html`

- [ ] **Step 1: Measure file size**

Run: `du -h /home/rain/learn_ai/superpowers/chapter_1/resume/index.html`

Expected: < 50 KB (single HTML file with embedded CSS)

- [ ] **Step 2: Measure page load time**

Open DevTools Network tab, refresh page, check waterfall.

Expected: First Contentful Paint < 1 second on 3G throttle (DevTools setting).

- [ ] **Step 3: Optimize if needed**

If load time > 2s:
- Remove unused CSS rules
- Compress inline images (if any)
- Minify CSS/HTML (optional for static site)

For a resume site, performance is typically not an issue. Skip unless needed.

- [ ] **Step 4: Check accessibility**

Run: Axe DevTools or WAVE browser extension on `index.html`

Check for:
- Color contrast: #fff on #0a0a0a should pass WCAG AAA
- Missing alt text (if images present)
- Missing form labels (if form present)

Expected: 0 critical issues, max 2-3 minor warnings.

---

### Task 5: Prepare for GitHub Pages Deployment

**Files:**
- Create: `resume/README.md` (deployment guide)
- Create: `resume/.gitignore`
- Verify: GitHub repository setup

- [ ] **Step 1: Create README.md with deployment instructions**

```markdown
# Ming Wan's Resume

A clean, minimal personal resume website built with HTML and CSS.

## Features
- Dark theme with professional styling
- Fully responsive (mobile, tablet, desktop)
- Pure frontend (no build process)
- Hosted on GitHub Pages

## Deployment to GitHub Pages

### Option 1: Use this repo directly
1. Ensure `index.html` is in root or in a `docs/` folder
2. Go to Repository Settings → Pages
3. Select source: "Deploy from a branch"
4. Branch: `main`, folder: `/ (root)` or `docs`
5. Save

Your site will be live at: `https://<username>.github.io/<repo-name>/`

### Option 2: Use a separate domain
Configure custom domain in Pages settings.

### Local Testing
```bash
cd resume
python3 -m http.server 8000
# Open http://localhost:8000
```

## Customization

Edit `index.html` to update:
- Name and role in hero section
- About section text
- Project details
- Experience entries
- Social links

All styles are inline in the `<style>` tag.

## Browser Support
- Chrome 90+
- Firefox 88+
- Safari 14+
- Edge 90+

## License
Personal website. No license needed.
```

- [ ] **Step 2: Create .gitignore**

```
# Node (if installing any packages in future)
node_modules/
package-lock.json

# IDE
.vscode/
.idea/

# OS
.DS_Store
Thumbs.db

# Local development
*.swp
*.swo
```

- [ ] **Step 3: Ensure GitHub repo is set up**

If not already done:
```bash
cd /home/rain/learn_ai/superpowers/chapter_1/resume
git init
git remote add origin https://github.com/<YOUR_USERNAME>/<REPO_NAME>.git
git branch -M main
```

- [ ] **Step 4: Push to GitHub**

```bash
git add .
git commit -m "docs: add deployment guide and gitignore"
git push -u origin main
```

- [ ] **Step 5: Enable GitHub Pages**

Navigate to: Settings → Pages
- Source: "Deploy from a branch"
- Branch: `main`, folder: `/ (root)`
- Save

Expected: "Your site is live at https://..." message appears.

- [ ] **Step 6: Verify site is live**

Open the GitHub Pages URL in browser (may take 1-2 minutes to appear).

Expected: Resume loads and displays correctly.

---

### Task 6: Create Optional Enhancements (Future)

**Files:**
- Not created in this plan

**Scope for future iterations:**
- Smooth scroll navigation
- Dark/light mode toggle (though brief specifies dark-only)
- Printable version (CSS `@media print`)
- Animation on scroll
- Analytics tracking
- SEO meta tags optimization

For now, skip these enhancements. Focus on solid foundation.

---

## Summary of Deliverables

✅ Production-ready `resume/index.html`  
✅ Fully responsive design (tested at 3 breakpoints)  
✅ Performance optimized (< 1s load)  
✅ Accessibility compliant (WCAG AA+)  
✅ `README.md` with deployment guide  
✅ `.gitignore` for clean repo  
✅ Deployed and live on GitHub Pages  

---

## Execution Options

Plan complete and saved to `docs/superpowers/plans/2026-03-25-resume-implementation.md`.

**Two ways to execute this plan:**

**1. Subagent-Driven (Recommended)**
- I dispatch a fresh subagent for each task
- Review after each task (functionality + code quality)
- Fast iteration, parallel processing possible

**2. Inline Execution**
- Execute all tasks in this session
- Batch review at checkpoints
- Simpler, but slower for large plans

**Which approach do you prefer?**
