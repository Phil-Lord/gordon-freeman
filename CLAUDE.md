# CLAUDE.md — Gordon Freeman: Freelance Operative

## Project Overview

This is a practice project and learning exercise. The site is a fictional portfolio/CV for Gordon Freeman — Theoretical Physicist and Freelance Crowbar Operative — built as a mock brochure site with a Half-Life theme.

The primary goal is not the content itself but hands-on familiarity with a modern static site stack, from local development through to live deployment, so that future sites can be built and shipped quickly and confidently.

---

## Tech Stack

- **Framework:** Astro (static output, minimal JavaScript)
- **CSS:** Tailwind CSS
- **Component library:** shadcn/ui (Radix, Nova preset)
- **Hosting:** Netlify (deployed via GitHub — every push to main deploys automatically)
- **Forms:** Netlify Forms
- **Domain:** Namecheap (or Netlify subdomain for practice)

---

## Learning Goals

This project exists to build practical familiarity with each layer of the stack. When making changes or adding features, prefer approaches that exercise the stack deliberately over the quickest possible solution.

### Core skills to practise

- **Astro fundamentals** — pages, layouts, components, content collections, and static routing
- **Tailwind CSS** — utility-first styling, responsive design, and mobile-first layout
- **shadcn/ui** — integrating and customising components within an Astro project
- **Netlify deployment** — build pipeline, environment variables, deploy previews, and branch deploys
- **Netlify Forms** — form handling without a backend, including the required `netlify` attribute and spam filtering

### Features to add over time

- A working contact form (Netlify Forms) with basic validation
- Responsive navigation with a mobile menu
- A services or skills section using shadcn card components
- An "About" or bio page
- Lighthouse performance optimisation — target 90+ across all categories
- Image optimisation using Astro's built-in `<Image />` component
- A simple content collection (e.g. past "missions" or projects) using Astro's MDX support
- An embedded third-party widget (e.g. a booking tool or calendar)

---

## Site Structure

```
/                  → Hero / landing page
/about             → Bio and background
/services          → What Gordon offers
/contact           → Contact form (Netlify Forms)
```

---

## Conventions

- Keep components small and single-purpose
- Use Tailwind utilities directly — avoid custom CSS unless necessary
- Prefer Astro `.astro` components; use React only if a shadcn component requires it
- No unnecessary dependencies — this is a brochure site, not an app
- All pages should be statically rendered (no SSR)

### Component structure

- Co-locating markup, `<style>`, and `<script>` in a single `.astro` file is idiomatic — don't split files preemptively
- Extract a component when the behaviour is reused across pages, or when a page is growing large enough that a self-contained feature is hurting readability
- A well-formed component owns its template, its styles, and its script in one file, and exposes behaviour via props

### Client-side scripts in `.astro` components

- Prefer plain `<script>` blocks — they are bundled by Vite (tree-shaken, type-checked) and run once on page load
- To pass a prop into a `<script>`, set a `data-*` attribute on a template element and read it in the script. **Avoid `define:vars`**, which forces the script inline and disables bundling
- Use `document.querySelectorAll(...)` over `getElementById` inside component scripts, so the same component can appear multiple times on a page without conflict
- Lift magic numbers (counts, sizes, timings) to named constants at the top of the script — easy to promote to props later

### Styles in `.astro` components

- `<style>` blocks are scoped by default — class names and `@keyframes` are hashed to the component
- Prefer scoped styles. Reach for `is:global` only when a script creates DOM elements at runtime that need styling (scoped classes won't apply to elements the template didn't author)
- When using `is:global`, namespace class and keyframe names clearly (e.g. `crowbar-stage`, `crowbar-fall`) to make collisions effectively impossible

---

## Deployment

- **Repo:** GitHub (main branch triggers production deploy)
- **Build command:** `astro build`
- **Publish directory:** `dist`
- **Node version:** 18+

Netlify deploy previews are available for all pull requests. Use these to test changes before merging.

---

## Notes for Claude Code

- This codebase is intentionally simple — avoid suggesting architectural patterns suited to larger applications
- When adding new UI, prefer shadcn components over building from scratch
- Netlify Forms requires a plain HTML `<form>` element with a `netlify` attribute (or `data-netlify="true"`) and a hidden `form-name` input to be detected at build time — keep this in mind when working on the contact page
- Tailwind class ordering: follow the conventional order (layout → spacing → typography → colour → effects)