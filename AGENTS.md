# AGENTS.md

This file provides guidance for AI coding agents working on this repository.

## Project Overview

**Solo** is a minimal Ghost theme focused on showcasing the work of an individual writer or creator. It is built for [Ghost](https://ghost.org), an open-source publishing platform.

## Tech Stack

- **Templating**: Handlebars (`.hbs` files)
- **Styling**: PostCSS with autoprefixer and cssnano
- **JavaScript**: Vanilla JS, minified via Gulp
- **Build Tool**: Gulp 5
- **Package Manager**: Yarn

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
yarn

# Build assets and watch for changes (development)
yarn dev

# Run theme validation
yarn test

# Package theme for distribution
yarn zip
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

Run `yarn test` to validate the theme using [gscan](https://github.com/TryGhost/gscan), Ghost's official theme validator. This checks for:

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
2. Run `yarn dev` to compile and watch for changes
3. Compiled CSS appears in `assets/built/`

## Resources

- [Ghost Theme Documentation](https://ghost.org/docs/themes/)
- [Ghost Handlebars Helpers](https://ghost.org/docs/themes/helpers/)
- [gscan Theme Validator](https://github.com/TryGhost/gscan)
