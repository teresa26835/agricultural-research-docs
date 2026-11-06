# Publishing this MkDocs project

Repository: https://github.com/teresa26835/agricultural-research-docs

1. Keep `mkdocs.yml`, `README.md`, and `catalog-info.yaml` at the repository root.
2. Put the Markdown pages inside `docs/`.
3. Put `deploy.yml` at `.github/workflows/deploy.yml`.
4. Remove the redundant root-level copies of `dashboard.md`, `diagnostics.md`, `interview.md`, `missingness.md`, `pipeline.md`, `regression.md`, and other moved pages. Remove `START_HERE_中文.txt` and `docs/interview.md` if present.
5. Commit. GitHub Actions runs `mkdocs gh-deploy --force`. In Settings > Pages choose branch `gh-pages`, root `/`.
6. Check https://teresa26835.github.io/agricultural-research-docs/ after deployment.
7. Replace placeholder DOI/dashboard URLs with real published links.

The archive is a corrected source snapshot, not an automatic edit of your GitHub repository.
