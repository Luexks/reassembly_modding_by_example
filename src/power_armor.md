# Power Armor
A shield block, with a shield radius so small that it the shield cannot be hit, redirects incoming damage that hits the block to the health pool of the shield. As the shield block can only be destroyed when its shield goes down, the survivability of the block will be dependent on the survivability of the shield.

If a shield's `delay` is 0 and the ship it is attached to has enough power, then it can spend the ship's power to regenerate any amount of damage without being destroyed, as long as the shield's `regen` and `strength` provide enough buffer for any incoming damage.

Shield blocks like this translate the power store of their ship directly into survivability, and are thus called 'power armor'.
```lua
{ 17000
	features=SHIELD
	health=1
    shield={
        strength=100
        regen=10000
        radius=1
        delay=0
		color=0xFFFF0000
		lineColor=0x0000FF
		damagedColor=0xFFFF0000
    }
}
```
The following example showcases the difference between power armor on a ship with high power generation (Green) and one without (Red) using the Red's Tempest.
```lua
{ 17001 features=GENERATOR generatorCapacityPerSec=0     powerCapacity=50000
    fillColor=0xFF0000 fillColor1=0xFF0000 }
{ 17002 features=GENERATOR generatorCapacityPerSec=10000 powerCapacity=50000
    fillColor=0x00FF00 fillColor1=0x00FF00 }
```
Notice how the power armor only takes damage when the ship's power runs out after enough fire:

<video height=256 controls>
  <source src="diagrams/power_armor.mp4" type="video/mp4">
  Your browser does not support the video tag.
</video>

Power armor is effective against damage spread out over time, especially lasers, but is vulnerable to high amounts of instantaneous damage that is greater than the buffer of the shield's `strength`.