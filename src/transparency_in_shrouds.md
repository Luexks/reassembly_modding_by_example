# Transparency in Shrouds
Because `fillColor`, `fillColor1`, and `lineColor` can have transparency with an alpha value less than `FF` (for example: `fillColor1=AAFFFFFF`, a partially transparent white), shrouds can contain transparency. This chapter contains facts about transparency in shrouds.
## When `lineColor` is Transparent
When `lineColor` is transparent, lines will still be rendered with full opacity, but if a shroud's fill color (`tri_color_id` or `tri_color1_id`) uses the transparent line color, it will take on the transparency. Likewise, if a shroud's `line_color_id` uses a transparent fill color, it will be rendered opaque.
## Overlaying Transparent Shrouds
When transparent shrouds are overlayed, only the lines of the topmost shroud are rendered, but the fill colors of all the shrouds are merged.