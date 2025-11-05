# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

This is a personal blog built with Jekyll and hosted on GitHub Pages. The blog features a Gruvbox-inspired dark theme with a minimalist design using the JetBrains Mono monospace font. The site is deployed automatically via GitHub Actions when changes are pushed to the main branch.

## Development Commands

### Local Development
```bash
bundle install                    # Install dependencies
bundle exec jekyll serve          # Run local dev server at http://localhost:4000
bundle exec jekyll serve --drafts # Run with drafts visible
bundle exec jekyll build          # Build the site to _site/
```

### Building for Production
```bash
JEKYLL_ENV=production bundle exec jekyll build
```

The GitHub Actions workflow automatically builds and deploys to GitHub Pages on push to main.

## Architecture

### Layout Hierarchy
The site uses a nested layout system:
- `default.html` - Base layout with header, footer, and main container
- `home.html` - Extends default, displays post list on homepage
- `post.html` - Extends default, displays individual blog posts with back link
- `tag.html` - Extends default, displays posts filtered by tag

### Tag System
Tags are implemented with a custom static approach:
- Each tag requires a corresponding HTML file in `/tags/` directory (e.g., `tags/emacs.html`)
- Tag files use front matter to specify layout and tag name:
  ```yaml
  ---
  layout: tag
  tag: emacs
  title: "Posts tagged: emacs"
  ---
  ```
- The `tag.html` layout reads `site.tags[page.tag]` to filter posts
- Posts link to tags via `{{ site.baseurl }}/tags/{{ tag | slugify }}/`
- **IMPORTANT**: When adding new tags to posts, you must manually create the corresponding tag page file, otherwise the tag links will be broken

### Content Organization
- Blog posts: `_posts/YYYY-MM-DD-title.md` with front matter (layout, title, date, tags)
- Drafts: `_drafts/YYYY-MM-DD-title.md` (not published by default)
- Static pages: Root-level `.md` files (e.g., `about.md`)
- Generated site: `_site/` (git-ignored)

### Styling
All styles are in a single file: `assets/css/style.css`
- Gruvbox color palette defined as CSS custom properties in `:root`
- Syntax highlighting uses custom classes (`.highlight .c`, `.highlight .k`, etc.)
- Mobile-responsive with media query breakpoint at 768px
- Theme emphasizes readability with careful typography choices

## Configuration

Site configuration is in `_config.yml`:
- Permalink structure: `/:year/:month/:day/:title/`
- Markdown processor: kramdown
- Syntax highlighter: rouge
- Plugins: jekyll-feed, jekyll-seo-tag

## Jekyll-Specific Conventions

### Post Front Matter
```yaml
---
layout: post
title: Post Title
date: YYYY-MM-DD
tags: [tag1, tag2]
---
```

### Liquid Template Variables
- `site.*` - Global site config from _config.yml
- `page.*` - Current page/post metadata
- `post.*` - Post metadata in loops
- `content` - Rendered markdown content

## GitHub Pages Deployment

The site deploys automatically via `.github/workflows/jekyll.yml`:
1. Triggers on push to main or manual workflow dispatch
2. Sets up Ruby 3.1 with bundler cache
3. Builds with `bundle exec jekyll build` (JEKYLL_ENV=production)
4. Uploads and deploys artifact to GitHub Pages

No manual deployment steps required after pushing to main.
