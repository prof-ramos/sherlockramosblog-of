# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

This is a Hugo static site built with the **PaperMod theme** in **ProfileMode**. The site is configured for Portuguese (pt-br) content and uses a custom navy color scheme. Hugo v0.146.0 is the fixed version used for builds.

## Development Commands

### Local Development
```bash
hugo server -D
```
Starts local server at `http://localhost:1313` with live reload. Includes draft posts (`draft: true`).

### Production Build
```bash
hugo --gc --minify
```
Generates optimized production build with garbage collection and minification.

```bash
./build.sh
```
**Use this before deploying or opening PRs.** Ensures Hugo v0.146.0 is installed and runs the official build pipeline.

### Content Creation
```bash
hugo new posts/nome-do-post.md
```
Creates new post using `archetypes/default.md` template. Use kebab-case for filenames.

### Validation Commands
```bash
hugo --gc --printI18nWarnings --printPathWarnings
```
Checks for broken links, missing translations, and asset issues before opening PRs.

## Architecture & Structure

### Content Organization
- **content/posts/**: Blog posts in Markdown
- **content/about/**: About page content
- All content should be in Portuguese unless specified otherwise
- Front matter uses YAML format with required fields: `title`, `date`, `draft`

### Theme Customization Architecture
- **DO NOT modify `themes/PaperMod/`** - treat as read-only to facilitate theme updates
- Custom CSS overrides: `assets/css/extended/custom.css`
- Custom layouts: Place in `layouts/` directory (currently empty, but this is where overrides should go)
- The site uses a custom navy color scheme defined in `custom.css` with separate light/dark mode variables

### Configuration
- **hugo.yaml**: Main site configuration
  - PaperMod is configured in ProfileMode (homepage shows profile, not post list)
  - Social icons configured in `params.socialIcons`
  - Menu structure defined in `menu.main`
  - Default language: `pt-br`

### Generated vs. Source Files
- **public/**: Generated output directory - NEVER edit manually
- **resources/**: Hugo cache directory - regenerated on builds with `--gc`
- Both should be in `.gitignore`

### Internal Documentation
Project maintains detailed Portuguese documentation in `docs/`:
- `1-personalizacao.md`: Theme customization guide
- `2-criacao-de-conteudo.md`: Content publishing workflow
- `3-mudanca-tema-navy.md`: Navy theme history
- `4-avaliacao-ui-ux.md`: UX evaluation report

## Coding Conventions

### File Naming
- Use **kebab-case** for all content files: `analise-ux.md`, not `analise_ux.md`
- Keep content in Portuguese unless otherwise specified

### Front Matter Format
Always use YAML (not TOML or JSON):
```yaml
---
title: "Post Title"
date: 2024-01-01
draft: true
tags: ["tag1", "tag2"]
summary: "Optional summary"
---
```

### CSS Customization
- Use 4-space indentation in `custom.css`
- Group variables by light/dark mode (`:root` and `.dark`)
- Use `!important` sparingly - currently used for color variables to ensure navy theme overrides

### Content Guidelines
- Prefer short headings
- Avoid embedded HTML when possible
- Use shortcodes sparingly to maintain theme compatibility
- All content should be in Portuguese

## Testing & Validation

There is no automated test suite. Manual validation required:

1. **During development**: Run `hugo server -D` and verify changes
2. **Monitor terminal warnings** for asset/link issues
3. **Before PRs**: Run `hugo --gc --printI18nWarnings --printPathWarnings`
4. **Visual changes**: Document manual verification and attach screenshots in PR

## Build System Details

### build.sh Script
- Downloads Hugo v0.146.0 Extended to `~/.local/bin/hugo` if not present or wrong version
- Currently configured for Linux 64-bit
- Runs `hugo --gc` (garbage collection enabled, minification not forced)
- This script ensures reproducible builds with the exact Hugo version

## Deployment Notes

- Output directory: `public/`
- Compatible with: Netlify, Vercel, GitHub Pages, or any static hosting
- No secrets should be versioned - configure sensitive variables in hosting platform
- Always run `./build.sh` before deploying to ensure correct Hugo version
