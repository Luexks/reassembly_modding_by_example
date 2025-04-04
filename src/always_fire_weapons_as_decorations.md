# Always Fire Weapons as Decorations
As weapons are so flashy, they can be used purely as cosmetics using the always fire features.

This chapter will contain a few common always fire weapon decorations.

When using always fire cannons cosmetically, it is important to check how [UPS](./ups.md) will affect the visuals as having too low a `roundsPerSec` on a high UPS will cause the cannon to flicker. It is thus recommeneded to have `roundsPerSec=120` by default unless lag due to the sheer amount of bullets becomes an issue.

## Frag Spike
```lua
{17000
	features=CANNON|ALWAYSFIRE
	sound=None                  -- Having a sound is annoying.
    cannon={
        -- Cosmetic fields:
		projectileSize=2        -- Override projectile size calculation based on damage.
        muzzleVel=10000         -- Affects length of the bullet.
        color=0xFFFFFFFF

        -- Functional fields:
        damage=0.0001           -- Prevents it from dealing damage.
        roundsPerSec=120        -- Minimal flicker on 60 UPS and above.
        range=0                 -- So that the bullet does not travel.
        power=0.0001            -- Cosmetics should not use power.
		recoil=0                -- Cosmetics should not have recoil.
		explosive=FINAL         -- Removes bullet end particle.
    }
}
```
<video height=256 controls>
  <source src="diagrams/always_fire_frag_spike.mp4" type="video/mp4">
  Your browser does not support the video tag.
</video>

## Laser Spike
```lua
{17000
	features=LASER|ALWAYSFIRE
	sound=None                  -- Having a sound is annoying.
    laser={
        -- Cosmetic fields:
        range=50
        width=3
        color=0xFFFFFFFF

        -- Functional fields:
        damage=0                -- Prevents it from dealing damage.
        power=0.0001            -- Cosmetics should not use power.
    }
}
```
<video height=256 controls>
  <source src="diagrams/always_fire_laser_spike.mp4" type="video/mp4">
  Your browser does not support the video tag.
</video>

You could also use a negative `width`, such as `width=-3` in the below example:

<video height=256 controls>
  <source src="diagrams/always_fire_laser_spike_negative_width.mp4" type="video/mp4">
  Your browser does not support the video tag.
</video>

## Laser Light
```lua
{17000
	features=LASER|ALWAYSFIRE|TURRET
	sound=None
	barrelSize={0.001,0.001}    -- Centers the laser.
    laser={
        -- Cosmetic fields:
        width=3                 -- Affects the size of the light.
        color=0xFFFFFFFF

        -- Functional fields:
        damage=0
        range=0
        power=0.0001
    }
}
```
<video height=256 controls>
  <source src="diagrams/always_fire_laser_light.mp4" type="video/mp4">
  Your browser does not support the video tag.
</video>

You can also make them flash:
```lua
    laser={
		burstyness=0.5
		pulsesPerBurst=1
		pulsesPerSec=1
        -- Other laser features here.
    }
```
<video height=256 controls>
  <source src="diagrams/always_fire_laser_light_flashing.mp4" type="video/mp4">
  Your browser does not support the video tag.
</video>

## Frag Tentacle
```lua
{17000
    features=ALWAYSFIRE|CANNON
	sound=None
	cannon={
        -- Cosmetic fields:
		projectileSize=1        -- Override bullet size calculation based on damage.
		muzzleVel=100           -- "Speed" of tentacle wave.
		range=50                -- Length of tentacle.
        color=0xAAFFFFFF
		spread=pi*0.25          -- Width of tentacle.
		burstyness=0.0203       -- Try to making this value as small as possible to
                                -- make the wave pattern cycle seemless.
		roundsPerBurst=60       -- Amount of bullets in a wave cycle.
		roundsPerSec=30         -- Fidelity of tentacle.
		
        -- Functional fields:
		pattern=WAVE
        damage=0.0001           -- Prevents it from dealing damage.
        power=0.0001            -- Cosmetics should not use power.
		recoil=0                -- Cosmetics should not have recoil.
		explosive=FINAL         -- Removes bullet end particle.
	}
}
```
<video height=256 controls>
  <source src="diagrams/always_fire_frag_tentacle.mp4" type="video/mp4">
  Your browser does not support the video tag.
</video>

## Lens Flare
A lens flare effect that does change direction when the ship it is on rotates.

1st stage: invisible anti-FSP stage with spread just above 180° to be centered and `muzzleVel=0` to make the frag always face in the same direction.

2nd stage: invisible 90° rotation stage by using `pattern=CONSTANT`.

