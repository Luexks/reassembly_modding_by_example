# Shrouding
A shroud is a purely decorative part of a block defined using the `shroud` field.

When a weapon with the [`TURRET`](./turreted_weapons.md) or [`ROTATOR`](./rotator_thrusters.md) is shrouded, the shroud takes on the rotation of the turret or rotator.
```lua
{ 17000
    fillColor=0xFF555555
    fillColor1=0xFFAAAAAA
    lineColor=0xFFFFFFFF
    shroud={
        {
            shape=SQUARE            -- Note that scales cannot be used.

            size={10.0,5.0}         -- Size values can be negative for mirroring.
                                    -- (Square shrouds' Y sizes are doubled)

            offset={2.5,0,0.01}     -- X and Y offset is relative to icon center *.
                                    -- Z is 3D draw order. Increment by 0.02.
                                    -- Higher Z shrouds are drawn on top.
                                    -- Equal Z shrouds intersect their lines.
                                    -- 0 Z sets Z by order of shroud shapes in the list.

            taper=0.5               -- Only for shrouds with shape=SQUARE.
                                    -- Multiplies width of the square's front.

            angle=90*pi/180         -- Angle in radians. (add '*pi/180' for degrees)
                                    -- If the shroud's size is a multiple of the
                                    -- shape's bounding box (for a scale 1 square
                                    -- this could be size={10.0*2,10.0*2}), the shroud
                                    -- is scaled and then rotated,

                                    -- but if not, the size is applied after
                                    -- rotation, so for shrouds that need precisely
                                    -- angled blocks, it may be worth making custom
                                    -- shapes that are angled to use for shrouding.

            -- Shroud colors are assigned by the colors of the block.
            -- 0: fillColor.
            -- 1: fillColor1.
            -- 2: lineColor.
            tri_color_id= 0         -- fillColor of the shroud.
            tri_color1_id=1         -- fillColor1 of the shroud.
            line_color_id=2         -- lineColor of the shroud.

            count=1                 -- Usually undefined.
                                    -- Works in the same way as barrelCount.
        }
        -- The other shrouds are defined using the compact format:
        { shape=OCTAGON size={10.0,10.0} offset={ 2.5, 0.0,0.02}               tri_color_id=2 tri_color1_id=2 line_color_id=0 }
        { shape=OCTAGON size={15.0,10.0} offset={-2.5, 0.0,0.02}               tri_color_id=0 tri_color1_id=0 line_color_id=1 }
        { shape=1239879 size={ 5.0, 5.0} offset={ 0.0,-5.0,0.03} angle=pi*-0.5 tri_color_id=2 tri_color1_id=2 line_color_id=0 }
    }
}
```

\* [Icon Center](./centering_shrouds_on_non-turreted_blocks.md#icon-center)