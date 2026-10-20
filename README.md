# MemeRadar AI — deployable prototype v0.1

A small Node.js application for testing the MemeRadar AI product concept. It includes a responsive dashboard, token search/filtering, a browser-persisted watchlist, token detail views, CSV export, a risk distribution chart, a demo data mode, and an optional live DexScreener search mode.

## Requirements
- Node.js 18 or newer
- Internet access only for live DexScreener data (demo mode works without it)

## Run locally
```bash
npm start
```
Open `http://localhost:3000`.

## Test the API
```bash
curl http://localhost:3000/api/health
curl 'http://localhost:3000/api/tokens?mode=demo'
curl 'http://localhost:3000/api/tokens?mode=live&q=solana'
```

## Deploy on Render
1. Create a new **Web Service** from this project repository or upload the files to a Git repository.
2. Runtime: **Node**.
3. Build command: leave blank (no dependencies required).
4. Start command: `npm start`.
5. Render sets `PORT` automatically; the server reads it.
6. Deploy and open the provided HTTPS URL. Start in demo mode, then click **Use live data** to test the public DexScreener search API.

## Deploy on Railway
1. Create a project from the Git repository.
2. Use the detected Node app; start command is `npm start`.
3. Generate a public domain from the service settings.

## Deploy on a VPS
Install Node.js 18+, copy the folder, run `npm start`, and place a reverse proxy such as Caddy or Nginx in front of it with HTTPS enabled.

## API endpoints
- `GET /api/health` — health check.
- `GET /api/tokens?mode=demo` — simulated dataset.
- `GET /api/tokens?mode=live&q=solana` — DexScreener public search results filtered to Solana pairs.
- `GET /api/token?address=<token-address>` — fetch token pairs from DexScreener and apply heuristic scores.

## Important limitations
- **This is a test prototype, not a production trading system.** It does not execute trades or connect wallets.
- Live results are search results, not a complete feed of newly created or graduating tokens. Lifecycle labels are inferred from pair age and are approximate.
- The live risk score uses liquidity and short-term volatility heuristics. It does **not** inspect contract bytecode, mint/freeze authority, holder concentration, deployer wallet history, liquidity locks, honeypot/sellability, or wash trading.
- DexScreener availability, rate limits and data coverage can vary.
- The browser watchlist is stored in localStorage and is specific to that browser/device; there is no user authentication or server-side database yet.
- Before public release, add authentication, server-side persistence, rate limiting, provider error monitoring, formal security checks, tests, privacy disclosures, and a more robust on-chain indexing and risk-analysis pipeline.
- This app is not financial advice. Scores are not probabilities of profit and must not be treated as token safety guarantees.
