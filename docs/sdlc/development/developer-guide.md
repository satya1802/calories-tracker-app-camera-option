# Developer Guide

> Maintained by QuorQ AI SDLC. Text between `sdlc:auto` markers is regenerated; anything outside them is yours and is kept.

<!-- sdlc:auto:start status -->
_Up to date._
<!-- sdlc:auto:end status -->

<!-- sdlc:auto:start source -->
Generated from commit `3dd6d23` · model `claude-sonnet-5`
<!-- sdlc:auto:end source -->

<!-- sdlc:auto:start overview -->
This is a generated scaffold for a calories-tracker app that lets a user photograph food and see its calorie count. It is two separate apps in one repo: a Vite + React (TypeScript) single-page frontend whose screens were already design-approved and currently run entirely on seeded sample data, and a FastAPI backend that has no approved architecture yet beyond a health-check endpoint and the plumbing (SQLAlchemy models/Base, Pydantic schemas, a stub response shape, CORS, and a SQLite-by-default database) needed to add real endpoints later.
<!-- sdlc:auto:end overview -->

<!-- sdlc:auto:start prerequisites -->
- Node.js (for npm and the Vite/React/TypeScript frontend)
- Python 3.12 (matches backend/Dockerfile)
- pip
- Docker and Docker Compose (optional, for the Postgres service in docker-compose.yml)
<!-- sdlc:auto:end prerequisites -->

<!-- sdlc:auto:start setup -->
1. Clone the repository
2. Copy .env.example to .env and fill in values as needed
3. cd frontend && npm install
4. cd backend && pip install -r requirements.txt
5. (Optional) From the repo root, run `docker-compose up -d` to start the Postgres database defined in docker-compose.yml if you want to point DATABASE_URL at Postgres instead of the SQLite default
<!-- sdlc:auto:end setup -->

<!-- sdlc:auto:start run -->
| Name | Command | Description |
|---|---|---|
| frontend dev | `npm run dev` | Starts the Vite dev server for the React SPA (run from frontend/) |
| frontend build | `npm run build` | Bundles the frontend with Vite; does not typecheck (run from frontend/) |
| frontend preview | `npm run preview` | Serves the production build locally (run from frontend/) |
| backend dev | `uvicorn app.main:app --reload` | Runs the FastAPI backend with auto-reload (run from backend/) |
| db | `docker-compose up` | Starts the Postgres 16 database container defined at the repo root |
<!-- sdlc:auto:end run -->

<!-- sdlc:auto:start structure -->
| Path | Purpose |
|---|---|
| `backend/` | FastAPI service: app package (main, database, models, schemas, routers), requirements.txt, Dockerfile, tests/ |
| `backend/app` | Application code: main.py (entrypoint, CORS, health route), database.py (engine/session), models.py (SQLAlchemy Base), schemas.py (Pydantic models/StubResponse), routers/ (one router per architecture component) |
| `backend/tests` | Pytest tests, currently covering the health check |
| `frontend/` | Vite + React SPA: approved screens running on seeded sample data, package.json, config files, e2e tests |
| `frontend/src` | App source: main.tsx entrypoint, lib/ (api client, UI/icon vocabulary, navigation), index.css, test-setup.ts |
| `frontend/e2e` | Playwright acceptance test specs |
| `.quorq/` | Platform metadata (handoff.json) for the Quorq AI SDLC platform |
| `docker-compose.yml` | Defines the Postgres database service for local development |
<!-- sdlc:auto:end structure -->

<!-- sdlc:auto:start conventions -->
- Backend: one FastAPI router per architecture component that owns endpoints, under app/routers/
- Backend: every unimplemented route returns a typed StubResponse (schemas.py) rather than raising, keeping the service startable with a complete OpenAPI doc
- Backend: SQLAlchemy models inherit from the shared Base in database.py; main.py imports models before calling Base.metadata.create_all
- Backend: DATABASE_URL env var selects the database, defaulting to local SQLite (sqlite:///./app.db) for a zero-dependency start
- Backend: ALLOWED_ORIGINS env var (comma-separated) configures CORS; falls back to localhost Vite dev origins
- Backend: code style enforced by ruff (ruff.toml), linted/formatted via ruff check/format
- Frontend: screens live under src/screens/ with one module per approved screen; src/App.tsx holds the navigation shell/route table; src/lib/ui.tsx and icons.tsx define the shared component/icon vocabulary (per frontend/README.md)
- Frontend: API access is centralized in src/lib/api.ts (API_BASE_URL/API_SECRET_KEY from Vite env vars, apiFetch helper) but screens currently use seeded sample data instead of calling it
- Frontend: component tests sit beside the components they cover and are picked up by Vitest; Playwright e2e specs live in e2e/ and are excluded from the Vitest run
- Frontend: code style enforced by ESLint (eslint.config.js) and Prettier (.prettierrc)
<!-- sdlc:auto:end conventions -->

<!-- sdlc:auto:start testing -->
| Name | Command | Description |
|---|---|---|
| frontend unit tests | `npm test` | Runs Vitest component tests under src/ (jsdom environment) |
| frontend lint | `npm run lint` | Runs ESLint over the frontend app |
| frontend typecheck | `npm run typecheck` | Runs tsc --noEmit (not run automatically by build) |
| frontend e2e | `npm run test:e2e` | Runs Playwright acceptance tests from e2e/; builds/serves the app locally unless E2E_BASE_URL is set (run npm run test:e2e:install first to fetch the Chromium browser) |
| backend tests | `pytest` | Runs backend tests (currently test_health.py) with pythonpath set via pytest.ini |
| backend lint | `ruff check .` | Lints the backend codebase with ruff |
| backend format check | `ruff format .` | Formats/checks backend code style with ruff |
<!-- sdlc:auto:end testing -->

<!-- sdlc:auto:start troubleshooting -->
| Problem | Solution |
|---|---|
| Frontend `npm run build` succeeds but the app fails type checks or deployment | Run `npm run typecheck` (tsc --noEmit) separately, since build does not typecheck |
| Frontend calls to the backend are blocked by the browser (CORS error) | Set the ALLOWED_ORIGINS env var on the backend to the frontend's origin (comma-separated for multiple); it defaults to http://localhost:5173 and http://127.0.0.1:5173 |
| Backend can't connect to Postgres even though docker-compose is running | Set DATABASE_URL to point at the Postgres service (see docker-compose.yml for user/password/db); without it the backend defaults to a local SQLite file (app.db) |
| `pytest` run from backend/ fails with `ModuleNotFoundError: app` | Run pytest from the backend/ directory so pytest.ini's `pythonpath = .` setting applies |
| Playwright e2e tests fail immediately with a missing browser error | Run `npm run test:e2e:install` to fetch Chromium before `npm run test:e2e` |
<!-- sdlc:auto:end troubleshooting -->
