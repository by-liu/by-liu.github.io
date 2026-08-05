# Personal website agent guide

## Purpose

This repository contains Bingyuan Liu's public personal and academic website.
The production site is built with Astro from `site/` and published at
https://by-liu.github.io/.

The previous Wowchemy site is not part of the working tree. It is recoverable
from the `legacy-wowchemy-site` tag and Git history.

## Repository map

- `site/`: active Astro project and the source of truth for website content.
- `.github/workflows/deploy.yml`: GitHub Pages build and deployment workflow.
- `README.md`: local development, content, and deployment overview.
- `site/AGENTS.md`: detailed instructions for UI and writing changes.

Do not edit generated output in `site/dist/`, generated Astro metadata in
`site/.astro/`, or dependencies in `site/node_modules/`.

## Working principles

- Preserve the site's minimal, understated visual language. Let the work,
  experience, and publications provide the emphasis.
- Treat light mode as the design reference. Dark mode is an explicit visitor
  choice and must remain readable and visually consistent.
- Keep layouts responsive across laptop, phone, and tablet widths.
- Prefer semantic HTML, accessible labels, useful alt text, and keyboard-safe
  interactions.
- Keep public claims accurate. Verify publication metadata, links, employment
  wording, metrics, and other factual statements before changing them.
- Preserve user changes and avoid unrelated cleanup.
- Do not commit, push, change GitHub settings, or deploy unless the user asks.

## Standard workflow

Run commands from `site/` unless a command is explicitly repository-level.

```sh
npm ci
npm run dev -- --host 127.0.0.1 --port 4322
npm run validate
```

Use http://localhost:4322 for local review. Before handing off a change, run
`npm run validate`, review relevant desktop and mobile layouts, and check both
light and dark themes when presentation is affected.

## Deployment

Pushing a change under `site/` or to the deployment workflow on `master`
triggers GitHub Pages automatically. The workflow builds only `site/`; never
commit `site/dist/`.

When deployment is requested:

1. Confirm the worktree is clean except for intended changes.
2. Run `npm run validate` from `site/`.
3. Review the staged diff before committing.
4. Push to `master`.
5. Monitor the `Deploy personal site` workflow and verify the live route.
