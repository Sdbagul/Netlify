# Netlify

A simple static HTML site ready to be hosted on Netlify. This repository contains the source files for a lightweight static website (HTML, CSS, assets) and guidance for local development, Netlify deployment, and a few common Netlify features (redirects, headers, serverless functions).

## Table of contents

- [About](#about)
- [Preview](#preview)
- [Quick start](#quick-start)
- [Local development](#local-development)
- [Deploying to Netlify](#deploying-to-netlify)
- [Recommended files for Netlify](#recommended-files-for-netlify)
- [Netlify CLI (optional)](#netlify-cli-optional)
- [Custom domain & HTTPS](#custom-domain--https)
- [Project structure (example)](#project-structure-example)
- [Contributing](#contributing)
- [Troubleshooting](#troubleshooting)
- [License](#license)
- [Author](#author)

## About

This repository contains a static HTML website intended to be served from Netlify (or any static host). Use it as a personal site, project landing page, documentation, or marketing page.

## Preview

If you enable Git-based deployment in Netlify, your site will be available at:
- https://<your-site-name>.netlify.app

You can add screenshots to `assets/img/` and reference them below or in the repo README.

## Quick start

1. Clone the repo:
   ```bash
   git clone https://github.com/Sdbagul/Netlify.git
   cd Netlify
   ```

2. Open `index.html` in your browser to preview statically, or use a local server (recommended).

## Local development

- Quick local server (Python 3):
  ```bash
  python -m http.server 8000
  # open http://localhost:8000
  ```

- Using VS Code: install and run the "Live Server" extension and open `index.html`.

- If you have a build step (Sass, bundler, static site generator), run its build command before previewing.

## Deploying to Netlify

Two common ways:

1. Netlify Deploy via Git (recommended)
   - Push this repository to GitHub.
   - Go to https://app.netlify.com and "New site from Git".
   - Connect your Git provider (GitHub).
   - Select the repo `Sdbagul/Netlify`.
   - If the site is pure static HTML:
     - Build command: (leave blank)
     - Publish directory: `/` or `dist` depending on your repo structure
   - Click Deploy — Netlify will build and publish automatically on every push.

2. Netlify CLI / manual deploy
   - Install the Netlify CLI (see below) and use `netlify deploy` for quick previews or `netlify deploy --prod` for production.

## Recommended files for Netlify

- netlify.toml (optional): configures redirects, headers, functions, build settings
  ```toml
  [build]
    # If no build step, you can omit command
    publish = "public" # or "/" or "dist" depending on your repo
    # command = "npm run build"

  # Example redirect: rewrite all not-found routes to index.html (useful for SPAs)
  [[redirects]]
    from = "/*"
    to = "/index.html"
    status = 200
  ```

- _redirects (optional): simple redirect rules placed in the publish directory
  ```
  # Single file format
  /old-path  /new-path  301
  /*        /index.html  200
  ```

- _headers (optional): set custom HTTP headers
  ```
  /assets/*
    Cache-Control: public, max-age=31536000
  /index.html
    X-Frame-Options: DENY
  ```

- `netlify/functions/` (optional): serverless functions for backend logic (JS/TS)

## Netlify CLI (optional)

Install:
```bash
npm install -g netlify-cli
```

Common commands:
- Login:
  ```bash
  netlify login
  ```
- Connect a site or create one:
  ```bash
  netlify init
  ```
- Run local dev server (supports functions, redirects):
  ```bash
  netlify dev
  ```
- Deploy a draft:
  ```bash
  netlify deploy
  ```
- Deploy to production:
  ```bash
  netlify deploy --prod
  ```

## Custom domain & HTTPS

- In Netlify dashboard -> Site settings -> Domain management -> Add custom domain.
- Netlify provisions Let's Encrypt SSL automatically for verified domains.
- If using a subdomain, add CNAME or ALIAS records per Netlify instructions.

## Project structure (example)

Adjust to match your repository:

```
Netlify/
├─ index.html
├─ about.html
├─ contact.html
├─ assets/
│  ├─ css/
│  │  └─ styles.css
│  ├─ js/
│  │  └─ main.js
│  └─ img/
│     └─ screenshot.png
├─ netlify.toml         # optional
├─ _redirects           # optional
└─ README.md
```

If your published folder is `public` or `dist`, set the publish directory accordingly in Netlify settings or `netlify.toml`.

## Contributing

Contributions are welcome. Suggested workflow:
1. Fork the repository
2. Create a branch: `git checkout -b feat/awesome`
3. Make changes and commit
4. Push to your fork and open a Pull Request

Please include a description of the change and screenshots if the UI changed.

## Troubleshooting

- Not seeing changes after deploy:
  - Check that you committed and pushed to the branch Netlify is watching.
  - Verify the publish directory and build command in Site settings.
- Redirects not working:
  - Use `_redirects` or `netlify.toml` in the publish directory.
  - Confirm the file is included in the deployed build.
- Functions failing:
  - Ensure functions are placed in `netlify/functions` or configure `functions` directory in `netlify.toml`.

Useful logs:
- Deploy logs in Netlify dashboard
- Local logs with `netlify dev`

## License

If you want a permissive license, add a `LICENSE` file (e.g., MIT). This repo currently has no license specified.

## Author

Sdbagul

Contact: add your preferred contact method (email, Twitter, LinkedIn, etc.) here.

---

If you'd like, I can:
- Add a starter `index.html` and basic CSS,
- Generate a `netlify.toml` tailored to your repo layout,
- Create example `_redirects` or a serverless function scaffold.
Tell me which and I'll add it to the repo.
