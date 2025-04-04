# Other Features and Fields

Here are some other features and fields that are certainly useful, but undeserving of having their own sections.

## Health and Mass
Directly define exact values for health and mass.

Unnecessary for most cases when `durability` and `density` exist.
```lua
{ 17000
    health=50
    mass=50
}
```

## No Regen
Blocks with `NOREGEN` do not regenerate after taking damage or being destroyed.
```lua
{ 17000
    features=NOREGEN
}
```

## Commands that do not give resources on death
`FREERES` is strongly recommended for launchables with commands.
```lua
{ 17000
    features=COMMAND|FREERES
}
```
