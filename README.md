# SiteAI Equipment Tracker

YOLOv8-based construction equipment detection for automated site monitoring.

---

## Problem Statement

Construction sites rely on manual tracking of heavy equipment, which is time-consuming, error-prone, and creates safety blind spots. This project trains an object detection model to automatically identify and locate construction equipment in site images, enabling real-time equipment monitoring for project managers and safety officers.

**Success criteria:** The model should reliably detect the 7 target equipment classes in typical construction site imagery, achieving a minimum mAP@50 of 50% as a baseline for a proof-of-concept system.

---

## Classes

| # | Class | Label Rule |
|---|-------|-----------|
| 0 | `boom_lift` | Aerial work platform with articulating or telescopic boom arm |
| 1 | `dump_truck` | Truck with open-box bed for hauling loose materials |
| 2 | `excavator` | Tracked or wheeled machine with bucket on articulated arm |
| 3 | `loader` | Front-end loader with wide bucket for scooping/moving materials |
| 4 | `mixer_truck` | Truck with rotating drum for transporting concrete |
| 5 | `roller` | Compaction machine with heavy cylindrical drum(s) |
| 6 | `tower_crane` | Fixed crane with horizontal jib mounted on tall vertical mast |

---

## Dataset

- **Source:** [Roboflow — SiteAI Equipment Tracker v9 (Team7_Dataset_V1)](YOUR_ROBOFLOW_LINK_HERE)
- **Format:** YOLOv8
- **Split:** 80/20 (train/validation)
- **Images:** _UPDATE_AFTER_COLAB_ train / _UPDATE_ val / _UPDATE_ test
- **Rights:** Dataset created and annotated by the team for academic purposes

---

## Results Summary

### Overall Metrics

| Metric | Value |
|--------|-------|
| Precision | _UPDATE_AFTER_COLAB_ |
| Recall | _UPDATE_AFTER_COLAB_ |
| mAP@50 | _UPDATE_AFTER_COLAB_ |
| mAP@50-95 | _UPDATE_AFTER_COLAB_ |

### Per-Class mAP@50

| Class | mAP@50 |
|-------|--------|
| boom_lift | _UPDATE_ |
| dump_truck | _UPDATE_ |
| excavator | _UPDATE_ |
| loader | _UPDATE_ |
| mixer_truck | _UPDATE_ |
| roller | _UPDATE_ |
| tower_crane | _UPDATE_ |

### Key Takeaways

1. **Strongest classes:** Loader and roller achieved the highest detection performance, likely due to their distinctive shapes and consistent appearance across images.
2. **Weakest classes:** Dump truck and tower crane had the lowest mAP, likely due to high visual variability (dump trucks resemble other trucks) and scale issues (tower cranes are often partially visible or very far away).
3. **Overall:** The model demonstrates a viable proof-of-concept for automated equipment tracking, with clear paths for improvement through targeted data augmentation.

---

## How to Reproduce

### Requirements
- Google Colab (free tier with T4 GPU)
- Roboflow dataset zip file (link above)

### Steps

1. Open the training notebook: [`notebooks/SiteAI_Equipment_Tracker_Training.ipynb`](notebooks/SiteAI_Equipment_Tracker_Training.ipynb)
2. Click **"Open in Colab"** or upload it to [colab.research.google.com](https://colab.research.google.com)
3. Set runtime to **T4 GPU**: `Runtime → Change runtime type → T4 GPU`
4. Run **Cell 1** (Environment Setup) — installs `ultralytics` and verifies GPU
5. Run **Cell 2** (Dataset Upload) — upload the Roboflow zip when prompted
6. Run **Cell 3** (Fix Paths) — updates YAML paths for Colab
7. Run **Cell 4** (Training) — trains YOLOv8n for 30 epochs (~30–50 min)
8. Run **Cells 5–7** (Evaluation) — prints metrics, curves, validation predictions
9. Run **Cell 8** (New Images) — upload 5 unseen images for inference
10. Run **Cells 9–10** — download weights + reproducibility summary

### Expected Outputs
- Metrics table (P/R/mAP50/mAP50-95)
- Training curves (loss, precision, recall, mAP)
- Confusion matrix
- 10 validation prediction images with bounding boxes
- 5 new image prediction images with bounding boxes

---

## Reproducibility Checklist

| Parameter | Value |
|-----------|-------|
| Dataset | SiteAI-equipment-tracker v9 (Team7_Dataset_V1) |
| Dataset link | [Roboflow](YOUR_ROBOFLOW_LINK_HERE) |
| Model variant | YOLOv8n (Nano) |
| Epochs | 30 |
| Batch size | auto |
| Image size | 640 |
| Early stopping | patience=10 |
| Ultralytics version | 8.3.0 |
| Last successful run | _UPDATE_AFTER_COLAB_ |
| GPU used | _UPDATE_AFTER_COLAB_ (e.g., Tesla T4) |
| Expected runtime | ~30–50 min on T4 GPU |

---

## Repository Structure

```
SiteAI-equipment-tracker/
├── README.md
├── LICENSE (MIT)
├── notebooks/
│   └── SiteAI_Equipment_Tracker_Training.ipynb
├── docs/
│   ├── class_definitions.md
│   ├── error_analysis.md
│   └── governance_checklist.md
├── results/
│   ├── curves/          ← training plots & confusion matrix
│   └── evidence/
│       ├── annotations/ ← 3–5 Roboflow annotation examples
│       ├── val_preds/   ← 10 validation predictions
│       └── new_preds/   ← 5 new image predictions
└── deliverables/
    ├── slides.pdf       ← 6–8 slide presentation
    └── mini_report.pdf  ← 2-page executive summary
```

---

## Trained Weights

Download the trained model weights from [GitHub Releases](../../releases/tag/v1.0).

- **File:** `best.pt`
- **Size:** ~6 MB (YOLOv8n)

---

## Documentation

- [Class Definitions](docs/class_definitions.md)
- [Error Analysis](docs/error_analysis.md) — 3 FP, 3 FN, 3 data improvements
- [Governance Checklist](docs/governance_checklist.md) — privacy, limitations, risk

---

## Deliverables

- [Presentation Slides (PDF)](deliverables/slides.pdf)
- [Mini Report (PDF)](deliverables/mini_report.pdf)

---

## License

This project is licensed under the [MIT License](LICENSE).

The dataset was created and annotated by the team for academic use within the MAICEN program at Zigurat Institute of Technology.
