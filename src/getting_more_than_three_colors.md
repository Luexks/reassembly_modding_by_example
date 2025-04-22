# Getting More Than Three Colors
As shrouds are limited to using the three colors of their block (`fillColor`, `fillColor1`, and `lineColor`), they can usually only have three colors, but there are ways to get around the limitations.
## Overlaying Transparent Shrouds
When transparent shrouds are overlayed, only the lines of the topmost shroud are rendered unless the shrouds have the same Z level, but the fill colors of all the shrouds are merged, which can be used to create more than three colors.

Below is an example of a shroud with 3 circles layered bottom up in the orders red, blue, and green, all with 50% transparency:
```lua
-- Shape 271390000 is a circle.
{ 17000
	features=INVISIBLE
	fillColor =0x7FFF0000
	fillColor1=0x7F00FF00
	lineColor =0x7F0000FF
	shroud={
		{ tri_color_id=0 tri_color1_id=0 line_color_id=0 shape=271390000 size={10.0,10.0} offset={2.500, 2.500,0.01} }
		{ tri_color_id=1 tri_color1_id=1 line_color_id=1 shape=271390000 size={10.0,10.0} offset={4.665,-1.250,0.01} }
		{ tri_color_id=2 tri_color1_id=2 line_color_id=2 shape=271390000 size={10.0,10.0} offset={0.335,-1.250,0.01} }
} }
```

![Transparency With All 50%](./diagrams/shroud_transparency_50.png)

Even though all the colors in the above example have the same 50% transparency, they do not blend equally.

This is because the shrouds are rendered in order from red, green, to blue (even if they all have the same Z level). So for the center, the red first mixes with the black background, then that is mixed with the green, then that is mixed with the blue.

If you wanted a grey center, you need to make the final ratios of the colors red, green, and blue all equal.

The alpha values in order of the colors in order of rendering are:
1. Red:     100%
2. Green:    50%
3. Blue:     33%
```lua
{ 17000
	features=INVISIBLE
	fillColor =0xFFFF0000
	fillColor1=0x7F00FF00
	lineColor =0x550000FF
	shroud={
		{ tri_color_id=0 tri_color1_id=0 line_color_id=0 shape=271390000 size={10.0,10.0} offset={2.500, 2.500,0.01} }
		{ tri_color_id=1 tri_color1_id=1 line_color_id=1 shape=271390000 size={10.0,10.0} offset={4.665,-1.250,0.01} }
		{ tri_color_id=2 tri_color1_id=2 line_color_id=2 shape=271390000 size={10.0,10.0} offset={0.335,-1.250,0.01} }
} }
```
![Transparency With Central Gr*y](./diagrams/shroud_transparency_gr,y.png)

