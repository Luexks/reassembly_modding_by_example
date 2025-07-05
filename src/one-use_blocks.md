# One-Use Blocks

A block with the `ONEUSE` feature explodes after it is activated or after it finishes activating depending on whatever feature its coupled with.

For example, a [cannon](./cannons.md) block with `ONEUSE` will explode after firing, and a [laser](./lasers.md) block with `ONEUSE` will explode after the laser decays.

```lua
{ 17000
    features=ONEUSE|CANNON
    -- Cannon fields here.
}
{ 17001
    features=ONEUSE|LASER
    -- Laser fields here.
}
```

The destruction of a one-use block does not inherently cause damage other blocks, but features like [`EXPLODE`](./explosive_blocks.md) can make them more destructive.

Features which `ONEUSE` works with:
 - [`CANNON`](./cannons.md): block is destroyed after firing a single bullet. If [burst fields](./cannons.md#firing-in-bursts) are defined, then the block will be destroyed after `roundsPerBurst` number of bullets have been fired.
 - [`CANNON`](./cannons.md) and [`CHARGING`](./charging_cannons_and_lasers.md): block is destroyed after firing a single bullet. If [burst fields](./cannons.md#firing-in-bursts) is defined, then `ONEUSE` does not function.
 - [`LASER`](./lasers.md): block is destroyed after laser finishes decaying. [Burst fields](./lasers.md#firing-in-bursts) do not work with `ONEUSE`, the laser acts as if there are no burst fields.
 - [`LASER`](./laser.md) and [`CHARGING`](./charging_cannons_and_lasers.md): block is destroyed after laser finishes decaying. [Burst fields](./lasers.md#firing-in-bursts) do not work with `ONEUSE`, the laser acts as if there are no burst fields.
 - [`LAUNCHER`](./launchers.md): block is destroyed after firing a single launchable.
 - [`SHIELD`](./shields.md): block is destroyed after shield loses its health.
 - [`FACTORY`](./factories.md): block is destroyed after the command built by the factory finishes growing and is released. ([`SELFFACTORY`](./factories.md#self-factories) and [`TELESPAWN`](./factories.md#telespawn) do not have this effect. Combinations of different factory fields have no noteworthy effects.).

Because the function of [cannon](./cannons.md), [laser](./lasers.md), and [shield](./shields.md) blocks are dependent on the energy stored by the ship, their destruction because of `ONEUSE` can be manipulated by controlling energy.

<video height=256 controls>
  <source src="diagrams/one-use.mp4" type="video/mp4">
  Your browser does not support the video tag.
</video>
