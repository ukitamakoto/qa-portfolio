# Browser card game

A card game about taking risks and knowing when to stop. It runs in the browser and as desktop builds for macOS and Windows, with local multiplayer (2 to 8 players) and an online server.

**Stack:** TypeScript · Vite · Node.js server · **Test tooling:** Playwright · Node's built-in test runner (`node:test`)

## What I did

- Built the game together with its test suites.
- Automated full play sessions in the browser: setup, turns, pause, saving and restoring, settings that survive a reload.
- Tested keyboard use and layout limits as part of the end-to-end runs.
- Covered the game rules and the online server with fast unit tests.

## Test strategy

| Level | Tool | What it covers |
|---|---|---|
| End-to-end | Playwright: one worker, traces and screenshots kept on failure | Menus, rules, local multiplayer, keyboard focus, saving and restoring, layout limits |
| Unit & integration | `node:test` (with tsx) | Game rules and scoring, the online server |

## Highlights

- **GAME-E2E-001**: the menu, the rules, keyboard focus and the settings all survive a reload.
- **GAME-E2E-006**: pressing Space on a focused button does not trigger a second action (keyboard accessibility).
- **GAME-E2E-004**: eight named players fit on screen without horizontal overflow.
- **GAME-E2E-005**: the contract badge agrees with the score.

## Catalogue

Test titles are kept in their original language (English or Portuguese). Client and product names are anonymized.

<!-- catalog:game:start -->
**95 test cases** · 35 end-to-end · 60 unit & integration

#### End-to-end

| ID | Suite | Scenario |
|---|---|---|
| GAME-E2E-001 | browser | menu, rules, keyboard focus and settings persist after reload |
| GAME-E2E-002 | browser | local two-player turns, keyboard actions, pause and restored save |
| GAME-E2E-003 | browser | local four-player setup, custom names and turn handoff |
| GAME-E2E-004 | browser | local setup accepts eight named players without horizontal overflow |
| GAME-E2E-005 | browser | contract badge agrees with score for three even numbers |
| GAME-E2E-006 | browser | Space activates a focused Guardar button without drawing another card |
| GAME-E2E-007 | browser | lost-points display includes the contract bonus on a busted hand |
| GAME-E2E-008 | browser | round result requires reward choices and the reserved action is usable next round |
| GAME-E2E-009 | browser | reward choices arrive through a slot-style reveal and respect reduced motion |
| GAME-E2E-010 | browser | victory is rendered after the final action and rematch resets the game |
| GAME-E2E-011 | browser | solo bots finish a full round without input after the human banks |
| GAME-E2E-012 | browser | 1280 × 720 and narrow layouts keep game actions accessible |
| GAME-E2E-013 | online | online chat exchanges escaped messages and keeps the shared history |
| GAME-E2E-014 | online | one move redraws the acting screen at most twice |
| GAME-E2E-015 | online | host can open a full eight-seat online table with bots |
| GAME-E2E-016 | online | two independent browsers share a room, turns, fixed seats and reconnect without overwriting the local save |
| GAME-E2E-017 | online | server advances bots; disconnect freezes play and the host can replace a missing player |
| GAME-E2E-018 | online | remote choices and rewards stay private, peek stays private, and host controls the next round |
| GAME-E2E-019 | specials | freeze selection, pause, restored choice and visible last card in 3D |
| GAME-E2E-020 | specials | draw-two can choose self and then another target during a nested effect |
| GAME-E2E-021 | specials | steal shows the exact cards and duplicate warning; selected boost changes both hands |
| GAME-E2E-022 | specials | peek is gated, ordered, restorable and never changes the last reveal to a preview |
| GAME-E2E-023 | specials | reverse and skip update order and the large reveal without requesting a target |
| GAME-E2E-024 | specials | bot resolves its special and hands a forced peek to the human without revealing it |
| GAME-E2E-025 | specials | old saves keep an exact backup and migrate when the next action is saved |
| GAME-E2E-026 | tavern | 3D bots render, play and retain their match when switching views |
| GAME-E2E-027 | tavern | eight-player table renders seven opponents without clipping or overlapping nameplates |
| GAME-E2E-028 | tavern | reduced motion stays still, camera remains controllable and local turns move seats |
| GAME-E2E-029 | tavern | loss of WebGL falls back to a playable 2D table without losing progress |
| GAME-E2E-030 | tavern-motion | card flight freezes on pause and completes after resuming without changing the save |
| GAME-E2E-031 | tavern-motion | freeze and stolen-card effects play once and expire |
| GAME-E2E-032 | tavern-motion | reduced motion settles cards and suppresses special particles, including after a setting change |
| GAME-E2E-033 | tutorial | guided practice follows a deterministic hand and preserves an existing match |
| GAME-E2E-034 | tutorial | exit, restart and mobile layout do not mark an unfinished tutorial as complete |
| GAME-E2E-035 | tutorial | leaving a tutorial opened from pause resumes the same local table |

#### Unit & integration

<details><summary><b>engine</b> · 21 cases</summary>

