# Commands
```lua
{ 17000
    features=COMMAND
    blurb="The ship of this command cannot regenerate at all."
}
{ 17001
    features=COMMAND|REGROWER
    blurb="The command's ship can regenerate missing parts but not using debris."
}
{ 17002
    features=COMMAND|ASSEMBLER
    blurb="The command's ship can regenerate normally and by using debris."
}
```
Commands commonly have either the `REGROWER` or the `ASSEMBLER` features.

`REGROWER` allows the ship to be able to regenerate missing parts.

`ASSEMBLER` is the same as `REGROWER`, but also allows ships to reassemble themselves using parts from debris.

## The `command` Field
Commands can also contain the `command` field, but it is unnecessary for most ships as the values it contains are controlled by [`factions.lua`](./factions.lua.md) and how Reassembly handles blueprints.

Most use cases do not need to define all three command flags.
```lua
{ 17000
    features=COMMAND
    command={
        flags=RECKLESS|HATES_PLANTS -- These take priority over the faction's AI flags.
        faction=98                  -- Faction ID this command will be assigned to.
        blueprint="98_Test_Ship"    -- Blueprint that the command will become.
    }
}
```
## Command Flags
These are the flags which are used for [`command={flags}`](./commands.md#the-command-field) and in [`aiflags`](./factions.lua.md).
 - `NONE`: does nothing.
 - `METAMORPHOSIS`: AI will occasionally change blueprints.
 - `FOLLOWER`: follows player.
 - `ATTACK`: overrides all other command flags and makes AI attack ruthlessly. Used internally for tournament mode.
 - `FLOCKING`: move in a flock with nearby allied ships at the speed of the slowest one.
 - `RECKLESS`: disengage less.
 - `AGGRESSIVE`: initiate attack more easily.
 - `CAUTIOUS`: initiate attack less easily.
 - `SOCIAL`: call for help when attacked.
 - `PEACEFUL`: never initiate attack. Will still engage in combat if attacked, if nearby station is being captured, or if nearby allied ship with the `SOCIAL` AI flag is under attack.
 - `WANDER`: wander randomly if nothing else to do. Recommended for most factions.
 - `HATES_PLANTS`: kill plants if in range.
 - `FORGIVING`: stop attacking more easily.
 - `TRACTOR_TRANSIENT`: grab blocks from the environment and use them.
 - `DODGES`: dodge projectiles.
 - `RIPPLE_FIRE`: use ripple fire on weapons.
 - `SPREAD_FIRE`: use spread fire on weapons.
 - `BAD_AIM`: aim poorly.
 - `POINT_DEFENSE`: act like a point defense drone.
 - `INACTIVE`: become a vegetable, yum.
 - `SMART_FIRE`: use spread fire when enemy is expected to dodge.
 - `NO_PARENT`: do not follow parent ship.
 - `CHILDREN_SET`: used internally for AI ships that should not change their children blueprints as set by the player.
 - `BLUEPRINT_SET`: used internally for AI ships that should not change their own blueprint as set by the player.
 - `HANGOUT`: used to make the Anisoptera ship spin in circles :P.
 - `PACIFIST`: never attack even when attacked.
 - `FIRE_AT_WILL`: ignore parent ship target.

The following command flags can also be used for normal factions but at set in vanilla in the bindings menu:
 - `ALWAYS_KITE`: always attack from max range.
 - `ALWAYS_RUSH`: always attack at closest range regardless of incoming damage.
 - `ALWAYS_MANEUVER`: always dodging while attacking.
 - `AI_BINDING`: attack from range of highest binding weapon that has not been destroyed.