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
