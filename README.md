# Delhi NCR Metro Route Planner

React 19 and TypeScript frontend with a Python 3.13 and Flask 3.1.3 backend. The browser requests network data and route results from the Flask JSON API. Flask validates the versioned read-only JSON network and calculates routes using a station-line adjacency graph, indexed binary min-heap, Dijkstra, and predecessor reconstruction.

**GitHub:** <https://github.com/ribslearnstocode/dpcs-delhi-metro>
**Vercel production:** <https://dpcs-delhi-metro.vercel.app>

## Run locally

From the repository root in PowerShell:

```powershell
python -m venv backend/.venv
backend/.venv/Scripts/python.exe -m pip install -r backend/requirements-lock.txt
cd website
npm ci
npm run build
cd ..
backend/.venv/Scripts/waitress-serve.exe --host=127.0.0.1 --port=5000 --call backend.app:create_app
```

Open <http://127.0.0.1:5000>. For frontend development, keep Flask running and use `npm run dev` from `website/`; Vite on port 5173 proxies `/api` to port 5000.

## API

| Method | Endpoint | Purpose |
| --- | --- | --- |
| GET | `/api/health` | API status and loaded network version/count |
| GET | `/api/network` | Validated network JSON |
| POST | `/api/routes` | Calculate the fastest estimated route |

`POST /api/routes` accepts `sourceId`, `destinationId`, and optional `networkVersion`. The frontend validates network and route responses with Zod. Route costs are coursework estimates, not live schedules.

## Verify

```powershell
backend/.venv/Scripts/python.exe -m pytest backend/tests -q
cd website
npm test
npm run build
$env:APP_URL='http://127.0.0.1:5000'
npm run test:browser
```

Backend tests compare all selectable station pairs to an independent Floyd–Warshall oracle. Browser checks run against the built website served by Waitress.

## Deploy to Vercel

Vercel builds the React client with `build.py`, copies the result to root `public/`, and runs the Flask app exposed by root `app.py` as a Python Function. The Vercel configuration is in `pyproject.toml` and `vercel.json`.

The GitHub Pages `github-pages` branch remains unchanged. The Flask-backed source is maintained separately for Vercel.
