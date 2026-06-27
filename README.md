# Ranjan Kumar Jena — Portfolio Website

A professional DevOps Engineer portfolio — static, single-origin HTML/CSS/JS.  
No build tools, no npm, no frameworks. Drop files and serve.

---

## Repo Structure

```
portfolio/
├── index.html                  ← Main landing page
├── css/
│   ├── style.css               ← Global styles
│   └── detail.css              ← Project detail page styles
├── js/
│   └── main.js                 ← Nav highlight, minor interactions
├── pages/
│   ├── project-ecommerce.html  ← Detail: E-Commerce platform
│   ├── project-gps.html        ← Detail: GPS Tracking platform
│   └── project-template.html  ← ✏️ Copy this for new projects
└── assets/
    └── screenshots/            ← Drop project screenshots here
```

---

## Adding a New Project

### Step 1 — Add a card in `index.html`

Copy the block below and paste it before the `project-card--add` div inside `#projects`:

```html
<div class="project-card">
  <div class="project-header">
    <div class="project-status"><span class="dot green"></span>Production</div>
    <div class="project-num">03</div>   <!-- increment number -->
  </div>
  <h4 class="project-title">Your Project Title</h4>
  <p class="project-desc">
    Short description of what the project does and the problem it solves.
  </p>
  <div class="project-tags">
    <span>AWS</span><span>Docker</span><span>Kubernetes</span>
  </div>
  <div class="project-footer">
    <div class="project-highlights">
      <span>↓ XX% some metric</span>
      <span>Key achievement</span>
    </div>
    <a href="pages/project-yourname.html" class="btn-detail">Full Details →</a>
  </div>
</div>
```

### Step 2 — Create a detail page

Copy `pages/project-template.html` → `pages/project-yourname.html`  
Fill in all `✏️  EDIT` sections.

### Step 3 — Add screenshots

Drop image files into `assets/screenshots/` and uncomment the `<img>` tags in the detail page.

---

## Deployment

### NGINX

```nginx
server {
    listen 80;
    server_name yourdomain.com;

    root /var/www/portfolio;
    index index.html;

    location / {
        try_files $uri $uri/ =404;
    }
}
```

Upload the `portfolio/` folder contents to `/var/www/portfolio/` (or wherever your NGINX root points).

### Apache Tomcat (as a static webapp)

1. Zip the `portfolio/` folder as `ROOT.war` (or `portfolio.war`):
   ```bash
   cd portfolio
   zip -r ../portfolio.war .
   ```
2. Drop the `.war` into `$CATALINA_HOME/webapps/`.
3. Access at `http://your-server:8080/portfolio/` (or `http://your-server:8080/` if using `ROOT.war`).

### AWS S3 Static Hosting (optional)

```bash
aws s3 sync portfolio/ s3://your-bucket-name/ --delete
aws s3 website s3://your-bucket-name/ --index-document index.html
```

---

## Customization Quick Reference

| What to change | Where |
|---|---|
| Name / title / tagline | `index.html` → hero section |
| Contact details | `index.html` → `#contact` section |
| Skills list | `index.html` → `#skills` section |
| Work history bullets | `index.html` → `#experience` section |
| Project cards | `index.html` → `#projects` section |
| Project detail pages | `pages/project-*.html` |
| Colors / fonts | `css/style.css` → `:root` variables |
| Nav brand initials | `index.html` → `.nav-brand` |
| Footer copyright year | `index.html` + `pages/*.html` → `footer` |

---

## Color Palette

| Variable | Hex | Usage |
|---|---|---|
| `--bg` | `#0d1117` | Page background |
| `--bg-alt` | `#131920` | Alternate sections |
| `--bg-card` | `#161d27` | Cards |
| `--accent` | `#3b82f6` | Blue accent, links |
| `--text` | `#d1d9e6` | Body text |
| `--text-muted` | `#6b7a8d` | Secondary text |
| `--green` | `#22c55e` | Status indicators |
