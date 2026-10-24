# Leon D. Silva — personal website

Published at https://ldsufrpe.github.io/ from the `source` branch.

## Runtime

Migrated to [al-folio v1.2](https://github.com/alshedivat/al-folio/releases/tag/v1.2), with the plugin versions pinned in `Gemfile` and resolved in `Gemfile.lock`. Jekyll builds the site using theme and feature gems; GitHub Actions publishes `_site` to `gh-pages`, which GitHub Pages serves. Theme internals are supplied by gems instead of local copies.

## Content

- `_pages/about.md`: biography and selected publications.
- `_data/cv.yml`: RenderCV data displayed at `/cv/`.
- `_bibliography/papers.bib`: publications and links.
- `_data/socials.yml`: academic profile identifiers and contact details.
- `_pages/projects.md` and `_pages/teaching.md`: projects and teaching materials.
- `_data/repositories.yml`: scientific software repositories.

Academic content was updated from the Lattes XML and Google Scholar PDF supplied on October 24, 2026. Private identity and residential data from the XML are not included. Publisher records and arXiv were used to resolve DOI, publication-year, and preprint-version differences.

## Local development

```sh
docker compose up --build
# http://localhost:8080/
```

Or, with Ruby 3.3.5, Bundler, Node.js, and ImageMagick installed:

```sh
bundle install
JEKYLL_ENV=production bundle exec jekyll build
bundle exec al-folio upgrade audit
bundle exec al-folio upgrade overrides audit
```

## Citation counts

The figures on the publications page are explicitly dated snapshots from the supplied Google Scholar PDF. Installing a new theme does not make them live. `al_citations` provides citation helpers; per-paper badges need matching Scholar identifiers and cached citation data.

The manual upstream updater is `python3 bin/update_scholar_citations.py` after installing `requirements.txt`. It reads the Scholar ID from `_data/socials.yml`. There is no scheduled citation workflow in this site. Before enabling one, ensure failures retain the last good data and that a successful update also rebuilds and publishes the site; commits made with `GITHUB_TOKEN` do not automatically trigger another push workflow.

The former `dev` branch is an independent, older migration attempt. Its sample citation cache belongs to Einstein and is not a source of this site’s metrics.

## Updating the runtime

Follow the [official installation and upgrade guide](https://github.com/alshedivat/al-folio/blob/v1.2/docs/INSTALL.md). Update exact plugin pins in both `Gemfile` and `_config.yml`, install dependencies, run the upgrade audits, and inspect the production build before publishing. Do not copy old `_layouts`, `_includes`, `_sass`, or feature JavaScript over the gem runtime.
