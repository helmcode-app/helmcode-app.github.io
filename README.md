# HelmCode Official Website (`helmcode-app.github.io`)

The official landing page, documentation, Terms of Service, and Privacy Policy for **HelmCode** — the mobile-first iPad AI coding console.

Built with **Jekyll** and hosted natively on GitHub Pages.

## Directory Structure

```
.
├── _config.yml         # Jekyll site configuration
├── Gemfile             # Ruby dependencies for local preview
├── _includes/          # Reusable components (head, nav, footer)
├── _layouts/           # Page templates (default, page)
├── assets/
│   ├── css/style.css   # Modern dark-mode developer aesthetics
│   ├── images/         # Official App Icon & media assets
│   └── js/main.js      # Responsive navigation, FAQ accordions, interactions
├── index.html          # Main landing page (iPad mockup, features, arch, quickstart)
├── terms.md            # Terms of Service (/terms/)
├── privacy.md          # Privacy Policy (/privacy/)
└── 404.html            # Custom 404 page
```

## Local Development

If you have Ruby & Bundler installed:

```bash
bundle install
bundle exec jekyll serve
```

Then visit [http://localhost:4000](http://localhost:4000).

## Deployment

Pushes to `main` branch automatically deploy via GitHub Pages.
