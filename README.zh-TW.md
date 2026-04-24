<div align="center" markdown="1">

# Note Template

[![publish-pages](https://github.com/Mai0313/note_template/actions/workflows/deploy.yml/badge.svg)](https://github.com/Mai0313/note_template/actions/workflows/deploy.yml)
[![code-quality](https://github.com/Mai0313/note_template/actions/workflows/code-quality-check.yml/badge.svg)](https://github.com/Mai0313/note_template/actions/workflows/code-quality-check.yml)
[![uv](https://img.shields.io/badge/-uv_dependency_management-2C5F2D?logo=python&logoColor=white)](https://docs.astral.sh/uv/)
[![Ruff](https://img.shields.io/endpoint?url=https://raw.githubusercontent.com/astral-sh/ruff/main/assets/badge/v2.json)](https://github.com/astral-sh/ruff)
[![license](https://img.shields.io/badge/License-MIT-green.svg?labelColor=gray)](https://github.com/Mai0313/note_template/tree/main?tab=License-1-ov-file)
[![PRs](https://img.shields.io/badge/PRs-welcome-brightgreen.svg)](https://github.com/Mai0313/note_template/pulls)

</div>

以 [Zensical](https://zensical.org/) + GitHub Pages 為核心的**筆記專案 template**。把 markdown 丟進 `docs/`、push 到 `main`,剩下的事情都會自動完成:linting 跟發佈到 GitHub Pages。

> **重要**:這是一個 template repo,請不要直接在上面開發。點 [Use this template](https://github.com/Mai0313/note_template/generate) 建立你自己的筆記 repo。

其他語言:[English](README.md) | [繁體中文](README.zh-TW.md) | [简体中文](README.zh-CN.md)

## 主要特色

- **零設定導覽列** — `docs/` 底下的資料夾結構直接反映到側邊欄 (透過 `awesome-pages` plugin)。
- **Pre-commit 套件齊全** — ruff、mdformat(+plugins)、codespell、nbstripout、mypy、shellcheck、gitleaks、uv hooks。即使你未來在 `docs/` 丟 `.py`、`.rs`、`.c`、notebook 也都能正常 lint。
- **自動發佈 GitHub Pages** — 每次 push `main`,`deploy.yml` 會用 Zensical build 並 publish。
- **完整 CI 衛生** — semantic PR 標題、auto-labeler、release-drafter、dependabot auto-merge、secret/CodeQL/Trivy 掃描、pre-commit 每日自動更新。

## Quick Start

### Template 使用者 (建立新筆記本)

1. **建立你的 repo** — 點 [Use this template](https://github.com/Mai0313/note_template/generate)。
2. **Clone 並安裝環境**:
    ```bash
    git clone https://github.com/YOUR_USERNAME/your_notebook.git
    cd your_notebook
    make uv-install               # 安裝 uv (每台機器只需一次)
    uv sync                       # 安裝 docs toolchain
    uv tool install pre-commit    # 安裝 pre-commit
    ```
3. **改名字**:
    - 更新 `pyproject.toml` (`name`、`description`、`project.urls`)。
    - 更新 `mkdocs.yml` (`site_name`、`site_url`、`repo_name`、`repo_url`、`site_author`)。
    - 更新三個 README (保留 badges,只改 repo URL)。
    - 更新 `.github/CODEOWNERS` 成你的 GitHub 帳號。
4. **確認**:
    ```bash
    make format        # 跑一次 pre-commit
    make serve         # 打開 http://0.0.0.0:9987 預覽
    ```

## 指令

```bash
make help          # 列出所有 target
make serve         # 本機預覽 (http://0.0.0.0:9987)
make build         # 把 site 渲染到 ./site
make format        # 跑所有 pre-commit hooks
make clean         # 清 cache 和 ./site
```

## 寫筆記

`docs/` 底下的任何檔案都會被渲染。要調整某個資料夾內筆記的排序,在那個資料夾放一個 `.pages`:

```yaml
# docs/projects/.pages
title: Projects
nav:
  - index.md
  - important-project.md
  - '...'
```

`tags` plugin 已啟用 — frontmatter 裡的 `tags:` 會自動變成可篩選的 tag 頁。

## CI / CD 概覽

所有 workflow 都在 `.github/workflows/`。主要的幾支:

| Workflow                    | 觸發時機               | 做什麼                                |
| --------------------------- | ---------------------- | ------------------------------------- |
| `deploy.yml`                | push `main` / tag `v*` | Zensical build + 發佈 GitHub Pages    |
| `code-quality-check.yml`    | PR                     | 跑 pre-commit                         |
| `code_scan.yml`             | push / PR              | gitleaks + CodeQL + Trivy             |
| `auto_labeler.yml`          | PR                     | 根據 `.github/labeler.yml` 上 label   |
| `auto_review_merge.yml`     | PR                     | 自動 approve + merge dependabot 的 PR |
| `pre-commit-updater.yml`    | 每日 cron              | 更新 pre-commit hooks 版本並開 PR     |
| `release_drafter.yml`       | push `main`            | 維護 draft release                    |
| `semantic-pull-request.yml` | PR                     | 強制 Conventional Commit 的 PR 標題   |

### Fork 後一次性設定

- 啟用 **GitHub Pages** (Settings → Pages → Source: GitHub Actions)。
- 開啟 **Workflow permissions: Read and write** (Settings → Actions → General)。

## 專案結構

```
note_template/
├── .github/                   # CI workflows、labels、issue templates
├── docs/
│   └── index.md               # 首頁 (其他子資料夾你自己建)
├── mkdocs.yml                 # Zensical / mkdocs-material 設定
├── pyproject.toml             # uv 管的 docs dependencies + lint 設定
└── Makefile
```

## Contributing

- 歡迎開 issue 或 PR。
- PR 標題請遵守 Conventional Commits (已強制)。
- Push 前請先 `make format`。

## License

MIT — 請見 `LICENSE`。
