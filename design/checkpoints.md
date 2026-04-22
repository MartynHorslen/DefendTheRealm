# Checkpoints & Pathfinding

## Checkpoints

Checkpoints are fixed square tiles placed on the map at design time. Each has a directional arrow indicating which direction the mob faces after touching it — this sets the general heading toward the next checkpoint.

Enemies must visit checkpoints in numbered order (1 → 2 → 3 → ...) before exiting the zone into the corridor toward the endzone.

## Pathfinding

Enemies use dynamic A* pathfinding. They navigate toward the next checkpoint via whatever open ground is available. They do not teleport or jump — they walk the full path.

**Key behaviour:** enemies head toward the nearest opening in the direction of the next checkpoint. If the player has built a long winding corridor with one opening at the far end, enemies walk the full length of that corridor. This is the core of the routing strategy.

## The Maze Strategy

The player's goal is to maximise path length between each checkpoint pair:

1. Build tower walls that block direct routes
2. Leave a single opening at the far end of a winding path
3. Enemies walk the longest available route to reach the opening
4. More ground covered = more shots taken from towers

The most effective strategies route enemies *away* from checkpoint 2 when leaving checkpoint 1, forcing a full traversal of the zone before doubling back.

## Blocking Prevention

Players cannot fully seal off a checkpoint — the game must always maintain a valid path. Two possible enforcement mechanisms (to be decided):

- **Tower destruction** — if the path is fully blocked, the nearest tower blocking the route is destroyed. Punishing but creates interesting risk/reward.
- **Checkpoint skip** — fully blocked checkpoint is skipped; enemy proceeds to the next one. Less punishing, breaks routing strategy.

**Preferred:** tower destruction — it creates meaningful tension and discourages lazy full-blocking.

## Cliff & Ramp Interaction

Cliff tiles are impassable. Ramp tiles are the only way through cliff features. This creates natural chokepoints the player cannot move — they must route around or funnel enemies through the ramps.
