# Transparency in Shrouds
Because `fillColor`, `fillColor1`, and `lineColor` can have transparency with an alpha value less than `FF` (for example: `fillColor1=7FFFFFFF`, a 50% transparent white), shrouds can contain transparency. This chapter contains facts about transparency in shrouds.

Below is a basic example of a shroud with transparency:
```lua
{ 17142
	group=98 features=PALETTE
	fillColor =0xAA5555AA
	fillColor1=0xAAFF33AA
	lineColor =0xFFFFFFFF
	shroud={
		{ tri_color_id=0 tri_color1_id=0 line_color_id=2 shape=SQUARE size={15.0,2.0} offset={-5.0, 5.0,0.01} }
		{ tri_color_id=1 tri_color1_id=1 line_color_id=2 shape=SQUARE size={15.0,2.0} offset={-5.0, -5.0,0.01} }
} }
```
<video width="auto" height="200" controls>
  <source src="diagrams/shroud_transparency_in_shrouds.mp4" type="video/mp4">
  Your browser does not support the video tag.
</video>

## When `lineColor` is Transparent
When `lineColor` is transparent, lines will still be rendered with full opacity, but if a shroud's fill color (`tri_color_id` or `tri_color1_id`) uses the transparent line color, it will take on the transparency. Likewise, if a shroud's `line_color_id` uses a transparent fill color, it will be rendered opaque.

An example of the same color ID being rendered opaque as a line color and transparent as a fill color:
```lua
-- Shape 271390000 is a circle.
{ 17000
	features=INVISIBLE
	fillColor =0x20FF0000
	fillColor1=0x2000FF00
	lineColor =0x200000FF
	shroud={
		{ tri_color_id=0 tri_color1_id=0 line_color_id=0 shape=271390000 size={10.0,10.0} offset={2.5, 15.0,0.01} }
		{ tri_color_id=1 tri_color1_id=1 line_color_id=1 shape=271390000 size={10.0,10.0} offset={2.5,  0.0,0.01} }
		{ tri_color_id=2 tri_color1_id=2 line_color_id=2 shape=271390000 size={10.0,10.0} offset={2.5,-15.0,0.01} }
} }
```
<video width="auto" height="200" controls>
  <source src="diagrams/shrouds_line_transparency.mp4" type="video/mp4">
  Your browser does not support the video tag.
</video>

## Overlaying Transparent Shrouds
Overlaying transparent shrouds is best explained in the context of [getting more that three colors](./getting_more_than_three_colors.md#overlaying-transparent-shrouds).