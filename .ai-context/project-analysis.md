# Jekyll Blog Project Analysis

> Generated: Auto-updated
> Project: aakiliqbal.github.io/blog

---

## 1. Theme & Identity

| Field | Value |
|-------|-------|
| **Theme** | `jekyll-theme-chirpy` v7.3.1 |
| **Site Title** | aakiliqbal |
| **Author** | Mohammad Aakil Iqbal |
| **URL** | `https://aakiliqbal.github.io/blog` |
| **Base URL** | `/blog` |
| **Tagline** | "A technical blog about programming, technology, and life." |
| **Language** | English |
| **Social - GitHub** | `aakiliqbal` |
| **Social - Twitter** | `iqbalthepal` |
| **Email** | aakiliqbal645@gmail.com |

---

## 2. Directory Structure

```
D:\GitHub\blog\
├── _config.yml              # Main Jekyll configuration
├── Gemfile                  # Ruby dependencies
├── Gemfile.lock             # Locked dependency versions
├── index.html               # Homepage (layout: home)
├── LICENSE
├── README.md
├── .nojekyll                # Tells GitHub Pages not to process with Jekyll
├── .editorconfig
├── .gitattributes
├── .gitignore
├── .gitmodules
│
├── _data/                   # Data files
│   ├── contact.yml          # Contact/social link options
│   └── share.yml            # Post sharing platforms
│
├── _plugins/                # Custom Jekyll plugins
│   └── posts-lastmod-hook.rb  # Auto-sets last_modified_at from git history
│
├── _posts/                  # Blog posts
│   ├── .placeholder
│   ├── 2025-08-31-discovering-the-magic-of-abacus.md
│   ├── 2025-09-01-getting-cozy-with-spring-boot-s-webclient.md
│   └── 2025-09-09-leetcode-merge-sorted-array.md
│
├── _tabs/                   # Tabbed navigation pages (Chirpy-specific)
│   ├── about.md             # About page (order: 4)
│   ├── archives.md          # Archives page (order: 3)
│   ├── categories.md        # Categories page (order: 1)
│   └── tags.md              # Tags page (order: 2)
│
├── assets/                  # Static assets
│   ├── avatar.png           # Sidebar avatar
│   ├── header-image.gif     # Animated header on about page
│   ├── img/
│   │   ├── leetcode/header.png
│   │   ├── 2025-08-31-discovering-the-magic-of-abacus/abacus-header.png
│   │   ├── 2025-09-01-getting-cozy-with-spring-boot-s-webclient/webclient-header.png
│   │   └── favicons/        # Favicon set
│   └── lib/                 # Third-party libs (empty)
│
├── _site/                   # Generated site output
│   └── assets/js/dist/      # Compiled theme JS (commons, home, post, page, categories, misc)
├── .jekyll-cache/           # Jekyll build cache
│
├── .github/
│   └── workflows/
│       ├── jekyll.yml           # CI/CD: Build & deploy to GitHub Pages
│       └── youtube-workflow.yml # Scheduled: Auto-update YouTube videos
│
├── .devcontainer/           # VS Code Dev Container config
│   ├── devcontainer.json
│   └── post-create.sh
│
├── .vscode/                 # VS Code workspace settings
├── tools/                   # Utility scripts
│   ├── run.sh               # Run jekyll serve with options
│   └── test.sh              # Build + html-proofer testing
│
└── .ai-context/             # AI context files (this directory)
    └── project-analysis.md
```

---

## 3. Key Configuration (`_config.yml`)

### Site & SEO
- **URL:** `https://aakiliqbal.github.io`
- **Base URL:** `/blog`
- **Webmaster verifications:** Configured for Google, Bing, Alexa, Yandex, Baidu, Facebook (all empty/unfilled)

### Analytics & Page Views
- **GoatCounter:** ID `aakiliqbal` (active)
- **Pageviews provider:** `goatcounter`
- Google Analytics, Umami, Matomo, Cloudflare, Fathom: configured but IDs are empty

### Theme & Appearance
- **Theme mode:** Not set (follows system preference, with toggle available)
- **TOC (Table of Contents):** Enabled globally (`toc: true`)
- **Avatar:** Custom Twitter profile image URL
- **PWA:** Enabled with offline cache (denies caching for `/blog/about`)

### Comments
- **Primary:** `giscus` (GitHub Discussions-based)
  - Repo: `aakiliqbal/blog`
  - Category: Q&A
  - Mapping: `title`
- **Secondary:** `utterances`
  - Repo: `aakiliqbal/blog`
  - Issue term: `title`

