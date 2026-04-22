# Towers & Elements

## Elemental System

Towers and enemies have elemental affinities. Matching a tower's element to an enemy's weakness deals bonus damage; mismatched elements deal reduced damage. This adds a target-prioritisation and tower-selection layer on top of maze routing.

## Known Elements (from original Power Towers — to be verified)

| Element | Effect | Tower Type |
|---------|--------|------------|
| Fire | Damage over time (burn) | Flame tower |
| Frost/Ice | Slows movement speed | Frost tower |
| Water | — | Water tower |
| Electric/Lightning | — | Lightning tower |
| Nature/Poison | Damage over time (poison) | Nature tower |
| Earth/Stone | High single-hit damage, slow fire rate | Catapult/ballista |
| Archer | Baseline physical damage, no element | Arrow tower |

*Elements and interactions TBD pending research into original game and our own design decisions.*

## Tower Categories

### Basic Towers (no power required)
- Archer tower — reliable physical damage, no elemental effect
- May serve as filler/maze-wall towers that contribute low damage

### Elemental Towers (power required)
- Require connection to the power grid to fire
- Higher damage and special effects vs matching enemy types
- Fire rate and effectiveness scale with available power

### Utility Structures (not towers)
- Grass Generator — power source, placed on grass
- Water Tap — power source, placed adjacent to water
- Connector — power chain link, no combat role

## Upgrade Path (draft)

Towers can be upgraded in place:
- **Level 1 → 2**: increased damage / fire rate
- **Level 2 → 3**: unlocks elemental special effect (burn, slow, etc.)
- Each upgrade increases power consumption

## Open Questions

- How many distinct tower types in MVP? (Recommendation: 3–4 to keep decisions meaningful)
- Do basic archer towers consume power, or are they genuinely free to run?
- Can towers have dual elements, or is each tower locked to one?
- Is there a tower that increases power output rather than dealing damage (power amplifier)?
- Strength/weakness chart — full matrix or simple rock-paper-scissors triangle?
