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
- **Images:** 59 validation images, 184 instances
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

Both models were trained for 50 epochs at 512×512 resolution on a Tesla T4 GPU.

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

### Key Takeaways

- **YOLOv8s outperforms YOLOv8n** across most metrics, with the biggest gains in recall (+12.4%) and mAP@50-95 (+7.5%)
- **Best performing classes:** mixer_truck (93.5%), loader (89.8%), roller (87.5%) — all above 85% mAP@50 with YOLOv8s
- **Weakest classes:** boom_lift, tower_crane, dump_truck — all below 50% mAP@50
- **Biggest improvement from YOLOv8s:** boom_lift jumped from 28.6% to 44.0% (+15.4%), likely due to the larger model's ability to capture finer features
- **Weak classes suffer from low recall** — the model misses many instances (false negatives), especially for dump_truck (30.6%) and tower_crane (31.1%)
- **boom_lift** has only 2 validation images / 5 instances — too few for reliable evaluation
- The larger YOLOv8s model costs 3.5× more compute but delivers meaningful accuracy gains, especially for underrepresented classes
- Both models serve as a viable proof-of-concept; weak classes need more training data and better annotation coverage

### External Benchmark

For reference, the same dataset trained with Roboflow's RF-DETR (Object Detection Small) achieved:
- mAP@50: 89.2%
- Precision: 88.0%
- Recall: 87.4%

This confirms the dataset quality is sufficient for high-accuracy detection. The gap between our YOLOv8s results (67.9% mAP@50) and RF-DETR (89.2%) suggests that a larger model architecture and/or more advanced training techniques could significantly improve performance.
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
   - Train YOLOv8s for 50 epochs (512×512) for comparison
   - Evaluate both models and display metrics + training curves
   - Show a visual performance dashboard
   - Display a side-by-side YOLOv8n vs YOLOv8s comparison chart
   - Run predictions on new test images downloaded from GitHub
   - Display a 6×6 evidence grid with class coverage
   - Print a reproducibility summary
5. Total runtime: ~30–50 minutes on T4 GPU

---

## Reproducibility Checklist

| Parameter | Value |
|-----------|-------|
| Models | YOLOv8n (Nano) + YOLOv8s (Small) |
| Framework | Ultralytics 8.4.18 |
| Python | 3.12.12 |
| PyTorch | 2.10.0+cu128 |
| Epochs | 50 |
| Image size | 512 |
| Batch size | auto |
| Early stopping | patience=15 |
| Cache | RAM |
| GPU | Tesla T4 (14913 MiB) |
| YOLOv8n params | 3,007,013 (8.1 GFLOPs) |
| YOLOv8s params | 11,128,293 (28.5 GFLOPs) |
| Dataset | GitHub Release v1.0 (auto-download) |
| New test images | GitHub repo (auto-download) |
| Manual uploads | None (fully cloud-based) |
| Last run | 2026-02-26 |

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
| 7b | Trains YOLOv8s — 50 epochs, 512px (for comparison) |
| 8 | Evaluates YOLOv8n — validation metrics + plots |
| 8b | Evaluates YOLOv8s — validation metrics + plots |
| 8c | Side-by-side YOLOv8n vs YOLOv8s comparison chart |
| 9 | Lists training output files |
| 9.a | Displays training visualizations (styled dark theme) |
| 9.b | Visual metrics dashboard (bar chart) |
| 10 | Saves best weights for download |
| 10.a | Downloads 5 new test images from GitHub (no manual upload) |
| 11 | Runs predictions on new test images and displays results |
| 11.a | 6×6 evidence grid with class coverage |
| 12 | Prints reproducibility summary with model comparison |

---

## Trained Weights

Download from [GitHub Release v1.0](https://github.com/Vagiadim/SiteAI-equipment-tracker-/releases/tag/v1.0):
- `dataset.zip` — Full dataset (YOLOv8 format)
- `best.pt` — Trained YOLOv8n weights (6.2 MB)

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