### Markdown & Syntax
- **Processor:** Kramdown
- **Syntax highlighter:** Rouge
- **Code blocks:** Line numbers enabled, starting at line 1
- **Footnote backlink:** Custom unicode character

### Collections & Defaults
- **Tabs collection:** Output enabled, sorted by `order`
- **Posts default layout:** `post`, comments enabled, TOC enabled
- **Posts permalink:** `/posts/:title/`
- **Tabs default layout:** `page`
- **Tabs permalink:** `/:title/`

### Pagination
- **Paginate:** 10 posts per page

### Archives
- **jekyll-archives:** Enabled for categories and tags
- **Tag permalinks:** `/tags/:name/`
- **Category permalinks:** `/categories/:name/`

### Performance
- **SASS style:** Compressed
- **HTML compression:** Enabled (clippings, comments, endings all set to `all`; disabled in development)

---

## 4. Dependencies

### Ruby Gems (Gemfile)
| Gem | Version | Purpose |
|-----|---------|---------|
| `jekyll-theme-chirpy` | ~> 7.3, >= 7.3.1 | The blog theme |
| `html-proofer` | ~> 5.0 | Testing broken links |
| `jekyll-compose` | latest | Jekyll plugin for post creation |
| `tzinfo` / `tzinfo-data` | >= 1, < 3 | Timezone support (Windows) |
| `wdm` | ~> 0.2.0 | Windows file watcher |

### Transitive Dependencies (from Gemfile.lock)
| Gem | Version | Purpose |
|-----|---------|---------|
| `jekyll` | 4.4.1 | Static site generator |
| `jekyll-archives` | 2.3.0 | Category/tag archives |
| `jekyll-include-cache` | 0.2.1 | Include caching |
| `jekyll-paginate` | 1.1.0 | Pagination |
| `jekyll-seo-tag` | 2.8.0 | SEO meta tags |
| `jekyll-sitemap` | 1.4.0 | XML sitemap |
| `kramdown` | 2.5.1 | Markdown processor (with GFM) |
| `rouge` | 4.6.0 | Syntax highlighting |
| `sass-embedded` | 1.91.0 | SCSS compilation |

**Platform:** `x64-mingw-ucrt` (Windows)
**Bundler version:** 2.7.1

**No Node.js dependencies** — no `package.json` exists.

---

## 5. Custom Plugins & Scripts

### `_plugins/posts-lastmod-hook.rb`
Custom Ruby plugin that hooks into Jekyll's post initialization to automatically set the `last_modified_at` front matter field based on the most recent git commit date for each post file.

### `tools/run.sh`
Convenience script to run `bundle exec jekyll serve` with options:
- `-H, --host [HOST]` — set bind host
- `-p, --production` — run in production mode
- Auto-detects Docker and adds `--force_polling`

### `tools/test.sh`
Builds the site in production mode and runs `html-proofer` to check for broken links (external URLs disabled, localhost URLs ignored).

---

## 6. GitHub Actions / CI/CD

### Workflow 1: `jekyll.yml` — Deploy to GitHub Pages
- **Trigger:** Push to `main` branch, or manual dispatch
- **Ruby version:** 3.1
- **Steps:**
  1. Checkout code
  2. Setup Ruby with bundler cache
  3. Configure GitHub Pages
  4. Build with Jekyll (`JEKYLL_ENV=production`)
  5. Upload artifact
  6. Deploy to GitHub Pages
- **Concurrency:** Single deployment at a time, no cancellation of in-progress runs
- **Permissions:** `contents: read`, `pages: write`, `id-token: write`

### Workflow 2: `youtube-workflow.yml` — Auto-Update YouTube Videos
- **Trigger:** Monthly cron (`0 0 1 * *`), or manual dispatch
- **Action:** Uses `gautamkrishnar/blog-post-workflow` to fetch latest videos from YouTube channel `UCXK4VE1yIjPBquHIpZi5uMA` and inject them into `_tabs/about.md` between `<!-- YOUTUBE:START -->` and `<!-- YOUTUBE:END -->` comment tags.

---

## 7. Dev Container Setup

**Image:** `mcr.microsoft.com/devcontainers/jekyll:2-bullseye`

**VS Code Extensions pre-installed:**
- Liquid snippets & Shopify Theme Check
- ShellCheck & shfmt
- EditorConfig, Prettier, Stylelint
- Markdown All in One
- Git Graph

**Post-create script (`.devcontainer/post-create.sh`):**
- Installs Node.js LTS + npm (if package.json exists)
- Installs `shfmt`
- Adds zsh plugins: `zsh-syntax-highlighting` and `zsh-autosuggestions`
- Disables `less` pager for `git log`

