# karlvelazquez.github.io

Karl Velazquez's personal website: career, research publications, teaching, hobbies, and
background. Built with [Astro](https://astro.build) as a static site and deployed to
[karlvelazquez.com](https://karlvelazquez.com) via GitHub Pages.

## Stack

- [Astro](https://astro.build) (static output), TypeScript
- Plain CSS with CSS custom properties, no framework
- Deployed via GitHub Actions to GitHub Pages (see `.github/workflows/deploy.yml`)

## Project structure

```
src/
  assets/images/   source photos (optimized by Astro's <Image /> at build time)
  components/      page sections (Hero, Career, Teaching, Life, Education, Footer, Header)
  layouts/         base HTML layout
  pages/           index.astro, the single page that assembles the sections
  styles/          global.css, design tokens and layout styles
public/
  CNAME            custom domain for GitHub Pages
knowledge-base/     research notes and source material (not part of the built site)
```

## Development

```bash
npm install
npm run dev       # start the local dev server
npm run build     # build the static site to dist/
npm run preview   # preview the production build locally
```

## Deployment

Pushing to `main` triggers `.github/workflows/deploy.yml`, which builds the site and publishes
`dist/` via GitHub Pages (the "GitHub Actions" Pages source, not a branch-based deploy). The
workflow can also be run manually via `workflow_dispatch`.
