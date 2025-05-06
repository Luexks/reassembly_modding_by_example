# Anti-PSF, Anti-BSF, and Anti-BDF Stages
This chapter covers how to create fragments that do not produce (or minimize) PSFs, BSFs, and BDFs.
## Anti-Primary Spawn Flash
There is no known way to fully get rid of a PSF, only to make them as invisible as possible and to prevent them from overlapping to reduce the accumulation of noticable opaqueness.
```lua
{ 17000
	features=CANNON
    cannon={
        roundsPerSec=1
        power=10
		
		projectileSize=0
        damage=1
        muzzleVel=1
        range=0
		color=0
		
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