Merging their colors is of course limited, but it is useful for creating gradients with a transparent shroud on top to get rid of the lines:
```lua
{ 17000
	scale=4
	fillColor =0xFFFFFFFF
	fillColor1=0xFFFFFFFF
	lineColor =0x11000000
	shroud={
		{ tri_color_id=2 tri_color1_id=2 line_color_id=1 shape=SQUARE size={2* 1,20} offset={-10,0,0.01} }
		{ tri_color_id=2 tri_color1_id=2 line_color_id=1 shape=SQUARE size={2* 2,20} offset={-10,0,0.01} }
		{ tri_color_id=2 tri_color1_id=2 line_color_id=1 shape=SQUARE size={2* 3,20} offset={-10,0,0.01} }
		{ tri_color_id=2 tri_color1_id=2 line_color_id=1 shape=SQUARE size={2* 4,20} offset={-10,0,0.01} }
		{ tri_color_id=2 tri_color1_id=2 line_color_id=1 shape=SQUARE size={2* 5,20} offset={-10,0,0.01} }
		{ tri_color_id=2 tri_color1_id=2 line_color_id=1 shape=SQUARE size={2* 6,20} offset={-10,0,0.01} }
		{ tri_color_id=2 tri_color1_id=2 line_color_id=1 shape=SQUARE size={2* 7,20} offset={-10,0,0.01} }
		{ tri_color_id=2 tri_color1_id=2 line_color_id=1 shape=SQUARE size={2* 8,20} offset={-10,0,0.01} }
		{ tri_color_id=2 tri_color1_id=2 line_color_id=1 shape=SQUARE size={2* 9,20} offset={-10,0,0.01} }
		{ tri_color_id=2 tri_color1_id=2 line_color_id=1 shape=SQUARE size={2*10,20} offset={-10,0,0.01} }
		{ tri_color_id=2 tri_color1_id=2 line_color_id=1 shape=SQUARE size={2*11,20} offset={-10,0,0.01} }
		{ tri_color_id=2 tri_color1_id=2 line_color_id=1 shape=SQUARE size={2*12,20} offset={-10,0,0.01} }
		{ tri_color_id=2 tri_color1_id=2 line_color_id=1 shape=SQUARE size={2*13,20} offset={-10,0,0.01} }
		{ tri_color_id=2 tri_color1_id=2 line_color_id=1 shape=SQUARE size={2*14,20} offset={-10,0,0.01} }
		{ tri_color_id=2 tri_color1_id=2 line_color_id=1 shape=SQUARE size={2*15,20} offset={-10,0,0.01} }
		{ tri_color_id=2 tri_color1_id=2 line_color_id=1 shape=SQUARE size={2*16,20} offset={-10,0,0.01} }
		{ tri_color_id=2 tri_color1_id=2 line_color_id=1 shape=SQUARE size={2*17,20} offset={-10,0,0.01} }
		{ tri_color_id=2 tri_color1_id=2 line_color_id=1 shape=SQUARE size={2*18,20} offset={-10,0,0.01} }
		{ tri_color_id=2 tri_color1_id=2 line_color_id=1 shape=SQUARE size={2*19,20} offset={-10,0,0.01} }
		{ tri_color_id=2 tri_color1_id=2 line_color_id=1 shape=SQUARE size={2*20,20} offset={-10,0,0.01} }
		
		{ tri_color_id=2 tri_color1_id=2 line_color_id=1 shape=SQUARE size={2*20,20} offset={-10,0,0.03} }
} }
```
![Shroud Gradient Opaque](./diagrams/shroud_gradient_opaque.png)

