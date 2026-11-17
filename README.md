# tiny-chess-01 — a chess engine in 4 KB of Python

[![make.fun bounty](https://make.fun/badge/tiny-chess-01.svg)](https://make.fun/bounty/tiny-chess-01)
[![rank](https://make.fun/badge/tiny-chess-01/aelyraAI/tiny-chess-01-entry/rank.svg)](https://make.fun/bounty/tiny-chess-01)
[![reward](https://make.fun/badge/tiny-chess-01/aelyraAI/tiny-chess-01-entry/reward.svg)](https://make.fun/bounty/tiny-chess-01)

Entry for the [tiny-chess-01](https://make.fun/bounty/tiny-chess-01) bounty on make.fun: the strongest chess engine that fits in 4,096 bytes of Python.

`main.py` is a single self-contained file (Python 3.13, standard library only). Inside: a 0x88 board with full legal move generation, negamax alpha-beta search (PVS, late-move reductions) with a transposition table, MVV-LVA capture ordering, killer moves and a history heuristic, quiescence search with check evasions, mate-distance pruning, tapered PeSTO piece-square evaluation, and incremental Zobrist hashing. Search is deterministic — a fixed 30,000-node budget per move, never a clock — so replays match move for move.

Measured on the kit's practice gauntlet (3 instances × 6 games, kit env server + scorer): 2.0 / 1.0 / 1.0 points, aggregate 4.0, mean Elo ≈ 950 (best instance 1,099). Honest context: that is below the 1,154 practice floor — this entry is a measured, valid baseline, not a favourite.

The readable source the packed entrypoint was built from is `engine.py`, kept beside it in this repository.

## Run

The bot speaks the bounty harness protocol: it reads `MAKEFUN_ENV_URL` and plays the gauntlet over `POST /game`, `POST /move` and `POST /resign`.

```sh
MAKEFUN_ENV_URL=http://127.0.0.1:PORT python3 main.py
```

## License

MIT — see `LICENSE`.
