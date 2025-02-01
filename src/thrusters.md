# Thrusters
```lua
{17000
    features=THRUSTER

    thrusterForce=50000 -- =50K

    -- When a thruster is turned on, its thruster force is multipled by
    -- its thruster boost for `thrusterBoostTime` seconds.
    thrusterBoost=2.0
    thrusterBoostTime=3.0

    -- Thruster trail colors are decided by these two 0xAARRGGBB values.
    -- thrusterColor controls the color of the main thruster trail,
    thrusterColor=0xAARRGGBB
    -- While thrusterColor1 controls the color of the trail
    -- immediately at the thruster.
    thrusterColor1=0xAARRGGBB
}
```