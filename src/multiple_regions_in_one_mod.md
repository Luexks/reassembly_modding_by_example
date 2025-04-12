# Multiple Regions in One Mod
Below is an example of a mod that contains different regions for factions 200, 300, and 400.
```lua
{
    -- No fields are defined in the outermost scope.
    subregions={
        {
            ident=200
            -- Other fields here.
        }
        {
            ident=300
            -- Other fields here.
        }
        {
            ident=400
            -- Other fields here.
        }
    }
}
```
The outermost brackets represent the entire galaxy, which is itself a region, but has unique functionality to allow multiple `subregions` definitions to coexist and extend each other.