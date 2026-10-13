# AGENTS.md

This file provides guidance for AI coding agents working on this repository.

## Project Overview

**Solo** is a minimal Ghost theme focused on showcasing the work of an individual writer or creator. It is built for [Ghost](https://ghost.org), an open-source publishing platform.

## Tech Stack

- **Templating**: Handlebars (`.hbs` files)
- **Styling**: PostCSS with autoprefixer and cssnano
- **JavaScript**: Vanilla JS, minified via Gulp
- **Build Tool**: Gulp 5
- **Package Manager**: pnpm

## Project Structure

```
├── *.hbs                    # Main template files (index, post, page, author, tag, default)
├── partials/                # Reusable Handlebars partials
│   └── icons/               # SVG icon partials
├── assets/
│   ├── css/                 # Source CSS files (edit these)
│   ├── js/                  # Source JS files (edit these)
│   ├── built/               # Compiled assets (do not edit directly)
│   ├── fonts/               # Web fonts
│   └── images/              # Theme images
├── locales/                 # Translation files (JSON)
├── gulpfile.js              # Build configuration
└── package.json             # Theme metadata and dependencies
```

## Development Commands

```bash
# Install dependencies
pnpm install

# Build assets and watch for changes (development)
pnpm dev

# Run theme validation
pnpm test

# Package theme for distribution
pnpm zip
```

## Key Guidelines

### Template Files (.hbs)

- Ghost uses Handlebars templating with custom helpers
- Main templates: `default.hbs` (base layout), `index.hbs` (homepage), `post.hbs` (single post), `page.hbs` (static pages), `author.hbs`, `tag.hbs`
- Partials in `partials/` are included via `{{> partial-name}}`
- Ghost-specific helpers include `{{#foreach}}`, `{{content}}`, `{{title}}`, `{{date}}`, `{{tags}}`, etc.

### CSS

- Edit files in `assets/css/`, not `assets/built/`
- Entry point is `assets/css/screen.css`
- Uses PostCSS with future CSS syntax support
- Compiled output goes to `assets/built/screen.css`

### JavaScript

- Edit files in `assets/js/`, not `assets/built/`
- Main entry point is `assets/js/main.js`
- Additional libraries can be placed in `assets/js/lib/`
- Compiled output goes to `assets/built/main.min.js`

### Theme Configuration

- Theme settings are defined in `package.json` under `config.custom`
- These settings appear in Ghost Admin under Design settings
- Available setting types: `color`, `select`, `text`, `boolean`, `image`

### Localization

- Translation files are in `locales/` as JSON
- Use `{{t "string"}}` helper in templates for translatable strings

## Testing

Run `pnpm test` to validate the theme using [gscan](https://github.com/TryGhost/gscan), Ghost's official theme validator. This checks for:

- Required files and structure
- Template syntax errors
- Deprecated features
- Best practices compliance

## CI/CD

The GitHub Actions workflow (`.github/workflows/main.yml`) automatically deploys the theme to Ghost when pushing to `main` or `master` branches.

## Common Tasks

### Adding a new partial
1. Create `.hbs` file in `partials/`
2. Include in templates with `{{> partial-name}}`

### Adding custom theme settings
1. Add setting definition to `package.json` under `config.custom`
2. Access in templates via `@custom.setting_name`

### Modifying styles
1. Edit CSS files in `assets/css/`
2. Run `pnpm dev` to compile and watch for changes
3. Compiled CSS appears in `assets/built/`

## Resources

- [Ghost Theme Documentation](https://ghost.org/docs/themes/)
- [Ghost Handlebars Helpers](https://ghost.org/docs/themes/helpers/)
- [gscan Theme Validator](https://github.com/TryGhost/gscan)


# Upstream guidance

## Scope

This package is the Solo Ghost theme. In the standalone mirror repository, this tree is pushed from `TryGhost/Themes/packages/solo` by subtree sync; make durable theme-content changes in `TryGhost/Themes` unless the task is explicitly repo-level metadata or GitHub settings.

## Commands

Use pnpm, pinned by `package.json`.

```bash
pnpm install
pnpm dev
pnpm test
pnpm zip
```

From the `TryGhost/Themes` monorepo root, validate this package with:

```bash
pnpm test:ci --theme solo
```

## Boundaries

- Edit source CSS in `assets/css/`, source JavaScript in `assets/js/`, and templates/partials as `.hbs` files.
- Keep generated `assets/built/` files in sync when source assets change.
- Do not commit `node_modules/`, secrets, or local Ghost content.
- Translation changes normally belong in `TryGhost/Themes/packages/theme-translations`; package-local locale overrides should be intentional and rebuilt.
