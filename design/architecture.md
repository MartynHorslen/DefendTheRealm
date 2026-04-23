# Technical Architecture

## Platform & Engine

- **Engine:** Godot 4
- **Language:** GDScript
- **Target platform:** Steam (Windows/Mac/Linux via native export)
- **Steam integration:** GodotSteam plugin (achievements, cloud saves, overlay)
- **Single player MVP** — multiplayer consideration built into scene structure but not implemented

## World Representation

### Grid System
- Each player zone is a fine grid (128x128 cells)
- Towers occupy an NxN block of cells and snap to the grid
- Fine enough to feel like free placement, clean enough for pathfinding and collision logic
- Godot Tilemap for visual terrain layer; separate 2D array for logic (passable/impassable)

### Scene Structure
```
GameZone (main scene)
  ├── TilemapLayer (visual terrain)
  ├── GridLogic (passable/impassable array, A* graph)
  ├── CheckpointManager (ordered checkpoint list)
  ├── TowerManager (placed towers, triggers path recalc)
  ├── PowerNetwork (cluster graph, distribution calc)
  ├── EnemyManager (spawner, active enemy instances)
  ├── BuilderUnit (player's context-menu builder avatar)
  └── UI (resource display, wave info, power indicators)
```

Single player: one GameZone active at a time.
Multiplayer (future): multiple GameZone instances, each owned by a player, connected via server with zone output (leaks) feeding shared EndZone scene.

## Pathfinding

### Pre-calculation Model
- Full canonical path calculated once per tower placement: spawn → checkpoint 1 → ... → checkpoint N → exit
- Uses A* on the GridLogic passable array
- Stored on GameZone as `canonical_path: Array[Vector2]`
- New enemy instances inherit canonical path on spawn — no per-spawn calculation
- On tower placement, `path_updated` signal emitted with new canonical path

### Blocking Prevention
- Before committing a tower placement, run A* to verify a valid path still exists through all checkpoints
- If no valid path: trigger blocking penalty (nearest blocking tower destroyed), revert placement
- Proactive — never allows an invalid state to persist

### Active Enemy Path Updates
On receiving `path_updated` signal, each active Enemy:
1. Determines their `next_checkpoint_index` (progress through the sequence)
2. Runs lightweight A* from current position to that checkpoint
3. Appends canonical path from that checkpoint onward
4. Updates movement target

```
# Pseudocode
GameZone:
  canonical_path: Array[Vector2]

  func on_tower_placed():
      if not valid_path_exists():
          trigger_blocking_penalty()
          return
      canonical_path = run_full_astar()
      emit_signal("path_updated", canonical_path)

Enemy:
  next_checkpoint_index: int

  func on_path_updated(canonical_path):
      my_path = astar_to_checkpoint(position, next_checkpoint_index)
                + canonical_path.slice_from(next_checkpoint_index)
```

## Power Network

### Node Types
```
PowerNode (base class):
  connections: Array[PowerNode]
  received_power: float

Generator extends PowerNode:
  base_output: float
  grass_remaining: float  # depletes over time

WaterTap extends PowerNode:
  base_output: float      # infinite, no depletion

Connector extends PowerNode:
  # receives and redistributes — no unique properties

Tower extends PowerNode:
  received_power: float   # drives fire rate + damage
  # terminal node — cannot be a link source
```

### Cluster Calculation
On any network change:
1. Union-find across all linked nodes to identify clusters
2. For each cluster:
   - Sum total supply (all generators + water taps)
   - Calculate path distance from each tower to nearest source
   - Distribute supply weighted by inverse distance
3. Update `received_power` on each tower
4. Update visual link rendering (thickness/colour reflects power flow)

### Linking UX
- Link action triggered from BuilderUnit context menu
- Player clicks source node (generator or connector only)
- Line renders from source to mouse: green/blue/yellow (in range) or red (out of range)
- Player clicks target node to complete link
- Cycle detection not required — cycles are valid within a cluster

## Multiplayer Considerations (future)

- Zone scenes are self-contained with defined inputs (wave_start, difficulty) and outputs (enemy_leaked signal)
- No game logic bleeds across zone boundaries
- EndZone listens to `enemy_leaked` from all connected zones
- Godot multiplayer API (RPCs + MultiplayerSynchronizer) can wrap zone communication
- Authoritative server model required at that point — single player is fully client-side

## Maps (MVP)

| Map | Description |
|-----|-------------|
| Power Towers | Faithful recreation of original layout — mixed terrain, cliffs, ramps, 6-8 checkpoints |
| Sandbox | Open square field, minimal terrain, checkpoints in simple zigzag — for learning and testing |

## Build & Export

- Godot export templates for Windows, Mac, Linux
- GodotSteam plugin integrated before first Steam build
- Steam Direct submission ($100 fee) when ready for Early Access
