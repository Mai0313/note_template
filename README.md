<div align="center" markdown="1">

# Note Template

[![publish-pages](https://github.com/Mai0313/note_template/actions/workflows/deploy.yml/badge.svg)](https://github.com/Mai0313/note_template/actions/workflows/deploy.yml)
[![code-quality](https://github.com/Mai0313/note_template/actions/workflows/code-quality-check.yml/badge.svg)](https://github.com/Mai0313/note_template/actions/workflows/code-quality-check.yml)
[![uv](https://img.shields.io/badge/-uv_dependency_management-2C5F2D?logo=python&logoColor=white)](https://docs.astral.sh/uv/)
[![Ruff](https://img.shields.io/endpoint?url=https://raw.githubusercontent.com/astral-sh/ruff/main/assets/badge/v2.json)](https://github.com/astral-sh/ruff)
[![license](https://img.shields.io/badge/License-MIT-green.svg?labelColor=gray)](https://github.com/Mai0313/note_template/tree/main?tab=License-1-ov-file)
[![PRs](https://img.shields.io/badge/PRs-welcome-brightgreen.svg)](https://github.com/Mai0313/note_template/pulls)

</div>

A production-ready **note-taking repository template** powered by [Zensical](https://zensical.org/) + GitHub Pages. Drop markdown into `docs/`, push to `main`, and the rest happens automatically: linting and publishing.

> **Important**: This is a template repository. Do not develop directly on it. Click [Use this template](https://github.com/Mai0313/note_template/generate) to start a new notebook.

Other Languages: [English](README.md) | [繁體中文](README.zh-TW.md) | [简体中文](README.zh-CN.md)

## Highlights

- **Zero-config navigation** — `docs/` layout is reflected in the sidebar automatically via `awesome-pages`.
- **Pre-commit suite** — ruff, mdformat(+plugins), codespell, nbstripout, mypy, shellcheck, gitleaks, uv hooks. Works out of the box if you ever drop `.py`, `.rs`, `.c`, or notebook files under `docs/`.
- **GitHub Pages deploy** — `deploy.yml` builds the site with Zensical and publishes on every push to `main`.
- **CI hygiene** — semantic-PR checks, auto-labeler, release-drafter, dependabot auto-merge, secret & CodeQL & Trivy scans, pre-commit auto-update.

## Quick Start

### For Template Users (Creating a New Notebook)

1. **Create your repository** — click [Use this template](https://github.com/Mai0313/note_template/generate).
2. **Clone and bootstrap**:
    ```bash
    git clone https://github.com/YOUR_USERNAME/your_notebook.git
    cd your_notebook
    make uv-install               # install uv (only once per machine)
    uv sync                       # install the docs toolchain
    ```
3. **Rebrand**:
    - Update `pyproject.toml` (`name`, `description`, `project.urls`).
    - Update `mkdocs.yml` (`site_name`, `site_url`, `repo_name`, `repo_url`, `site_author`).
    - Update all three README files (preserve badges, only swap repo URLs).
    - Update `.github/CODEOWNERS` with your GitHub username.
4. **Verify**:
    ```bash
    make format        # run pre-commit
    make serve         # preview at http://0.0.0.0:9987
    ```

## Commands

```bash
make help          # list all targets
make serve         # preview the site locally (http://0.0.0.0:9987)
make build         # render the site into ./site
make format        # run all pre-commit hooks
make clean         # clean caches and the ./site output
```

## Writing Notes

Anything under `docs/` is rendered. To customise the order of a subdirectory,
drop a `.pages` file into it:

```yaml
# docs/projects/.pages
title: Projects
nav:
  - index.md
  - important-project.md
  - '...'
```

The `tags` plugin is enabled — any entry in your frontmatter's `tags:` list
becomes a filterable tag in the sidebar.

## CI / CD Overview

All workflows live in `.github/workflows/`. The headline ones:

| Workflow                    | Trigger                   | What it does                                 |
| --------------------------- | ------------------------- | -------------------------------------------- |
| `deploy.yml`                | push to `main` / tag `v*` | Build with Zensical, publish to GitHub Pages |
| `code-quality-check.yml`    | PR                        | Run pre-commit                               |
| `code_scan.yml`             | push / PR                 | gitleaks + CodeQL + Trivy                    |
| `auto_labeler.yml`          | PR                        | Apply labels from `.github/labeler.yml`      |
| `auto_review_merge.yml`     | PR                        | Auto-review and merge dependabot PRs         |
| `pre-commit-updater.yml`    | daily cron                | Bump pre-commit hooks and open a PR          |
| `release_drafter.yml`       | push to `main`            | Maintain a draft release from commits        |
| `semantic-pull-request.yml` | PR                        | Enforce Conventional Commit PR titles        |

### One-time setup after forking

- Enable **GitHub Pages** (Settings → Pages → Source: GitHub Actions).
- Grant **Workflow permissions: Read and write** (Settings → Actions → General).

## Project Layout

```
note_template/
├── .github/                   # CI workflows, labels, issue templates
├── docs/
│   └── index.md               # Landing page (add your own subdirs)
├── mkdocs.yml                 # Zensical / mkdocs-material config
├── pyproject.toml             # uv-managed docs dependencies + lint config
└── Makefile
```

## Contributing

- Open issues or PRs.
- Follow Conventional Commits for PR titles (enforced).
- `make format` before you push.

## License

MIT — see `LICENSE`.
