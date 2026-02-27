# Error Analysis (Failure Modes) + Iteration Plan

## Model Performance & Error Analysis
**Project:** SiteAI Equipment Tracker (Team 7)
**Status:** Post-Training Evaluation (50 Epochs)

## 1. Evidence Source
The following analysis is based on the automated outputs generated in the `/results/` directory of this repository:
* **Metrics:** `Results.png`
* **Confusion Matrix:** `Confusion_matrix.png`
* **Visual Validation:** `val_batch0_pred.jpg` and `val_batch1_pred.jpg`

---

## 2. False Positives (FP) — Incorrect Predictions
*A False Positive occurs when the model identifies an object as equipment incorrectly.*

### FP #1 (Reference: val_batch0_pred.jpg)
* **What happened:** The model identified a stationary safety barrier as a **loader**.
* **Likely reason (hypothesis):** **Color Bias.** The training data contains a high frequency of "Construction Yellow" machinery. The model has developed a feature-weighting bias where large yellow rectangular objects are frequently misclassified as loaders regardless of their mechanical silhouette.

### FP #2 (Reference: val_batch1_pred.jpg)
* **What happened:** Structural scaffolding was identified as a **tower_crane**.
* **Likely reason (hypothesis):** **Texture Confusion.** Both scaffolding and tower cranes consist of high-contrast, metallic lattice structures. The YOLOv8n (Nano) architecture lacks the depth to distinguish between the specific geometry of a crane jib versus temporary site scaffolding in cluttered backgrounds.

---

## 3. False Negatives (FN) — Missed Detections
*A False Negative occurs when equipment is present on-site but the model fails to detect it.*

### FN #1 (Reference: val_batch0_labels.jpg vs val_batch0_pred.jpg)
* **What happened:** A **forklift** in the background was not detected.
* **Likely reason (hypothesis):** **Spatial Resolution Constraints.** With an input size of 512px, small-scale assets like forklifts occupy too few pixels for the model's final stride to extract meaningful features. This is a known limitation for distant monitoring in large-scale site surveillance.

### FN #2 (Reference: val_batch2_pred.jpg)
* **What happened:** An **excavator** was missed because it was partially behind a concrete column.
* **Likely reason (hypothesis):** **Occlusion Sensitivity.** The model struggles when the primary identifying feature (the articulating arm) is obscured. The current dataset lacks sufficient "occluded" examples to teach the model to infer the presence of a machine from partial visibility.

---

## 4. Prioritized Next Improvements (Data-Driven)

1. **Hard Negative Mining:** Add 100+ images of site "noise" (scaffolding, barriers, and fencing) without labels. This forces the model to learn what is *not* a machine, reducing False Positives.
2. **Class-Specific Upsampling:** Increase the number of instances for **backhoes** and **forklifts**. These classes are currently underrepresented compared to excavators, leading to lower recall.
3. **Multi-Scale Training:** Use "Multi-scale" flags in the next training run to help the model better identify machinery that appears at significantly different distances from the camera.


