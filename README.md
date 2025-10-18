# MyBlog (Hugo)

This Hugo site uses the Ananke theme (modified) and includes localized UI and CSS fixes.

Quick commands (PowerShell):

1. Preview locally (from `myblog` folder):

```powershell
# If hugo.exe is present in this folder
.\hugo.exe server -D

# Or if hugo is installed globally
hugo server -D
```

2. Rebuild the `public/` folder (static export):

```powershell
# From myblog folder
hugo
```

Notes about changes made by me:
- Theme partial `themes/ananke/layouts/partials/summary.html` now shows "Đọc tiếp".
- Theme partial `themes/ananke/layouts/partials/site-navigation.html` shows a GitHub link when `params.github` is set in `hugo.toml`.
- CSS changes in `themes/ananke/assets/ananke/css/_styles.css`:
  - Force consistent sans-serif font for article content and override `serif` class.
  - Added `.tag-badge` for consistent tag appearance.
- CSS changes in `themes/ananke/assets/ananke/css/_code.css`:
  - Set monospaced font for code blocks.
- Partial `themes/ananke/layouts/partials/tags.html` updated to use `.tag-badge`.

To see the final appearance, run the Hugo server command above and open http://localhost:1313

If you'd like, I can:
- Change more UI copy to Vietnamese (e.g., "More" → "Thêm"),
- Add profile/avatar to header, or
- Automatically run `hugo` and sync `public/` now (I cannot execute Hugo from here but I can provide the exact commands).
