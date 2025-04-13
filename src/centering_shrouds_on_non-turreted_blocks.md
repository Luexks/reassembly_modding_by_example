# Centering Shrouds on Non-Turreted Blocks
This chapter discusses how one can center their shrouds' offsets with an understanding of how shroud centers are defined for non-turreted blocks.
## Icon Center
A shape's icon center is where the center of its icon is. It is defined by the average position of the shape's vertices.
## Icon Radius
A shape's icon radius is the size of its icon. It is defined by the mininum distance between the maximum distance from the icon center to any vertex and the mininum distance from the icon center to any of the sides' midpoints.
## Shroud Center
A shape's shroud center is the position of a shroud at `offset={0.0,0.0,_}`. It is defined by icon center minus half the icon radius.

Subtract the block's shape's shroud center from the offset of a shroud to center it.

For example, if you want to center the shroud in the middle of a scale 1 square, you would probably use the Python program below to figure out that the shroud center is `{-2.5,0}`. Next, you would subtract `{-2.5,0}` from your shroud's offset, `{0.0,0.0,0.01}` to get `{2.5,0.0,0.01}`.
## Example Python Code for Calculating Shroud Centers
*Abstract things, as simple as they are, must be calculated using comedically complex looking Python programs.*
```py
import math

def get_icon_center(vertices: list[(float, float)]) -> (float, float):
    avg_x = sum(vertex[0] for vertex in vertices) / len(vertices)
    avg_y = sum(vertex[1] for vertex in vertices) / len(vertices)
    icon_center = (avg_x, avg_y)
    return icon_center

def get_max_dist_icon_center_to_vertex(icon_center: (float, float), vertices: list[(float, float)]) -> float:
    max_dist_icon_center_to_vertex = 0
    for vertex in vertices:
        dist_icon_center_to_vertex = math.dist(icon_center, vertex)
        max_dist_icon_center_to_vertex = max(
            max_dist_icon_center_to_vertex,
            dist_icon_center_to_vertex
        )
    return max_dist_icon_center_to_vertex

def get_min_dist_icon_center_to_side_midpoint(icon_center: (float, float), vertices: list[(float, float)]) -> float:
    min_dist_icon_center_to_side_midpoint = float('inf')
    for vertex_index in range(len(vertices)):
        vertex = vertices[vertex_index]
        next_vertex = vertices[(vertex_index + 1) % len(vertices)]
        side_mid_point = (
            (vertex[0] + next_vertex[0]) / 2,
            (vertex[1] + next_vertex[1]) / 2
        )
        dist_icon_center_to_side_midpoint = math.dist(icon_center, side_mid_point)
        min_dist_icon_center_to_side_midpoint = min(
            min_dist_icon_center_to_side_midpoint,
            dist_icon_center_to_side_midpoint
        )
    return min_dist_icon_center_to_side_midpoint

def get_icon_radius(vertices: list[(float, float)]) -> (float, float):
    icon_center = get_icon_center(vertices)
    max_dist_icon_center_to_vertex = get_max_dist_icon_center_to_vertex(icon_center, vertices)
    min_dist_icon_center_to_side_midpoint = get_min_dist_icon_center_to_side_midpoint(icon_center, vertices)
    icon_radius = min(
        max_dist_icon_center_to_vertex,
        min_dist_icon_center_to_side_midpoint
    )
    return icon_radius

def get_shroud_center(vertices: list[(float, float)]) -> (float, float):
    icon_center = get_icon_center(vertices)
    icon_radius = get_icon_radius(vertices)
    shroud_center = (icon_center[0] - 0.5 * icon_radius, icon_center[1])
    return shroud_center

# Add you own shapes using the following as examples:
shapes = [
    [(-5, -5), (-5, 5), (5, 5), (5, -5)],   # Square
    [(0, 0), (0, 5), (5, 0)],               # Triangle
    [(-10, -10), (50, 100), (0, 0)]         # ???
]

for shape in shapes:
    print(f"{shape}\n\t{get_shroud_center(shape)}\n")
```