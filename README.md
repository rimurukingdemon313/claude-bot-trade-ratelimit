# Paper Trading Bot Dashboard (TradeLocker)

A trading dashboard with a React frontend, an Express API server, and a Python
analysis/trading engine that connects to TradeLocker. This build includes
rate-limit hardening for TradeLocker's Cloudflare limits (HTTP 429 / error 1015).

## Stack

- Frontend: React 19, Vite 7, Tailwind CSS 4, TanStack Query, Recharts
- Server: Express 5 (TypeScript, bundled with esbuild at startup by `index.js`)
- Engine: Python (TradeLocker client/state, market data, risk engine, SMC analysis)

## Setup

```sh
npm install
pip install -r requirements.txt
cp .env.example .env   # fill in your own credentials
```

## Development / build

```sh
npm run typecheck   # TypeScript check
npm run build       # production frontend build -> dist/
npm start           # start the API server (serves the built frontend)
```

## Configuration

All credentials come from environment variables — see `.env.example`.
Never commit a real `.env` file.

## Diagnostics

```sh
python diagnose_tradelocker_connection.py
```

Checks credentials and connectivity to TradeLocker and reports what is failing.

## Tests

```sh
pytest        # 35 tests
```

## Demo

```sh
python run_smc_demo.py
```

## Docker

```sh
docker build -t paper-trading-dashboard .
docker run --env-file .env -p 5000:5000 paper-trading-dashboard
```

## Layout

```
src/            React app (pages, components, hooks)
server/         Express API (routes, lib, app entry)
analysis_engine/  Python analysis modules
tests/          Python test suite
index.js        Server bootstrap (bundles server/index.ts, then runs it)
Dockerfile      Container build
```
