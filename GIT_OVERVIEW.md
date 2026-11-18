# Git Overview

Log of work done in this repo. Add a row for every change.

## Commits

| Date | Commit | Branch | Summary |
|------|--------|--------|---------|
| 2026-04-22 | `51b49af` | main | Initial commit — full site (see below) |
| 2026-11-18 | (this commit) | `claude/chatgpt-brief-git-overview-6a4piv` | Added `CHATGPT_BRIEF.md` (handoff brief for ChatGPT) and `GIT_OVERVIEW.md` (this file) |

## What's in the initial commit (`51b49af`)

Built across the prompts in `prompts.md`:

| Step | Prompt | Result |
|------|--------|--------|
| v1 | Generate plumbing site: home, blog index, service index | `app/page.tsx`, `app/blog`, `app/services`, `components/home/*`, `components/site/*`, `lib/business.ts` |
| v2 | Blog post from `keywords.csv`, keyword cluster, log used keyword | `app/v2`, `content/blog-ai-slop.ts`, `references/used-keywords.md` (`plumber for low water pressure`) |
| v3 | Rewrite using voice references, SERP-matched, FAQ, Pexels images | `app/v3`, `content/blog-voiced.ts` (`plumber for running toilet`), `scripts/fetch-pexels.mjs`, `content/pexels.json`, `public/images/blog/*` |
| v4 | City+service landing page from `Service-keywords.csv` | `app/v4`, `content/landing-baldwin-park.ts` (`plumber baldwin park ca`), `components/seo/LocalBusinessJsonLd.tsx` |
| v5 | Apply on-page SEO checklist, keep voice | `app/v5`, `components/blog/{TableOfContents,Breadcrumbs,AuthorCard,SectionImage,BackToTop}.tsx`, `components/seo/BlogJsonLd.tsx`, `on-page-seo.md` |
| v6 | Lighthouse 100s, robots.txt, sitemap.xml | `app/v6`, `app/sitemap.ts`, `app/robots.ts`, `components/seo/{OrganizationJsonLd,TechSeoScorecard}.tsx` |
| v7 | Deploy to GitHub | Repo pushed |
| v8 | Google Search Console verification | `public/google2013973ec23e9db5.html` |

Also included: `.claude/skills/blog` and `.claude/skills/service` (repeatable generators), `references/*` (voice layer), `slideshow/*.html` (video explainer slides), `CLAUDE.md`, `project_specs.md`, `README.md`.
