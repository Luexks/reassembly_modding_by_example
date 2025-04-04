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