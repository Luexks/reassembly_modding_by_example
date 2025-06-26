# Point Defense Weapons

Point defense weapons have the `AUTOFIRE` field. They are set to the point defense binding by default and are used to automatically destroy down enemy [launchables](./launchers.md) and enemy ships if there are no other targets.

Point defense [cannons](./cannons.md) and [lasers](./lasers.md) are usually [turreted](./turreted_weapons.md) and have a high [`turretSpeed`](./turreted_weapons.html?highlight=turretSpeed), upwards of 20 radians (1146°) per second in vanilla Reassembly.

Point defense [missiles](./launchers.md#missile-launcher) and [drones](./launchers.md#drone-launcher) only need `AUTOFIRE` on the launcher, not the launchable. (The launchable is automatically given the [`POINT_DEFENSE`](./commands.html?highlight=POINT_DEFENSE#command-flags) by the game.)

```lua
{ 17000 name="Point Defense Cannon"
    features=CANNON|TURRET|AUTOFIRE
    turretSpeed=12
	cannon={
		damage=10
		roundsPerSec=10
		range=500
		muzzleVel=1500
        color=0xFFFFFFFF
	}
}
{ 17001 name="Point Defense Laser"
    features=LASER|TURRET|AUTOFIRE
	turretSpeed=20
	laser={
		damage=20
		range=500
		color=0xFFFFFFFF
		width=2
		decay=0.1
	}
}
{ 17002 name="Point Defense Missile Launcher"
	features=LAUNCHER|AUTOFIRE
	group=98
	shape=RECT_LAUNCHER1
	replicateBlock={
        features=COMMAND|EXPLODE|THRUSTER|TORQUER
        shape=MISSILE
        lifetime=16

        explodeDamage=25
        explodeRadius=5

        thrusterForce=3000
        thrusterColor=0xFFFFFFFF
        thrusterColor1=0xFFFFFFFF

        torquerTorque=10000
		
	}
}
{ 17003 name="Point Defense Drone Launcher"
	features=LAUNCHER|AUTOFIRE
	group=98
	shape=RECT_LAUNCHER1
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
            muzzleVel=1500
            range=500
            power=1
            color=0xFFFFFFFF
        }

        powerCapacity=100
        generatorCapacityPerSec=100
    }
}
```