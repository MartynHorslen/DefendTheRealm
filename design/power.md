# Power System

## Overview

Towers do not operate independently — they require power from a connected network. This adds a spatial strategy layer on top of tower placement. The power system uses a **proximity-weighted cluster model** — connected nodes form local grids, power distributes within each cluster weighted by path distance from the source.

## Power Sources

### Grass Generator
- Placed on grass terrain
- Consumes surrounding grass tiles at a set rate to generate power
- Finite — once surrounding grass is exhausted, output drops or stops
- Cheap to place; requires active zone management
- Natural early-game choice — build tight localised clusters around it

### Water Tap
- Placed adjacent to water terrain
- Draws power from water — does not deplete the source
- More expensive than a grass generator
- Reliable, infinite output — the premium mid/late game option
- Encourages extending your network toward water features on the map

## Power Distribution

### Connectors
- Placed between power sources and towers
- Explicitly linked by the player — power does not flow automatically by proximity
- Form chains and meshes across the map
- Take up space — routing connectors is a spatial decision, not just a logical one

### Cluster Model
Connected nodes (generators, connectors, towers) form isolated clusters. Power does not flow between disconnected clusters.

Within a cluster:
- Total supply = sum of all generator/water tap output in the cluster
- Total demand = sum of all tower power requirements
- Each tower receives a share of supply, **weighted by path distance from the nearest source** — towers closer to a generator receive proportionally more power than towers further away
- If supply < demand, all towers are under-powered proportionally

Multiple clusters can exist on the same map simultaneously. Each is calculated independently.

### Why Clusters Form Naturally
- Early game: tight clusters around cheap grass generators — localised, efficient
- Mid game: extend connectors toward water sources to form larger, more reliable grids
- Late game: manage multiple clusters or merge them under water tap power

## Linking (UX)

Power connections are made explicitly via the builder unit:

1. Select **Link** from the builder context menu
2. Click the **source node** (generator or connector only — towers are terminal, cannot be sources)
3. A line draws from the source to the mouse cursor:
   - **Green/blue/yellow** — within connection range, valid
   - **Red** — out of range, cannot connect
4. Click the **target node** to complete the link

Links are visible at all times. Line thickness, colour, and opacity reflect the power strength flowing through that connection — giving the player a live view of network health.

### Connection Rules
- Only generators and connectors can be link sources
- Towers are terminal nodes — they receive power but cannot distribute it
- No maximum connections per node — constraint is power dilution, not port count
- Cycles within a cluster are permitted — they become part of the distribution mesh
- Disconnected clusters are calculated independently

## Power Calculation

On any network change (link added, link removed, tower placed, tower sold, generator depleted):

1. **Find all clusters** — union-find across all linked nodes
2. **For each cluster:**
   - Sum total supply from all generators and water taps
   - Calculate path distance from each tower to its nearest source
   - Distribute supply proportionally, weighted by inverse distance
3. **Update each tower's received power** — drives fire rate and damage output

Calculation runs on the main thread. Power networks are small (tens of nodes) so this is effectively instant.

## Effect of Power on Towers

- **Full power** — tower fires at base rate with base damage
- **Partial power** — fire rate and damage scale proportionally (both affected)
- **No power** — tower is inert, does not fire
- A minimum power threshold (TBD) may be required before a tower activates at all

## Strategic Implications

- You cannot spam the strongest tower everywhere — power is the hard constraint
- Dense mazes near a source are efficient; distant towers need connector chains
- Selling a tower redistributes its power share to remaining cluster members
- A depleted grass generator forces a decision: expand toward water or place another generator
- Connector chains take up grid space — routing is a spatial puzzle within the maze puzzle

## Open Questions

- Exact formula for proximity-weighted distribution — linear falloff, exponential, or step-based?
- Minimum power threshold to activate a tower — yes or no?
- Can connectors be upgraded to boost power along a chain?
- What happens to a cluster when a connector mid-chain is destroyed by the tower-destruction blocking penalty — does the cluster split?
- Does generator upgrade increase base output, expand grass consumption radius, or both?
