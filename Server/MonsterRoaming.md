<h1>Monster Roaming</h1>

The engine offers a primitive way to create paths _(or roaming points)_ for monsters to travel.

<h2>Pieces of the Puzzle</h2>

For a roaming path to be set for a given monster, there is multiple places information must be set.

- Files
  - monster_roaming.lua
- Database Tables
  - RoamingResource
  - RoamingPointResource
 
<h3>Monster Roaming Script</h3>

Below is an example of how a roaming monster is spawned into the world by the `monster_roaming.lua` script.

```lua

--respawn_roaming_mob (group roaming ID, respawn monster ID, direction (angle), distance from roaming route (M meters), respawn period (seconds) )

	respawn_roaming_mob( 1001, 1000050, 180, 4, 10 )
	respawn_roaming_mob( 1001, 1000050, 60, 4, 10 )
	respawn_roaming_mob( 1001, 1000050, 300, 4, 10 )
```

In the above example you will make use of the `respawn_roaming_mob` script command. The command uses the following arguments:

- `roaming_id` - Linked to the **RoamingResource** and **RoamingPointResource**
- `monster_id` - The `id` _(MonsterResource)_ of the monster being spawned
- `direction` - The rotation/angle _(See example below)_ of the npc
- `distance` - The amount of distance the npc will spawn/roam from the center of the roaming path
- `respawn_period` - The amount of time it will take this monster to respawn if killed

<h4>Monster Direction</h4>

![Facing Diagram](https://i.imgur.com/yW9ssbO.png)

<h3>Roaming Resource</h3>

Below is an example of the `RoamingResource` entry linked to the above script example. _(id `1001`)_

![roaming_resource_ex](https://i.imgur.com/jCzv7Lv.png)

In the above example you will see the following fields.

- `id` - Roaming group id linked to by the _(monster_roaming.lua script)_
- `roaming_type` - The type of roaming the monster will perform _(See the `roaming_type` enumeration below)_
- `move_speed` - The speed at which the monster will roaming between listed points
- `hate_type` - The type of hatred the monster will display when fighting any player'(s) _(See the `hate_type` enumeration below)_
- `respawn_interval` - The amount of time _(in seconds)_ before the monster will respawn if killed
- `special_ability` - If provided sets special behaviours _(See the `special_ability` enumeration below)_

<h4>Roaming Type Enum</h4>

```
ROAMING_TYPE_ROUND			= 0
ROAMING_TYPE_GO_BACK		= 1
```

<h4>Hate Type Enum</h4>

```
HATE_TYPE_INDIVIDUAL		= 1 << 0
HATE_TYPE_SHARE_FIRST		= 1 << 1
HATE_TYPE_FULL_SHARE		= 1 << 2
```

<h4>Special Abilities</h4>

```
ATTRIBUTE_HEAL_HP_ON_COMEBACKHOME			= 1	// Whether or not to restore HP to the maximum when returning to the original position after the end of battle
```

<h3>Roaming Point Resource</h3>

Below is an example of the `RoamingPointResource` entries linked to the above `RoamingResource` entry. 

![roaming_point_ex](https://i.imgur.com/ZdcDXHi.png)

> **Note:** The first entry is the starting location, every entry after is a new point to be moved to past the previous entry.

In the above example you will see the following fields.

- `roaming_id` - Roaming group id linked to by the _(monster_roaming.lua script and the RoamingResource database table)_
- `point_id` - This points sequence in the roam. Starting at 0 _(The first point)_ and increasing by 1 per entry.
- `x` - The ingame x coordinate of this point
- `y` - The ingame y coordinate of this point
