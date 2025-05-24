# Fragbeams

Fragbeams are cannons that use fragments in such a way that they they look like a laser beam when fired.

This chapter will describe multiple distinct types of fragbeams, each example video includes the fragbeam firing at a [target](./further_ship_testing.html?highlight=target#spawning-targets-and-asteroids) without commands and with commands.

## Synchronous, Evenly Spaced Fragbeam

This fragbeam uses `pattern=SPIRAL`to make each bullet split into two travelling in opposite directions. After each split, the distance travelled by each stage decreases until the final stage is reached in synchrony. Because there are no uses of `rangeStdDev`, this fragbeam is evenly spaced.

```lua
{ 17000
    features=CANNON
	cannon={   damage= 1 muzzleVel=121*64 range=32 color=0xFFFFFFFF                                                                    explosive=FINAL|FRAG_NOFLASH roundsPerSec=0.5 recoil=0
	fragment={ damage= 1 muzzleVel=  1    range= 0 color=1                           pattern=ABSOLUTE|       CONSTANT spread=90*pi/180 explosive=FINAL|FRAG_NOFLASH
	fragment={ damage= 1 muzzleVel=121*32 range=32 color=1          roundsPerBurst=2 pattern=ABSOLUTE|SPIRAL          spread=90*pi/180 explosive=FINAL|FRAG_NOFLASH
	fragment={ damage= 1 muzzleVel=  1    range= 0 color=1                           pattern=ABSOLUTE|       CONSTANT spread=90*pi/180 explosive=FINAL|FRAG_NOFLASH
	fragment={ damage= 1 muzzleVel=121*16 range=16 color=1          roundsPerBurst=2 pattern=ABSOLUTE|SPIRAL          spread=90*pi/180 explosive=FINAL|FRAG_NOFLASH
	fragment={ damage= 1 muzzleVel=  1    range= 0 color=1                           pattern=ABSOLUTE|       CONSTANT spread=90*pi/180 explosive=FINAL|FRAG_NOFLASH
	fragment={ damage= 1 muzzleVel=121* 8 range= 8 color=1          roundsPerBurst=2 pattern=ABSOLUTE|SPIRAL          spread=90*pi/180 explosive=FINAL|FRAG_NOFLASH
	fragment={ damage= 1 muzzleVel=  1    range= 0 color=1                           pattern=ABSOLUTE|       CONSTANT spread=90*pi/180 explosive=FINAL|FRAG_NOFLASH
	fragment={ damage= 1 muzzleVel=121* 4 range= 4 color=1          roundsPerBurst=2 pattern=ABSOLUTE|SPIRAL          spread=90*pi/180 explosive=FINAL|FRAG_NOFLASH
	fragment={ damage= 1 muzzleVel=  1    range= 0 color=1                           pattern=ABSOLUTE|       CONSTANT spread=90*pi/180 explosive=FINAL|FRAG_NOFLASH
	fragment={ damage= 1 muzzleVel=121* 2 range= 2 color=1          roundsPerBurst=2 pattern=ABSOLUTE|SPIRAL          spread=90*pi/180 explosive=FINAL|FRAG_NOFLASH
	fragment={ damage=25 muzzleVel=  1    range= 1 color=0xFFFFFFFF                  pattern=ABSOLUTE                                  explosive=      FRAG_NOFLASH
	}}}}}}}}}}}}
}
```

<video height=256 controls>
  <source src="diagrams/fragbeam_1.mp4" type="video/mp4">
  Your browser does not support the video tag.
</video>

## Synchronous, Unevenly Spaced Fragbeam

This fragbeam uses multiple stages with `rangeStdDev` and decreasing range after each stage to cover a long distance with many bullets.

```lua
{ 17000
 	features=CANNON
	cannon={   damage= 1 muzzleVel=  1   range= 0                    color=1                           explosive=FINAL|FRAG_NOFLASH roundsPerSec=4    recoil=0
	fragment={ damage= 1 muzzleVel=500*4 range=10*4 rangeStdDev=10*4 color=1          pattern=ABSOLUTE explosive=FINAL|FRAG_NOFLASH roundsPerBurst=64
	fragment={ damage= 1 muzzleVel=500*3 range=10*3 rangeStdDev=10*3 color=1          pattern=ABSOLUTE explosive=FINAL|FRAG_NOFLASH
	fragment={ damage= 1 muzzleVel=500*2 range=10*2 rangeStdDev=10*2 color=1          pattern=ABSOLUTE explosive=FINAL|FRAG_NOFLASH
	fragment={ damage= 1 muzzleVel=500*1 range=10*1 rangeStdDev=10*1 color=1          pattern=ABSOLUTE explosive=FINAL|FRAG_NOFLASH
	fragment={ damage=10 muzzleVel=  5   range= 1                    color=0x7FFFFFFF pattern=ABSOLUTE explosive=      FRAG_NOFLASH
	}}}}}}
}
```

<video height=256 controls>
  <source src="diagrams/fragbeam_2.mp4" type="video/mp4">
  Your browser does not support the video tag.
</video>

## Small Sequential, Unevenly Spaced Fragbeam

Even though the "beam" is not stationary and it looks more like a long bullet, this can still be useful when aesthetics demand it.

This fragment works by spawning one large cluster of fragments, each slight differences in range from a low `rangeStdDev` value. After each finishes its range, they become the final stage and begin travelling. Because of the high velocity of the final stage, the small difference in delay before each fragment starts travelling is expressed as a line of bullets, which looks like a travelling fragbeam.

```lua
{ 17000
 	features=CANNON
	cannon={   damage= 1 muzzleVel=   1 range=  0               color=1          explosive=FINAL|FRAG_NOFLASH                   roundsPerSec=2 recoil=0
	fragment={ damage= 1 muzzleVel=  40 range=  1 rangeStdDev=1 color=1          explosive=FINAL|FRAG_NOFLASH roundsPerBurst=16
	fragment={ damage=20 muzzleVel=1000 range=500               color=0xFFFFFFFF explosive=      FRAG_NOFLASH
	}}}
}
```

<video height=256 controls>
  <source src="diagrams/fragbeam_3.mp4" type="video/mp4">
  Your browser does not support the video tag.
</video>

## Long Sequential, Unevenly Spaced Fragbeam

This is less like a fragbeam, and more like a bullet that leaves a long trail.

The fragment works by spawning one large cluster of fragments, each with a different range from the high `rangeStdDev` value. After each finishes its range, they become the final stage, which is stationary and is what looks like a fragbeam.

```lua
{ 17000
 	features=CANNON
	cannon={   damage= 1 muzzleVel=   1 range=  0                 color=1                                              roundsPerSec=2 recoil=0
	fragment={ damage= 1 muzzleVel=   1 range=  0                 color=1          roundsPerBurst=255
	fragment={ damage=50 muzzleVel=1000 range=750 rangeStdDev=250 color=0xFFFFFFFF
	fragment={ damage=50 muzzleVel=   1 range=  5                 color=0xFFFFFFFF                    pattern=ABSOLUTE
	}}}}
}
```

The example video below includes the Terran Interceptor flying into the fragbeam.

<video height=256 controls>
  <source src="diagrams/fragbeam_4.mp4" type="video/mp4">
  Your browser does not support the video tag.
</video>

## X-Spaced Barrel Beam

See the chapter for the X-spaced barrel beam [here](./x-spaced_barrel_beams.md).

Even though this is technically not a fragbeam (it requires no fragments to achieve a beam like effect, instead using the `barrelSpacing` field), it is still just as viable as all the other fragbeam variants in creating a laser out of cannon projectiles.

<video height=256 controls>
  <source src="diagrams/x-spaced_barrel_beam.mp4" type="video/mp4">
  Your browser does not support the video tag.
</video>