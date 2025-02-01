# blocks.lua

`blocks.lua` is well-named. It controls the blocks of a mod and can become the most complicated of all the files you work with in a Reassembly mod.

This section will be like a shopping list. Do you want to add a shield? Go to the shield chapter in the section on block features. Do you want to add block decals using shrouding? Go to the shrouding chapter.

But before you do any of that cool stuff, here's how to set up your `blocks.lua` and not have to deal with Reassembly undecipherable punctuation errors at you:

```lua
{
    {<ID here> -- First block
        <block stuff here>
    }
    {<Different ID here> -- Second block
        <more block stuff here>
    }
    {<Another Different ID here> -- Third block
        <even more block stuff here>
    }
}
```
Brackets are how the game keeps understands when one thing starts and ends and what something contains.

Below is how the above structure might be represented if it actually defined three blocks:
```lua
{
    {17000
        group=98
        sort=1
        fillColor=0x5555AA
        fillColor1=0x3333AA
        lineColor=0xFFFFFF
        shape=SQUARE
        scale=1
        name="Hull"
        blurb="1x1\nBasic structure"
        durability=1.001
        density=0.1
        features=PALETTE
    }
    -- Extended blocks copy the fields of the blocks they extend.
    {17001,extends=17000,scale=2}
    {17002,extends=17000,scale=3}
}
```

If you are a beginner, read [Basic Fields and Hull](./basic_fields_and_hull.md) and [Block Features](./block_features.md).
