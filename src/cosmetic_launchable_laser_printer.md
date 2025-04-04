# Cosmetic Launchable Laser Printer
A launchable-generating cosmetic laser printer effect can be created with a barrel-spaced laser block with a high barrel count to mimic a moving laser.

The laser printer blocks use a visible laser and an high fire rate invisible cannon to cycle through the barrels.

The direction of the laser is decided by the sign of `barrelSpacing`'s Y change, allowing for a mirrored version of the laser printer.

Both the laser printer's cycle time (1 second, because `barrelCount` / `roundsPerSec` = 1) and the launcher's `replicateTime` are the same, allowing for the two blocks to synchronize their functionality if activated at the right time.
```lua
{ 17000 features=LASER|CANNON|ALWAYSFIRE|TURRET
    name="Laser Printer Left -> Right"
	shape=271390000
	scale=4
	barrelCount=30
	barrelSize={0.0001,0.0001}
	barrelSpacing={0,-1}
	turretLimit=0
	sound=NONE
    laser={
        damage=0.0001
        range=40
        width=0.5
        color=0xFFFFFFFF
    }
	cannon={
		muzzleVel=0
		range=0
        color=0x01000000
        damage=0.0001
		roundsPerSec=30
		recoil=0
		explosive=FINAL
	}
}
{ 17001 extends=17000 name="Laser Printer Right -> Left" shape=271390001 barrelSpacing={0,1}}
{ 17002 features=LAUNCHER|TURRET|NOICON
    name="Launcher"
	scale=4
	turretLimit=0
	replicateBlock={
		features=NOCLIP_ALLY
		shape=MISSILE_SHORT
		scale=3
		lifetime=2
	}
	replicateTime=1
}
```
This shape is a direct copy of the base game's `RECT_LONG` with a mirrored counterpart for both directions of the laser printer.
```lua
{271390000, {{verts={{5, -5}, {-5, -5}, {-5, 5}, {5, 5}}, ports={{3, 0.5}, {0, 0.5},
           {1, 0.5}, {2, 0.5}}},
      {verts={{5, -10}, {-5, -10}, {-5, 10}, {5, 10}}, ports={{3, 0.25}, {3, 0.75}, {0, 0.5}, {1, 0.25},
           {1, 0.75}, {2, 0.5}}},
      {verts={{5, -15}, {-5, -15}, {-5, 15}, {5, 15}}, ports={{3, 0.167}, {3, 0.5}, {3, 0.833}, {0, 0.5},
           {1, 0.167}, {1, 0.5}, {1, 0.833}, {2, 0.5}}},
      {verts={{5, -20}, {-5, -20}, {-5, 20}, {5, 20}}, ports={{3, 0.125}, {3, 0.375}, {3, 0.625}, {3,
            0.875}, {0, 0.5}, {1, 0.125}, {1, 0.375}, {1, 0.625}, {1, 0.875}, {2, 0.5}}},
      {verts={{5, -25}, {-5, -25}, {-5, 25}, {5, 25}}, ports={{3, 0.1}, {3, 0.5}, {3, 0.9}, {0, 0.5},
          {1, 0.1}, {1, 0.5}, {1, 0.9}, {2, 0.5}}},
      {verts={{5, -30}, {-5, -30}, {-5, 30}, {5, 30}}, ports={{3, 0.083}, {3, 0.25}, {3, 0.417}, {3, 0.583},
           {3, 0.75}, {3, 0.917}, {0, 0.5}, {1, 0.083}, {1, 0.25}, {1, 0.417}, {1, 0.583}, {1, 0.75},
          {1, 0.917}, {2, 0.5}}},
      {verts={{5, -35}, {-5, -35}, {-5, 35}, {5, 35}}, ports={{3, 0.071}, {3, 0.357}, {3, 0.643}, {3,
            0.929}, {0, 0.5}, {1, 0.071}, {1, 0.357}, {1, 0.643}, {1, 0.929}, {2, 0.5}}},
      {verts={{5, -40}, {-5, -40}, {-5, 40}, {5, 40}}, ports={{3, 0.062}, {3, 0.188}, {3, 0.312}, {3,
            0.438}, {3, 0.562}, {3, 0.688}, {3, 0.812}, {3, 0.938}, {0, 0.5}, {1, 0.062}, {1, 0.188},
          {1, 0.312}, {1, 0.438}, {1, 0.562}, {1, 0.688}, {1, 0.812}, {1, 0.938}, {2, 0.5}}},
      {verts={{5, -45}, {-5, -45}, {-5, 45}, {5, 45}}, ports={{3, 0.056}, {3, 0.278}, {3, 0.5}, {3, 0.722},
           {3, 0.944}, {0, 0.5}, {1, 0.056}, {1, 0.278}, {1, 0.5}, {1, 0.722}, {1, 0.944}, {2, 0.5}}},
      {verts={{5, -50}, {-5, -50}, {-5, 50}, {5, 50}}, ports={{3, 0.05}, {3, 0.15}, {3, 0.25}, {3, 0.35},
           {3, 0.45}, {3, 0.55}, {3, 0.65}, {3, 0.75}, {3, 0.85}, {3, 0.95}, {0, 0.5}, {1, 0.05}, {1,
            0.15}, {1, 0.25}, {1, 0.35}, {1, 0.45}, {1, 0.55}, {1, 0.65}, {1, 0.75}, {1, 0.85}, {1, 0.95},
           {2, 0.5}}}}},
{271390001 {} mirror_of=271390000}
```
The laser printer is placed next to the turreted launcher it seem like they are one mechanism.
<video height=256 controls>
  <source src="diagrams/cosmetic_laser_printer.mp4" type="video/mp4">
  Your browser does not support the video tag.
</video>