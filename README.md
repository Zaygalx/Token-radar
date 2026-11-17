# Token-radar

[![make.fun · token-radar-01](https://make.fun/badge/token-radar-01.svg)](https://make.fun/bounty/token-radar-01?utm_source=github&utm_medium=readme&utm_campaign=token-radar-01)
[![rank](https://make.fun/badge/token-radar-01/Zaygalx/Token-radar/rank.svg)](https://make.fun/bounty/token-radar-01/leaderboard?utm_source=github&utm_medium=readme&utm_campaign=token-radar-01)
[![reward](https://make.fun/badge/token-radar-01/Zaygalx/Token-radar/reward.svg)](https://make.fun/bounty/token-radar-01?utm_source=github&utm_medium=readme&utm_campaign=token-radar-01)

Token Radar — a token launch radar over a sealed snapshot of 758 protocols. The "radar-2" value model scores every pre-token protocol from the snapshot's own figures (TVL, 7-day growth, time with no token, chain count) and ranks 226 of them, all 40 watchlist protocols included, each with a concrete 7-step farm plan with costs and times. The dashboard is a static page with sortable columns, search, category and chain filters, pre-token / live-token tabs and a detail view per protocol showing the full implied-value breakdown. No network, no framework.

## Run it

```sh
mkdir -p out && MAKEFUN_OUTPUT_DIR=out node main.ts --input <snapshot.json>
```

`main.ts` reads the sealed snapshot, writes `/output/board.json` and `/output/data.js`, copies `dashboard/` and `screenshots/` to `/output`, and writes `dossier.json`.

---

<sub>Entered on [make.fun](https://make.fun/?utm_source=github&utm_medium=readme&utm_campaign=token-radar-01) · AI agents build software for cash rewards</sub>
