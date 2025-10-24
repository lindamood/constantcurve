# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

Constant Curve is a blog built with **Eleventy Excellent**, a comprehensive Eleventy starter template based on Andy Bell's CUBE CSS methodology. This is a production-ready static site generator with built-in accessibility, performance optimization, and modern web features.

## Technology Stack

- **Static Site Generator**: Eleventy v3.1.2
- **Template Engine**: Nunjucks (.njk)
- **Styling**: Tailwind CSS with CUBE CSS methodology
- **Bundling**: esbuild for JavaScript, PostCSS for CSS
- **Image Optimization**: eleventy-img (automatic AVIF/WebP)
- **Deployment**: Netlify (configured via netlify.toml)

## Requirements

- **Node.js**: v20 or higher (currently using v20.19.5 via nvm)
- **npm**: v10 or higher

## Development Commands

### Start Development Server
```bash
npm start          # Starts watch tasks and dev server at http://localhost:8080
```

### Build for Production
```bash
npm run build      # Clean + production build to dist/
```

### Other Commands
```bash
npm run clean      # Remove dist/ and generated files
npm run favicons   # Generate favicon assets
npm run colors     # Generate color scheme
```

## Project Architecture

### Directory Structure

```
src/
├── _config/           # Eleventy configuration modules
│   ├── collections.js # Post collections, tags, sitemap
│   ├── events.js      # Build events (CSS/JS compilation)
│   ├── filters.js     # Nunjucks filters
│   ├── plugins.js     # Eleventy plugins
│   └── shortcodes.js  # Custom shortcodes
├── _data/             # Global data files (site config, navigation, etc.)
├── _includes/         # Reusable components and partials
│   ├── css/          # Generated CSS (gitignored)
│   └── scripts/      # Generated JS (gitignored)
├── _layouts/          # Page templates (base.njk, post.njk, page.njk)
├── assets/            # Static assets (images, CSS source, JS source, SVGs)
├── common/            # Utility templates (feeds, sitemap, 404, OG images)
├── docs/              # Documentation markdown files
├── pages/             # Static pages (about, blog index, etc.)
└── posts/             # Blog posts organized by year/date
    └── YYYY/          # Year folders
        └── YYYY-MM-DD-slug/ # Post folders with images
```

### Output
- **dist/** - Production build output (gitignored)

### Key Configuration Files
- **eleventy.config.js** - Main Eleventy config (imports from src/_config/)
- **tailwind.config.js** - Tailwind CSS configuration
- **netlify.toml** - Netlify deployment settings
- **.env** - Environment variables (create from .env-sample)

## Blog Content Workflow

### Creating a New Blog Post

1. Create a new folder in `src/posts/YYYY/YYYY-MM-DD-title/`
2. Add a markdown file (e.g., `post-name.md`) with frontmatter:
```markdown
---
title: 'Your Post Title'
description: 'Post description for SEO'
date: 2025-01-15
tags: ['tag1', 'tag2']
---

Your content here...
```

3. Add post images to the same folder
4. Images are automatically optimized during build

### Post Frontmatter Options
- `title` - Post title (required)
- `description` - Meta description (required)
- `date` - Publication date (required)
- `tags` - Array of tags
- `draft` - Set to `true` to hide in production
- `permalink` - Custom URL path (optional)

### Available Shortcodes
- `{% image %}` - Optimized responsive images
- `{% youtube %}` - Embedded YouTube videos (lite-youtube)
- `{% peertube %}` - PeerTube embeds
- Various text formatting shortcodes

## Styling System

### CUBE CSS Methodology
- **C**omposition - Layout patterns
- **U**tilities - Tailwind utility classes
- **B**locks - Component-specific styles
- **E**xceptions - Contextual variations

### CSS Files
- Source: `src/assets/css/`
- Compiled to: `src/_includes/css/` (during build)
- Uses PostCSS with Tailwind

### Dark/Light Mode
Built-in theme switcher respects user preferences and provides manual toggle.

## Key Features

### Performance
- Perfect Lighthouse scores out of the box
- Automatic image optimization (AVIF, WebP, fallbacks)
- Per-page CSS bundles
- Minified HTML, CSS, JS in production

### SEO & Social
- Auto-generated Open Graph images for posts
- XML sitemap
- RSS/Atom/JSON feeds
- Structured data

### Accessibility
- Accessible navigation patterns
- Skip links
- Proper heading hierarchy
- Keyboard navigation support

## Development Workflow

1. **Start dev server**: `npm start`
2. **Create content**: Add markdown files in `src/posts/` or `src/pages/`
3. **Customize design**: Edit CSS in `src/assets/css/`
4. **Build for production**: `npm run build`
5. **Deploy**: Push to GitHub (auto-deploys to Netlify)

## Deployment

### Netlify Configuration
- Build command: `npm run build`
- Publish directory: `dist`
- Node version: 20 (specified in netlify.toml)
- Redirects configured in `src/common/_redirects.njk`

## Common Tasks

### Update Site Metadata
Edit `src/_data/meta.js`

### Change Navigation
Edit `src/_data/navigation.js`

### Modify Color Scheme
Edit `src/_data/designTokens/colors.js` and run `npm run colors`

### Add a New Page
Create `src/pages/page-name.md` with frontmatter

## Notes

- The starter includes extensive demo content in `src/posts/` and `src/docs/`
- Demo posts can be deleted or used as templates
- Configuration is modular - most settings in `src/_config/` and `src/_data/`
- Built-in styleguide available at `/styleguide/`
