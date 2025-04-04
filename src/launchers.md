# Launchers
Below is an example launcher that fires a missile that does nothing and dies after 2 seconds.
```lua
{ 17000
	features=PALETTE|LAUNCHER
	shape=RECT_LAUNCHER
	replicateBlock={
		shape=MISSILE
		lifetime=2
	}
	replicateTime=1
	launcherPower=100
	launcherOutSpeed=100
	launcherAngVel=0
}
```
Launchables (what launchers fire) should not have IDs or a `group` value.

Because launchers generate a fully customisable block, they can be very diverse.

The rest of this chapter will contain the most common launcher variants.
## Mine Layer
Mines have the [`EXPLODE`](./explosive_blocks.md) feature.
```lua
	replicateBlock={
        features=EXPLODE
		shape=HEPTAGON
		lifetime=20

        explodeDamage=100
        explodeRadius=100
	}
```
## Torpedo Launcher
Torpedoes have the [`EXPLODE`](./explosive_blocks.md) and [`THRUSTER`](./thrusters.md) features.
```lua
	replicateBlock={
        features=EXPLODE|THRUSTER
		shape=MISSILE
		lifetime=8

        explodeDamage=100
        explodeRadius=100

        thrusterForce=3000
        thrusterColor=0xFFFFFFFF
        thrusterColor1=0xFFFFFFFF
	}
```
## Missile Launcher
Missiles have the [`COMMAND`](./command_cores.md), [`EXPLODE`](./explosive_blocks.md), [`THRUSTER`](./thrusters.md), and [`TORQUER`](./torquers.md) features.
```lua
	replicateBlock={
        features=COMMAND|EXPLODE|THRUSTER|TORQUER
		shape=MISSILE
		lifetime=8

        explodeDamage=100
        explodeRadius=100

        thrusterForce=3000
        thrusterColor=0xFFFFFFFF
        thrusterColor1=0xFFFFFFFF

        torquerTorque=10000
	}
```
## Drone Launcher
Drones have the [`COMMAND`](./command_cores.md), [`NOCLIP_ALLY`](./noclipping_blocks.md), [`FREERES`](./other_features_and_fields.md#command-core-that-does-not-give-resources-on-death), [`THRUSTER`](./thrusters.md), [`TORQUER`](./torquers.md), [`GENERATOR`](./generators.md), either [`CANNON`](./cannons.md) or [`LASER`](./lasers.md), and usually [`TURRET`](./turreted_weapons.md) features.
### Cannon Drone
```lua
	replicateBlock={
        features=COMMAND|NOCLIP_ALLY|FREERES|THRUSTER|TORQUER|GENERATOR|CANNON|TURRET
		shape=DISH_MISSILE
        scale=3
		lifetime=30

        thrusterForce=3000
        thrusterColor=0xFFFFFFFF
        thrusterColor1=0xFFFFFFFF

        torquerTorque=10000

        turretSpeed=4

        cannon={
            damage=20
            roundsPerSec=5
            muzzleVel=500
            range=500
            power=1
            spread=0.1
            color=0xFFFFFFFF
        }

        powerCapacity=100
        generatorCapacityPerSec=100
	}
```
### Laser Drone
```lua
	replicateBlock={
        features=COMMAND|NOCLIP_ALLY|FREERES|THRUSTER|TORQUER|GENERATOR|LASER|TURRET
		shape=DISH_MISSILE
        scale=3
		lifetime=30

        thrusterForce=3000
        thrusterColor=0xFFFFFFFF
        thrusterColor1=0xFFFFFFFF

        torquerTorque=10000

        turretSpeed=4

        laser={
            damage=20
            range=500
            power=2
            width=2
            color=0xFFFFFFFF
            decay=0.05
        }

        powerCapacity=100
        generatorCapacityPerSec=100
	}
```
## Launcher Drone Launcher
It is very possible to create drones that fire launchables. Below is an example for a drone that fires drones; a mothership drone?
```lua
{ 17111
	group=98
	features=PALETTE|LAUNCHER
	shape=RECT_LAUNCHER1
	replicateBlock={
        features=COMMAND|NOCLIP_ALLY|FREERES|THRUSTER|TORQUER|GENERATOR|LAUNCHER
		shape=MISSILE_LAUNCHER
        scale=3
		lifetime=20
		density=1

        thrusterForce=3000
        thrusterColor=0xFFFF0000
        thrusterColor1=0x00000001

        torquerTorque=10000

		replicateBlock={
			features=COMMAND|NOCLIP_ALLY|FREERES|THRUSTER|TORQUER|GENERATOR|LASER|TURRET
			shape=MISSILE_SHORT
			scale=1
			lifetime=20
			density=1

			thrusterForce=3000
			thrusterColor=0xFF0000FF
			thrusterColor1=0x00000001

			torquerTorque=10000

			turretSpeed=4
			
			laser={
				damage=20
				range=500
				width=0.5
				power=1
				decay=0.1
				color=0xFFFFFFFF
			}
			
			powerCapacity=100
			generatorCapacityPerSec=100
		}
		replicateTime=1
		launcherPower=1
		launcherOutSpeed=100
		launcherAngVel=0
		
        powerCapacity=100
        generatorCapacityPerSec=100
	}
	replicateTime=1
	launcherPower=100
	launcherOutSpeed=100
	launcherAngVel=0
}
```
<video height=256 controls>
  <source src="diagrams/drone_collectoriszation_of_the_masses.mp4" type="video/mp4">
  Your browser does not support the video tag.
</video>