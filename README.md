# Best‑Locator Landing Page

Marketing website for **Best‑Locator**, the universal selector generator for UI testing.
This repository contains the **static landing page** (HTML/CSS/JS) that is deployed on Netlify.

> If you are looking for the CLI README (how to install and use the tool), see the product repository.
> The public install command for users is: `npm install -g bestlocator`.

---

## Table of Contents
- [Overview](#overview)
- [Live URLs](#live-urls)
- [Features](#features)
- [Project Structure](#project-structure)
- [Local Development](#local-development)
- [SEO & Metadata](#seo--metadata)
- [Content Editing Guide](#content-editing-guide)
- [Accessibility](#accessibility)
- [Deployment (Netlify)](#deployment-netlify)
- [Maintenance Checklist](#maintenance-checklist)
- [License](#license)

---

## Overview

- **Type**: Static site (no framework build required)
- **Purpose**: Product marketing + documentation entry points
- **Primary CTA**: Install via npm — `npm install -g bestlocator`

## Live URLs

- **Production**: `https://<your-domain>`
- **Netlify Site**: `https://<your-site>.netlify.app`
- **Preview Deploys**: Created per-branch/PR by Netlify

> Replace the placeholders above with your actual domains.

---

## Features

- Responsive layout with semantic HTML landmarks (`<header>`, `<main>`, `<section>`, `<footer>`)
- Hero with primary CTA
- Sections: Features, How it works, Frameworks, Selectors, Comparison
- Social meta: Open Graph + Twitter Cards
- JSON‑LD: `SoftwareApplication` and `FAQPage`
- Sitemap + Robots automatically generated (optional build step)
- Accessibility helpers (skip link, aria labels)

---

## Project Structure

```
.
├─ index.html              # Main entry (use this as the canonical page)
├─ index.seo.html          # SEO-optimized variant (for review or future split)
├─ robots.txt              # Crawler directives
├─ sitemap.xml             # Sitemap (can be generated at build time)
├─ INSTALL-SNIPPETS.md     # CLI install snippets (source for page content)
└─ assets/                 # Images, icons, CSS, JS (if applicable)
```

> If you don’t use `index.seo.html`, keep `index.html` as the only entry and ensure
> its `<head>` includes all the meta/schema you need.

---

## Local Development

No build step is required. You can open the HTML file directly in a browser or serve it locally.

```bash
# Option A: Open file directly (double click index.html)

# Option B: Serve with a simple HTTP server (recommended for relative paths)
# Python 3:
python -m http.server 8080
# Node (http-server):
npx http-server . -p 8080
```

Then visit: `http://localhost:8080`

---

## SEO & Metadata

- **Title & Description**: Keep them concise and aligned with the main keyword.
- **Canonical**: Ensure `<link rel="canonical">` points to the production URL.
- **Open Graph & Twitter**: Verify images exist and are under ~150 KB (recommended 1200×630).
- **JSON‑LD**:
  - `SoftwareApplication`: include `softwareVersion`, `downloadUrl`, `operatingSystem`, `applicationCategory`.
  - `FAQPage`: 3–5 questions that match content visible on the page.
- **Robots & Sitemap**: place both at site root. Submit `sitemap.xml` in Search Console.

> If you use Netlify, you can auto‑generate `robots.txt` and `sitemap.xml` during build.
> See `scripts/generate-seo.js` and `plugins/seo-verify/` (optional).

---

## Content Editing Guide

Common spots to update:

- **Hero CTA**: Keep command text in sync with the product — `npm install -g bestlocator`.
- **Features/Comparison**: Update bullets to reflect current product capabilities.
- **Docs Links**: Point “Documentation”/“View on GitHub” to the correct repositories.
- **FAQ**: Align the JSON‑LD and the visible FAQ questions/answers.

When adding sections:

1. Use `<section aria-labelledby="...">` and a unique heading `id`.
2. Prefer headings in order (H1 → H2 → H3).
3. Avoid duplicate IDs and ensure anchor links are unique.

---

## Accessibility

- Keep the **skip link** visible on focus.
- Provide **alt text** for images and role/labels where needed.
- Maintain sufficient **color contrast** (check with WCAG AA as a baseline).

---

## Deployment (Netlify)

**Option A — No build** (static publish):

- `netlify.toml`:
  ```toml
  [build]
  publish = "."
  command = "echo no-build"
  ```

**Option B — Generate SEO assets on build**:

- `netlify.toml`:
  ```toml
  [build]
  publish = "."
  command = "node scripts/generate-seo.js ."

  [[headers]]
  for = "/sitemap.xml"
    [headers.values]
    Content-Type = "application/xml; charset=utf-8"

  [[headers]]
  for = "/robots.txt"
    [headers.values]
    Content-Type = "text/plain; charset=utf-8"

  [[plugins]]
  package = "./plugins/seo-verify"
  ```

- Add the provided `scripts/generate-seo.js` and `plugins/seo-verify/` if you want
  generation + verification during deploy.

---

## Maintenance Checklist

- [ ] Update **canonical** and social links when the domain changes
- [ ] Verify **og:image/twitter:image** paths (exist, optimized)
- [ ] Keep **install command** text in sync: `npm install -g bestlocator`
- [ ] Re‑submit `sitemap.xml` to **Search Console** after major content changes
- [ ] Audit **accessibility** (headings order, contrast, focus states) on new sections

---

## License

Add your preferred license (e.g., MIT).

---

### Notes

- This README is for the **landing page repo**. The CLI README (usage, API, dev setup) should live in the CLI repository.
- If both live in a monorepo, include links between the packages/apps for clarity.
