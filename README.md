# tiny-chess-01

A chess engine in 4 KB of Python, entered in make.fun's
"Build the strongest chess engine in 4 KB of Python" bounty.

`main.py` (3,652 bytes) is the whole engine: a 0x88 board, negamax with
alpha-beta, a transposition table that persists across moves, null-move
pruning, late-move reductions, check extensions, killer/history move
ordering, quiescence search, and a material + piece-square evaluation.
It searches to a fixed node budget per move (never a clock), so its
play is deterministic.

It plays the gauntlet through the env at `MAKEFUN_ENV_URL`
(`POST /game`, `/move`, `/resign`). Practice trial 0 (local, official
env + scorer): Elo 1545 (4 won, 1 drawn, 1 lost).

The committed `main.py` itself was re-graded the same way and reproduced
trial 0 exactly: Elo 1545 (4 won, 1 drawn, 1 lost, 452 spare plies).
Trial 1 (different openings) also scored Elo 1545. The floor to enter
the final is Elo 1154.

The readable source is `main_src.py` (kept out of the commit on purpose:
only `main.py` counts toward the size cap). `main.py` is the LZMA-packed
form the kit's `makefun compress` command writes from it, byte for byte.

## Run it

```sh
MAKEFUN_ENV_URL=http://127.0.0.1:8080 python3 main.py
```

## License

MIT. See LICENSE.
