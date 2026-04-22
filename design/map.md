# Map & Zones

## Layout

The full map is an 8-player layout arranged around a central endzone:

```
[TL]  [TM]  [TR]
[ML]  [EZ]  [MR]
[BL]  [BM]  [BR]
```

- **8 player zones** — corners (TL, TR, BL, BR) and edge-centres (TM, BM, ML, MR)
- **Central endzone (EZ)** — shared target; if enemies reach this, players lose lives
- **Corridors** — narrow connecting paths between zones and the endzone; not buildable

## Terrain Types

Each player zone contains a mix of:

| Terrain | Description | Buildable |
|---------|-------------|-----------|
| Grass | Standard open land | Yes — towers, generators |
| Water | Rivers/pools | No — but water taps can be placed on adjacent tiles |
| Cliff | Raised rocky areas | No |
| Ramp | Access points through cliffs | No — but enemies can use them |
| Path tile | Fixed checkpoint squares | No |
| Corridor | Zone-to-zone connections | No |

## Spawn Points

Two player zones share each spawn point on the edges of the map. Enemies spawn at the edge of each player's zone and must navigate checkpoints before reaching the corridor to the endzone.

## Zone Geography (reference layout — top-right zone)

Based on the original Power Towers map, a single zone contains:
- Spawn point on the outer edge
- 6–8 checkpoint tiles arranged in a zigzag/spiral pattern across the zone
- At least one cliff feature with ramps (creates natural chokepoints)
- Mixed grass and water terrain
- One or two natural corridor exits toward the endzone

## Single-Player Prototype

For MVP, one zone is built out fully. The enemy enters from the spawn edge and must reach the corridor exit. The player builds the maze within the zone.
