# Overview & Vision

## Concept

Defend The Realm is a browser-based tower defence game with two distinctive mechanical layers on top of the genre baseline:

1. **Checkpoint maze routing** — enemies pathfind dynamically around towers, but must visit fixed checkpoints in order. The player's goal is to maximise the path length between each checkpoint pair by building tower walls with a single opening at the far end.

2. **Power network management** — towers require power routed from generators via connector chains. Power splits across connected towers, so more towers on a circuit means less power per tower (slower fire rate / reduced effectiveness). Managing the grid is as important as placing towers.

## Design Philosophy

- **Depth over width** — fewer tower types with more meaningful upgrades and interactions, not 40 towers that blur together
- **Spatial puzzles** — the routing mechanic makes each checkpoint gap a puzzle to solve, not just a lane to fill
- **Resource tension** — power is finite and splits; you can't have everything at full strength
- **Same universe as CTR** — shared lore, factions, visual language; units and structures should feel familiar to CTR players

## Target Platform

Browser-based (no install). Desktop first, mobile considered later.

## Scope (MVP)

- Single player
- One map (8-zone layout with central endzone)
- ~4 tower types with elemental variants
- Power system (generator, connector, water tap)
- ~3 enemy types
- Escalating waves with a lose condition (enemies reach endzone)
- No hero unit in MVP — construction via click-to-place UI

## Anti-Features (things we are deliberately not building)

- Pay-to-win mechanics or premium towers
- Gacha / loot box progression
- Auto-play or idle mechanics — this is an active strategy game
- Excessive tower variety that dilutes decision-making
