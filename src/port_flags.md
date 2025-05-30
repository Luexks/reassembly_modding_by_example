# Port Flags

For normal ports, do not have to define their port types as they are automatically set to `DEFAULT`.

Here are the different port flags:
 - `THRUSTER_OUT`: where thrust will be generated from. Must be on a side facing left, the back of the shape. Colored yellow.
 - `THRUSTER_IN`: where thrusters connect to other thrusters and to normal blocks. Colored blue.
 - `WEAPON_OUT`: where [`cannons`](./cannons.md) and [lasers](./lasers.md) fire from. Connects to `WEAPON_IN`. Colored yellow.
 - `WEAPON_IN`: connects to `WEAPON_OUT` to add cannon boost modifiers (does not work for lasers). Colored blue.
 - `LAUNCHER`: port of a [`LAUNCHER`](./launchers.md) block that launchables will generate from. Colored yellow.
 - `MISSILE`: port of a launchable (a [`replicateBlock`](./launchers.html?highlight=replicateBlock#launchers)) that will attach to one of its launcher's `LAUNCHER` ports. Colored blue.
 - `ROOT`: port of a [`ROOT`](./roots.md) or [`SEED`](./seeds.md) block used by plants and buildings to attach to [`ENVIRONMENT`](./environmental_blocks.md) blocks. Colored yellow.
 - `NONE`: no port on this side, ensures that it always draws a line. Define as `{<side index>,0,NONE}`.
 - `NORMAL`: same as defining the port with no port type.

If a side has no defined ports then it will render no line.