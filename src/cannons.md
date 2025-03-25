# Cannons
Below is an example cannon which has the most basic features. 
```lua
{17000
    features=CANNON
    cannon={
        damage=100      -- ...per shot fired.
        roundsPerSec=5
        muzzleVel=1000  -- Velocity of bullet.
        range=1000      -- Distance travelled by bullet before it is destroyed.
        power=10        -- ...per shot fired.
        spread=0.1      -- Maximum random spread of bullets in radians.
        color=0xFFFFFFFF  -- AARRGGBB color value.
        recoil=1        -- ...per shot fired.
    }
}
```
To be precise, that definition of bullet range is not correct, as bullets are destroyed based a duration calculated from just their `muzzleVel` and the `range`.

If the bullet was fired from a stationary ship, then it would travel 1000 units at 1000 units per second over 1 second. However, if the bullet was fired from a moving ship, then the bullet would inherit its velocity.

For the above example, if the ship firing the bullet was travelling in the same direction as the bullet being fired, the bullet would travel a greater distance with a greater speed over the same amount of time. 
## Firing in Bursts
If you want a cannon to fire in bursts, you need to define its `burstyness` and `roundsPerBurst`.

The way that a cannon using `burstyness` fires is defined by its `burstyness`, `roundsPerBurst`, and `roundsPerSec`. Keep in mind that `roundsPerSec` is always constant.

The value of `burstyness` must be between 0.0 and 1.0.

A burstyness of 0 means that a cannon will not fire in bursts and a burstyness of 1 means that a cannon will fire the value of `roundsPerBurst` all at once.

Burstyness values in between 0 and 1 will fire however many `roundsPerBurst` they have, wait, and then fire another burst again.
```lua
{17000
    features=CANNON
    cannon={
        -- This cannon will fire 5 bullets at once every 1 second.
        burstyness=1
        roundsPerSec=5
        roundsPerBurst=5

        -- Other cannon fields here.
    }
}
```
## Bullet Damage Output
Think of a bullet's damage output as its health which it 'spends' on damaging blocks. When the bullet runs out of damage output, it is destroyed.

More specifically, when a bullet (that's non-`explosive=ENABLED`) hits a block, it deal as much of its damage to the block as it can. If the bullet had more remaining damage output than the block's remaining health before the collision, then the bullet will continue existing with the block's prior remaining health subtracted from its damage output.
## Explosive Cannons
If you want a cannon to fire explosives, you need to define its `explosive` and `explodeRadius`.

The `explosive` field has three flags for non-fragment bullets:
 - `ENABLED`: bullet explodes when hitting a target. 
 - `FINAL`: bullet explodes at either the end of its range or when the bullet's damage output is exhausted.
 - `PROXIMITY`: bullet snaps its explosion to the closest enemy block relative to its explode radius.

([Explosive flags for fragments](./fragments.md#explosive-flags-for-fragments))

```lua
{17000
    features=CANNON
    cannon={
        -- This bullet will explode on hitting a block.
        -- It will deal its damage to all blocks in a radius of 50.
        explosive=ENABLED
        explosiveRadius=50
        -- Other cannon fields here.
    }
}
```
The `explosive` field is a flag type, so the way it works is similar to the `features` field for blocks. This means you can combine `explosive` flags for a desired effect, but this is unnecessary to know about with the three explosive flags stated prior unless you want to use [Fragments](./fragments.md).