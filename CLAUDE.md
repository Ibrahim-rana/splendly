# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project

**Spendly** — a Flask + SQLite expense tracker (currency: rupees). This is a step-by-step teaching scaffold: most features are stubs labelled with the step that implements them (e.g. "coming in Step 7"). When implementing a step, replace the matching placeholder rather than adding parallel routes.

## Commands

A virtualenv lives in `venv/` (Windows layout: `venv\Scripts\`).

```powershell
venv\Scripts\Activate.ps1          # activate (PowerShell)
pip install -r requirements.txt
python app.py                      # dev server on http://localhost:5001 (debug on)
pytest                             # run tests (pytest + pytest-flask)
pytest tests/test_x.py::test_name  # single test
```

No tests exist yet; `pytest-flask` is installed, so tests are expected to use an `app` fixture in a `conftest.py`. No linter is configured.

## Architecture

- `app.py` — single module holding the Flask `app` and all routes. Implemented: `/`, `/register`, `/login` (GET only, render templates). Stubs returning placeholder strings: `/logout` (Step 3), `/profile` (Step 4), `/expenses/add` (Step 7), `/expenses/<id>/edit` (Step 8), `/expenses/<id>/delete` (Step 9).
- `database/db.py` — empty until Step 1. Intended contract: `get_db()` returns a `sqlite3` connection with `row_factory` set and foreign keys enabled; `init_db()` creates tables with `CREATE TABLE IF NOT EXISTS`; `seed_db()` inserts dev sample data. The DB file is `expense_tracker.db` (gitignored).
- `templates/` — Jinja2; every page extends `base.html` (blocks: `title`, `head`, `content`, `scripts`). The navbar in `base.html` currently always shows Sign in / Get started — it has no logged-in state yet.
- The login and register forms already `POST` to `/login` and `/register` (fields include `email`, `password`), but those routes only accept GET — POST handling must be added when auth is implemented.
- `static/css/style.css` — one stylesheet driven by CSS custom properties on `:root` (`--ink*`, `--paper*`, `--accent`, `--danger`, `--radius-*`, fonts DM Serif Display / DM Sans). Reuse these tokens and existing classes (`btn-primary`, `btn-ghost`, `form-group`, `form-input`) for new pages.
- `static/js/main.js` — empty placeholder, loaded on every page via `base.html`.
