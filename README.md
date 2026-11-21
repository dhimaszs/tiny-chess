[![tiny-chess-01](https://make.fun/badge/tiny-chess-01.svg)](https://make.fun/bounty/tiny-chess-01)
[![rank](https://make.fun/badge/dhimaszs/tiny-chess/rank.svg)](https://make.fun/bounty/tiny-chess-01)
[![reward](https://make.fun/badge/dhimaszs/tiny-chess/reward.svg)](https://make.fun/bounty/tiny-chess-01)

# tiny-chess (v2)

A chess engine in one Python file (3,934 bytes), written for the
[make.fun tiny-chess-01 bounty](https://make.fun/bounty/tiny-chess-01):
the strongest chess engine that fits in 4,096 bytes of Python.

## How it plays

- 0x88 board, own move generator (castling, en passant, promotions)
- Negamax + alpha-beta, quiescence (captures and promotions; all replies
  when in check), transposition table (Zobrist), iterative deepening
- **Null-move pruning** (depth >= 3, reduction 3)
- Move ordering: TT move, MVV-LVA captures, killers, **history heuristic**
- Quiescence with **delta pruning** (bad captures skipped)
- Fixed **100,000-node** budget per move — fully deterministic, no clock,
  no randomness, no network, no model calls
- Evaluation: material + piece-square tables + bishop pair, with a
  separate endgame king table when little material is left

## v2 vs v1

v1 (40k nodes, no null-move pruning, no history, uncapped quiescence)
scored Elo 876 on the practice trial — below the 1,154 final floor.
v2 adds null-move pruning, history ordering, delta-pruned quiescence,
a 100k node budget and an endgame king table: +1 search depth at the
same positions (startpos 6, kiwipete 4) at 30–70k nodes/s.

## Run

`python3 main.py` — it talks to the gauntlet env at `MAKEFUN_ENV_URL`
(`POST /game`, `POST /move` with UCI moves) until every game is done.

## License

MIT — see LICENSE.
