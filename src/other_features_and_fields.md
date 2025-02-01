# Other Features and Fields

Here are some other features and fields that are certainly useful, but undeserving of having their own sections.

## Health and Mass
Explicitly define exact values for health and mass.
Unnecessary for most cases when `durability` and `density` exist.
```lua
{17000
    health=50
    mass=50
}
```

## No Regen
Block does not regenerate after taking damage or being destroyed.
```lua
{17000
    features=NOREGEN
}
```

## Command core that does not give resources on death
Strongly recommended for launchables with command cores.
```lua
{17000
    features=COMMAND|FREERES
}
```
