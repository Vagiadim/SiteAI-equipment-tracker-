# SiteAI Equipment Tracker

**YOLOv8 construction equipment detection for automated site monitoring**

MAICEN M4U3 Assignment — Team 7

[![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/Vagiadim/SiteAI-equipment-tracker-/blob/main/notebooks/M4U3_Assignment_Team_7_object_detection.ipynb)

---

## Problem Statement

Construction sites require continuous monitoring of heavy equipment for safety, logistics, and progress tracking. Manual monitoring is time-consuming and error-prone. This project uses **YOLOv8** object detection to automatically identify and locate construction equipment in site images, providing a proof-of-concept for automated site monitoring.

**Success criteria:** Achieve mAP@50 > 50% across all classes with a fully cloud-reproducible pipeline.

---

## Dataset

- **Source:** Roboflow (SiteAI-equipment-tracker, Team 7)
- **Format:** YOLOv8 (exported from Roboflow)
- **Split:** 80/20 (train/val)
- **Image size:** 512×512
- **Download:** Automatically downloaded from [GitHub Release v1.0](https://github.com/Vagiadim/SiteAI-equipment-tracker-/releases/tag/v1.0)

### Classes (7)

| Class | Description |
|-------|------------|
| boom_lift | Aerial work platform with articulating or telescoping boom |
| dump_truck | Truck with open-box bed for transporting loose material |
| excavator | Tracked machine with bucket arm for digging |
| loader | Wheeled machine with front-mounted bucket |
| mixer_truck | Truck with rotating drum for transporting concrete |
| roller | Compaction machine for flattening surfaces |
| tower_crane | Fixed crane with horizontal jib mounted on tall mast |

---

## Results

Results from training YOLOv8n for 50 epochs at 512×512 resolution on a Tesla T4 GPU.

### Overall Metrics

| Metric | Value |
|--------|-------|
| Precision | _UPDATE AFTER RUN_ |
| Recall | _UPDATE AFTER RUN_ |
| mAP@50 | _UPDATE AFTER RUN_ |
| mAP@50-95 | _UPDATE AFTER RUN_ |

### Per-Class Performance (mAP@50)

| Class | mAP@50 | Status |
|-------|--------|--------|
| boom_lift | _UPDATE_ | |
| dump_truck | _UPDATE_ | |
| excavator | _UPDATE_ | |
| loader | _UPDATE_ | |
| mixer_truck | _UPDATE_ | |
| roller | _UPDATE_ | |
| tower_crane | _UPDATE_ | |

### Key Takeaways

- Best performing classes: _UPDATE AFTER RUN_
- Weakest classes: _UPDATE AFTER RUN_
- The model serves as a viable proof-of-concept for automated construction equipment detection
- Weak classes can be improved with more training data and better annotation coverage

---

## How to Reproduce

> **One-click reproduction:** Click the Colab badge above, select T4 GPU, and hit Run All. No manual uploads needed.

### Step-by-step:

1. Click the **Open in Colab** badge above (or open the notebook from `notebooks/`)
2. Go to **Runtime → Change runtime type → T4 GPU**
3. Click **Runtime → Run all**
4. The notebook will automatically:
   - Install dependencies
   - Download the dataset from GitHub Release v1.0
   - Extract and configure dataset paths
   - Remove Roboflow metadata for independence
   - Train YOLOv8n for 50 epochs (512×512)
   - Evaluate and display metrics + training curves
   - Show a visual performance dashboard
   - Run predictions on 10 validation images
   - Display a 6×6 evidence grid with class coverage
   - Download and run predictions on 5 new unseen images from GitHub
   - Print a reproducibility summary
5. Total runtime: ~30–50 minutes on T4 GPU

---

## Reproducibility Checklist

| Parameter | Value |
|-----------|-------|
| Model | YOLOv8n (Nano) |
| Framework | Ultralytics |
| Epochs | 50 |
| Image size | 512 |
| Batch size | auto |
| Early stopping | patience=15 |
| Cache | RAM |
| GPU | Tesla T4 (Google Colab) |
| Dataset | GitHub Release v1.0 (auto-download) |
| New test images | GitHub repo (auto-download) |
| Manual uploads | None (fully cloud-based) |

---

## Repository Structure

```
SiteAI-equipment-tracker-/
├── README.md
├── LICENSE (MIT)
├── notebooks/
│   └── M4U3_Assignment_Team_7_object_detection.ipynb
├── docs/
│   ├── error_analysis.md
│   ├── governance_checklist.md
│   └── class_definitions.md
├── results/
│   ├── curves/
│   └── evidence/
│       ├── annotations/
│       ├── val_preds/
│       ├── new_preds/
│       └── new_test_images/
└── deliverables/
    ├── slides.pdf
    └── mini_report.pdf
```

---

## Notebook Structure

| Cell | What It Does |
|------|-------------|
| 1 | Environment setup — installs Ultralytics, checks GPU |
| 2 | Downloads dataset.zip from GitHub Release v1.0 |
| 3 | Unzips dataset and inspects folder structure |
| 4 | Locates and displays data.yaml configuration |
| 5 | Fixes dataset paths for Colab (auto-detects valid/val) |
| 6 | Removes Roboflow metadata for platform independence |
| 7 | Trains YOLOv8n — 50 epochs, 512px, auto batch, patience=15 |
| 8 | Evaluates model — regenerates validation plots |
| 9 | Lists training output files |
| 9.a | Displays training visualizations (styled dark theme) |
| 9.b | Visual metrics dashboard (bar chart) |
| 10 | Saves best weights for download |
| 10.a | Downloads 5 new test images from GitHub (no manual upload) |
| 11 | Runs predictions on new test images and displays results |
| 11.a | 6×6 evidence grid with class coverage |
| 12 | Prints reproducibility summary |

---

## Trained Weights

Download from [GitHub Release v1.0](https://github.com/Vagiadim/SiteAI-equipment-tracker-/releases/tag/v1.0):
- `dataset.zip` — Full dataset (YOLOv8 format)
- `best.pt` — Trained model weights

---

## Documentation

- [`docs/error_analysis.md`](docs/error_analysis.md) — False positives, false negatives, and data improvement plan
- [`docs/governance_checklist.md`](docs/governance_checklist.md) — Privacy, limitations, and risk assessment
- [`docs/class_definitions.md`](docs/class_definitions.md) — Label rules for all 7 classes

---

## Deliverables

- [`deliverables/slides.pdf`](deliverables/slides.pdf) — Presentation slides (6–8 slides)
- [`deliverables/mini_report.pdf`](deliverables/mini_report.pdf) — 2-page summary report

---

## License

This project is licensed under the [MIT License](LICENSE).

---

## Team

**Team 7** — MAICEN Module 4, Unit 3  
Zigurat Institute of Technology
