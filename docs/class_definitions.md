# Class Definitions + Label Rules

## AECO Context
This dataset supports object detection for construction equipment to improve site monitoring, logistics planning, and progress documentation.

## Classes
- boom_lift
- excavator
- mixer_truck
- roller
- tower_crane

## Label rules (what counts as a correct box)
1. Draw the bounding box tightly around the visible object silhouette (minimal background).
2. Label only when at least ~50% of the object is visible.
3. If heavily occluded (<30% visible), do not label.
4. If multiple instances exist, label each instance separately.
5. Keep class naming consistent with the Roboflow export.

## Common edge cases
- Partial view: label only if key geometry is visible (e.g., excavator arm + body).
- Long objects (boom lifts/cranes): include full visible structure even if extended.
- Overlaps: label both objects if both are clearly visible.
