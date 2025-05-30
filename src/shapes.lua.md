# shapes.lua

`shapes.lua` is also well-named. It controls the shapes used by the blocks in [`blocks.lua`](./blocks.lua.md) by using a block's `shape` field.

## Quickly, the one limitation

However, before you understand how to create custom shapes, you need to understand the limitations of shape modding. Luckily, there's only one main limitation.

<video height=256 autoplay loop muted>
  <source src="diagrams/polygon_overlap.mp4" type="video/mp4">
  Your browser does not support the video tag.
</video>

Shapes in Reassembly cannot be concave, sort of. This is because Reassembly polygons are rendered by drawing triangles from the starting vertex. (More precisely, the triangles are constructed from the starting vertex and each of its non-adjacent sides.)

This makes certain concave shapes possible with the correct first vertex. However, other concave shapes, that have no vertex with an unobstructed line of sight to each other vertex, are not possible.

## The Syntax

```lua
{
{ <ID here>          -- First shape
    {                -- List of different scales
        {            -- Scale 1
            <vertex and port stuff here>
        }
        {            -- Scale 2
            <vertex and port stuff here>
        }
        {            -- Scale 3
            <vertex and port stuff here>
        }
    }
}
{ <Different ID here> -- Second block
    {                -- List of only one scale
        {            -- Scale 1
            <vertex and port stuff here>
        }
    }
}
{ <Another Different ID here> -- Third block
    <more of the same>
}
}
```

Just as with `blocks.lua`, Reassembly understands where one thing starts and ends using curly brackets in a `shapes.lua`.

Shape IDs are not relocated on the Steam Workshop, so to avoid shape ID conflicts have them somewhere in the range: 10000000 <= shape ID <= 4294967295. You should have the last three digits of your first shape ID be `000` so that you can easily add new shapes with incrementing IDs. For example, the first ID you could have could be `12345000`, then `12345001`, and so on.

Shape scales are defined with two lists:
1. `verts`: contains the vertices of a shape in clockwise order. Each vertex is one `{X,Y}` pair.
2. `ports`: contains the ports (i.e.: the connecting points) of the sides. Each port is defined with `{<side index>,<port position>, <port type (optional)>}`:

    1. Side index, starting from zero.
    2. Position along the side, between 0.0 and 1.0. (Clockwise, from one vertex to the next).
    3. Port type (optional).

Below is how a `shapes.lua` containing a square, a 1:2 right triangle, and a mirrored 1:2 right triangle would look:

```lua
{
{ 271390000 { -- Square
    {
        -- A normal 1x1 square is actually 10x10 units.
        verts={ {-5,-5} {-5,5} {5,5} {5,-5} }
        ports={ {0,1/2} {1,1/2} {2,1/2} {3,1/2} }
    }
} }
{ 271390001 { -- 1x2rightTriL
    {
        verts={ {-10,-5} {-10,5} {10,-5} }
        -- Only go up to three decimal places for vertices and port positions.
        -- 22.361 is the side length of the hypotenuse (irrational side).
        ports={ {0,1/2} {{1,6.181/22.361} 1,16.181/22.361} {2,1/4} {2,3/4} }
    }
} }
{ 271390002 {} mirror_of=271390001 } -- 1x2rightTriR
}
```

And here is a `blocks.lua` that would match the example above:

```lua
{
{ 17000
    name="Square"
    group=98
    shape=271390000
}
{ 17001 extends=17001 scale=2 }
{ 17002 extends=17001 shape=271390001 name="1x2rightTriL" }
{ 17003 extends=17001 shape=271390002 name="1x2rightTriR" }
}
```
