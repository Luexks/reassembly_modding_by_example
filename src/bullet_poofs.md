# Bullet Poofs
There are four types of bullet poofs:
 - Spawn poofs (SPs): when a bullet is spawned, the bullet spawns an SP.
 - Despawn poofs (DPs): when a bullet reaches the end of its lifetime, the bullet spawns a DP.
 - Primary spawn poofs (PSPs): the SP of the primary bullet stage. If fired from a turreted weapon, the PSP pins to where it was spawned on the turret.
 - Hit despawn poofs (HDPs): the DP of a non-explosive bullet that hits a block and is despawned from running out of damage to deal. These travel in a random direction.

Notice how PSPs are twice the radius and are brighter than DPs:
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

In the above example, the SPs are stationary but the DPs are not. This is because bullet poofs inherit the velocity of whatever spawned them, which in the case above includes a stationary ship and a moving projectile.

Below is a slow motion example to show how bullet poofs inherit velocity from a two-stage cannon:
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

When aesthetics demand it, bullet poofs can be removed using [anti-bullet poof stages](./anti-bullet_poof_stages.md).