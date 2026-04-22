# Enemies & Waves

## Enemy Properties

Each enemy has:
- **Health** — total damage to kill
- **Speed** — affects how long they spend in the maze (slower = more shots taken)
- **Elemental affinity** — determines weakness/resistance to tower elements
- **Armour type** — physical, magical, unarmoured (affects which towers are most effective)
- **Reward** — gold/resources dropped on kill

## Enemy Types (draft)

| Type | Speed | Health | Affinity | Notes |
|------|-------|--------|----------|-------|
| Infantry | Medium | Medium | None | Baseline unit |
| Fast Runner | High | Low | None | Hard to hit, low value |
| Brute | Low | Very High | Earth | Tanky; slow enough to absorb lots of fire |
| Fire Spawn | Medium | Medium | Fire | Resistant to fire, weak to frost/water |
| Frost Walker | Low | High | Frost | Resistant to slow effects |
| Poison Creep | High | Low | Nature | Applies poison debuff to nearby towers? |

*Types TBD — to be designed around the elemental system once that is finalised.*

## Wave Structure

- Waves are timed — enemies spawn at intervals within each wave
- Difficulty scales across waves: more enemies, higher health, faster speeds, mixed types
- Later waves mix elemental types, forcing the player to have diverse tower coverage
- A rest period between waves allows selling/repositioning towers

## Leak Penalty

If an enemy reaches the endzone corridor:
- Player loses a life (or lives scale with enemy health/type)
- Enemy is removed from play
- Enough leaks = game over

## Wave Escalation Ideas

- **Swarm waves** — many weak fast enemies; tests fire rate
- **Armoured waves** — few slow high-health enemies; tests damage output
- **Elemental waves** — all one element; punishes mono-element tower builds
- **Mixed waves** — requires diverse elemental coverage
- **Boss waves** — single very high health enemy with multiple elemental resistances

## Open Questions

- Does enemy speed interact with the routing strategy? (A very fast enemy may not benefit much from a longer maze)
- Are there flying enemies that ignore tower walls and pathfind directly? (Would bypass the maze mechanic — probably not for MVP)
- Can enemies have abilities (self-heal, split on death, call reinforcements)?
