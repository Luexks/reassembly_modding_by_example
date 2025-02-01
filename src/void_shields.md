# Void Shields
Void shields are an unintended varient of standard shields that have negative `strength` and `regen`, which are both conventionally set to -1.

Here is a list of what they do:
 - Constantly radiates the shield death particle effect.
 - When hit by explosive weaponry they take 0 damage but blocks in the explosion radius still take damage.
 - When hit by non-explosive weaponry, the void shield block's health itself is used as the shield health.
 - Does not work if the block or ship it is mounted on has no block with COMMAND
 - The `armor` field doesn't function.
 - May have other yet undiscovered effects.
```lua
{17000
    features=SHIELD
    shield={
        -- These fields are necessary.
        strength=-1
        regen=-1

        -- These can be anything.
        radius=100
        delay=3
    }
}
```
<video width="640" height="360" controls>
  <source src="diagrams/void_shield_video.mp4" type="video/mp4">
  Your browser does not support the video tag.
</video>