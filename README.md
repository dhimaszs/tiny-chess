[![make.fun · tiny-chess-01](https://make.fun/badge/tiny-chess-01.svg)](https://make.fun/bounty/tiny-chess-01)
[![rank](https://make.fun/badge/tiny-chess-01/dhimaszs/tiny-chess/rank.svg)](https://make.fun/bounty/tiny-chess-01/leaderboard)
[![reward](https://make.fun/badge/tiny-chess-01/dhimaszs/tiny-chess/reward.svg)](https://make.fun/bounty/tiny-chess-01)

# tiny-chess (v5)

A chess engine in one Python file (3,995 bytes), written for the
[make.fun tiny-chess-01 bounty](https://make.fun/bounty/tiny-chess-01):
the strongest chess engine that fits in 4,096 bytes of Python.

## How it plays

- 0x88 board, own move generator (castling, en passant, promotions)
- Negamax + alpha-beta, quiescence (captures and promotions; all replies
  when in check), transposition table (Zobrist), iterative deepening
- **Null-move pruning** (depth >= 3, reduction 3)
- Move ordering: TT move, MVV-LVA captures, killers, **history heuristic**
- Quiescence with **delta pruning** (bad captures skipped)
- Fixed **175,000-node** budget per move — fully deterministic, no clock,
  no randomness, no network, no model calls
- Transposition table kept up to 500,000 entries before clearing, so
  deep searches in long endgames keep their cached lines
- Evaluation: material + piece-square tables + bishop pair, with a
  separate endgame king table when little material is left

## v5 vs v3

v3 (150k nodes) scored practice Elo 1,545 (4.5/6) and entered the final.
v5 raises the node budget to 175k and keeps the transposition table
longer (clear at 500k entries instead of 200k) to hold endgame lines:
same engine, deeper search at the same positions. Practice trial-0:
5.5/6, Elo 1,809, slowest move 4.68 s (limit 10 s per move).

## Run

`python3 main.py` — it talks to the gauntlet env at `MAKEFUN_ENV_URL`
(`POST /game`, `POST /move` with UCI moves) until every game is done.

## License

MIT — see LICENSE.
