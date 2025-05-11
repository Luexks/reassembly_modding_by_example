# Bullet Shaping

Using the fragment system to create specific looks for a cannon projectile is called bullet shaping.

This chapter covers various types of common bullet shapes:
 - [Fragball](./bullet_shaping.md#fragball)
 - [Spikey Fragball](./bullet_shaping.md#spikey-fragball)
 - [Reverse Bullet](./bullet_shaping.md#reverse-bullet)
 - [2-Tail Bullet](./bullet_shaping.md#2-tail-bullet)
 - [3-Tail Bullet](./bullet_shaping.md#3-tail-bullet)
 - [8-Point Star](./bullet_shaping.md#8-point-star)
 - [X Shape Lense Flare Bullet](./bullet_shaping.md#x-shape-lens-flare-bullet)
 - [9-Point Saw](./bullet_shaping.md#9-point-saw).

## Fragball

A simple ball of 5 fragments that keeps its formation by inheriting velocity from the primary stage.

```lua
{ 17000
	features=CANNON
    cannon={
        damage=1
        roundsPerSec=1
        power=10
        muzzleVel=200
        range=0
		color=0xAAFFFFFF
		explosive=FINAL
		fragment={
			roundsPerBurst=5
			damage=25
			spread=360*pi/180
			muzzleVel=1
			range=    1
			color=0xAAFFFFFF
			explosive=FRAG_NOFLASH
		}
    }
}
```

<video height=256 controls>
  <source src="./diagrams/frag_fragball.mp4" type="video/mp4">
  your browser does not support the video tag.
</video>

## Spikey Fragball

Same as the other fragball but with more bullets with a higher velocity so that they are rendered with longer tails.

```lua
{ 17000
	features=CANNON
    cannon={
        damage=1
        roundsPerSec=5
        power=10
        muzzleVel=1500
        range=0
		color=0xAAFFFFFF
		explosive=FINAL
		fragment={
			roundsPerBurst=12
			damage=25
			spread=360*pi/180
			muzzleVel=1
			range=    1
			color=0xAAFFFFFF
			explosive=FRAG_NOFLASH
		}
    }
}
```

<video height=256 controls>
  <source src="./diagrams/frag_spikey_fragball.mp4" type="video/mp4">
  your browser does not support the video tag.
</video>

## Reverse Bullet

Simple bullet that appears backwards.

```lua
{ 17000
	features=CANNON
    cannon={
        damage=1
        roundsPerSec=1
        power=10
        muzzleVel=500
        range=0
		color=0xAAFFFFFF
		explosive=FINAL
		fragment={
			spread=180*pi/180
			pattern=CONSTANT
			explosive=FRAG_NOFLASH

			damage=50
			muzzleVel=1
			range=    0.5
			color=0xAAFFFFFF
		}
    }
}
```

<video height=256 controls>
  <source src="./diagrams/frag_reverse_bullet.mp4" type="video/mp4">
  your browser does not support the video tag.
</video>


## 2-Tail Bullet

Two angled bullets inherit velocity from the primary stage to create an arrow shape.

```lua
{ 17000
	features=CANNON
    cannon={
        damage=1
        roundsPerSec=1
        power=10
        muzzleVel=500
        range=0
		color=0xAAFFFFFF
		explosive=FINAL
		fragment={
			roundsPerBurst=2
			damage=25
			spread=30*pi/180
			muzzleVel=1
			range=    0.5
			color=0xAAFFFFFF
			explosive=FRAG_NOFLASH
			pattern=SPIRAL
		}
    }
}
```

<video height=256 controls>
  <source src="./diagrams/frag_2-tail_bullet.mp4" type="video/mp4">
  your browser does not support the video tag.
</video>

## 3-Tail Bullet

Three angled bullets inherit velocity from the primary stage to create a bullet with three tails.

```lua
{ 17000
	features=CANNON
    cannon={
        damage=1
        roundsPerSec=1
        power=10
        muzzleVel=1000
        range=0
		color=0xAAFFFFFF
		explosive=FINAL
		fragment={
			roundsPerBurst=3
			damage=25
			spread=30*pi/180
			muzzleVel=1
			range=    0.5
			color=0xAAFFFFFF
			explosive=FRAG_NOFLASH
			pattern=SPIRAL
		}
    }
}
```

<video height=256 controls>
  <source src="./diagrams/frag_3-tail_bullet.mp4" type="video/mp4">
  your browser does not support the video tag.
</video>

## 8-Point Star

Eight bullets in a uniform `SPIRAL` pattern to create an 8-pointed star bullet.

```lua
{ 17000
	features=CANNON|PALETTE
    cannon={
        damage=1
        roundsPerSec=1
        power=10
        muzzleVel=1000
        range=0
		color=0xAAFFFFFF
		explosive=FINAL
		fragment={
			roundsPerBurst=8
			damage=25
			spread=157.5*pi/180
			muzzleVel=1
			range=    0.5
			color=0xAAFFFFFF
			explosive=FRAG_NOFLASH
			pattern=SPIRAL
		}
    }
}
```

<video height=256 controls>
  <source src="./diagrams/frag_8-point_star.mp4" type="video/mp4">
  your browser does not support the video tag.
</video>

## X Shape Lens Flare Bullet

Similar to the [X shape lens flare always fire decoration](./always_fire_weapons_as_decorations.md#x-shape-lens-flare).

A more complex bullet that creates an X-shaped bullet that always faces in the same direction using `muzzleVel=0` and still travels in the fired direction by inheriting velocity from the primary stage.

The function of the stages are as follows:
1. Creates a [PSP](./bullet_poofs.html?highlight=PSP#bullet-poofs) and supplies the velocity inherited by the rest of the fragment.
2. Stage with `muzzleVel=0` to force the fragment to face either right or left.
3. Rotates the fragment by 45° degrees.
4. Splits the fragment into four bullets spread over a 270° spread.
5. The actual bullet stage that can deal damage and is visible.

```lua
{ 17000
	features=CANNON
    -- 1st stage:
    cannon={   damage=1 muzzleVel=1000 range=0 color=0xAAFFFFFF explosive=FINAL              roundsPerSec=1 power=10 
    -- 2nd stage:
	fragment={ damage=1 muzzleVel=   0 range=0 color=1          explosive=FINAL|FRAG_NOFLASH
    -- 3rd stage:
	fragment={ damage=1 muzzleVel=   1 range=0 color=1          explosive=FINAL|FRAG_NOFLASH spread= 45*pi/180 pattern=CONSTANT
    -- 4th stage:
	fragment={ damage=1 muzzleVel=   1 range=0 color=1          explosive=FINAL|FRAG_NOFLASH spread=135*pi/180 pattern=SPIRAL roundsPerBurst=4
    -- 5th stage (actual bullet):
	fragment={
		damage=100
		muzzleVel=1
		range=    0.5
		color=0xAAFFFFFF
	}}}}}
}
```

<video height=256 controls>
  <source src="./diagrams/frag_x_shape_lens_flare_bullet.mp4" type="video/mp4">
  your browser does not support the video tag.
</video>

## 9-Point Saw

A complex saw blade ring of bullets made out of nine bullets.

The function of each stage is as follows:
1. Creates a [PSP](./bullet_poofs.html?highlight=PSP#bullet-poofs) and moves the fragment backwards a small distance. This accounts for the distance which the fragment moves forwards while assembling the saw formation so that it looks like the saw blade spawns from the right place.
2. Reverses the fragment again so that it faces forwards without changing its position.
3. Splits the fragment into 9 bullets which then travel outwards almost instantly.
4. Cancels out the fragment's velocities so that it no longer changes position.
5. This stage rotates by 60° anticlockwise using `pattern=CONSTANT`. This stage is also the actual bullet stage that can deal damage and is visible.

```lua
{ 17000
	features=CANNON
    -- 1st stage:
    cannon={   damage=1 muzzleVel=-1000 range= -10 color=0xAAFFFFFF explosive=FINAL              roundsPerSec=1 power=10
    -- 2nd stage:
    fragment={ damage=1 muzzleVel=-2000 range=   0 color=1          explosive=FINAL|FRAG_NOFLASH
    -- 3rd stage:
    fragment={ damage=1 muzzleVel=  400 range=  12 color=1          explosive=FINAL|FRAG_NOFLASH pattern=SPIRAL roundsPerBurst=9 spread=0.5*320*pi/180
    -- 4th stage:
    fragment={ damage=1 muzzleVel= -400 range=   0 color=1          explosive=FINAL|FRAG_NOFLASH
    -- 5th stage (actual bullet):
    fragment={
        damage=25
        spread=60*pi/180
        muzzleVel=1
        range=    0.5
        color=0xFFFFFFFF
        explosive=FRAG_NOFLASH
        pattern=CONSTANT
    }}}}}
}
```

<video height=256 controls>
  <source src="./diagrams/frag_9-point_saw.mp4" type="video/mp4">
  your browser does not support the video tag.
</video>