---

## 8. CSS/SCSS Structure

The project uses the Chirpy theme's built-in SCSS from the gem. No custom `_sass/` directory exists in the project root.

**Configuration:** `sass.style: compressed` for minified output.

The theme provides:
- Dark/light mode variables
- Responsive breakpoints
- Component styles (sidebar, post content, TOC, etc.)

---

## 9. Content Summary

### Blog Posts (3 published)
| Date | Title | Categories | Tags |
|------|-------|-----------|------|
| 2025-08-31 | Discovering the Magic of the Abacus | MATHEMATICS, ABACUS | ABACUS, TOOLS |
| 2025-09-01 | Getting Started with Spring Boot's WebClient | SPRING, WEBCLIENT | PROGRAMMING |
| 2025-09-09 | LeetCode #1 - Merge Sorted Array | LEETCODE, IMPORTANT QUESTION 1/150 | PROGRAMMING, LEETCODE, ARRAY, TWO POINTER, SORTING |

### Tab Pages
| Page | Order | Layout |
|------|-------|--------|
| Categories | 1 | `categories` |
| Tags | 2 | `tags` |
| Archives | 3 | `archives` |
| About | 4 | `page` |

---

## 10. Customizations & Unique Aspects

1. **Rich About Page** (`_tabs/about.md`):
   - Animated GIF header
   - Typing SVG animation from readme-typing-svg
   - GitHub visitor badges, commit badges, follower count badges
   - Spotify "Now Playing" and "Recently Played" widgets
   - Skills & tools displayed as shields.io badges (Java, Python, Spring Boot, AWS, Unity, Blender, etc.)
   - Collapsible GitHub Stats section
   - Auto-updated YouTube video feed via GitHub Actions

2. **Custom Avatar:** Uses a Twitter profile picture as the sidebar avatar.

3. **GoatCounter Analytics:** Privacy-friendly analytics service configured and active.

4. **Dual Comment Systems:** Both Giscus (primary) and Utterances configured, pointing to `aakiliqbal/blog`.

5. **Git-Based Last Modified Dates:** Custom plugin auto-tracks post edit timestamps.

6. **HTML Compression:** Aggressive HTML minification in production.

7. **PWA Support:** Progressive Web App features enabled with installable capability and offline caching.

8. **No Custom Layouts/Includes:** Relies entirely on the Chirpy theme gem.

9. **Compiled Assets:** The `_site/assets/js/dist/` directory contains pre-compiled vanilla JavaScript assets specific to layouts (e.g. `home`, `post`, `categories`) for performance optimization.

---

## 11. Build & Deployment Summary

| Aspect | Details |
|--------|---------|
| **Build Tool** | Jekyll 4.4.1 via Bundler |
| **Ruby Version** | 3.1 (in CI) |
| **Deployment** | GitHub Pages via GitHub Actions |
| **Trigger** | Push to `main` branch |
| **Testing** | `html-proofer` via `tools/test.sh` |
| **Local Dev** | `tools/run.sh` or `bundle exec jekyll serve` |
| **Dev Environment** | VS Code Dev Container (Debian Bullseye + Jekyll) |
| **Base URL** | `/blog` |
| **Production URL** | `https://aakiliqbal.github.io/blog` |

---

## 12. Useful Commands

```bash
# Install dependencies
bundle install

# Run local development server
bundle exec jekyll serve

# Run in production mode
JEKYLL_ENV=production bundle exec jekyll serve

# Run using convenience script
tools/run.sh

# Build site
bundle exec jekyll build

# Test for broken links
tools/test.sh
```

---

## 13. Key File Paths Reference

| Purpose | Path |
|---------|------|
| Main config | `_config.yml` |
| Ruby deps | `Gemfile` |
| Homepage | `index.html` |
| Contact data | `_data/contact.yml` |
| Share data | `_data/share.yml` |
| Custom plugin | `_plugins/posts-lastmod-hook.rb` |
| Blog posts | `_posts/` |
| Tab pages | `_tabs/` |
| About page | `_tabs/about.md` |
| CI/CD - Jekyll | `.github/workflows/jekyll.yml` |
| CI/CD - YouTube | `.github/workflows/youtube-workflow.yml` |
| Dev Container | `.devcontainer/devcontainer.json` |
| Run script | `tools/run.sh` |
| Test script | `tools/test.sh` |
| Avatar | `assets/avatar.png` |
| Favicons | `assets/img/favicons/` |
