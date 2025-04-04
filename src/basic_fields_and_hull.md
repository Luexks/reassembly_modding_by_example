# Basic Fields and Hull

Below are some basic fields that should be defined for every block, using hull as a example:
```lua
{ 17000		 -- This is the block's ID that the game uses to keep track of things.
        	 -- Keep them within the range 17000-26000.

	group=98 -- The command `palette 98` will spawn this block.
	sort=1 	 -- Orders blocks in the campaign's databank.


	-- A block's color alternates between fillColor and fillColor1.

	-- All 3 color fields can be either 0xRRGGBB, for red green blue,
	-- or 0xAARRGGBB, for alpha (the less the alpha, the greater the transparency),
	-- then red, green, blue.
	fillColor=0x5555AA
	fillColor1=0x3333AA
	-- Note that lines do not render transparency even when defined with 0xAARRGGBB.
	lineColor=0xFFFFFF


	-- Base game shapes are text, custom shapes are whole numbers.
	shape=SQUARE
	-- Scales count up from 1.
	scale=1


	name="Hull"
	blurb="1x1\nBasic structure"

	-- Block health is calculated per block based on its durability and area,
	durability=1.00001
	-- Don't set durability to 1 if you want to use block extensions as
	-- block health will not be recalculated for each block.


	-- Block mass is calculated per block based on its density and area,
	density=0.1

	-- The greater the grow rate, the faster the block grows.
	growRate=20


	-- Give every block the PALETTE feature if you want it to show up in the campaign.
	features=PALETTE
}
{ 17001 extends=17000 scale=2 blurb="2x2\nBasic structure" }
```