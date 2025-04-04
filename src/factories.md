# Factories
There are multiple types of factory blocks, but the default `FACTORY` factories are the most common.

```lua
{ 17000
    -- TRACTOR is not strictly necessary for factories. 
    features=FACTORY|TRACTOR
    -- Factories tend to also store R and collect R.
    tractorRange=500
    capacity=50
}
```
## Other Types of Factories
### Self-Factory
To-do. Documentation states that ships with `SELFFACTORY` can only spawn their own design.
```lua
{ 17000
    features=SELFFACTORY
}
```
### Telespawn
`TELESPAWN` is like `FACTORY`, but ships are 'teleported' in, fully built, and for no R cost.
```lua
{ 17000
    features=TELESPAWN
}
```
