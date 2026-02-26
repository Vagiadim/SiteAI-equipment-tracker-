# Class Definitions + Label Rules

## AECO Context
This dataset supports object detection for construction equipment to improve site monitoring, logistics planning, and progress documentation.

---

### Core Equipment Classes
These definitions ensure the YOLOv8 model aligns with AECO site standards.

| ID | Equipment Class | Operational Definition |
| :--- | :--- | :--- |
| 0 | **Boom Lift** | Aerial platforms for high-access architectural finishing. |
| 1 | **Dump Truck** | Heavy vehicles for hauling earthwork and debris. |
| 2 | **Excavator** | Primary machinery for foundation and trenching. |
| 3 | **Loader** | Material handling for stockpiles and site clearing. |
| 4 | **Mixer Truck** | Concrete transport and active pouring monitoring. |
| 5 | **Roller** | Soil and asphalt compaction for site preparation. |
| 6 | **Tower Crane** | Vertical lifting for structural assembly. |
| 7 | **Forklift** | Logistics and palletized material movement. |
| 8 | **Backhoe** | Dual-purpose digging and loading equipment. |

---

## Label rules (what counts as a correct box)
1. Draw the bounding box tightly around the visible object silhouette (minimal background).
2. Label only when at least ~50% of the object is visible.
3. If heavily occluded (<30% visible), do not label.
4. If multiple instances exist, label each instance separately.
5. Keep class naming consistent with the Roboflow export.
   
---  

### Implementation Notes
* **Visual Variability:** Tower cranes and dump trucks often require higher confidence thresholds.
* **Safety Compliance:** Detection of these classes supports real-time exclusion zone monitoring.



## Common edge cases
- Partial view: label only if key geometry is visible (e.g., excavator arm + body).
- Long objects (boom lifts/cranes): include full visible structure even if extended.
- Overlaps: label both objects if both are clearly visible.
