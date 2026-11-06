# Research documentation starter

This folder is a **MkDocs documentation site** with TechDocs-compatible Markdown content. For a lightweight public site, publish it using MkDocs + GitHub Pages; that does **not** require a Backstage installation. To use official Backstage TechDocs, connect the repository to an existing Backstage instance and configure its TechDocs plugin. This ZIP does not itself create a hosted TechDocs URL.

## Local preview
```
python -m pip install mkdocs
mkdocs serve
```
Open the local URL printed by MkDocs. To publish to GitHub Pages, configure repository permissions and run `mkdocs gh-deploy` from the repository root, or use a GitHub Actions workflow. If your existing GitHub Pages site already uses the root URL, prefer a separate repository or subpath to avoid overwriting it.

## Backstage TechDocs
Official TechDocs normally uses `mkdocs.yml` and `docs/`, plus a Backstage catalog entity (`catalog-info.yaml`) and `techdocs-core` plugin. See https://backstage.io/docs/features/techdocs/ . The supplied `mkdocs.yml` uses standard MkDocs search to work without Backstage. Replace `plugins: - search` with `plugins: - techdocs-core` after installing `mkdocs-techdocs-core` when integrating into Backstage.