3rd stage: visible lens flare using 2 frags that always face in the same direction using `pattern=SPIRAL`.
```lua
{17000
	features=CANNON|ALWAYSFIRE
	sound=None
	cannon={
	-- 1st stage:
		muzzleVel=0
		range=0
        color=0x01000000
		spread=pi*0.5*1.0001
		pattern=ABSOLUTE
        damage=0.0001
		roundsPerSec=120
		recoil=0
		explosive=FINAL
		fragment={
	-- 2nd stage:
			muzzleVel=1
			range=0
			color=0x01000000
			pattern=CONSTANT
			damage=0.0001
			explosive=FINAL|FRAG_NOFLASH
			spread=pi*1/2
			fragment={
	-- 3rd stage:
				projectileSize=2
				muzzleVel=3000
				range=0
				color=0xFFFFFFFF
				pattern=SPIRAL
				damage=0.0001
				explosive=FINAL|FRAG_NOFLASH
				spread=pi*1/2
				roundsPerBurst=2
			}
		}
	}
}
```
<video height=256 controls>
  <source src="diagrams/always_fire_lens_flare.mp4" type="video/mp4">
  Your browser does not support the video tag.
</video>

# X Shape Lens Flare
You can also make lens flares with an 'X' shape.

This X-shaped lens flare does not contain the 90° rotating 2nd stage of the standard lens flare frag as the X shape does not require it.

The visible (2nd) stage's `roundsPerBurst` is changed from `2` to `4` and its `spread` is changed from `pi*1/2` (180°) to `pi*3/4` (270°).
```lua
{17000
	features=CANNON|ALWAYSFIRE
	sound=None
	cannon={
	-- 1st stage:
		muzzleVel=0
		range=0
        color=0x01000000
		spread=pi*0.5*1.0001
		pattern=ABSOLUTE
        damage=0.0001
		roundsPerSec=120
		recoil=0
		explosive=FINAL
		fragment={
	-- 2nd stage:
			projectileSize=2
			muzzleVel=3000
			range=0
			color=0xFFFFFFFF
			pattern=SPIRAL
			damage=0.0001
			explosive=FINAL|FRAG_NOFLASH
			spread=pi*3/4
			roundsPerBurst=4
		}
	}
}
```
<video height=256 controls>
  <source src="diagrams/always_fire_lens_flare_x.mp4" type="video/mp4">
  Your browser does not support the video tag.
</video>

## Frag Rings
Here is an example of a basic frag ring you could make for a generator:

1st stage: invisible anti-FSP stage with spread just above 180° is used to center the frag.

2nd stage: invisible stage of a 20-round burst in a uniform spiral which are sent outwards.

3rd stage: this is the stage visible to the player. `pattern=ABSOLUTE` is used to reset the bullet velocities, and `projectileSize`, `muzzleVel`, and `color` affect how the frag looks. 
```lua
{17000
	features=CANNON|ALWAYSFIRE|GENERATOR
	sound=None
	shape=OCTAGON
	scale=3
    cannon={
	-- 1st stage:
        damage=0.0001
		projectileSize=0.001
        muzzleVel=1
        range=0
        power=0.01
		recoil=0
        roundsPerSec=120
		pattern=CONSTANT
		spread=pi*0.5*1.0000001
        color=0x01000001
		fragment={
	-- 2nd stage:
			damage=0.0001
			projectileSize=0.1
			muzzleVel=10*60
			range=10
			pattern=ABSOLUTE|SPIRAL
			roundsPerBurst=20
			spread=pi*340/360
			explosive=FINAL|FRAG_NOFLASH
			color=0x01000000
			fragment={
	-- 3rd stage:
				damage=0.0001
				projectileSize=0.1
				muzzleVel=-1
				range=0
				pattern=ABSOLUTE
				explosive=FINAL|FRAG_NOFLASH
				color=0xFFFFFFFF
			}
		}
    }
	-- Generator fields here.
}
```
<video height=256 controls>
  <source src="diagrams/always_fire_frag_ring_1.mp4" type="video/mp4">
  Your browser does not support the video tag.
</video>

## Poof Particle Emitter
A simple fragless setup that emits 120 frag despawn poofs every second. A neat effect for a generator. 
```lua
{17000
	features=CANNON|ALWAYSFIRE|GENERATOR
	sound=None
	shape=OCTAGON
	scale=3
	cannon={
		projectileSize=1
		muzzleVel=100
		range=0
        color=0xFFFFFFFF
		spread=pi
		pattern=ABSOLUTE
        damage=0.0001
		roundsPerSec=120
		recoil=0
	}
	-- Generator fields here.
}
```
<video height=256 controls>
  <source src="diagrams/always_fire_poof_particle_emitter.mp4" type="video/mp4">
  Your browser does not support the video tag.
</video>

## Launchable Laser Printer
See the main page for the [Launchable Laser Printer](./cosmetic_launchable_laser_printer.md).

<video height=256 controls>
  <source src="diagrams/cosmetic_laser_printer.mp4" type="video/mp4">
  Your browser does not support the video tag.
</video>