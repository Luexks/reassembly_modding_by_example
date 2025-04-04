# Other Collision: Bumper and Elasticity
## Elasticity
Bounciness of a block when it collides.
More elasticity means more bounciness.
Should be between 0.0 and 1.0.
```lua
{ 17000
    elasticity=0.4
}
```
## Bumper
Does not take melee damage when colliding. Anti-melee armor.
```lua
{ 17000
    features=BUMPER
}
```