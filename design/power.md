# Power System

## Overview

Towers do not operate independently — they require power routed from a source via a connected chain. This adds a network management layer on top of tower placement. More towers on a circuit means less power per tower.

## Power Sources

### Grass Generator
- Placed on grass terrain
- Consumes surrounding grass tiles at a set rate to generate power
- Finite — once surrounding grass is exhausted, output drops or stops
- Cheap to place; requires active zone management

### Water Tap
- Placed adjacent to water terrain
- Draws power from water — does not deplete the source
- More expensive than a grass generator
- Reliable, infinite output — the premium option

## Power Distribution

### Connectors
- Placed between power source and towers
- Form a chain: `Generator → Connector → Connector → Tower`
- Power travels along the chain and splits equally at each branch point
- A tower must be linked to the chain to receive power

### Power Splitting
- Each connector or tower on a circuit receives an equal share of the source's output
- Example: one generator powering 8 towers gives each tower 1/8 power
- Low power = slower fire rate / reduced effectiveness
- Upgrading a generator increases total output without changing split behaviour

## Strategic Implications

- You cannot spam the strongest tower everywhere — power becomes the constraint
- Dense mazes need more generators or water taps to sustain them
- Connector chains take up space and must be routed thoughtfully
- Swapping out towers mid-game redistributes power to remaining towers (can be used tactically)

## Open Questions

- Does power level affect damage, fire rate, or both?
- Is there a minimum power threshold below which a tower does nothing?
- Can connectors be upgraded to carry more power without splitting?
- What happens to power when a connector in the chain is destroyed by an enemy (from tower destruction blocking penalty)?
