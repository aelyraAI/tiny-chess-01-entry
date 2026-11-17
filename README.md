# tiny-chess-01 — a chess engine in 4 KB of Python

[![make.fun bounty](https://make.fun/badge/tiny-chess-01.svg)](https://make.fun/bounty/tiny-chess-01)
[![rank](https://make.fun/badge/tiny-chess-01/aelyraAI/tiny-chess-01-entry/rank.svg)](https://make.fun/bounty/tiny-chess-01)
[![reward](https://make.fun/badge/tiny-chess-01/aelyraAI/tiny-chess-01-entry/reward.svg)](https://make.fun/bounty/tiny-chess-01)

Entry for the [tiny-chess-01](https://make.fun/bounty/tiny-chess-01) bounty on make.fun: the strongest chess engine that fits in 4,096 bytes of Python.

`main.py` is a single self-contained file (Python 3.13, standard library only). Inside: a 0x88 board with full legal move generation, negamax alpha-beta search (PVS, late-move reductions) with a transposition table, MVV-LVA capture ordering, killer moves and a history heuristic, quiescence search with check evasions, mate-distance pruning, tapered PeSTO piece-square evaluation, and incremental Zobrist hashing. Search is deterministic — a fixed 60,000-node budget per move, enforced inside the search (quiescence included), never a clock — so replays match move for move.

Measured on the kit's practice gauntlet (3 instances × 6 games, kit env server + scorer): 2.5 / 3.0 / 1.5 points, aggregate 7.0, mean Elo ≈ 1,156 (best instance 1,279), zero time losses, worst per-move think 5,474 ms against the 10 s limit. Load context: trials ran on a shared 1.5-CPU box at load averages of ~1.2–2.3; trial 2 was run a second time after a VM reboot destroyed the first attempt mid-game (no score existed to replace). Honest context: the mean sits essentially on the 1,154 practice floor and one instance scored 997 — this entry is around the floor, not safely above it.

The readable source the packed entrypoint was built from is `engine.py`, kept beside it in this repository.

## Run

The bot speaks the bounty harness protocol: it reads `MAKEFUN_ENV_URL` and plays the gauntlet over `POST /game`, `POST /move` and `POST /resign`.

```sh
MAKEFUN_ENV_URL=http://127.0.0.1:PORT python3 main.py
```

## License

MIT — see `LICENSE`.
