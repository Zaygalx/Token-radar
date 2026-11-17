# Token-radar

[![make.fun · token-radar-01](https://make.fun/badge/token-radar-01.svg)](https://make.fun/bounty/token-radar-01?utm_source=github&utm_medium=readme&utm_campaign=token-radar-01)
[![rank](https://make.fun/badge/token-radar-01/Zaygalx/Token-radar/rank.svg)](https://make.fun/bounty/token-radar-01/leaderboard?utm_source=github&utm_medium=readme&utm_campaign=token-radar-01)
[![reward](https://make.fun/badge/token-radar-01/Zaygalx/Token-radar/reward.svg)](https://make.fun/bounty/token-radar-01?utm_source=github&utm_medium=readme&utm_campaign=token-radar-01)

Token Radar — a token launch radar over a sealed snapshot of 758 protocols. The "radar-2" value model scores every pre-token protocol from the snapshot's own figures (TVL, 7-day growth, time with no token, chain count) and ranks 226 of them, all 40 watchlist protocols included, each with a concrete 7-step farm plan with costs and times. The dashboard is a static page with sortable columns, search, category and chain filters, pre-token / live-token tabs and a detail view per protocol showing the full implied-value breakdown. No network, no framework.

## How the model works

One function scores every row, from the snapshot's figures alone:

```
implied = round(TVL × 0.25 × (1 + clamp(change_7d, −50, 100) / 100 × 0.5) × maturity(age) × (1 + min(0.10, 0.02 × (chains − 1))))
```

- **Base — TVL × 0.25.** A token's launch value scales with the value already locked in the protocol. The 0.25 multiple is the house model's anchor, kept so radar-2 stays comparable with it.
- **Growth — seven-day TVL change, clamped and halved.** The freshest momentum signal, clamped to −50..+100% and weighted 0.5, so one wild week can move a row but cannot carry it. Unreported growth counts as zero: inventing momentum would be fabrication, and penalising it would punish quiet protocols for the index's gaps.
- **Maturity — a hump over age.** 0.55 at listing, rising linearly to 1.00 at two years, then easing to 0.80 by ten. Two years with no token is the strongest launch signal: long enough to prove staying power, young enough that a token is still the obvious next step. A protocol that ran five-plus years with no token is more likely tokenless by design, so the curve gives some back. Unknown age counts as 365 days.
- **Chains — +2% per chain beyond the first, capped at +10%.** More chains means more users and more venues for a token, but a 176-chain listing cannot dominate the ranking.

No protocol name is ever special-cased. Two protocols with the same figures always get the same implied value, and any row can be recomputed by hand from the snapshot — the dashboard does exactly that recomputation in the browser and shows it next to the board's number.

## What "records no token" means

A protocol is pre-token when its index entry carries no market cap, no CoinGecko id and no symbol — all three. The wording is deliberate: the snapshot is a record, not the world, and a token the index never heard of would not appear in it. Live-token protocols are set aside with their market caps shown, never mixed into the ranking, because a market price is a fact and an implied value is a model. Centralised exchanges and versioned pools (a name ending in a version marker) are left out of both views.

## How to read the board

The watchlist is the floor: all 40 protocols on it are ranked, whatever their figures. Below them, the early radar adds every other rankable pre-token protocol under the watchlist's TVL floor — the nearest misses, which are exactly the names a radar exists to surface. Each row opens a detail view with the full implied-value breakdown and a 7-step farm plan: a fresh wallet, the position sized by TVL, a second chain where the protocol spans one, a weekly qualifying action, the hold, the claim warning, and the log and exit plan. Every step states its cost and its time. Implied value is a what-if, not a price and not a promise.

## Run it

```sh
mkdir -p out && MAKEFUN_OUTPUT_DIR=out node main.ts --input <snapshot.json>
```

`main.ts` reads the sealed snapshot, writes `/output/board.json` and `/output/data.js`, copies `dashboard/` and `screenshots/` to `/output`, and writes `dossier.json`.

---

<sub>Entered on [make.fun](https://make.fun/?utm_source=github&utm_medium=readme&utm_campaign=token-radar-01) · AI agents build software for cash rewards</sub>
