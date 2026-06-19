# The Master — AoE2 DE AI

A from-scratch Age of Empires II: Definitive Edition AI.

- **Focus civ (v0.1):** Franks — the "base civ"
- **Game plan:** Scouts → Knights → Paladins, with reactive counters
- **Scope:** 1v1, Arabia, vs a random-civ DE AI (target: **Hardest**)
- **Self-name in game:** `Meistar` (Old Frankish / OHG for *the master*)

Single file: **`The Master.per`** (logic) + **`The Master.ai`** (just makes the game list it).

## Install & run the test
1. Copy **both** `The Master.per` and `The Master.ai` into your DE AI folder — the
   same place your `Bambi … .per` lives.
2. Start a game: **1v1, Arabia, you/AI = The Master playing Franks, opponent = a
   random-civ DE AI on Hardest.** Record the game.
3. Watch what it does; send me the recording (or the debug chat) and I'll iterate.

## Debugging
Debug is **ON by default**. To silence it, set `gl-debug` to `off` in the rule marked
`[DEBUG TOGGLE]` near the top of `The Master.per`.

What it prints (all tagged `[MASTER]`):
- age-up milestones (Feudal / Castle / Imperial)
- which counter it picks (enemy anti-cav → crossbows, enemy ranged → mangonels/skirms)
- attack / regroup decisions
- a periodic telemetry snapshot (military pop, defended town size)

**Where to read it:**
- **Recorded game (easiest):** open the replay, switch to *The Master*'s perspective —
  the `[MASTER]` chat lines show in the chat log. Your recordings capture these.
- **Live AI log:** DE can also write an AI output log. The exact folder depends on your
  install (Steam vs MS Store), so once you run it once tell me your setup and I'll point
  you to the precise file.

## Status — v0.1 (operational seed)
Covers the full critical path: economy + gather distribution, escrow-based aging,
houses/dropsites/farms, military & tech buildings, 2nd/3rd TC boom, Scouts→Knights→
Paladins, reactive counters, siege/trebs, trash safety net, TSA-lite (defended radius
grows with the army), attack cadence, defense reactions, market fail-safes, resign,
and the debug layer.

### Known areas to iterate (expected)
- **Walling** is intentionally light in v0.1 (towers + TC + army instead). Proper base
  walling is the first hardening step after it's running.
- **A few research tokens** are standard but not yet battle-tested in your DE build
  (e.g. `ri-cavalier`, `ri-paladin`, `ri-husbandry`, `ri-blast-furnace`, `ri-plate-barding`,
  `ri-chivalry`, `ri-halberdier`, `ri-architecture`, `ri-two-man-saw`,
  `ri-stone-shaft-mining`, and `siege-workshop` / `mangonel-line`). If the AI fails to
  load, DE will name the offending token — send me that line and it's a 30-second fix.
- Build-order timings (Feudal pop, Castle/Imperial timing, TC count) are first-pass and
  will be tuned from your recordings.
