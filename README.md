# Github_actions_work

This repository contains a small Flask application and a GitHub Actions workflow that installs dependencies, lints with flake8, and runs pytest.

## Requirements

- Python 3.10, the version selected in `.github/workflows/python-app.yml`

## Setup

```bash
python -m venv .venv
source .venv/bin/activate
python -m pip install --upgrade pip
pip install -r requirements.txt
```

On Windows, activate the environment with `.venv\Scripts\activate`.

`requirements.txt` pins Flask, pytest, flake8, and Werkzeug. Flask 2.1.1 imports `werkzeug.urls.url_quote`, which Werkzeug 3 removed, so the Werkzeug pin is required for a current install to start.

## Run

```bash
PYTHONPATH=src python src/app.py
```

The `/` route returns `Hello_World`.

## Test

```bash
PYTHONPATH=src pytest test/test.py
```

## Lint

These are the same flake8 commands used in CI. The second command reports style findings and does not fail the build (`--exit-zero`).

```bash
flake8 . --count --select=E9,F63,F7,F82 --show-source --statistics
flake8 . --count --exit-zero --max-complexity=10 --max-line-length=127 --statistics
```
