# regions.lua
`regions.lua` controls how sectors procedurally generate in the galaxy by defining regions.
```lua
{
	-- General region identity:
	ident=98                    -- Region ID should be same as group.
                                -- (Technically does not have to be,
                                -- but it is strongly recommended.)

	color=0x5555AA              -- Color on galaxy map.
    
	faction=98                  -- Faction of the region.
                                -- Region name is taken from the faction.
	
    -- Region Spawning:
	count=3                     -- Number of this region on the map.

	position={0.90,0.95}        -- Range of this region's position 0.0-1.0.
                                -- 0.0 is the center of the galaxy,
                                -- 1.0 is at the edge.

	radius={0.05,0.10}          -- Range of this region's size 0.0-1.0.
                                -- 0.0 could just not spawn the region,
                                -- 1.0 could make the region galaxy-sized.

	type=2                      -- Defines the region's shape.
                                -- 0: Voronoi - evenly spaced, recommended (bias:).
                                -- 1: Splats  - what the Reds use.
                                -- 2: Circles - what most factions use.
	
	-- Standard fleets (See explanation below):
	fleets={
		{ 98 {
			{0,1000}
			{1,3000}
		} }
		{ 8 {
			{0,3000}
		} }
	}
	fleetCount={1,4}            -- Range of number of ships per fleet in each sector.
	fleetFraction=1.0           -- Probability that a fleet spawns
								-- in each sector 0.0-1.0.
	
	-- Fortresses (entities that surrounded damaged stations):
	fortress={
		"98_Fortress_1"
		"98_Fortress_2"
		"98_Fortress_3"
	}
	fortressCount={3, 6}         -- Range of fortresses per damaged station.
	fortressRadius={500, 500}    -- Range of distances of fortresses from station.
	
	-- Unique spawns:
	unique={
		{
			"98_Special_Station"
		}
		{
			"98_Other_Thing_1"
			"98_Other_Thing_2"
		}
		{
			"8_interceptor"
		}
	}
	uniqueFraction=0.5          -- Probability that a unique fleet spawns
								-- in each sector 0.0-1.0.
	
	-- Asteroids:
	ambient={1,2}               -- List that decides what spawns on asteroids.
	                            -- 0: Nothing.
                                -- 1: Green plants.
                                -- 2: Blue plants.
                                -- 3: Pink plants.
                                -- Only -1: only faction structures.

	asteroidDensity={0.1,0.2}   -- Range of density of asteroids in region 0.0-1.0.
	asteroidSize={12,24}        -- Range of block count per asteroid.
	asteroidFlags=PENROSE       -- See all flags below.
}
```
## Fleets
<!-- `fleetFraction` is the probability of a sector in the region containing a fleet.

`fleets` controls how much P is allocated to a fleet of a faction in a sector at different distances from the center of a region.

`fleetCount` controls the ranges of ship counts for each faction of a fleet. -->
When a sector is generated in this region, each type of fleet in `fleets` has `fleetFraction` (0.0-1.0) probability to spawn.

Each type of fleet in `fleets` has a faction ID. Each type of fleet also has a list of number pairs, with the 2nd number being a P allocation for every spawned fleet, and the 1st number being which distance from the center of the region the P allocation is for.

In other words, `fleets` controls how much P is allocated to a fleet of a faction in a sector at different distances from the center of a region.

`fleetCount` is a list of ranges of ship numbers for the fleet type at the same index.

So, every time a fleet is spawned in a sector, a random number in the range of the relevant `fleetCount` element is chosen to decide how many ships will be in the fleet. Then, the relevant P allocation for the fleet (dependent on the sector's distance from the center of the region) is spread out between the number of ships in the fleet.
```lua
    fleets={
		{ 98    -- Faction ID of the faction that can spawn
				-- in a sector in this region.
			{
				-- Each faction 98 fleet in the center of the region has 10000P total.
				{0.0,10000}

				-- Each faction 98 fleet halfway into the region has 3000P total.
				{0.5, 3000}

				-- Each faction 98 fleet at the edge of the region has 1000P total.
				{1.0, 1000}
			}
		}
		{ 8     -- The Terrans (faction 8) could also spawn in this region.
			{ 
				-- No Terrans can spawn in the center of the region.
				{0.0,    0}

				-- No Terrans can spawn close to the edge of the region.
				{0.75,    0}

				-- Terran fleets can spawn at the edge of the region
				-- and the each have 1000P total.
				{1.0, 1000}
			}
		}
    }

	fleetCount={
		{4,8}	-- Each faction 98 fleet has 4 to 8 ships.
		{10,16} -- Each Terran fleet has 10 to 16 ships.
	}

				-- Every sector in this region has a 75% chance of spawning a
				-- faction 98 fleet and a 75% of spawning a Terran fleet.
	fleetFraction=0.75
```