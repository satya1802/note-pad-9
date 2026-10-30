# Developer Guide

> Maintained by QuorQ AI SDLC. Text between `sdlc:auto` markers is regenerated; anything outside them is yours and is kept.

<!-- sdlc:auto:start status -->
_Up to date._
<!-- sdlc:auto:end status -->

<!-- sdlc:auto:start source -->
Generated from commit `6432196` · model `claude-sonnet-5`
<!-- sdlc:auto:end source -->

<!-- sdlc:auto:start overview -->
note pad is a generated two-app repository from the Quorq AI SDLC platform: a Vite + React 19 single-page app (the approved, reviewed UI, currently running on seeded sample data) and a FastAPI backend that is still a scaffold -- it exposes only a health check, with SQLAlchemy models, Pydantic schemas and a router package in place but no endpoints implemented yet. The backend defaults to a local SQLite file so it runs with no external database, while docker-compose provides a Postgres 16 container for when DATABASE_URL is pointed at it; the frontend's API client (src/lib/api.ts) is the seam prepared for wiring screens to the real API.
<!-- sdlc:auto:end overview -->

<!-- sdlc:auto:start prerequisites -->
- Node.js and npm (for the frontend, built with Vite 6 / React 19 / TypeScript 5.6)
- Python 3.12 and pip (matches backend/Dockerfile base image)
- Docker and Docker Compose (to run the Postgres 16 database via docker-compose.yml)
<!-- sdlc:auto:end prerequisites -->