They can also fade into the background:
```lua
{ 17000
	features=INVISIBLE
	scale=4
	fillColor =0xFFFFFFFF
	fillColor1=0xFFFFFFFF
	lineColor =0x050000FF
	shroud={
		{ tri_color_id=2 tri_color1_id=2 line_color_id=1 shape=SQUARE size={2* 1,20} offset={-10,0,0.01} }
		{ tri_color_id=2 tri_color1_id=2 line_color_id=1 shape=SQUARE size={2* 2,20} offset={-10,0,0.01} }
		{ tri_color_id=2 tri_color1_id=2 line_color_id=1 shape=SQUARE size={2* 3,20} offset={-10,0,0.01} }
		{ tri_color_id=2 tri_color1_id=2 line_color_id=1 shape=SQUARE size={2* 4,20} offset={-10,0,0.01} }
		{ tri_color_id=2 tri_color1_id=2 line_color_id=1 shape=SQUARE size={2* 5,20} offset={-10,0,0.01} }
		{ tri_color_id=2 tri_color1_id=2 line_color_id=1 shape=SQUARE size={2* 6,20} offset={-10,0,0.01} }
		{ tri_color_id=2 tri_color1_id=2 line_color_id=1 shape=SQUARE size={2* 7,20} offset={-10,0,0.01} }
		{ tri_color_id=2 tri_color1_id=2 line_color_id=1 shape=SQUARE size={2* 8,20} offset={-10,0,0.01} }
		{ tri_color_id=2 tri_color1_id=2 line_color_id=1 shape=SQUARE size={2* 9,20} offset={-10,0,0.01} }
		{ tri_color_id=2 tri_color1_id=2 line_color_id=1 shape=SQUARE size={2*10,20} offset={-10,0,0.01} }
		{ tri_color_id=2 tri_color1_id=2 line_color_id=1 shape=SQUARE size={2*11,20} offset={-10,0,0.01} }
		{ tri_color_id=2 tri_color1_id=2 line_color_id=1 shape=SQUARE size={2*12,20} offset={-10,0,0.01} }
		{ tri_color_id=2 tri_color1_id=2 line_color_id=1 shape=SQUARE size={2*13,20} offset={-10,0,0.01} }
		{ tri_color_id=2 tri_color1_id=2 line_color_id=1 shape=SQUARE size={2*14,20} offset={-10,0,0.01} }
		{ tri_color_id=2 tri_color1_id=2 line_color_id=1 shape=SQUARE size={2*15,20} offset={-10,0,0.01} }
		{ tri_color_id=2 tri_color1_id=2 line_color_id=1 shape=SQUARE size={2*16,20} offset={-10,0,0.01} }
		{ tri_color_id=2 tri_color1_id=2 line_color_id=1 shape=SQUARE size={2*17,20} offset={-10,0,0.01} }
		{ tri_color_id=2 tri_color1_id=2 line_color_id=1 shape=SQUARE size={2*18,20} offset={-10,0,0.01} }
		{ tri_color_id=2 tri_color1_id=2 line_color_id=1 shape=SQUARE size={2*19,20} offset={-10,0,0.01} }
		{ tri_color_id=2 tri_color1_id=2 line_color_id=1 shape=SQUARE size={2*20,20} offset={-10,0,0.01} }
		
		{ tri_color_id=2 tri_color1_id=2 line_color_id=1 shape=SQUARE size={2*20,20} offset={-10,0,0.03} }
} }
```
![Shroud Gradient Transparent](./diagrams/shroud_gradient_transparent.png)

Sadly, there is no way to truly avoid rendering lines, as, when hiding lines, there must always be some higher-layered transparent shroud with its own rendered lines.
## Never Firing Non-Turreted Launcher
A non-turreted [never firing launcher](./always_and_never_firing_weapons.html?highlight=LAUNCHER|NEVERFIRE), can hold a launchable that can have its own three colors and its own shroud.

The following example has 6 different colors (blending together to make two grays) using a small custom launcher and launchable shape:
```lua
{ 17000
	features=COMMAND|GENERATOR|INVISIBLE|LAUNCHER|NEVERFIRE|NOICON
	shape=271390004
	fillColor =0xFFFF0000
	fillColor1=0x7F00FF00
	lineColor =0x550000FF
	aihint_range=0
    launcherPower=inf
	shroud={
		{ tri_color_id=0 tri_color1_id=0 line_color_id=0 shape=271390002 size={10.0,10.0} offset={2.500, 2.500,0.02} }
		{ tri_color_id=1 tri_color1_id=1 line_color_id=1 shape=271390002 size={10.0,10.0} offset={4.665,-1.250,0.02} }
		{ tri_color_id=2 tri_color1_id=2 line_color_id=2 shape=271390002 size={10.0,10.0} offset={0.335,-1.250,0.02} }
	}
	replicateBlock={
		shape=271390005
		fillColor =0xFF00FFFF
		fillColor1=0x7FFF00FF
		lineColor =0x55FFFF00
		shroud={
			{ tri_color_id=0 tri_color1_id=0 line_color_id=0 shape=271390002 size={10.0,10.0} offset={22.500, 2.500,0.02} }
			{ tri_color_id=1 tri_color1_id=1 line_color_id=1 shape=271390002 size={10.0,10.0} offset={24.665,-1.250,0.02} }
			{ tri_color_id=2 tri_color1_id=2 line_color_id=2 shape=271390002 size={10.0,10.0} offset={20.335,-1.250,0.02} }
		}
	}
}
```
![Non-Turreted Never Firing Launcher Shroud](./diagrams/shroud_non-turreted_never_firing_launcher.png)