| ID | Suite | Case |
|---|---|---|
| GAME-U-001 | engine | the 85-card deck has exact number and special frequencies and starts without dealt hands |
| GAME-U-002 | engine | seeded shuffles are repeatable, accept zero, and do not mutate configuration |
| GAME-U-003 | engine | empty hands and shield-only hands cannot bank; boosts alone can bank |
| GAME-U-004 | engine | every number or special draw advances exactly one active seat |
| GAME-U-005 | engine | a duplicate busts pending points, preserves past score and revealed hand |
| GAME-U-006 | engine | a shield consumes exactly itself and the duplicate, keeping the player active |
| GAME-U-007 | engine | six distinct numbers automatically secure the contract, boosts and [game] bonus |
| GAME-U-008 | engine | contract qualification uses number cards and applies its bonus once |
| GAME-U-009 | engine | banking scores immediately, skips resolved seats, and rotating starters get fresh rounds |
| GAME-U-010 | engine | reaching the target waits for the full round and equal top scores share victory |
| GAME-U-011 | engine | the final highest total wins even when someone else crossed the target first |
| GAME-U-012 | engine | a round where everyone busts closes with no points awarded |
| GAME-U-013 | engine | a sole active player keeps their own turn until they resolve |
| GAME-U-014 | engine | refilling uses only discard and never returns cards held by players |
| GAME-U-015 | engine | defensive exhausted positions terminate instead of hanging or drawing undefined |
| GAME-U-016 | engine | risk and bot decisions depend on public composition, never future card order |
| GAME-U-017 | engine | a bot banks a winning total and chases an already secured opponent total |
| GAME-U-018 | engine | actions, nextRound and successful restores do not share mutable state |
| GAME-U-019 | engine | save validation rejects malformed, incompatible and inconsistent state |
| GAME-U-020 | engine | saved physical duplicates, wrong event cards and inactive turns are rejected |
| GAME-U-021 | engine | 80 seeded bot games finish, preserve cards and points, and round-trip every action |

</details>

<details><summary><b>http</b> · 1 cases</summary>

| ID | Suite | Case |
|---|---|---|
| GAME-U-022 | http | HTTP transport authenticates streams, synchronizes two sessions and rejects foreign origins and oversized input |

</details>

<details><summary><b>rewards</b> · 7 cases</summary>

| ID | Suite | Case |
|---|---|---|
| GAME-U-023 | rewards | configuration accepts eight seats, rejects nine and keeps every id unique |
| GAME-U-024 | rewards | round end offers every player three unique valid rewards and blocks the next round |
| GAME-U-025 | rewards | weighted draft gives trailing players substantially more disruptive choices |
| GAME-U-026 | rewards | choices are immutable, restricted to each offer and required before nextRound |
| GAME-U-027 | rewards | reserved freeze, draw-two, steal, reverse, skip and peek use normal effects without adding physical cards |
| GAME-U-028 | rewards | bots choose from their own draft and spend the reserve on their next turn |
| GAME-U-029 | rewards | save validation rejects forged reward offers, selections and pending sources |

</details>

<details><summary><b>rooms</b> · 13 cases</summary>

| ID | Suite | Case |
|---|---|---|
| GAME-U-030 | rooms | only the host starts; rooms enforce capacity, unique names and authentication |
| GAME-U-031 | rooms | turn ownership, optimistic revision and deduplication prevent forged and double draws |
| GAME-U-032 | rooms | a room can start with eight total seats and distinct bot identities |
| GAME-U-033 | rooms | Visão is private; neither draw order nor random seed is transmitted |
| GAME-U-034 | rooms | disconnect waits for the same seat; host can substitute only after the grace period |
| GAME-U-035 | rooms | host migrates after disconnect; leaving passes the seat to a bot |
| GAME-U-036 | rooms | server restart restores the exact game, identities and processed request identifiers |
| GAME-U-037 | rooms | chat is authenticated, trimmed, rate limited, capped and does not conflict with game revisions |
| GAME-U-038 | rooms | rooms saved before chat are restored with an empty compatible history |
| GAME-U-039 | rooms | round rewards are private and only the authenticated seat can choose its own option |
| GAME-U-040 | rooms | bots act one delay after their turn and settle round rewards in a single step |
| GAME-U-041 | rooms | people choosing rewards from the same round-end view are not rejected as stale |
| GAME-U-042 | rooms | 20 complete multiplayer matches resolve specials, rounds and rematches with server authority |

</details>

<details><summary><b>specials</b> · 18 cases</summary>

| ID | Suite | Case |
|---|---|---|
| GAME-U-043 | specials | expanded deck has exactly three of each action card |
| GAME-U-044 | specials | freeze requires another active target and secures its complete round score |
| GAME-U-045 | specials | freeze can stop an empty hand without granting points |
| GAME-U-046 | specials | draw two can target self or another seat and advances from the original turn only once |
| GAME-U-047 | specials | forced draws stop on bust; a shield absorbs a duplicate and allows the second draw |
| GAME-U-048 | specials | forced draws stop immediately when a sixth distinct number secures [game] |
| GAME-U-049 | specials | nested draw-two choices preserve actor, remaining outer draw and original next seat |
| GAME-U-050 | specials | nested freeze and peek remain restorable when the origin has been stopped |
| GAME-U-051 | specials | reverse changes next seat immediately and skip follows that direction |
| GAME-U-052 | specials | skip in a two-player game skips one turn, never ends the target round |
| GAME-U-053 | specials | steal transfers the selected card, recalculates bonuses and keeps last reveal as Roubo |
| GAME-U-054 | specials | stealing a duplicate consumes protection or busts the thief |
| GAME-U-055 | specials | stealing the sixth distinct card secures [game] and updates the donor contract |
| GAME-U-056 | specials | specials cannot target banked players and harmlessly resolve without eligible opponents |
| GAME-U-057 | specials | peek reveals exactly the next two in order, buys neither and resumes after confirmation |
| GAME-U-058 | specials | peek across a refill preserves the existing top card and card conservation |
| GAME-U-059 | specials | restoration rejects forged decisions, directions, queues and private previews |
| GAME-U-060 | specials | version-one and version-two saves migrate to the 85-card rules without mutating input |

</details>
<!-- catalog:game:end -->

[← Back to the portfolio](../../README.md)