<!-- sdlc:auto:start setup -->
1. Clone the repository.
2. cd backend && pip install -r requirements.txt
3. (optional) Start Postgres from the repo root: docker compose up -d -- then set DATABASE_URL to point at it before starting the backend; unset, the backend uses a local sqlite:///./app.db file automatically.
4. cd backend && uvicorn app.main:app --reload -- starts the API on http://localhost:8000.
5. cd frontend && npm install
6. (optional) Set VITE_API_BASE_URL (defaults to http://localhost:8000) and VITE_API_SECRET_KEY if the backend requires a bearer token.
7. cd frontend && npm run dev -- starts the SPA on the Vite dev server (default http://localhost:5173, already allowed by backend CORS).
<!-- sdlc:auto:end setup -->

<!-- sdlc:auto:start run -->
| Name | Command | Description |
|---|---|---|
| backend dev | `uvicorn app.main:app --reload` | Run the FastAPI app with autoreload (from backend/); serves /health and the OpenAPI docs. |
| backend docker build | `docker build -t note-pad-backend backend` | Build the backend image per backend/Dockerfile (runs as non-root user, exposes 8000). |
| backend docker run | `docker run -p 8000:8000 note-pad-backend` | Run the built backend container, serving the FastAPI app on port 8000. |
| db up | `docker compose up -d` | Starts the Postgres 16 container defined in docker-compose.yml (db=app, user=app, password=app, port 5432). |
| frontend dev | `npm run dev` | Starts the Vite dev server for the React SPA (from frontend/). |
| frontend build | `npm run build` | Bundles the app with Vite; does not typecheck. |
| frontend preview | `npm run preview` | Serves the production build locally (used as the e2e target when E2E_BASE_URL is unset). |
| frontend typecheck | `npm run typecheck` | Runs tsc --noEmit; not run by the build, but worth running before shipping. |
<!-- sdlc:auto:end run -->

<!-- sdlc:auto:start structure -->
| Path | Purpose |
|---|---|
| `backend/` | FastAPI service: Dockerfile, requirements.txt, pytest/ruff config, and the app package. |
| `backend/app/` | Application code: main.py (entrypoint, CORS, health route), database.py (engine/session), models.py (SQLAlchemy Base, currently empty), schemas.py (Pydantic models, StubResponse). |
| `backend/app/routers/` | Scaffold for per-architecture-component routers; empty until endpoints are implemented. |
| `backend/tests/` | Pytest tests, currently test_health.py covering the health endpoint. |
| `frontend/` | Vite + React SPA: package.json, Vite/Playwright/ESLint/Prettier/Tailwind config, index.html. |
| `frontend/src/` | Application source: main.tsx entrypoint, index.css (brand tokens as CSS variables), test-setup.ts. |
| `frontend/src/lib/` | Shared library code: api.ts (API base URL + apiFetch client, not yet used by screens), ui.tsx and icons.tsx (component/icon vocabulary), navigate.ts. |
| `frontend/e2e/` | Playwright acceptance tests (e.g. example.spec.ts), run against a locally built+served app or a deployed URL via E2E_BASE_URL. |
| `.quorq/` | Quorq platform metadata (handoff.json) generated alongside the codebase. |
<!-- sdlc:auto:end structure -->

<!-- sdlc:auto:start conventions -->
- Backend follows one router per approved architecture component, one route per API-spec endpoint; every generated route currently returns a typed StubResponse (endpoint/status/detail) until implemented.
- SQLAlchemy models all inherit from the shared Base in app/database.py and must be imported in app/models.py so main.py's Base.metadata.create_all(bind=engine) registers them on startup -- no migrations yet.
- Backend config is environment-driven: DATABASE_URL (defaults to local SQLite) and ALLOWED_ORIGINS (comma-separated, defaults to the Vite dev origins) rather than hardcoded values.
- Frontend screens render seeded sample data by design; src/lib/api.ts (API_BASE_URL/API_SECRET_KEY via VITE_API_BASE_URL/VITE_API_SECRET_KEY, apiFetch helper) is the intended seam for wiring real backend calls.
- Frontend uses the @/ path alias for src/, Tailwind CSS v4 via @tailwindcss/vite, and React Router with a basename from Vite's import.meta.env.BASE_URL.
- TypeScript strict mode is on but noImplicitAny and strictNullChecks are disabled, so npm run build (no typecheck) can pass while npm run typecheck fails -- run typecheck explicitly.
- Vitest component tests live beside the components they cover under src/, scoped by vite.config.ts's `include` so Playwright's e2e specs aren't picked up by Vitest.
<!-- sdlc:auto:end conventions -->

<!-- sdlc:auto:start testing -->
| Name | Command | Description |
|---|---|---|
| frontend unit | `npm run test` | Runs Vitest component tests under src/ (jsdom environment, passes with no tests present). |
| frontend e2e install | `npm run test:e2e:install` | Installs the Chromium browser Playwright needs. |
| frontend e2e | `npm run test:e2e` | Runs Playwright specs in e2e/; without E2E_BASE_URL it boots the backend (from backend/.venv) and builds+previews the frontend itself. |
| frontend lint | `npm run lint` | ESLint over the whole app; this is the gate the platform runs during development. |
| backend test | `pytest` | Runs backend/tests/ (pytest.ini sets pythonpath=. so `import app` resolves); run from backend/. |
| backend lint | `ruff check .` | Lints the backend per backend/ruff.toml; run from backend/. |
<!-- sdlc:auto:end testing -->

<!-- sdlc:auto:start troubleshooting -->
| Problem | Solution |
|---|---|
| `pytest` fails with an import error for `app` | Run pytest from the backend/ directory; pytest.ini sets pythonpath=. to make `import app` work relative to that directory. |
| Frontend's `npm run build` succeeds but `tsc` would fail / deployment typechecks fail | Run `npm run typecheck` (tsc --noEmit) explicitly -- build does not typecheck by design, so catch issues like untyped useState before shipping. |
| Browser calls to the backend are blocked by CORS | Set the backend's ALLOWED_ORIGINS env var to the frontend's actual origin (comma-separated for multiple); it defaults only to the Vite dev server origins. |
| `npm run test:e2e` can't reach the backend | playwright.config.ts's webServer runs `../backend/.venv/bin/python -m uvicorn ...`, so create a virtualenv at backend/.venv and `pip install -r requirements.txt` into it before running e2e tests (unless E2E_BASE_URL points at an already-running deployment). |
| Data doesn't persist the way you expect / backend seems to ignore Postgres | The backend defaults to a local SQLite file (sqlite:///./app.db) unless DATABASE_URL is set; start the db with `docker compose up -d` and export DATABASE_URL pointing at it (e.g. postgresql+psycopg://app:app@localhost:5432/app) before starting uvicorn. |
<!-- sdlc:auto:end troubleshooting -->
