# Bullet Flashes

There are three types of bullet flashes:
 - Bullet spawn flashes (BSFs): when a bullet is spawned, the bullet spawns a BSF.
 - Bullet despawn flashes (BDFs): when a bullet reaches the end of its lifetime, the bullet spawns a BDF.
 - Primary spawn flashes (PSFs): the BSF of the primary bullet stage. If fired from a turreted weapon, the PF pins to where it was spawned on the turret.

Notice how PSFs are twice the radius and are brighter than BDFs:
```lua
{ 17000 
    features=CANNON
    cannon={
        damage=100
        roundsPerSec=0.5
        muzzleVel=200
        range=100
        power=10
        color=0xFFFFFFFF
    }
}
```
<video height=256 controls>
  <source src="diagrams/frag_flashes.mp4" type="video/mp4">
  Your browser does not support the video tag.
</video>

In the above example, the PSFs are stationary but the BDFs are not. This is because bullet flashes inherit the velocity of whatever spawned them, which in the case above includes a stationary ship and a moving projectile.

Below is a slow motion example to show how bullet flashes inherit velocity from a two-stage cannon:
```lua
{ 17000
    features=CANNON
    cannon={
        damage=50
        roundsPerSec=0.5
        muzzleVel=200
        range=100
        power=10
		color=0xFFFFFFFF
		fragment={
			damage=50
			roundsPerBurst=1
			muzzleVel=200
			range=100
			color=0xFFFFFFFF
		}
    }
}
```
<video height=256 controls>
  <source src="diagrams/frag_flashes_2.mp4" type="video/mp4">
  Your browser does not support the video tag.
</video>

When aesthetics demand it, bullet flashes can be removed using [anti-PSF, anti-BSF, and anti-BDF stages](./anti-psf,_anti-BSF,_and_anti-bdf_stages.md).