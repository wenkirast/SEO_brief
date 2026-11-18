# Brief for ChatGPT — Plumbing Co SEO Demo Site

Paste everything below the line into ChatGPT.

---

## Context

You are helping on a Next.js 15 demo site that shows, step by step, how to take a website from "AI scaffold" to "ranks on Google." It was built with Claude Code for a YouTube video ("50K Clicks/Mo with Claude Code"). The business is fictional: **Plumbing Co**, a Melbourne inner-south plumber (Prahran, est. 2009, 18,420 jobs, 4.9★ from 412 Google reviews). One extra page targets a US city (Baldwin Park, CA).

Repo: `wenkirast/SEO_brief`. Hosting: Vercel. Google Search Console verification file is already in `public/`.

## Stack and hard constraints

- Next.js 15 App Router, TypeScript, Tailwind CSS 3, React 19
- `output: 'export'`, `trailingSlash: true`, `images.unoptimized` — fully static; `out/` is the deployable
- Content lives in flat TS files in `content/`. No database, no CMS, no Supabase, no auth
- Never use `cookies()`, `headers()`, `searchParams`, `cache: 'no-store'`, `dynamic = 'force-dynamic'`, or API routes
- Any `[slug]` route needs `generateStaticParams`
- Images come from Pexels at build time via `node scripts/fetch-pexels.mjs` (env `PEXEL_API`), saved to `public/images/blog/<post>/<section>.jpg`, credits in `content/pexels.json`
- Design: premium, minimal, one accent colour (indigo), no emojis, no generic gradients
- Done = `npm run build` passes and every route is `○ (Static)`

## What each page demonstrates

| Route | Stage | Content |
|-------|-------|---------|
| `/` | Ch 2 — scaffold (the "v1") | Homepage: Hero, FeatureGrid, HowItWorks, Testimonials, ServiceAreas, FinalCta |
| `/blog`, `/services` | Ch 2 | Index pages |
| `/v2` | Ch 3a — AI slop | Post on `plumber for low water pressure`, written with no voice files |
| `/v3` | Ch 3b — voiced | Post on `plumber for running toilet`, written against `references/` |
| `/v4` | Ch 5 — landing page | `plumber baldwin park ca` city+service page, homepage layout, LocalBusiness schema |
| `/v5` | Ch 6a — on-page SEO | v3 post + TOC, breadcrumbs, author card, FAQ, Article/FAQPage/BreadcrumbList/Person JSON-LD, internal + external links |
| `/v6` | Ch 6b — technical SEO | v5 + sitemap, robots, canonical, OG/Twitter meta, Organization schema, Lighthouse-tuned, TechSeoScorecard |

## Key files

- `lib/business.ts` — single source of truth (name, NAP, hours, service areas, reviews, siteUrl)
- `content/blog-ai-slop.ts` (v2), `content/blog-voiced.ts` (v3/v5/v6, includes `faqs[]` and author), `content/landing-baldwin-park.ts` (v4), `content/toilet-repair.ts`
- `components/{site,home,blog,seo}/` — one component per file
- `lib/markdown.ts` — minimal markdown renderer
- `app/sitemap.ts`, `app/robots.ts`
- `on-page-seo.md` — 80+ item on-page checklist (v5/v6 must pass it)
- `references/` — voice layer (see below)
- `keywords.csv` (blog keywords), `Service-keywords.csv` (city+service keywords)
- `.claude/skills/blog` and `.claude/skills/service` — repeatable generators for new posts/landing pages
- `slideshow/*.html` — visual explainer slides used in the video

## Voice rules (apply to any copy you write)

Read `references/voice.md`, `humour.md`, `stats.md`, `stories.md`, `opinions.md` first. Writer persona is "Marco."

- Banned: "unlock", "leverage", "seamless", "world-class", "in today's fast-paced world", exclamation marks, emojis
- Lead with the answer, then context
- Only use numbers from `stats.md`; never round, never invent
- Max one story (from `stories.md`) and one opinion (from `opinions.md`, backed by a number) per piece
- Humour is dry and aimed at the industry, never puns
- Tell readers when NOT to hire us
- Before finishing, check `voice.md` → "Tells that it's AI-written" and remove matches

## Keyword rules

- Primary keyword must come from the CSV and must not already be in `references/used-keywords.md`
- Used so far: `plumber for low water pressure` (v2), `plumber for running toilet` (v3/v5/v6), `plumber baldwin park ca` (v4)
- Secondaries: CSV first, invent 4–5 same-intent ones only if missing; log the cluster in `used-keywords.md` before writing
- Blog posts: match format and length (±20%) of SERP top 3, cover what they all cover plus 1–2 gaps, answer at the top, FAQ from People Also Ask

## Known gaps / inconsistencies

- There is no `app/v1` folder; the homepage at `/` is the v1 scaffold
- `CLAUDE.md` says v4 is a toilet-repair page; the shipped v4 is the Baldwin Park landing page (`content/toilet-repair.ts` exists but is not the v4 source)
- README references `Plumbing-Keywords_list_2026-04-20 (1).csv`; the file in the repo is `keywords.csv`
- `project_specs.md` describes an earlier MDX-based plan (about/contact pages, `[slug]` routes) that was not built as written
- `/blog` and `/services` skills create `app/blog/<slug>` and `app/services/<slug>` routes; none have been generated yet
- `business.siteUrl` falls back to a placeholder unless `NEXT_PUBLIC_SITE_URL` is set

## How to help

When I ask for something:
1. State which files you would change and why
2. Give diffs or targeted snippets, not full rewrites
3. Keep within the SSG constraints and voice rules above
4. Flag anything that would break `npm run build` or a static route
