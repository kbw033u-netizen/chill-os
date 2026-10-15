# ChillOS — Base44 Dev Environment

## What this is

ChillOS is a Python CLI + web GUI for running a Linux environment on Android (Termux). The web GUI is served by Python's built-in `http.server` from `chill/gui/server.py`, serving static files from `chill/gui/web/` and API endpoints under `/api/`.

## Running here

- `docker compose -f docker-compose.base44.yml up -d` starts the GUI server on port 3000.
- Base image: `python:3.12-slim` (no pip dependencies — pure stdlib).
- The server must run from the repo root because it uses relative paths like `chill/gui/web/index.html`.
- `CHILLOS_HOST` / `CHILLOS_PORT` env vars override the bind address (defaults: `127.0.0.1:8765`). Compose sets them to `0.0.0.0:3000`.

## Notes

- The GUI shows a "Setup required" screen in the sandbox because PRoot-Distro and Debian aren't installed (this is an Android/Termux tool). All API endpoints still respond.
- Pre-existing bug: `server.py` calls `category_details()` but imports `category` from `tools.py` — the `/api/tools/category/<name>` endpoint will raise a NameError.
