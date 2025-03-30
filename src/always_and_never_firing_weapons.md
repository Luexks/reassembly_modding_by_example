# Always Fire Weapons
Cannons and lasers can be given the `ALWAYSFIRE` feature to continuously fire with enough energy. The launcher alternative is `AUTOLAUNCH`.
```lua
{17000
    features=CANNON|ALWAYSFIRE
}
{17001
    features=LASER|ALWAYSFIRE
}
{17002
    features=LAUNCHER|AUTOLAUNCH
}
```
The inverse for cannons and lasers is the `NEVERFIRE` feature, and for launchers it is `NEVERLAUNCH`.
```lua
{17000
    features=CANNON|NEVERFIRE
}
{17001
    features=LASER|NEVERFIRE
}
{17002
    features=LAUNCHER|NEVERLAUNCH
}
```
These features can be combined and omitted to create extremely unique weapons.

For example, one could have a turreted launcher that has an always-firing laser with multiple barrels to imitate a sci-fi drone laser-printer.