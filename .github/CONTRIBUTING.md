# Contributing Guide

Thank you for your interest in contributing to this notes / documentation site. This document describes how to set up the local environment, the conventions used, and the workflow expected for issues and pull requests.

## Table of Contents

- [Code of Conduct](#code-of-conduct)
- [Ways to Contribute](#ways-to-contribute)
- [Reporting Issues](#reporting-issues)
- [Development Setup](#development-setup)
- [Local Workflow](#local-workflow)
- [Writing Style](#writing-style)
- [Branching Model](#branching-model)
- [Commit Convention](#commit-convention)
- [Pull Request Process](#pull-request-process)
- [Code Review](#code-review)
- [Security Reports](#security-reports)
- [Licensing](#licensing)

## Code of Conduct

All contributors are expected to behave professionally and respectfully. Personal attacks, harassment, and discriminatory language are not tolerated. By participating, you agree to uphold a welcoming environment for everyone.

## Ways to Contribute

- Fixing typos, grammar, broken links, and stale information
- Adding new notes, articles, or tutorials
- Improving navigation, structure, and metadata
- Suggesting tooling or design improvements
- Translating content into additional languages

## Reporting Issues

Before opening a new issue:

1. Search existing issues to avoid duplicates.
2. Verify the problem appears on the latest content of `main`.

Please include:

- The page URL or file path involved
- A clear description of the problem (incorrect content, broken link, rendering issue, etc.)
- Screenshots when relevant
- Browser, OS, or environment information for rendering issues

## Development Setup

This site uses [`uv`](https://docs.astral.sh/uv/) for Python and dependency management, and **Zensical** as the static site generator.

```bash
# Install uv (one-time setup)
make uv-install

# Clone your fork
git clone https://github.com/<your-username>/<repo>.git
cd <repo>

# Install dependencies
uv sync

# Install pre-commit hooks
uv run pre-commit install
```

## Local Workflow

Common tasks are exposed via the `Makefile`. Run `make help` to list all targets. Frequently used ones:

```bash
make format    # Run pre-commit hooks (mdformat, codespell, ...)
make serve     # Serve the site locally at http://0.0.0.0:9987
make build     # Build the static site into ./site
make clean     # Remove caches and build artifacts
```

Always run `make format` before opening a pull request.

## Writing Style

- Use clear, concise language.
- Prefer present tense and active voice.
- Use sentence case for headings.
- Wrap lines at a reasonable length to ease review diffs.
- Place images and other assets near the page that uses them.
- Use relative links for internal references.
- Provide alt text for all images.
- Validate code blocks compile or run when claiming to do so.

When adding a new page, ensure it is reachable from the navigation defined in `mkdocs.yml`.

## Branching Model

- `main` is the default branch and is deployed automatically.
- Content branches: `docs/<short-description>`
- Tooling branches: `chore/<short-description>` or `ci/<short-description>`
- Fix branches: `fix/<short-description>`

## Commit Convention

Commit messages follow [Conventional Commits](https://www.conventionalcommits.org/) and **must be written in English**.

Format:

```
<type>(<optional scope>): <short summary>

<optional body>

<optional footer>
```

Allowed types:

| Type       | Purpose                                                |
| ---------- | ------------------------------------------------------ |
| `doc`      | Documentation or content changes                       |
| `fix`      | Correction of incorrect content or broken behavior     |
| `feat`     | A new feature in the site or tooling                   |
| `refactor` | Restructuring content or code without changing meaning |
| `style`    | Formatting or stylistic changes                        |
| `chore`    | Build, tooling, or auxiliary changes                   |
| `ci`       | Continuous integration changes                         |
| `revert`   | Reverting a previous commit                            |

Reference issues with `Closes #123` or `Refs #123` when applicable.

## Pull Request Process

1. Ensure your branch is up to date with the target branch.
2. Run `make format` locally and verify the site builds with `make build`.
3. Ensure CI checks pass on the pull request.
4. Use a descriptive title following the commit convention; it is validated by **semantic-pull-request**.
5. Fill out the pull request template, including motivation, summary, and screenshots when relevant.
6. Mark the PR as **draft** while still in progress.
7. Request review only after self-review and a green CI.

Pull requests are typically merged via **squash merge** to keep history linear.

## Code Review

- Address all review comments or explain why a change is not needed.
- Keep discussions technical, focused, and respectful.
- Resolve conversations only after the concern has been addressed.

## Security Reports

Please **do not** report security vulnerabilities through public issues. Refer to [`SECURITY.md`](./SECURITY.md) for the responsible disclosure process.

## Licensing

By contributing, you agree that your contributions will be licensed under the project's license (see [`LICENSE`](../LICENSE)). Ensure that you have the right to submit any content, code, or assets you contribute.
