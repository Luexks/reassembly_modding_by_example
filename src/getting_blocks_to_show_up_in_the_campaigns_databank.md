# Getting Blocks to Show Up in the Campaign's Databank

Use `PALETTE` for everything you want a player to access, use `NOPALETTE` for everything you don't want a player to access. 

When a block has `PALETTE`, it will always shows up in campaign databank regardless of being present on one of the faction's ships.
```lua
{ 17000
    features=PALETTE
}
```
When a block has `NOPALETTE`, it will never shows up in campaign databank.
`NOPALETTE` blocks cannot be accessed by scaling in the campaign.
```lua
{ 17000
    features=NOPALETTE
}
```
