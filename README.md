# Token Radar

A token launch radar for the make.fun bounty **Build the best token launch radar**
(`token-radar-01`). It ranks pre-token DeFi protocols by an implied value
derived only from the sealed DefiLlama snapshot, and shows a reader how to
farm each one.

## What it does

- `main.ts` (Node 22, standard library only) reads `/input/snapshot.json`,
  scores every rankable pre-token protocol with the model in `lib/model.ts`,
  and writes `/output/board.json`, `/output/data.js`, `/output/dashboard/`,
  `/output/screenshots/` and `/output/dossier.json`.
- The board covers all 40 watchlist protocols plus every other rankable
  pre-token protocol in the snapshot (198 rows), ranked by implied value.
- The dashboard is a static page with no network: a top-10 chart, watchlist
  top-10 cards, a sortable/filterable table (Top 25 / 50 / 100), a detail
  view with the model's own inputs and a farm plan per protocol, and a model
  sandbox that recomputes implied values live.

## The model (radar-2)

```
implied = round(tvl_usd x 0.25 x sizeDamp
          x (1 + clamp(change_7d, -60, 120) / 100 x 0.5)
          x (0.55 + min(age_days, 1460) / 1460 x 0.45)
          x breadth)
sizeDamp  = clamp(($100M / tvl_usd)^0.15, 0.55, 1)
breadth   = 1 + 0.04 per extra chain, up to 5 extra chains
```

Signal is buy when implied value per TVL dollar reaches 0.20, watch at 0.15,
avoid below. Implied value is a model, not a price and not a promise, and it
never predicts whether or when a token is issued. A protocol "records no
token" when DefiLlama records none for it; that is not proof it has none.

## Run it locally

```sh
mkdir -p out && MAKEFUN_OUTPUT_DIR=out node main.ts --input token-radar-01-kit/input/snapshot.json
```

Then open `out/dashboard/index.html` in a browser. The program is
deterministic: two runs on the same snapshot write the same bytes.

## License

MIT — see `LICENSE`.
