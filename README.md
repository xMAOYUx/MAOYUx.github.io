# Matteo Steinbach - Personal Portfolio

Live Site: https://mattc-try.github.io

A modern, responsive portfolio website built with Astro + Tailwind CSS featuring light/dark mode, optimized for cryptography researchers and cybersecurity professionals.

---

## Quick Start

```bash
# Install dependencies
npm install

# Start development server
npm run dev

# Build for production
npm run build

# Preview production build
npm run preview
```

---

## How to Update Content

All portfolio content is centralized in **one file** for easy editing:

### src/data/portfolio.ts

| Section | What to Edit |
|---------|--------------|
| **Profile** | profile object - name, title, email, GitHub, LinkedIn, Signal, resume URL |
| **About** | about object - summary, highlights, research insight |
| **Publications** | publications array - add/edit academic papers |
| **Projects** | projects array - add/edit GitHub projects |
| **Reading List** | readingList object - description, PDF URL, highlights |
| **Conferences** | conferencePhotos array - add event photos |
| **Skills** | skillCategories array - tech stack categories |

### Example: Update Your Email
```typescript
export const profile = {
  email: "your-new-email@example.com",  // Change this
  // ...
};
```

### Example: Add a New Project
```typescript
{
  id: "my-new-project",
  title: "Project Name",
  description: "What it does...",
  techStack: ["Rust", "Python"],
  githubUrl: "https://github.com/mattc-try/repo-name",
  featured: true,
  category: "cryptography",
},
```

---

## Adding Files

| File Type | Location |
|-----------|----------|
| Resume/CV | public/cv/matteo-steinbach-cv.pdf |
| Paper PDFs | public/papers/your-paper.pdf |
| Conference Photos | public/images/conferences/ |
| Reading List PDF | public/reading-list.pdf |

---

## Deploy to GitHub Pages

### Step 1: Configure Astro for GitHub Pages

Edit astro.config.mjs:
```javascript
import { defineConfig } from 'astro/config';
import tailwindcss from '@tailwindcss/vite';

export default defineConfig({
  site: 'https://mattc-try.github.io',
  // If deploying to a subdirectory, add: base: '/repo-name/',
  vite: {
    plugins: [tailwindcss()],
  },
});
```

### Step 2: Create GitHub Actions Workflow

Create .github/workflows/deploy.yml:
```yaml
name: Deploy to GitHub Pages

on:
  push:
    branches: [main]
  workflow_dispatch:

permissions:
  contents: read
  pages: write
  id-token: write

jobs:
  build:
    runs-on: ubuntu-latest
    steps:
      - name: Checkout
        uses: actions/checkout@v4
      
      - name: Setup Node
        uses: actions/setup-node@v4
        with:
          node-version: 20
          cache: npm
      
      - name: Install dependencies
        run: npm ci
      
      - name: Build
        run: npm run build
      
      - name: Upload artifact
        uses: actions/upload-pages-artifact@v3
        with:
          path: ./dist

  deploy:
    needs: build
    runs-on: ubuntu-latest
    environment:
      name: github-pages
      url: ${{ steps.deployment.outputs.page_url }}
    steps:
      - name: Deploy to GitHub Pages
        id: deployment
        uses: actions/deploy-pages@v4
```

### Step 3: Enable GitHub Pages

1. Go to your repo > Settings > Pages
2. Under Build and deployment, select GitHub Actions
3. Push to main branch - site deploys automatically!

---

## SEO Optimization (Already Configured)

Your site includes these SEO features in src/layouts/Layout.astro:

### Meta Tags
- Title and Description
- Open Graph (Facebook, LinkedIn)
- Twitter Cards
- Canonical URL
- Robots meta

### To Customize SEO
Edit the head section in src/layouts/Layout.astro:
```html
<title>Matteo Steinbach | Cryptography Researcher</title>
<meta name="description" content="Your SEO description here" />
<meta property="og:title" content="Matteo Steinbach" />
<meta property="og:description" content="Cryptography Researcher..." />
<meta property="og:image" content="https://mattc-try.github.io/og-image.jpg" />
```

### Add an OG Image
1. Create a 1200x630px image
2. Save as public/og-image.jpg
3. Update the og:image meta tag

---

## Additional SEO Tips

### 1. Submit to Search Engines
- Google Search Console: https://search.google.com/search-console
- Bing Webmaster Tools: https://www.bing.com/webmasters

### 2. Create a Sitemap
Astro can auto-generate: npm run astro add sitemap

### 3. Add robots.txt
Create public/robots.txt:
```
User-agent: *
Allow: /
Sitemap: https://mattc-try.github.io/sitemap-index.xml
```

### 4. Performance
- Astro outputs static HTML (fast!)
- Tailwind purges unused CSS
- Images should be optimized (use WebP)

---

## Commands

| Command | Action |
|---------|--------|
| npm run dev | Start dev server at localhost:4321 |
| npm run build | Build to ./dist/ |
| npm run preview | Preview build locally |

---

## License

MIT License - Feel free to use as a template for your own portfolio!
