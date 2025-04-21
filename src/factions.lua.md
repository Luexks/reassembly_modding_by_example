# factions.lua
`factions.lua` controls general faction identity.
```lua
{
	98={                            -- Faction ID should be same as group.
                                    -- (Technically does not have to be,
                                    -- but it is strongly recommended.)
		name="My Faction"

		playable=2                  -- 0: Unplayable.
                                    -- 1: Unlockable by killing a >1000P ship.
                                    -- 2: Always playable.

		start="98_Starter_Ship"     -- Requires this format to work.

		primaries=3                 -- Amount of primary colors.
		color0=0x5555AA
		color1=0x3333AA
		color2=0xFFFFFF

        -- Explosion color does not have to be defined.
        -- If defined, either color is randomly picked for each explosion.
		explosionColor0=0xFF0000
        explosionColor1=0xFFAA00

		thrustSFX=0                 -- 0: Normal thrust SFX.
                                    -- 1: 'Magic' thrust SFX.

		aiflags=BAD_AIM|CAUTIOUS    -- How ships of this faction will act.
                                    -- Some ships deviate on an individual basis.
									-- *
	}
	-- More factions:
	256={
		-- Fleet fields here.
	}
	888={
		-- Fleet fields here.
	}
}
```
`aiflags` uses [command flags](./commands.md#command-flags).