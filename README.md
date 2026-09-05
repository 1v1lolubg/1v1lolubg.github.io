# The Orange Desk — Astro + Tailwind Blog

A production-ready, AdSense-compliant blog built with Astro Content Collections and Tailwind CSS.

## Getting started

```bash
npm install
npm run dev
```

Then open http://localhost:4321.

To build for production:

```bash
npm run build
npm run preview
```

## What's included

- **Content Collections** (`src/content/config.ts`) — strict Zod schemas for `blog` and `authors`, with `blog.author` as a typed reference to `authors`.
- **Responsive layout** (`src/layouts/BaseLayout.astro`) — sticky header, desktop nav, and a slide-out mobile drawer with a vanilla-JS toggle (no framework dependency), 48px minimum tap targets.
- **Blog layout** (`src/layouts/BlogLayout.astro`) — wraps articles with breadcrumbs and `prose prose-orange lg:prose-lg` typography.
- **Dynamic routes**:
  - `src/pages/blog/[...slug].astro` — renders markdown via `render(entry)`, includes Article JSON-LD, in-article ad slots, author box, and related posts.
  - `src/pages/author/[id].astro` — author profile with Person JSON-LD, qualifications, and their filtered article list.
- **AdSense mandatory pages** — `/about`, `/contact`, `/editorial-policy`, `/privacy-policy` (with AdSense/DART cookie clauses), `/terms`, `/disclaimer`.
- **`/editorial-team`** — E-E-A-T author showcase.
- **`public/ads.txt`** — placeholder ready for your real publisher ID.

## Before you deploy — replace these placeholders

1. **AdSense publisher ID**: search for `ca-pub-XXXXXXXXXXXXXXXX` (in `BaseLayout.astro` and `AdSlot.astro`) and `pub-0000000000000000` (in `public/ads.txt`) and replace with your real IDs.
2. **Ad slot IDs**: the `slotId` props on `AdSlot` in `[...slug].astro` (`1111111111`, `2222222222`) are placeholders — swap in real ad unit IDs from your AdSense account.
3. **Site URL**: update `site` in `astro.config.mjs` and `siteUrl` constants in `[...slug].astro` / `author/[id].astro` to your real domain.
4. **Images**: this repo ships without binary image assets. Add real files at the paths referenced in the sample markdown (e.g. `public/images/authors/john-doe.jpg`, `public/images/posts/budget-guide-cover.jpg`) or update the frontmatter `avatar` / `coverImage` fields to point at your CDN.
5. **Contact form**: the form in `/contact` posts to `/api/contact`, which isn't implemented (Astro's static output has no server by default). Wire it to a form backend (e.g. Formspree, Netlify Forms) or add an Astro server endpoint if you deploy with an adapter.
6. **Legal pages**: the privacy/terms/disclaimer copy is a solid starting template but is not legal advice — have a lawyer review before publishing, especially the AdSense/DART cookie clauses and any jurisdiction-specific requirements.

## Adding a new post

Create a new `.md` file in `src/content/blog/`, matching the frontmatter shape in `sample-post.md`. The `author` field must match the filename (slug) of a file in `src/content/authors/`.

## Adding a new author

Create a new `.md` file in `src/content/authors/`, matching `john-doe.md`.
