# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

A Flask web application that displays course information. Courses are defined as in-memory objects in `src/models.py` (no database).

## Commands

```bash
# Install dependencies (using venv)
python -m venv venv
source venv/bin/activate   # Windows: venv\Scripts\activate
uv pip install -r requirements.txt

# Run the app (serves at http://127.0.0.1:5000)
python src/app.py

# Run tests
python -m unittest discover -s tests
```

## Architecture

- **`src/app.py`** — Flask app factory and route registration. Routes are wired via `app.add_url_rule()` pointing to view functions in `views.py`.
- **`src/views.py`** — View functions (`index`, `course`). Each returns a rendered Jinja2 template.
- **`src/models.py`** — `Course` class and a hardcoded `courses` list (title, description, instructor, duration). No database.
- **`src/templates/`** — Jinja2 templates using `layout.html` as the base template (block: `content`). `layout.html` also embeds CSS inline alongside linking `static/css/styles.css`.
- **`tests/test_app.py`** — unittest-based tests using Flask's test client. The test file manually adds `src/` to `sys.path`.

## Key Details

- Python path: tests prepend `src/` to `sys.path` so imports resolve from the `src/` directory, not the project root.
- Routes: `/` (index) and `/course/<course_id>` (course detail).
- No database, ORM, or migrations — all data lives in `models.py`.
- Dependencies: Flask, gunicorn, python-dotenv (see `requirements.txt`).

## Unit tests

- whenever you add a new code or change anything, add unit tests to it and make sure they pass
