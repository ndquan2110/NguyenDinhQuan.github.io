# Copilot instructions for this repository

This repository is a Hugo static site (personal blog) built with the Ananke theme. The guidance below is tailored to help AI coding agents be immediately productive when making content, site, or theme changes.

High-level architecture
- Hugo site root: the project root contains `hugo.toml`, `content/`, `layouts/`, `themes/`, `static/`, `assets/`, and the generated `public/` folder.
- Theme: `themes/ananke/` contains the Ananke theme (modified). Theme assets and templates are edited in-place (not as a remote module).
- Generated output: `public/` is the static export produced by `hugo` — treat it as build output, not the source of truth for content edits.

Key directories and what to edit
- Content (posts/pages): `content/posts/` and `content/` — add or edit `.md` files (TOML front matter is used; see `content/posts/hello-world.md`).
- Site config: `hugo.toml` — site-wide params (title, baseURL, theme, menu, and `params.github` used by the theme to show a GitHub link).
- Theme templates: `themes/ananke/layouts/partials/` — examples of modified partials in this repo:
  - `themes/ananke/layouts/partials/site-navigation.html` — adds a GitHub link when `params.github` is set.
  - `themes/ananke/layouts/partials/tags.html` — updated to use the `.tag-badge` class (CSS defined below).
  - `themes/ananke/layouts/_default/single.html` — includes `tags.html`.
- Theme assets/styles: `themes/ananke/assets/ananke/css/` — custom CSS additions and fixes are in:
  - `_styles.css` — forced sans-serif for article content and `.tag-badge` styling.
  - `_code.css` — enforces monospaced fonts for code blocks.
- Static & public: `static/` is for custom static files; `public/` is the build output — don't edit `public/` directly for site changes.

Build / preview / deploy workflows (PowerShell examples)
- Local preview with Hugo (development server):
  - If `hugo.exe` is present in repo root: `.\\hugo.exe server -D`
  - Or if Hugo is installed globally: `hugo server -D`
  - Visit: http://localhost:1313
- Build static site (generate `public/`):
  - `hugo` (runs from repo root)
- Important: `public/` is overwritten when you run `hugo`. Use version control for source files in `content/`, `themes/`, `layouts/`, `assets/`, not `public/`.

Conventions and patterns you should follow
- Content front matter: uses TOML-style front matter (see `content/posts/hello-world.md`). Fields commonly used: `date`, `draft`, `title`, `tags`, `categories`.
- Tag & category generation: Tags are placed in front matter `tags = ["tagname"]`. The theme generates tag pages under `public/tags/`.
- Localization / UI text: i18n is handled via theme i18n files (see `themes/ananke/i18n/`). The repo includes some Vietnamese UI changes — prefer editing theme i18n files or partials for UI copy.
- Small UI tweaks live in theme assets: CSS changes are in `themes/ananke/assets/ananke/css/` — run Hugo to compile assets as needed.
- Keep theme modifications small & explicit: Many theme files appear modified (see README notes). When changing theme behavior, update the corresponding partial in `themes/ananke/layouts/partials/` and keep a short comment explaining why.

Integration points & external deps
- The Ananke theme package declares Node dev deps for CSS tooling in `themes/ananke/package.json` (postcss/cssnano). These are only needed if you intend to modify and build theme CSS via Node tooling. For most edits, editing the CSS files directly and running `hugo` is sufficient.
- GitHub link: `params.github` in `hugo.toml` controls display of a GitHub link in the header (see `site-navigation.html`).

Typical tasks and where to make the change (examples)
- Change site title: update `title` in `hugo.toml`.
- Add a new post: create a new file `content/posts/YYYY-MM-DD-my-post.md` with TOML front matter (match style in `hello-world.md`).
- Change tag appearance: edit `themes/ananke/assets/ananke/css/_styles.css` — `.tag-badge` is already defined; follow its pattern.
- Change header copy or navigation: edit `themes/ananke/layouts/partials/site-navigation.html`.

Precise examples (for the agent)
- To show the GitHub link the theme expects `params.github` to be set in `hugo.toml`. Example:
  - `params.github = "https://github.com/hphuc2302/your-repo"`
- Tag badge usage: the theme's tags partial renders tags; the CSS class to use is `.tag-badge` (defined in `themes/ananke/assets/ananke/css/_styles.css`).

Quality gates & developer checks
- Sanity checks an agent should run before proposing changes:
  - Confirm edits are in source folders (`content/`, `themes/`, `layouts/`, `assets/`). Avoid editing `public/` unless updating generated output intentionally.
  - Basic preview: recommend running `hugo server -D` locally to visually verify template/CSS/content changes.
  - When adding or editing CSS, check `themes/ananke/assets/ananke/css/` for matching conventions (variables are not used; styles are locally scoped).

When to run Node tooling
- The theme lists `postcss` and other Node tools in `themes/ananke/package.json`. Only run Node build steps if you're changing CSS source and need PostCSS processing. Otherwise, editing final CSS files and rebuilding with `hugo` is fine.

Files worth inspecting for context
- `README.md` — repo-specific notes and quick commands (contains notes about modified partials and CSS files).
- `hugo.toml` — site configuration and `params.github`.
- `content/posts/hello-world.md` — canonical content front matter example.
- `themes/ananke/layouts/partials/site-navigation.html` — header and GitHub link insertion point.
- `themes/ananke/assets/ananke/css/_styles.css` and `_code.css` — site-specific CSS overrides.

Editing style for AI suggestions
- Use short, focused diffs; change only the minimal number of files.
- When suggesting copy/text changes, prefer editing theme i18n entries or the partials rather than searching/replace across `public/`.
- Add a one-line comment at the top of modified theme partials explaining the intent, e.g. `<!-- Modified: show GitHub link when params.github exists -->`.

If anything is unclear
- Ask for permission before running Node/npm installs or executing Hugo on the user's machine.
- If a requested change touches CI/deploy pipelines (not present in this repo), request details about deployment (GitHub Pages, netlify, etc.).

---
Please review this draft. Tell me which sections you want expanded or any local conventions I missed and I'll iterate.