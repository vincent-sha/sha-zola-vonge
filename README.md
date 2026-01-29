# Vonge Zola 主题（中文说明）
![](screenshot.png)

这是对原始 [Vonge Hugo Bookshop template](https://github.com/CloudCannon/vonge-hugo-bookshop-template) 的 Zola 移植版，由 [CloudCannon](https://cloudcannon.com/) 最初创建并在 MIT 许可下发布。

Vonge 是一个简洁、现代的个人作品集、博客或落地页主题。该 Zola 版本旨在**可通过 `config.toml` 和结构化的 front matter 块全面配置**，且**不依赖 Bookshop**。

> ✨ 适合希望快速搭建专业外观、可配置内容区块的开发者与内容作者。

演示地址：https://paberr.github.io/vonge-zola-theme/

---

## 🚀 特性

- 使用内容区块（content blocks）实现灵活的主页与内页布局
- 通过 front matter 的 `extra.content_blocks` 可定制内容
- 干净的排版与响应式布局
- 带分页的博客列表
- 作品集（Projects）和客户推荐（Testimonials）支持
- SEO 友好的结构
- MIT 许可

---

## 📦 安装（快速入门）

1. 下载主题（推荐使用子模块）

```bash
git submodule add https://github.com/paberr/vonge-zola-theme themes/vonge
```

2. 在你的站点根目录 `config.toml` 中至少添加：

```toml
theme = "vonge"
taxonomies = [
  { name = "tags", feed = true },
]
```

3. 复制示例内容开始构建：

```bash
cp -r themes/vonge/content/* content/
```

4. 本地预览：

```bash
zola serve
# 访问 http://127.0.0.1:1111
```

---

## 🔧 推荐配置（参考 Statichunt 示例与常见部署需求）

在 `config.toml` 中可以使用如下示例作为起点（请根据你的站点信息替换 `base_url`、作者和社交信息）：

```toml
base_url = "https://USERNAME.github.io/REPO-NAME"  # 替换为实际站点 URL
theme = "vonge"
compile_sass = true
generate_feeds = true
feed_filenames = ["atom.xml"]
minify_html = true
build_search_index = true

taxonomies = [
  { name = "tags", feed = true },
]

[markdown.highlighting]
theme = "catppuccin-mocha"
```

说明：
- `compile_sass`：自动编译主题中的 Sass（如使用主题自带样式则开启）。
- `build_search_index`：生成用于前端搜索的索引文件（若使用 JS 搜索库可开启）。
- `generate_feeds` / `feed_filenames`：启用 Atom/RSS 输出。

---

## 👷 使用（结构化 front matter）

主题使用 **结构化 front matter** 来构建灵活页面布局。例如 `content/blog/_index.md`：

```toml
+++
title = "Blog"
sort_by = "date"
paginate_by = 6

[extra]
content_blocks = [
  { block = "page-heading", title = "Blog", description = "Vonge blog features productivity, tips, inspiration and strategies for massive profits. Find out how to set up a successful blog or how to make yours even better!" },
  { block = "posts-list", show_posts = true },
  { block = "newsletter", newsletter_title = "Join my mailing list", newsletter_description = "Get inspiration, updates and, cool stuff!", newsletter_identifier = "", newsletter_button = "Subscribe" }
]
+++
```

你也可以通过编辑主题的模板和 SCSS 来创建或扩展自定义区块。

---

## 🚀 部署建议（示例：GitHub Pages via Actions）

下面给出一个简单的 GitHub Actions 工作流示例，用于在 `push` 到 `main` 时构建并发布到 GitHub Pages（使用 `peaceiris/actions-gh-pages`）：

```yaml
name: Build and Deploy

on:
  push:
    branches: [ main ]

jobs:
  build:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4
        with:
          submodules: true
      - name: Install Zola
        run: |
          sudo apt-get update
          sudo apt-get install -y zola
      - name: Build
        run: zola build -o public
      - name: Deploy to GitHub Pages
        uses: peaceiris/actions-gh-pages@v3
        with:
          github_token: ${{ secrets.GITHUB_TOKEN }}
          publish_dir: ./public
```

注意：不同 CI 环境安装 Zola 的方式不同，也可以使用官方提供的二进制或第三方的 setup-zola action。

---

## 🙏 致谢

本主题基于 CloudCannon 的原始 [Vonge Hugo Bookshop template](https://github.com/CloudCannon/vonge-hugo-bookshop-template) 改编而来，所有设计归原作者所有。

---

## 📄 贡献

欢迎对本移植版提交 PR、Issue 或改进建议！

---

## 📎 原始英文 README（保留）

If you prefer the original English README, it is retained in the repository history; the demo is at https://paberr.github.io/vonge-zola-theme/.
