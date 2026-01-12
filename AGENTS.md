# Repository Guidelines

## Project Structure & Module Organization
- Content lives in Markdown/MyST files at the repo root (`index.md`, `about.md`, `blogs.md`) and under `blog/<year>/...`. Keep per-post assets in `images/` or `_static/` with relative links.
- Site configuration is in `myst.yml`; update the ToC/nav and plugin settings there when adding pages.
- Custom build helpers reside in `src/` (`blogpost.py` plugin plus small utilities). Generated HTML lands in `_build/html`; feeds (`atom.xml`, `rss.xml`) are copied there during the preview script.
- `_static/` holds shared images/icons (e.g., `kinotate.png`); avoid committing `_build/` unless explicitly publishing artifacts.

## Build, Test, and Development Commands
- `uv sync` — create/update `.venv` from `pyproject.toml`/`uv.lock`.
- `source .venv/bin/activate` — activate the environment for local commands.
- `myst build --html` — build static HTML. Set `BASE_URL=/subpath` if previewing a non-root deploy.
- `./local-preview.sh` — full workflow: sync deps, build, copy feeds, and serve `_build/html` at `PORT` (default 8000). Use `SERVE=0` to skip the server.

## Coding Style & Naming Conventions
- Python helpers follow PEP 8 with 4-space indentation; prefer type hints and small, composable functions in `src/`.
- Markdown: start files with MyST frontmatter as needed; use `#` for page titles and sentence-case headings. Keep slug folders under `blog/YYYY/` and name posts descriptively (e.g., `ai-notebook.md`).
- Keep assets lowercase-kebab and prefer relative paths (`./images/foo.png`).

## Testing Guidelines
- No automated test suite. Validate changes by building: `myst build --html` (fails on frontmatter/parse errors). For site changes, run `./local-preview.sh` and spot-check pages, links, and feed files in `_build/html/`.
- If you add Python logic, run `python -m compileall src` or `uv run python -m compileall src` to catch syntax issues.

## Commit & Pull Request Guidelines
- Use concise, imperative commits; the history favors short prefixes like `fix:` or simple verbs (`add`, `update`, `chore`). Group related edits per commit.
- PRs should state scope, user-visible outcomes, and any BASE_URL or deploy considerations. Include screenshots/gifs for layout/content changes and note how you validated (`myst build`, local preview).
- Link to related issues/tasks when available and call out any follow-up items (new posts, nav updates, asset additions).
