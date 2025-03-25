# UPS
UPS represents 'physics updates per seconds', or in other words, Reassembly's simulation step rate.

Reassembly mods should be made to function at UPS settings 60 or higher.
<video height=256 controls>
  <source src="diagrams/ups.mp4" type="video/mp4">
  Your browser does not support the video tag.
</video>

UPS should beg kept in mind when creating cannons or launchers that do a lot in a short amount of time, such as having a high `roundsPerSec`, a high `muzzleVel` with a short `range`, or constantly producing blocks with an instant `replicateTime`.

It is recommened to make UPS-affected blocks function identically across UPS settings above 60 to ensure that all players have the same experience and to avoid requiring players to switch UPS settings.