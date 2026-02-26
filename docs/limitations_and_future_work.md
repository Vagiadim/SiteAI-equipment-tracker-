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


*Key Takeaway: YOLOv8s outperforms YOLOv8n across most metrics, with the biggest gains in recall (+12.4%) and mAP@50-95 (+7.5%)*
---

### 2. Future Work & Scalability
To transition this proof-of-concept into a site-wide management tool, the following developments are proposed:

* **BIM Integration:** Connecting AI detection logs to Building Information Modeling (BIM) schedules to automatically compare actual equipment presence against the planned logistics phase.
* **Temporal Tracking:** Implementing DeepSORT or ByteTrack algorithms to assign unique IDs to machines, allowing for "Engine-on" time analysis and idle-time reduction.
* **Synthetic Data Augmentation:** Utilizing digital twins to generate "edge-case" training images (e.g., equipment accidents or near-misses) to improve safety monitoring without real-world risk.
* **Edge Deployment:** Optimizing the model for NVIDIA Jetson or similar edge devices to allow for local, real-time processing without relying on high-latency cloud uploads.

---
*This document serves as a roadmap for scaling the SiteAI Tracker from an academic exercise to a viable site supervision utility.*
