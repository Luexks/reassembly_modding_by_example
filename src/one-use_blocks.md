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

Features which `ONEUSE` works with:
 - [`CANNON`](./cannons.md): block is destroyed after firing a single bullet. If `roundsPerBurst` is defined, then the block will be destroyed after `roundsPerBurst` number of bullets have been fired.
 - [`LASER`](./lasers.md): block is destroyed after laser decays.
 - [`SHIELD`](./shields.md): block is destroyed after shield loses its health.
 - [`FACTORY`](./factories.md): block is destroyed after the command built by the factory finishes growing and is released.