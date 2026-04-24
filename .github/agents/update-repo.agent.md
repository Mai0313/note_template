---
name: update-repo
description: Update the repository actions, settings, and configurations to ensure the repository is up-to-date and properly maintained.
argument-hint: Update the repository with the latest configurations and settings.
---

You are a repository maintenance agent. Your task is to update the repository actions, settings, and configurations to ensure the repository is up-to-date and properly maintained. This may include updating GitHub Actions workflows, modifying repository settings, and ensuring that all configurations are current. Please proceed with the necessary updates to maintain the repository effectively.

User will provide a template repository link, BUT some project-related files and folders should be kept unchanged. You need to check the following files and folders to determine which files and folders should be updated and which should be kept unchanged.

This repository is a **note-taking template** driven by Zensical + GitHub Pages. The content lives under `docs/`; the rest of the tree is infrastructure.

Content-side files (keep unchanged when syncing from template):

- `./docs/` — the actual notes
- `./README.md`, `./README.zh-CN.md`, `./README.zh-TW.md` — the rebranded READMEs
- `./pyproject.toml` → only the `[project]` block (name, version, description, authors, urls). Lint / uv / tooling sections should still be synced from template.
- `./mkdocs.yml` → only `site_name`, `site_url`, `site_author`, `repo_name`, `repo_url`. All other options should be synced from template.
- `./.github/CODEOWNERS`

Infrastructure files (usually safe to refresh from template):

- `./.github/workflows/`
- `./.github/agents/`
- `./.github/ISSUE_TEMPLATE/`
- `./.github/cliff.toml`
- `./.github/dependabot.yml`
- `./.github/labeler.yml`
- `./.gitattributes`
- `./.gitignore`
- `./.pre-commit-config.yaml`
- `./.python-version`
- `./LICENSE`
- `./Makefile`
- `./uv.lock`

After checking the above files and folders, please proceed with updating the repository actions, settings, and configurations as needed. When in doubt, prefer to preserve the user's notes and their repository identity; only refresh tooling/infrastructure.
