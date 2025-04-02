# Features and Fields Not To Use
There are various features and fields that shouldn't be used because they are either used by the game internally, are unnecessary for their purpose, or are disliked by the community.

Ignore these guidelines if the cons do not affect you.
## Armor
The value of armor is subtracted from all the damage output of all non-explosive cannon bullets.
```lua
{17000
    armor=10
}
```
The armor value on shields causes bullets to 'slide' around shield's radius if the subtracted damage from the bullet causes its damage to be below the armor value.
```lua
{17000
    features=SHIELD
    shield={
        armor=100.
        -- Other shield features here.
    }
}
```
## Perishable
Used to allow the `lifetime` field to be used but is now unnecessary.
```lua
{17000
    features=PERISHABLE
    lifetime=5
}
```
## Persistent
Used internally for keeping map objectives, stations, and agents functional.
```lua
{17000
    features=PERSISTENT
}
```
## Deactivating Command Cores
Used during early development by Terran stations making them unable to be truly destroyed, only deactivated.
```lua
{17000
    features=COMMAND|DEACTIVATES
}
```
## Launch
Used internally for launchables like missiles and seeds grown from launchers. Do not use.
```lua
{17000
    features=LAUNCH
}
{17001
    features=LAUNCHER
    replicateBlock={
        features=LAUNCH
    }
}
```
## Auto-Launch
Identical to [`ALWAYSFIRE`](./always_and_never_firing_weapons.md#always-fire-weapons), but only works for not-turreted launchers and is used put on the launchable in the same way as [`LAUNCH`](./features_and_fields_not_to_use.md#launch).

It is unique in that it overrides [`NEVERFIRE`](./always_and_never_firing_weapons.md#never-fire-weapons) and is selectable in the bindings menu, but as neither of these traits are useful, [`ALWAYSFIRE`](./always_and_never_firing_weapons.md#always-fire-weapons) should be used instead.
```lua
{17000
    features=LAUNCHER
    replicateBlock={
        features=AUTOLAUNCH
    }
}
{17001
    features=LAUNCHER|NEVERFIRE
    replicateBlock={
        features=AUTOLAUNCH
    }
}
```
## Growing and Ungrowing
Used internally for blocks that are either growing or ungrowing.
```lua
{17000
    features=GROW
}
{17001
    features=UNGROW
}
```
## Unique
Block cannot be scaled, deleted, or copied in the editor. Used internally for the ship the player is editing in the constructor and ships exported from the constructor.
```lua
{17000
    features=UNIQUE
}
```