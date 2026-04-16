# 📝 Blogs — Static Blog Platform

A clean, responsive, and fully static blog website built with **pure HTML5, CSS3, and Vanilla JavaScript** — no frameworks, no dependencies, no build tools. Articles are served as standalone HTML pages and the entire site is auto-deployed to **GitHub Pages** via a GitHub Actions CI/CD pipeline.

**Live Site →** `https://vikasprajapati1998.github.io/Blogs/`

---

## 📑 Table of Contents

- [Overview](#overview)
- [Live Articles](#live-articles)
- [Project Structure](#project-structure)
- [Architecture & Flow](#architecture--flow)
- [Features](#features)
- [Tech Stack](#tech-stack)
- [CI/CD Pipeline](#cicd-pipeline)
- [Getting Started (Clone & Run Locally)](#getting-started-clone--run-locally)
- [Adding a New Blog Post](#adding-a-new-blog-post)
- [License](#license)

---

## Overview

This repository is a **zero-dependency static blog** designed for simplicity and speed. Each blog post is a self-contained HTML file with its own stylesheet (`.css`) and interactivity script (`.js`). The home page (`index.html`) displays all articles in a responsive card grid. Any push to the `main` branch triggers a GitHub Actions workflow that automatically publishes the latest content to GitHub Pages.

---

## Live Articles

| # | Title | Topic Tag | Published | Read Time |
|---|-------|-----------|-----------|-----------|
| 1 | [New Scope in AI: Trends and Implications](contents/html/New_Scope_in_AI-_Trends_and_Implications.html) | New Scope in AI | Apr 01, 2026 | ~7 min |
| 2 | [The Value of a Nobel Prize](contents/html/The_Value_of_a_Nobel_Prize.html) | Value of Nobel Prize | Apr 01, 2026 | ~6 min |

---

## Project Structure

```
Blogs/
│
├── index.html                      # 🏠 Home page — blog card grid listing all posts
├── style.css                       # 🎨 Home page stylesheet (CSS Grid, card hover, responsive)
├── script.js                       # ⚡ Home page JS (IntersectionObserver scroll animation)
│
├── images/
│   └── BlogLogo.png                # 🖼️  Hero banner image displayed in the site header
│
├── contents/
│   ├── html/                       # 📄 Individual blog post HTML files
│   │   ├── New_Scope_in_AI-_Trends_and_Implications.html
│   │   └── The_Value_of_a_Nobel_Prize.html
│   │
│   ├── css/                        # 🎨 Per-post stylesheets (reading bar, article layout)
│   │   ├── New_Scope_in_AI-_Trends_and_Implications.css
│   │   └── The_Value_of_a_Nobel_Prize.css
│   │
│   ├── js/                         # ⚡ Per-post interactivity scripts
│   │   ├── New_Scope_in_AI-_Trends_and_Implications.js
│   │   └── The_Value_of_a_Nobel_Prize.js
│   │
│   └── images/                     # 🖼️  Per-post image assets (organized by post name)
│       ├── New_Scope_in_AI-_Trends_and_Implications/
│       │   ├── ai_trends_forecast.png
│       │   ├── edge_ai_architecture.png
│       │   └── qkv_attention_flow.png
│       └── The_Value_of_a_Nobel_Prize/
│           ├── qkv_nobel_prize_economic_value.png
│           ├── qkv_nobel_prize_legacy.png
│           └── qkv_nobel_prize_taxation.png
│
├── .github/
│   └── workflows/
│       └── static.yml              # 🚀 GitHub Actions — auto-deploy to GitHub Pages
│
├── LICENSE                         # 📜 Repository license
└── README.md                       # 📖 This file
```

### Naming Convention

All per-post assets follow a consistent, predictable naming pattern:

```
<Post_Title_Slug>.html        →  contents/html/
<Post_Title_Slug>.css         →  contents/css/
<Post_Title_Slug>.js          →  contents/js/
<Post_Title_Slug>/            →  contents/images/  (subfolder per post)
```

This 1-to-1 mapping between a post and its assets makes adding, updating, or removing a post entirely straightforward.

---

## Architecture & Flow

```
┌─────────────────────────────────────────────────────────────┐
│                        REPOSITORY                           │
│                                                             │
│  index.html  ──── style.css                                 │
│       │       └── script.js                                 │
│       │                                                     │
│       │  Blog Card Grid (CSS Grid, auto-fill)               │
│       │  Each card links to a post inside contents/html/    │
│       │                                                     │
│       └──► contents/html/<Post>.html                        │
│                  │                                          │
│                  ├── contents/css/<Post>.css                │
│                  ├── contents/js/<Post>.js                  │
│                  └── contents/images/<Post>/*.png           │
│                                                             │
└─────────────────────────────────────────────────────────────┘
                           │
              Git push to main branch
                           │
                           ▼
┌─────────────────────────────────────────────────────────────┐
│              GitHub Actions  (static.yml)                   │
│                                                             │
│  1. Checkout repository                                     │
│  2. Configure GitHub Pages environment                      │
│  3. Upload entire repo as Pages artifact                    │
│  4. Deploy → https://vikasprajapati1998.github.io/Blogs/   │
└─────────────────────────────────────────────────────────────┘
```

### Request Flow (End-User Perspective)

```
User visits homepage
       │
       ▼
  index.html loaded
  style.css applied (gradient header, card grid)
  script.js executed (IntersectionObserver animates cards on scroll)
       │
       ▼
  User clicks "Read →" on a blog card
       │
       ▼
  contents/html/<Post>.html loaded
  contents/css/<Post>.css applied (article layout, reading progress bar)
  contents/js/<Post>.js executed:
    ├── Reading progress bar (updates on scroll)
    ├── Copy buttons injected into <pre> code blocks
    └── Smooth-scroll for in-page anchor links
```

---

## Features

### Home Page (`index.html`)

| Feature | Implementation |
|---|---|
| Responsive blog card grid | CSS Grid with `repeat(auto-fill, minmax(300px, 1fr))` |
| Card scroll-reveal animation | `IntersectionObserver` API (no layout jank, GPU-composited) |
| Hover lift effect | CSS `transform: translateY(-3px)` + `box-shadow` transition |
| Full-width hero banner | `object-fit: cover` at `50vh` height |
| CSS custom properties | Centralized design tokens (`--accent`, `--bg`, `--fg`, etc.) |
| Mobile-first breakpoints | `@media` at `640px` and `1024px` |

### Individual Blog Post Pages (`contents/html/`)

| Feature | Implementation |
|---|---|
| Reading progress bar | Fixed `<div id="readingBar">` updated via `scroll` event listener |
| Copy-code buttons | Dynamically injected `<button>` elements on all `<pre>` blocks |
| Smooth anchor scrolling | `scrollIntoView({ behavior: 'smooth' })` for `a[href^="#"]` |
| Breadcrumb navigation | `← All Blogs` link back to `index.html` |
| Estimated read time | Statically authored in article metadata (`~N min read`) |
| Scoped per-post styling | Each post has its own `.css` file, no style bleed between posts |

---

## Tech Stack

| Layer | Technology |
|---|---|
| Markup | HTML5 (semantic elements: `<article>`, `<header>`, `<time>`, `<nav>`) |
| Styling | CSS3 — Custom Properties, CSS Grid, Flexbox, `clamp()` |
| Interactivity | Vanilla JavaScript (ES5-compatible IIFE pattern) |
| Hosting | GitHub Pages |
| CI/CD | GitHub Actions |
| Version Control | Git / GitHub |

**No external dependencies.** No npm, no bundler, no runtime framework. The entire site is plain HTML files that open in any browser.

---

## CI/CD Pipeline

The file `.github/workflows/static.yml` defines the deployment pipeline:

```yaml
on:
  push:
    branches: ["main"]    # Auto-deploys on every push to main
  workflow_dispatch:       # Also supports manual trigger from Actions tab

permissions:
  contents: read
  pages: write
  id-token: write

concurrency:
  group: "pages"
  cancel-in-progress: false   # Ongoing deployments are never cancelled
```

**Deployment steps:**

1. **Checkout** — checks out the full repository at the pushed commit
2. **Setup Pages** — configures the GitHub Pages environment and base URL
3. **Upload artifact** — packages the entire repository root as the Pages artifact
4. **Deploy** — publishes to GitHub Pages and outputs the live URL

> Deployment typically completes in under 60 seconds after a push.

---

## Getting Started (Clone & Run Locally)

### Prerequisites

- [Git](https://git-scm.com/) installed
- Any modern web browser (Chrome, Firefox, Edge, Safari)
- *(Optional)* A local static file server for accurate relative-path resolution

### Clone the Repository

```bash
git clone https://github.com/VikasPrajapati1998/Blogs.git
cd Blogs
```

### Run Locally

**Option 1 — Open directly in a browser (simplest):**

```bash
# macOS
open index.html

# Linux
xdg-open index.html

# Windows
start index.html
```

**Option 2 — Serve with Python's built-in HTTP server (recommended):**

```bash
# Python 3
python3 -m http.server 8080

# Then open in browser:
# http://localhost:8080
```

**Option 3 — Serve with Node.js `serve` package:**

```bash
npx serve .
# Then open the URL shown in the terminal
```

> Using a local server (Options 2 or 3) ensures all relative asset paths (`contents/html/`, `contents/images/`, etc.) resolve correctly, which is the same behavior as the live GitHub Pages environment.

---

## Adding a New Blog Post

Follow these steps to add a new article to the blog:

### 1. Create the Post HTML

Copy an existing post as a template:

```bash
cp contents/html/New_Scope_in_AI-_Trends_and_Implications.html \
   contents/html/Your_New_Post_Title.html
```

Edit the new file and update:
- `<title>` and `<meta name="description">`
- `<link rel="stylesheet">` → point to your new CSS file
- `<span class="topic-tag">`, `<h1 class="article-title">`, `<time datetime="...">`, `<span class="reading-time">`
- The `<div class="article-body">` section with your content

### 2. Create the Post CSS

```bash
cp contents/css/New_Scope_in_AI-_Trends_and_Implications.css \
   contents/css/Your_New_Post_Title.css
```

Customize colors or typography if needed.

### 3. Create the Post JS

```bash
cp contents/js/New_Scope_in_AI-_Trends_and_Implications.js \
   contents/js/Your_New_Post_Title.js
```

Update the `<script src="">` path in your HTML to point to this file.

### 4. Add Post Images

```bash
mkdir -p contents/images/Your_New_Post_Title
# Copy or move your images into this directory
```

Reference them in your HTML using relative paths:

```html
<img src="../images/Your_New_Post_Title/your_image.png" alt="Description" />
```

### 5. Register the Post on the Home Page

Open `index.html` and add a new `<article>` block inside the `<!-- BLOG_ENTRIES_START -->` / `<!-- BLOG_ENTRIES_END -->` markers:

```html
<article class="blog-card" data-date="2026-05-01T09:00:00">
  <div class="card-body">
    <span class="tag">Your Topic Tag</span>
    <h2 class="card-title">
      <a href="contents/html/Your_New_Post_Title.html">Your New Post Title</a>
    </h2>
    <p class="card-excerpt">A short excerpt or description of the post.</p>
    <div class="card-footer">
      <time datetime="2026-05-01T09:00:00">May 01, 2026</time>
      <a class="read-btn" href="contents/html/Your_New_Post_Title.html">Read →</a>
    </div>
  </div>
</article>
```

### 6. Commit and Push

```bash
git add .
git commit -m "Add new post: Your New Post Title"
git push origin main
```

The GitHub Actions workflow will automatically detect the push and deploy the updated site to GitHub Pages within ~60 seconds.

---

## License

This project is licensed under the terms of the [LICENSE](LICENSE) file included in this repository.

---

> Built with ❤️ by [Vikas Prajapati](https://github.com/VikasPrajapati1998) · Powered by GitHub Pages
