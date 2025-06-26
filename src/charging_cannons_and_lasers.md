# Charging Cannons and Lasers

[Cannons](./cannons.md) and [lasers](./lasers.md) with the `CHARGING` feature must have their key binding held down and released to fire. It has two fields: `chargeMaxTime` and `chargeMin`d.

 - `chargeMaxTime` is the time in seconds needed for the weapon to achieve maximum charge, letting it deal its defined damage.
 - `chargeMin` is the fraction (between 0.0 and 1.0) of charge at which the weapon may fire, but with less damage.

```lua
{ 17000
    features=CANNON|CHARGING

    chargeMaxTime=2
    chargeMin=0.5
    -- Charge time:        2 seconds.
    -- Min Discharge time: 1 second.

    cannon={
        damage=25
        range=100
        muzzleVel=100
        roundsPerSec=1
        color=0xFFFFFFFF
    }
}
{ 17001
    features=LASER|CHARGING

    chargeMaxTime=2
    chargeMin=0.5
    -- Charge time:        2 seconds.
    -- Min Discharge time: 1 second.

    LASER={
        damage=25
        range=100
        width=2
        decay=1
        color=0xFFFFFFFF
    }
}
```

When a charging weapon is fired, it creates a unique effect (its size depends on how charged the weapon was):

<video height=512 controls>
  <source src="diagrams/charging.mp4" type="video/mp4">
  Your browser does not support the explodeRadius tag.
</video>
