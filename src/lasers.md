# Lasers

Below is an example laser which has the most basic features. 
```lua
{ 17000
    features=LASER
    laser={
        damage=100      -- ...per second of contact.
        range=1000
        power=10        -- ...per second firing.
        width=2         -- ...of laser.
        color=0xFFFFFFFF  -- AARRGGBB color value.
        decay=0.1       -- Seconds after firing ceases for laser to fade away.
    }
}
```
## Firing in Bursts
If you want a laser to fire in bursts, you need to define its `burstyness`, `pulsesPerBurst`, and `pulsesPerSec`.

Burst firing lasers work similarly to burst firing cannons (see [Cannons: Firing in Bursts](./cannons.md#firing-in-bursts)), but `roundsPerSec` and `roundsPerBurst` are replaced by `pulsesPerSec` and `pulsesPerBurst` respectively.
```lua
{ 17000
    features=LASER
    laser={
        burstyness=0.5
        pulsesPerBurst=5
        pulsesPerSec=5
        -- Other laser fields here.
    }
}
```
## Lasers that Exert Force
There are two types of force a laser can exert: an immobilization force and a linear force.
### Imobilization Force
When a target is continuously hit by an imobilization laser, the `immobilizeForce` is exerted on the target to keep them in the same location as when they were initially hit.
```lua
{ 17000
    features=LASER
    laser={
        immobilizeForce=100000
        -- Other laser fields here.
    }
}
```
### Linear Force
Force exerted in the direction of the laser. Positive `linearForce` drives targets away, negative `linearForce` draws them in.
```lua
{ 17000
    features=LASER
    laser={
        linearForce=100000
        -- Other laser fields here.
    }
}
```
## Explosive Lasers
If you want a laser to be explosive, you need to define its `explosive` and `explodeRadius`.

The `explosive` field has three flags for lasers:
 - `ENABLED`: todo. 
 - `FINAL`: todo.
 - `PROXIMITY`: todo.

```lua
{ 17000
    features=LASER
    cannon={
        -- This laser will explode on hitting a block.
        -- It will deal its damage to all blocks in a radius of 50.
        explosive=ENABLED
        explodeRadius=50
        -- Other laser fields here.
    }
}
```