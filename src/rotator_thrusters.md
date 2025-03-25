# Rotator Thrusters
```lua
{17000
    features=THRUSTER|ROTATOR

    -- Similar fields to those of turreted weapons.
    rotatorSpeed=6
    rotatorLimit=pi -- *

    -- Other thruster fields are identical:
    thrusterForce=50000
    thrusterBoost=2.0
    thrusterBoostTime=3.0
    thrusterColor=0xFFFFFFFF
    thrusterColor1=0xFFFFFFFF
}
```

\* [Rotator Limit Bug](./rotator_thrusters.md#rotator-limit-bug)

A basic rotator thruster to show that it rotates weirdly with different player control schemes:
<video height=256 controls>
  <source src="diagrams/thruster_rotator.mp4" type="video/mp4">
  Your browser does not support the video tag.
</video>

## Rotator Limit Bug
The field `rotatorLimit` is bugged such that the rotator thruster always faces towards the front of the ship instead of the front of the block as one would expect.

Here is an example of 4 rotator thrusters with `turretLimit=pi` using the scale 2 `CANNON` shape to show that they face outwards from the command core:
```lua
{17000
    features=PALETTE|THRUSTER|ROTATOR
	shape=CANNON
	scale=2
	rotatorLimit=pi
}
```
<video height=256 controls>
  <source src="diagrams/thruster_rotator_limit_pi.mp4" type="video/mp4">
  Your browser does not support the video tag.
</video>

And here is the same thing but with `turretLimit=0`:
```lua
{17000
    features=PALETTE|THRUSTER|ROTATOR
	shape=CANNON
	scale=2
	rotatorLimit=0
}
```
<video height=256 controls>
  <source src="diagrams/thruster_rotator_limit_0.mp4" type="video/mp4">
  Your browser does not support the video tag.
</video>