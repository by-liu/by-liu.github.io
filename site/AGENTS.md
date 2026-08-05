# Astro site development guide

These instructions apply to the active website under `site/`. Also follow the
repository-level `../AGENTS.md`.

## Architecture and content map

- `src/pages/index.astro`: homepage structure and section-specific styles.
- `src/data/profile.ts`: education, work experience, and publication data.
- `src/pages/publications.astro`: full curated publication list.
- `src/content/blog/`: Markdown and MDX writing collection.
- `src/layouts/ArticleLayout.astro`: shared article presentation.
- `src/components/Figure.astro`: full-width article figures with captions.
- `src/components/Callout.astro`: restrained emphasis for key ideas.
- `src/styles/global.css`: design tokens, prose styling, and dark theme.
- `public/`: static images, favicons, and the downloadable resume.
- `src/content.config.ts`: required writing frontmatter and content schema.

## Visual direction

- Keep the presentation minimal, calm, and editorial rather than promotional.
- Avoid oversized cards, badges, gradients, decorative dashboards, excessive
  bold text, and generic "AI-generated" visual motifs.
- Company names are primary and roles are secondary in work experience.
- Use spacing, typography, and hierarchy before adding borders or containers.
- Light mode is the default. The header control applies and persists dark mode.
- Reuse existing CSS variables and components before introducing new patterns.

## Writing workflow

Create each article as `src/content/blog/<descriptive-slug>.mdx`. Use `.md` only
when the article does not need imported Astro components.

Start with this frontmatter:

```yaml
---
title: "Clear article title"
description: "A concise one- or two-sentence summary."
date: 2026-08-05
updated: 2026-08-05 # optional; remove when not needed
type: technical     # technical, essay, or note
tags: [topic]
draft: true
featured: false
---
```

The schema is enforced by `src/content.config.ts`:

- `type: technical` renders the label "Technical note".
- `type: essay` uses the serif article body treatment.
- `type: note` is for shorter or less formal writing.
- `draft: true` excludes the article from routes, the Writing page, homepage,
  and RSS. Change it to `false` only after review.
- Published articles are sorted newest first. The homepage shows the latest
  three published articles. `featured` is reserved and is not currently used
  for ordering or selection.

For MDX articles, components can be imported with:

```mdx
import Figure from '../../components/Figure.astro';
import Callout from '../../components/Callout.astro';
```

Store article assets in `public/images/writing/<slug>/` and reference them with
root-relative paths such as `/images/writing/<slug>/overview.png`.

Example figure:

```mdx
<Figure
  src="/images/writing/<slug>/overview.png"
  alt="A concrete description of what the figure communicates"
  caption="A concise caption that supports the surrounding argument."
  source="Original source"
  sourceUrl="https://example.com/source"
/>
```

Example callout:

```mdx
<Callout label="Key idea">
  Keep emphasis concise and useful to a reader scanning the article.
</Callout>
```

Inline math uses `$...$`; display math uses `$$...$$`. Use fenced code blocks
with a language identifier. Prefer normal prose flow over too many callouts,
figures, headings, or UI blocks.

## Editorial and source standards

- Write in Bingyuan's voice; do not invent opinions, experience, results, or
  personal anecdotes.
- Ground technical and factual claims in primary or authoritative sources.
- Link claims close to the relevant text and include a short References section
  when an article relies on several sources.
- Give figures accurate alt text and captions. Credit external figures and link
  the original source. Confirm reuse is appropriate; otherwise create an
  original diagram or describe the idea in text.
- Do not reproduce substantial copyrighted text or an entire external article.
- Keep titles, descriptions, and opening paragraphs specific and free of hype.

## Review checklist

Before publishing an article:

1. Confirm frontmatter passes the collection schema.
2. Check factual claims, citations, dates, names, and external links.
3. Review headings, formulas, code, figures, captions, and alt text.
4. Test desktop and mobile widths in both light and dark themes.
5. Set `draft: false` only after content review.
6. Run `npm run validate`.
7. Verify the article route, `/writing/`, the homepage list, and `/rss.xml`.

## Commands

```sh
npm run dev -- --host 127.0.0.1 --port 4322
npm run check
npm run build
npm run validate
```

The local preview should stay on port 4322 unless the user requests otherwise.
