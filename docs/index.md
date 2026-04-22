---
title: Home
---

# Note Template

Welcome to your fresh notebook. This site is powered by
[Zensical](https://zensical.org/) + [mkdocs-material](https://squidfunk.github.io/mkdocs-material/)
and is published automatically to GitHub Pages whenever you push to `main`.

## How to use this template

1. Click **Use this template** on GitHub, or clone this repo and repoint the remote.
2. Edit `mkdocs.yml` — change `site_name`, `site_url`, `repo_name`, `repo_url`.
3. Drop your notes anywhere under `docs/`. The left-hand navigation is generated
    automatically by the [awesome-pages plugin](https://github.com/lukasgeiter/mkdocs-awesome-pages-plugin).
4. Commit and push. GitHub Actions will:
    - run `pre-commit` on every PR (markdown formatting, spell check, secret scan),
    - publish the rendered site to GitHub Pages,
    - push a static-site Docker image to `ghcr.io/<owner>/<repo>:latest` for offline backup.

## Previewing locally

```bash
uv sync
make serve                # http://0.0.0.0:9987
```

Or, to host the already-built site from a Docker image:

```bash
make build
docker compose up notes   # http://127.0.0.1:8080
```

## Next steps

Start writing. Folders you create under `docs/` (for example `docs/notes/`,
`docs/weekly/`, `docs/projects/`, `docs/references/`) show up in the sidebar
without any extra configuration.
