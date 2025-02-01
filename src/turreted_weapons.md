# Turreted Weapons
Cannons, lasers, and launchers can all be turreted.
```lua
{17000
    features=CANNON|TURRET
    cannon={
        -- Cannon fields here.
    }
    turretSpeed=6
    turretLimit=pi
}
{17001
    features=LASER|TURRET
    LASER={
        -- LASER fields here.
    }
    turretSpeed=6
    turretLimit=pi
}
{17002
    features=LAUNCHER|TURRET
    replicateBlock={
        launcherSpeed=100
        -- Other replicated block fields here.
    }
    -- launcherOutSpeed is not used for turreted launchers.
    turretSpeed=6
    turretLimit=pi
}
```
Note that turreted launchers use `launcherSpeed` defined on the replicated block to control the speed that the launchable is fired at.
## Barrel Appearance
Turreted cannons and lasers both display barrels which have fields that control how the look and where their bullets are fired from.
```lua
{17000
    features=CANNON|TURRET  -- Same fields for `LASER|TURRET`
    barrelSize={5,2.5}      -- Length and width dimensions of the barrel.
                            -- (Height value is doubled.)
    barrelOffset={10,0}     -- Offset of (first if there are multiple) barrel.
    barrelSpacing={0,10}    -- Spacing between each barrel if there are multiple.
    barrelCount=2
    barrelTaper=0.75        -- Multiplier on barrel width at the end of the barrel.
                            -- Lasers have it default to 0. 
}
```
## Invisible Barrels
If you want a barrel to be near-invisible then use two near-zero values for its `barrelSize`;
```lua
{17000
    features=CANNON|TURRET
    barrelSize={0.001,0.001}
}
```
If you want the remove the dot that is created by this method, then cover it up using a shroud seemlessly-colored shroud on a higher Z level.