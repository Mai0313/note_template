<div align="center" markdown="1">

# Note Template

[![publish-pages](https://github.com/Mai0313/note_template/actions/workflows/deploy.yml/badge.svg)](https://github.com/Mai0313/note_template/actions/workflows/deploy.yml)
[![code-quality](https://github.com/Mai0313/note_template/actions/workflows/code-quality-check.yml/badge.svg)](https://github.com/Mai0313/note_template/actions/workflows/code-quality-check.yml)
[![uv](https://img.shields.io/badge/-uv_dependency_management-2C5F2D?logo=python&logoColor=white)](https://docs.astral.sh/uv/)
[![Ruff](https://img.shields.io/endpoint?url=https://raw.githubusercontent.com/astral-sh/ruff/main/assets/badge/v2.json)](https://github.com/astral-sh/ruff)
[![license](https://img.shields.io/badge/License-MIT-green.svg?labelColor=gray)](https://github.com/Mai0313/note_template/tree/main?tab=License-1-ov-file)
[![PRs](https://img.shields.io/badge/PRs-welcome-brightgreen.svg)](https://github.com/Mai0313/note_template/pulls)

</div>

以 [Zensical](https://zensical.org/) + GitHub Pages 为核心的**笔记仓库 template**。把 markdown 丢进 `docs/`、push 到 `main`,剩下的事情全部自动完成:linting 和发布到 GitHub Pages。

> **重要**:这是一个 template 仓库,请不要直接在上面开发。点 [Use this template](https://github.com/Mai0313/note_template/generate) 建立你自己的笔记仓库。

其他语言:[English](README.md) | [繁體中文](README.zh-TW.md) | [简体中文](README.zh-CN.md)

## 主要特色

- **零配置导航** — `docs/` 底下的目录结构会自动反映到侧边栏 (通过 `awesome-pages` plugin)。
- **Pre-commit 套件齐全** — ruff、mdformat(+plugins)、codespell、nbstripout、mypy、shellcheck、gitleaks、uv hooks。未来在 `docs/` 放 `.py`、`.rs`、`.c`、notebook 都能正常 lint。
- **自动发布 GitHub Pages** — 每次 push `main`,`deploy.yml` 会用 Zensical build 并 publish。
- **完整 CI 卫生** — semantic PR 标题、auto-labeler、release-drafter、dependabot auto-merge、secret/CodeQL/Trivy 扫描、pre-commit 每日自动更新。

## Quick Start

### Template 使用者 (建立新笔记本)

1. **建立你的仓库** — 点 [Use this template](https://github.com/Mai0313/note_template/generate)。
2. **Clone 并安装环境**:
    ```bash
    git clone https://github.com/YOUR_USERNAME/your_notebook.git
    cd your_notebook
    make uv-install               # 安装 uv (每台机器只需一次)
    uv sync                       # 安装 docs toolchain
    ```
3. **改名字**:
    - 更新 `pyproject.toml` (`name`、`description`、`project.urls`)。
    - 更新 `mkdocs.yml` (`site_name`、`site_url`、`repo_name`、`repo_url`、`site_author`)。
    - 更新三个 README (保留 badges,只改 repo URL)。
    - 更新 `.github/CODEOWNERS` 成你的 GitHub 账号。
4. **确认**:
    ```bash
    make format        # 跑一次 pre-commit
    make serve         # 打开 http://0.0.0.0:9987 预览
    ```

## 指令

```bash
make help          # 列出所有 target
make serve         # 本机预览 (http://0.0.0.0:9987)
make build         # 把 site 渲染到 ./site
make format        # 跑所有 pre-commit hooks
make clean         # 清 cache 和 ./site
```

## 写笔记

`docs/` 底下的任何文件都会被渲染。要调整某个文件夹内笔记的排序,在那个文件夹放一个 `.pages`:

```yaml
# docs/projects/.pages
title: Projects
nav:
  - index.md
  - important-project.md
  - '...'
```

`tags` plugin 已启用 — frontmatter 里的 `tags:` 会自动变成可筛选的 tag 页。

## CI / CD 概览

所有 workflow 都在 `.github/workflows/`。主要几支:

| Workflow                    | 触发时机               | 做什么                                |
| --------------------------- | ---------------------- | ------------------------------------- |
| `deploy.yml`                | push `main` / tag `v*` | Zensical build + 发布 GitHub Pages    |
| `code-quality-check.yml`    | PR                     | 跑 pre-commit                         |
| `code_scan.yml`             | push / PR              | gitleaks + CodeQL + Trivy             |
| `auto_labeler.yml`          | PR                     | 根据 `.github/labeler.yml` 上 label   |
| `auto_review_merge.yml`     | PR                     | 自动 approve + merge dependabot 的 PR |
| `pre-commit-updater.yml`    | 每日 cron              | 更新 pre-commit hooks 版本并开 PR     |
| `release_drafter.yml`       | push `main`            | 维护 draft release                    |
| `semantic-pull-request.yml` | PR                     | 强制 Conventional Commit 的 PR 标题   |

### Fork 后一次性配置

- 启用 **GitHub Pages** (Settings → Pages → Source: GitHub Actions)。
- 开启 **Workflow permissions: Read and write** (Settings → Actions → General)。

## 项目结构

```
note_template/
├── .github/                   # CI workflows、labels、issue templates
├── docs/
│   └── index.md               # 首页 (其他子目录你自己建)
├── mkdocs.yml                 # Zensical / mkdocs-material 配置
├── pyproject.toml             # uv 管的 docs dependencies + lint 配置
└── Makefile
```

## Contributing

- 欢迎开 issue 或 PR。
- PR 标题请遵守 Conventional Commits (已强制)。
- Push 前请先 `make format`。

## License

MIT — 参见 `LICENSE`。
