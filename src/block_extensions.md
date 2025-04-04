# Block Extensions

The `extends` field takes the Block ID of another block and duplicates all of that block's data into the new block. Fields after the `extends` field give the new block its differences. 

```lua
{
    { 17000
        name="My First Block"
        group=78
        sort=0
        shape=SQUARE
        scale=1
        features=PALETTE
        -- Other block stuff here.
    }
    { 17001 extends=17000 scale=2
        name="My Second Block, which is exactly the same,"
        blurb="but is scale 2 and has a blurb and a different name."
    }
}
```

Looks at the above block of ID '17001'. It uses block extension, an great utility that makes block creation productive and concise.

Block extensions allow you to not have to rewrite stuff over and over again. It's especially useful for creating hull palettes. 
