# Muzzle Flash
Muzzle flash is a desirable effect for making cannons look like they fire rounds with more force.
## Poof Muzzle Flash
This cannon uses a coloured [PSP](./bullet_poofs.html?highlight=PSP#bullet-poofs) to make a circular muzzle flash.
```lua
{ 17000
	features=CANNON
    cannon={
    -- Muzzle flash stage:
        roundsPerSec=1
        power=10
		
		projectileSize=2
		color=0xFFFFAA00
		
        damage=1
        muzzleVel=0
        range=0
		
		fragment={
    -- Actual bullet:
			damage=50
			muzzleVel=200
			range=200
			color=0xFFFFFFFF
		}
    }
}
```
<video height=256 controls>
  <source src="./diagrams/frag_poof_muzzle_flash.mp4" type="video/mp4">
  Your browser does not support the video tag.
</video>

## Bullet Muzzle Flash
This cannon uses a coloured bullet to make a bullet-shaped muzzle flash.

Below are what the stages do in order:
1. An invisible [anti-PSP stage](./anti-bullet_poof_stages.md#anti-primary-spawn-poof-anti-psp-stages).
2. The visible bullet that makes the shape of a muzzle flash. Exists for 1000/40, or 0.04 seconds.
3. This stage takes the fragment back in front of the gun. This means that the cannon does not look like it is shooting from behind itself.
4. The actual bullet's stage.
```lua
{ 17000
	features=CANNON
    -- Muzzle flash stages:
        -- Stage 1:
    cannon={   damage=1 muzzleVel=    1   range=  0   color=1          roundsPerSec=10 power=10 
        -- Stage 2:
	fragment={ damage=1 muzzleVel=-1000   range=-40   color=0xFFFFAA00 explosive=FINAL              projectileSize=5 spread=0.2
        -- Stage 3:
	fragment={ damage=1 muzzleVel=-1000*4 range=-40*4 color=1          explosive=FINAL|FRAG_NOFLASH
	fragment={
    -- Actual bullet (stage 4):
		damage=50
		muzzleVel=1
		range=    1
		color=0xFFFFFFFF
		explosive=FRAG_NOFLASH
	}}}}
}
```
<video height=256 controls>
  <source src="./diagrams/frag_bullet_muzzle_flash.mp4" type="video/mp4">
  Your browser does not support the video tag.
</video>