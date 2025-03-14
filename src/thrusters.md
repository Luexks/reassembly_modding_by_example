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
## Thruster Colors
The following videos each show the area of one thruster color type on a stationary vessel with `thrusterForce=50000`:
 - Only `thrusterColor`
```
{17000
    thrusterForce=50000
    thrusterColor=0xffffffff
    thrusterColor1=0x01000000
}
```
<video height=256 controls>
  <source src="diagrams/thruster_color_only_-.mp4" type="video/mp4">
  Your browser does not support the video tag.
</video>

 - Only `thrusterColor1`
```
{17000
    thrusterForce=50000
    thrusterColor=0x01000000
    thrusterColor1=0xffffffff
}
```
<video height=256 controls>
  <source src="diagrams/thruster_color_only_1.mp4" type="video/mp4">
  Your browser does not support the video tag.
</video>