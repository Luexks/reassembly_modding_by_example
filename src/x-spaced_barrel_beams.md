# X-Spaced Barrel Beams
Also called just 'barrel beams' or alternatively 'hellbores'.

X-spaced barrel beams fire an evenly spaced "beam" of burst bullets across multiple X-spaced invisible barrels. They can penetrate enemy ships.

Key fields:
 - `barrelCount` = `roundsPerBurst`.
 - Near 1 `burstyness`.
 - High `roundsPerSec` compared to normal cannons to counteract high `roundsPerBurst`.
 - (Low `muzzleVel` and `range` if you want it to be a stationary beam.)
 - (Low `recoil` if you do not want to be flung around because of high `roundsPerBurst`.)
```lua
{ 17000
	features=CANNON|TURRET
	barrelSize={0.000001,0.000001}
	barrelCount=32
	barrelSpacing={20,0}
	barrelOffset={32*20*0.5,0}
    cannon={
        damage=100
        roundsPerSec=32*2
		roundsPerBurst=32
		burstyness=1
        muzzleVel=2
        range=1
        color=0xFFFFFFFF
        recoil=0
    }
}
```
<video height=256 controls>
  <source src="diagrams/x-spaced_barrel_beam.mp4" type="video/mp4">
  Your browser does not support the video tag.
</video>

When a ship has no commands, it is difficult for the beam to penetrate it as the bullets are required to hit the side of a ship, unlike when attacking ships that have a command.

The XSBB has the advantage of both being a consistent weapon to use and acting the same across different [UPS](./ups.md) settings, as there are no high speed fragments that can travel different distances across different UPS settings.

However, the XSBB has the disadvantage of spawning bullets inside of enemy ships, which may not be desirable from a balancing standpoint. Moreover, it is subject to the XSBB desync glitch, in which bullets randomly do not spawn when fired.