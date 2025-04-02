# Always and Never Firing Weapons
## Always Fire Weapons
Cannons, lasers, and launchers can be given the `ALWAYSFIRE` feature to continuously fire with enough energy. Weapons with `ALWAYSFIRE` are unselectable in the bindings menu and are ignored by the AI.
```lua
{17000
    features=CANNON|ALWAYSFIRE
}
{17001
    features=LASER|ALWAYSFIRE
}
{17002
    features=LAUNCHER|ALWAYSFIRE
}
```

## Never Fire Weapons
The inverse of `ALWAYSFIRE` is `NEVERFIRE`.

`launcherPower=inf` is necessary for non-turreted launchers, as otherwise, AI-controlled ships can fire the launchable.
```lua
{17000
    features=CANNON|NEVERFIRE
}
{17001
    features=LASER|NEVERFIRE
}
{17002
    features=LAUNCHER|NEVERFIRE
    launcherPower=inf
}
{17003
    features=LAUNCHER|TURRET|NEVERFIRE
}
```

`ALWAYSFIRE` takes priority over `NEVERFIRE`.