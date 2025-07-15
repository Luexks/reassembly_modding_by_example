# Cannon Boosts

Cannon boosters have the `CANNON_BOOST` feature, they can change various statistics of a cannon. They can attach to cannons and can connect to other cannon boosters to use multiple boosters, such as for the Tinkrell faction.

They can affect both spinal and [turreted](./turreted_weapons.md) cannons. Their effects on damage, muzzle velocity, and roundsPerSec can be seen on the barrels of turreted cannons.

A cannon boost shape is normally used for cannon boosters, such as [`DISH_WEAPON`, `ISOTRI_25_WEAPON`, and `RECT_CANNON_BOOST`](./vanilla_shapes.md#cannon-boosters), but they can also use non-cannon boost shapes, as cannon boosting can be done through normal ports. Here is a link to the [custom cannon boost shapes](./cannon_boost_shapes.md) chapter.

The `cannonBoost` field is a list of containers for statistic modifers, which affect a specific quality of the cannon. They are formatted as in the example below:

```lua
{ 17000 
    features=CANNON_BOOST
    shape=SQUARE_1
    cannonBoost={
        { damage       ={1,0} }
        { range        ={1,0} }
        { muzzleVel    ={1,0} }
        { power        ={1,0} }
        { roundsPerSec ={1,0} }
        { explodeRadius={1,0} }
        { spread       ={1,0} }
    }
}
```

The first number is the multiplier and the second number is the adder. Both can be positive or negative.

Note that balancing cannon boosters can difficult.
