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
    features=PERISHABLE
    lifetime=5
}
```

## Deactivating Command Cores
Used to be used for Terran stations making them unable to be truly destroyed, only deactivated.
```lua
{17000
    features=COMMAND|DEACTIVATES
}
```

## Launch
Used internally for missiles and seeds that can be launched by the player. Do not use.
```lua
{17000
    features=LAUNCH
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