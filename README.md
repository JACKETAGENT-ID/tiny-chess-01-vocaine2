# tiny-chess-01 — vocaine entry (piece-list engine)

A deterministic chess engine in one packed `main.py` (<= 4,096 bytes).

Design: piece-list board (per-colour, per-type square lists with a square
index for O(1) removal), precomputed knight/king attack tables and sliding
rays, incremental Zobrist key and incremental tapered score.

Search: iterative deepening under a fixed node budget (never a clock),
alpha-beta with PVS, transposition table, null-move pruning, late-move
reductions, check extensions, futility pruning, and a quiescence search
over captures and promotions (all evasions when in check).

Evaluation: tapered middlegame/endgame piece-square tables, passed and
doubled pawns, bishop pair, rook on open files.

It plays the make.fun env protocol (POST /game, /move, /resign) using only
MAKEFUN_ENV_URL. No randomness, no wall clock: same position, same move.
