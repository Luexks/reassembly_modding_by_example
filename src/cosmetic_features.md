# Cosmetic Features

All of the following features are purely decorative and do not affect block function.

## Invisible Blocks

Block does not render. This includes feature icons but excludes [barrels](./turreted_weapons.md#barrel-appearance) (not the turret circle beneath) and [shrouds](./shrouding.md).

```lua
{ 17000
    feature=INVISIBLE
}
```

## Internal Lines

Block always renders lines.

```lua
{ 17000
    features=INTLINES
}
```

## No Icon

Block doesn't renders icons.

```lua
{ 17000
    features=NOICON
}
```

## No Recolor

Block is not recolored by color schemes.

```lua
{ 17000
    features=NORECOLOR
}
```
