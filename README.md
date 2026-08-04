# Bingyuan Liu’s personal website

A minimal personal and academic website built with Astro and published at
[by-liu.github.io](https://by-liu.github.io/).

The active website source is under [`site/`](site/). Files elsewhere in the
repository belong to the previous static site and are retained during the
migration, but they are not included in the Astro deployment.

## Local development

```sh
cd site
npm ci
npm run dev -- --host 127.0.0.1 --port 4322
```

Open <http://localhost:4322>.

## Validation

Run the complete local check before committing:

```sh
cd site
npm run validate
```

This runs Astro’s type and content checks, then creates a production build in
`site/dist/`.

## Content

- Profile, work experience, education, and publication data:
  `site/src/data/profile.ts`
- Homepage: `site/src/pages/index.astro`
- Longer writing: `site/src/content/blog/`
- Static assets and downloadable résumé: `site/public/`

## Deployment

GitHub Pages is deployed by `.github/workflows/deploy.yml`. A push to `master`
that changes the Astro site or deployment workflow builds `site/` and publishes
the generated artifact. The workflow can also be started manually from the
repository’s Actions tab.

The repository’s Pages source must be set to **GitHub Actions**. No generated
`dist/` files are committed.
