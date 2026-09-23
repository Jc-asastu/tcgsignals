# TCGSignals

A trading-card catalog and price-exploration app for Pokémon and One Piece cards, built with Next.js, TypeScript, and Supabase.

> **Data notice:** The repository mixes imported card data with estimated prices and generated price histories. Some charts and percentage changes are simulations, not observed market history. Do not use them for trading or valuation decisions.

## Explore

- Browse cards and sets with search, filters, and pagination.
- Inspect card details, displayed prices, and charts.
- Keep a browser-local portfolio; positions are stored in `localStorage`, not synced to an account.
- Query the read-only `/api/v1` endpoints; the in-app reference is at `/docs`.

## Data provenance

- Pokémon imports can use price fields supplied by the Pokémon TCG API.
- The One Piece import and seed utilities can generate percentage changes or estimated prices.
- `src/app/api/seed/prices/route.ts` estimates missing prices from rarity ranges and generates random changes.
- `scripts/seed-price-history.ts` creates a simulated 90-day history. Its generated rows currently use the source label `tcgplayer`; that label does **not** prove those points were observed there.

The current UI and database do not consistently distinguish imported observations from estimates and simulations. Verify source, timestamp, and provenance before making any market claim.

## Run locally

1. Install dependencies with `npm ci`.
2. Set up a Supabase project and apply the SQL files in `supabase/migrations/` in order.
3. Configure `NEXT_PUBLIC_SUPABASE_URL` and `NEXT_PUBLIC_SUPABASE_ANON_KEY` locally. Administrative imports also require `SUPABASE_SERVICE_ROLE_KEY`, which must remain server-side and must never be committed.
4. Run `npm run dev` and open `http://localhost:3000`.

`npm run lint` and `npm run build` are the available project checks. There is no automated test script yet.

## Before relying on market data

Separate observed, estimated, and simulated records in storage and the UI; correct synthetic source labels; document update cadence and attribution; and validate the deployed dataset. Until then, treat prices and charts as exploratory demo data.
