# BetterChess — a chess engine for Claude

Ask Claude about a chess position today and it answers from memory. Sometimes the
memory is wrong: a knight "attacking" a square it cannot reach, a pin that is not
there, a confident evaluation of nothing. It sounds exactly as sure when it is wrong
as when it is right, which is the worst possible property in a coach.

BetterChess replaces recall with computation. Every claim about an attack, a defender
or an evaluation is calculated from the actual board by a real engine and handed to
Claude as fact.

## Install

Claude → Settings → Connectors → Add custom connector:

```
https://mcp.betterchess.co
```

Sign in with a BetterChess account. Nothing installs. No terminal, no Node, no
Stockfish build, no config file. Works on the free Claude plan, and on your phone.

## Tools

| Tool | Returns |
|---|---|
| `chess_analyse` | Top moves with real evaluations; side to move, check, undefended pieces and their attackers, material. Plus what the opponent would play if it were their turn, and — with `considering` — what a move you are thinking of playing actually walks into, with the refutation. |
| `chess_attacks` | The exact squares a given piece attacks. The one that stops confident nonsense about knights, pins and discovered attacks. |
| `chess_review` | Walks a finished game and reports only the moves where the evaluation genuinely swung. The two moves that decided it, not forty small inaccuracies. |

Give any of them a FEN, a PGN, or the moves so far. There are no commands — ask in
plain language and Claude picks the tool.

## Why `considering` exists

A blunder ranks last, so no amount of `multipv` surfaces it. The move you are about
to play has to be asked about by name:

```
"I want to play Rxd4 here. Is that good?"

→ verdict: loses
  evalAfter: mate for Black
  refutation: Ra1+ Rd1 Rxd1+ Nf1 Rxf1#
```

That is a real position from a real game that was lost to exactly that move, with
an engine running and nothing warning about it.

## Fair play

**Never for a live game against a person.** Using an engine to choose moves against
a human opponent is cheating; chess.com and Lichess detect it and close accounts.
The server instructs Claude to ask who the opponent is and to decline while the
answer is a person.

Fine, and what this is built for: games against a bot or computer opponent, games
that are already over, and any position you are studying.

## Pricing

Free accounts get a daily analysis budget. Pro is $5.99/month, removes the cap and
unlocks `chess_review`. Cancel anytime.

Docs: https://betterchess.co/docs
