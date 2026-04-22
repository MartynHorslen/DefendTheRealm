# Multiplayer

## Mode: Last Longer

Up to 8 players each defend their own zone independently. Enemies spawn in each player's zone simultaneously. The last player with lives remaining wins.

This is competitive, not co-op — your zone is your responsibility. Another player's weak defence does not directly affect your zone, but the shared endzone means leaked enemies from any zone contribute to a shared threat pool (TBD).

## Zone Independence

- Each player builds their own maze within their zone
- Towers in one zone do not attack enemies in another zone
- Power networks are zone-local
- Players cannot interact with or sabotage other zones (friendly or otherwise)

## Shared Endzone

Enemies that leak from any player's zone travel via corridors to the central endzone. Whether leaked enemies contribute to a shared life pool or each player tracks lives independently is a key design decision:

- **Shared lives** — creates co-op pressure even in competitive mode; one weak player hurts everyone
- **Independent lives** — pure last-longer; your survival is entirely on you

**Recommendation:** independent lives for MVP — cleaner competitive experience, avoids frustration at teammates.

## Elimination

When a player runs out of lives their zone stops spawning enemies. Remaining players continue with escalating waves. The final surviving player wins.

## Spectating

Eliminated players should be able to watch remaining zones — seeing others' routing strategies is part of the social experience.

## Single-Player Mode

One zone, survival against escalating waves. No endgame win condition — survive as long as possible, score tracked by waves survived. This is the MVP target.

## Open Questions

- Do all 8 player zones run simultaneously on the same map, or is multiplayer instanced per lobby?
- Is there any interaction between players (trading resources, sending support towers, sabotage mechanics)?
- What is the wave sync mechanism — do all players see the same wave at the same time, or does each player have an independent wave counter?
- Can a skilled player extend their run indefinitely or is there a hard wave cap?
