[![make.fun · tiny-chess-01](https://make.fun/badge/tiny-chess-01.svg)](https://make.fun/bounty/tiny-chess-01)
[![rank](https://make.fun/badge/tiny-chess-01/dhimaszs/tiny-chess/rank.svg)](https://make.fun/bounty/tiny-chess-01/leaderboard)
[![reward](https://make.fun/badge/tiny-chess-01/dhimaszs/tiny-chess/reward.svg)](https://make.fun/bounty/tiny-chess-01)

# tiny-chess (v3)

A chess engine in one Python file (3,992 bytes), written for the
[make.fun tiny-chess-01 bounty](https://make.fun/bounty/tiny-chess-01):
the strongest chess engine that fits in 4,096 bytes of Python.

## How it plays

- 0x88 board, own move generator (castling, en passant, promotions)
- Negamax + alpha-beta, quiescence (captures and promotions; all replies
  when in check), transposition table (Zobrist), iterative deepening
- **Null-move pruning** (depth >= 3, reduction 3)
- Move ordering: TT move, MVV-LVA captures, killers, **history heuristic**
- Quiescence with **delta pruning** (bad captures skipped)
- Fixed **150,000-node** budget per move — fully deterministic, no clock,
  no randomness, no network, no model calls
- Evaluation: material + piece-square tables + bishop pair, with a
  separate endgame king table when little material is left

## v3 vs v2

v2 (100k nodes) scored practice Elo 1,451 (4.0/6) and entered the final.
v3 raises the node budget to 150k: same engine, deeper search at the
same positions. Practice trial-0: 4.5/6, Elo 1,545, slowest move 4.73 s
(limit 10 s per move).

## Run

`python3 main.py` — it talks to the gauntlet env at `MAKEFUN_ENV_URL`
(`POST /game`, `POST /move` with UCI moves) until every game is done.

## License

MIT — see LICENSE.
