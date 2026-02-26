# Strategic Analysis: Model Limitations & Future Deployment
**Sector:** AECO (Architecture, Engineering, Construction, and Operations)

---

### 1. Technical & Environmental Limitations
While the current YOLOv8n model provides a strong baseline for equipment tracking, several environmental factors on active construction sites impact real-world performance:

* **Dynamic Occlusion:** On high-density sites, equipment is frequently obscured by structural elements (scaffolding, formwork) or other machinery, leading to intermittent tracking gaps.
* **Lighting & Atmospheric Conditions:** The current training dataset is optimized for clear daylight. Performance may degrade during night shifts, heavy dust storms (common in GCC regions), or low-visibility weather.
* **Scale Inconsistency:** Detection confidence for smaller assets (e.g., Forklifts) is lower when captured from high-altitude mounting points, such as tower crane cabins, compared to ground-level CCTV.
* **Visual Mimicry:** The model occasionally struggles with "Dump Trucks" vs. general logistics vehicles due to high visual similarity in chassis design.

**This called for a comparison between models on YOLOv8n and YOLOv8s, as well as a training run on Roboflow, resulting in the following:**
### Model Comparison — Overall Metrics

| Metric | YOLOv8n (Nano) | YOLOv8s (Small) | Improvement |
|--------|---------------|----------------|-------------|
| Precision | 0.712 | 0.752 | +5.6% |
| Recall | 0.565 | 0.635 | +12.4% |
| mAP@50 | 0.637 | 0.679 | +6.6% |
| mAP@50-95 | 0.465 | 0.500 | +7.5% |
| Parameters | 3.0M | 11.1M | 3.7× |
| GFLOPs | 8.1 | 28.5 | 3.5× |
| Training time | 0.123 hrs (~7 min) | 0.217 hrs (~13 min) | 1.8× |
| Weights size | 6.2 MB | 22.5 MB | 3.6× |

### Per-Class Comparison (mAP@50)

| Class | YOLOv8n | YOLOv8s | Change | Status |
|-------|---------|---------|--------|--------|
| mixer_truck | 0.883 | 0.935 | +5.2% | ✅ Excellent |
| roller | 0.879 | 0.875 | -0.4% | ✅ Excellent |
| loader | 0.828 | 0.898 | +7.0% | ✅ Excellent |
| excavator | 0.766 | 0.754 | -1.2% | ✅ Good |
| dump_truck | 0.422 | 0.451 | +2.9% | ⚠️ Weak |
| tower_crane | 0.394 | 0.404 | +1.0% | ⚠️ Weak |
| boom_lift | 0.286 | 0.440 | +15.4% | ⚠️ Weak |

#### *Key Takeaway: Confirmation that the dataset quality is sufficient for high-accuracy detection.*
#### *The gap between our YOLOv8s results (67.9% mAP@50) and RF-DETR (89.2%) suggests that a larger model architecture and/or more advanced training techniques could significantly improve performance.*
---

### 2. Future Work & Scalability
To transition this proof-of-concept into a site-wide management tool, the following developments are proposed:

* **BIM Integration:** Connecting AI detection logs to Building Information Modeling (BIM) schedules to automatically compare actual equipment presence against the planned logistics phase.
* **Temporal Tracking:** Implementing DeepSORT or ByteTrack algorithms to assign unique IDs to machines, allowing for "Engine-on" time analysis and idle-time reduction.
* **Synthetic Data Augmentation:** Utilizing digital twins to generate "edge-case" training images (e.g., equipment accidents or near-misses) to improve safety monitoring without real-world risk.
* **Edge Deployment:** Optimizing the model for NVIDIA Jetson or similar edge devices to allow for local, real-time processing without relying on high-latency cloud uploads.

---
*This document serves as a roadmap for scaling the SiteAI Tracker from an academic exercise to a viable site supervision utility.*
