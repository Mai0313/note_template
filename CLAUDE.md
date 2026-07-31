# Project Initialization Guide

This repository is a note and documentation website template built with Zensical and `mkdocs-material`. Turn it into a new project with a clear subject, owner, and publishing purpose. Do not merely rename the repository and start accumulating Markdown files.

## Establish the project before editing

Before changing content, confirm with the user or infer from existing project material:

- The intended readers: private notes, a team, a public audience, or a deliberate combination.
- The subject and boundary of the knowledge base, such as engineering notes, project documentation, course material, research records, or a reference site. Do not mix audiences or content types in an unstructured tree.
- Whether the site is public or private, whether GitHub Pages should remain enabled, and whether `main` or `master` is the default branch.
- The owner, GitHub account or organization, repository name, site URL, primary language, license, and contribution model.

When a critical decision is absent, create only a reviewable content skeleton. Do not invent an identity, domain, license restriction, or treat `Mai0313`, `Wei`, and `note_template` as information for the new project.

## Initialization order

1. Inventory template placeholders in `README.md`, `README.zh-TW.md`, `README.zh-CN.md`, `docs/index.md`, `mkdocs.yml`, `pyproject.toml`, `.github/CODEOWNERS`, and `.github/workflows/`.
2. Apply one consistent project identity to the three READMEs, `docs/index.md`, and the relevant values in `mkdocs.yml`: `site_name`, `site_url`, `site_author`, `site_description`, `repo_name`, `repo_url`, `edit_uri`, and `extra.social`. Update the project metadata and URLs in `pyproject.toml` as well.
3. Create a top-level `docs/` structure that follows the confirmed content boundary. Possible areas include `guides/`, `references/`, `projects/`, `weekly/`, `decisions/`, and `assets/`, but create only categories that serve the project. Every durable area should have an understandable landing page or index.
4. Adjust publishing, permissions, and collaboration settings only after the project identity and intended operating model are known, then validate the result.

## README and badges

- Never delete an existing README badge. This rule applies to every current badge in all three README files, including status, tooling, license, and pull request badges.
- Existing badges may be updated so their URLs and labels point to the new repository, and new badges may be added when they reflect a real project capability. Do not claim a CI check, published site, license, or quality gate that is not enabled.
- Keep or rewrite each README as a truthful entry point for the new project: its purpose and scope, local preview instructions, content navigation, publishing model, and contribution rules. Keep the project name, URLs, and operational instructions consistent across the three language versions.

## Documentation architecture and Markdown

- `docs/` is the rendered site source. The `awesome-pages` plugin derives navigation from its directory tree and supports `.pages` files for local titles and ordering. Add a category only when it will grow beyond a single page.
- Long-lived pages should state their title, purpose, reader prerequisites, and maintenance responsibility. Use YAML front matter `tags:` with the existing tags plugin for cross-cutting discovery, but do not use tags as a substitute for information architecture.
- Use relative links for internal references and verify them with `make build`. When moving or renaming a page, update its incoming links, navigation configuration, and README references at the same time.
- Store images, diagrams, and downloadable assets in a tracked location close to the page that uses them. Use meaningful filenames and alt text. Check license, privacy, and file size before committing material. Never put secrets, private personal data, or unlicensed assets in a public documentation repository.
- The existing Material extensions support admonitions, code annotations, tabs, mathematics, and task lists. Use them only where they improve comprehension, and verify their actual Zensical rendering locally.

## Publishing and automation

- `deploy.yml` runs `uv sync --frozen` and `uv run zensical build`, then publishes `site/` to GitHub Pages. For a public documentation site, retain this deployment flow, select GitHub Actions as the Pages source, and confirm that the workflow has the permissions needed to deploy.
- During initialization, modify existing GitHub Actions rather than deleting them. Preserve and adapt `code-quality-check.yml`, `code_scan.yml`, `auto_labeler.yml`, `semantic-pull-request.yml`, Dependabot, the pre-commit updater, and release drafting for the new branch names, maintenance model, and security requirements.
- `auto_review_merge.yml` automatically approves and merges Dependabot pull requests, while `release_drafter.yml` creates draft releases. Before enabling these behaviors for a new project, confirm that its maintainers accept both the automation and the associated `write-all` permissions.
- Update `.github/CODEOWNERS`, `dependabot.yml`, `labeler.yml`, `.github/CONTRIBUTING.md`, and `.github/cliff.toml` to match the actual owner, branching model, and release requirements. Do not leave template-author reviewers or public links behind.
- Apply least privilege to every workflow. Before changing `permissions`, verify what each action requires. Do not disable security scanning or broaden permissions merely to make a workflow pass.

Only GitHub Actions may be removed later. Remove an action only when there is concrete evidence that it no longer serves the established project, the user explicitly confirms its removal, and the related README, CI expectations, and verification instructions are updated in the same change. Do not remove other template safeguards, badges, hooks, lint configuration, or documentation merely because they appear unused during initialization.

## Tooling and verification

This repository uses `uv` for the Python documentation toolchain:

```bash
uv sync
make fmt
make build
make serve
```

- After changing Markdown, configuration, or CI, run `make fmt` and then `make build`. Use `make serve` to inspect navigation, links, images, Material features, and the landing page.
- The Makefile target is `fmt`, not `format`, despite the current README and contribution guide using `make format`. When initializing a new project, correct those references rather than adding an empty alias that hides the inconsistency. `make fmt` runs `uvx pre-commit run -a`, including mdformat, codespell, gitleaks, YAML, and TOML checks. Do not disable hooks or delete configuration to conceal formatting, spelling, secret, or configuration failures.
- When changing dependencies in `pyproject.toml`, update and commit the corresponding `uv.lock`. The frozen install in `deploy.yml` rejects an out-of-sync lockfile.
- When editing GitHub Actions, verify YAML syntax, triggers, branch names, action versions, artifact paths, and permissions. If a workflow cannot be fully executed locally, state which checks must run in the pull request.

## Handling template remnants

Replace template text, author names, repository URLs, site URLs, and the generic landing-page greeting during initialization because they would otherwise misrepresent the new project. This is distinct from deleting project capabilities.

Keep the template's badges permanently, updating or adding them as the new project requires. Keep GitHub Actions during initialization and modify them to fit. Later removal is restricted to GitHub Actions and requires evidence, explicit user confirmation, and coordinated documentation and validation updates.
