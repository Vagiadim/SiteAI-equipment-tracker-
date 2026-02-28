# SiteAI Equipment Tracker — YOLOv8 Deployment

**Autonomous Object Detection for AECO Heavy Equipment**

MAICEN M4U3 | Team 7 — Elia Reyes, Rafael Cervantes, Talin Abu Gharbieh, Vagia Dimara, Juan Pablo Garcia

---

## Problem Statement

Struck-by accidents involving heavy machinery are among the leading causes of fatalities on construction sites. Manual equipment tracking is error-prone and cannot scale across large AECO projects. This project develops a computer vision system that automatically detects and classifies 7 types of heavy construction equipment from site photographs, enabling real-time monitoring for safety and logistics.

**Success Criteria:** Achieve >60% mAP@50 on a multi-class construction equipment dataset using a lightweight, edge-deployable YOLOv8 model trained entirely in the cloud.

---

## Final Deliverables (Short PDF Pack)
As per the assignment requirements, the final presentation deck and executive summary report are hosted directly in this repository:

* 📄 **[Executive Mini Report (PDF)](deliverables/B02_M04_U03_REPORT-MiniReport_VD_PUBLISHED_v04.pdf)**
* 📊 **[Presentation Slides (PDF)](deliverables/B02_M04_U03_SLIDES-YOLOv8_VD_PUBLISHED_v02.pdf)**
  
---

## Classes & Label Rules

| # | Class | Description | Label Rule |
|---|-------|-------------|------------|
| 1 | boom_lift | Aerial work platform with articulated boom | Bounding box around full machine including boom arm |
| 2 | dump_truck | Heavy truck with tilting bed for material transport | Full vehicle including bed (raised or lowered) |
| 3 | excavator | Tracked machine with hydraulic arm and bucket | Full machine including arm in any position |
| 4 | loader | Wheeled machine with front bucket | Full vehicle including bucket |
| 5 | mixer_truck | Concrete mixer with rotating drum | Full vehicle including drum and chute |
| 6 | roller | Compaction machine with steel drum(s) | Full machine including drums |
| 7 | tower_crane | Fixed crane with horizontal jib on lattice tower | Full visible structure (mast + jib) |

---

## Dataset

- **Source:** [Roboflow Universe — SiteAI Equipment Tracker v18](https://universe.roboflow.com/juanp-garcia/siteai-equipment-tracker/dataset/18)
- **Source images:** 581 annotated images across 7 classes
- **After augmentation (3x):** 1,509 total images (rotation ±3°, brightness ±15%, exposure ±10%)
- **Split:** 80/20 train/validation
- **Preprocessing:** Auto-orient + resize to 512×512 pixels
- **Format:** YOLOv8 (exported from Roboflow, hosted on GitHub Release)

---

## How to Reproduce

**Zero setup required — fully cloud-based.**

1. Open [`notebooks/M4U3_Assignment_Team_7_object_detection_FINAL.ipynb`](notebooks/M4U3_Assignment_Team_7_object_detection_FINAL.ipynb) on GitHub
2. Click **"Open in Colab"** at the top of the notebook
3. In Colab: **Runtime → Change runtime type → T4 GPU**
4. Click **Runtime → Run All**
5. All results are generated automatically in ~30 minutes

The notebook downloads the dataset from GitHub Releases, trains both models, runs validation, generates all plots, and runs inference on new test images — no manual uploads or API keys needed.

---

## Results Summary

### Overall Metrics

| Metric | YOLOv8n | YOLOv8s | RF-DETR (benchmark) |
|--------|---------|---------|---------------------|
| mAP@50 | 64.4% | 70.8% | 89.2% |
| Precision | 76.8% | 87.0% | 88.0% |
| Recall | 57.2% | 63.9% | 87.4% |
| mAP@50-95 | 47.0% | 56.7% | — |

### Key Takeaways

1. **YOLOv8s outperforms YOLOv8n** across all metrics (+6.4% mAP@50, +10.2% Precision), confirming that scaling model capacity works when dataset volume is sufficient.
2. **Production-ready classes:** mixer_truck (99.5%), roller (97.8%), and loader (94.5%) achieve near-perfect detection.
3. **Weak classes remain:** dump_truck (58.9%) and tower_crane (39.6%) require targeted data collection and resolution upscaling.

---

## Reproducibility Checklist

| Parameter | Value |
|-----------|-------|
| Dataset version | [SiteAI Equipment Tracker v18](https://universe.roboflow.com/juanp-garcia/siteai-equipment-tracker/dataset/18) |
| Dataset hosted at | [GitHub Release v1.0](https://github.com/Vagiadim/SiteAI-equipment-tracker-/releases/tag/v1.0) |
| Model variants | YOLOv8n (3M params) + YOLOv8s (11.2M params) |
| Epochs | 50 (early stopping patience: 15) |
| Batch size | auto |
| Image size | 512×512 |
| GPU | Tesla T4 (Google Colab) |
| Ultralytics version | 8.4.18 |
| PyTorch version | 2.10.0+cu128 |
| Framework | Google Colab (Python 3) |

---

## Repository Structure

```
SiteAI-equipment-tracker-/
├── notebooks/
│   └── M4U3_Assignment_Team_7_object_detection_FINAL.ipynb
├── docs/
│   ├── error_analysis.md
│   ├── class_definitions.md
│   └── governance_checklist.md
├── results/
│   ├── curves/          # PR curves, F1 curves, confusion matrix
│   └── evidence/        # Validation predictions, 6×6 grid, new test images
├── deliverables/
│   ├── B02_M04_U03_REPORT-MiniReport_VD_PUBLISHED_v04.pdf
│   └── B02_M04_U03_SLIDES-YOLOv8_VD_PUBLISHED_v02.pdf
├── README.md
└── LICENSE              # MIT
```

---

## Error Analysis (Summary)

**Primary failure mode:** False Negatives (equipment missed entirely — classified as background).

From the confusion matrix (YOLOv8s):
- **dump_truck:** 12 instances missed — vehicle blends into earthwork backgrounds
- **tower_crane:** 8 missed + 7 false positives — thin lattice lost at 512px; scaffolding confused for crane
- **excavator:** 4 missed — unusual arm poses underrepresented in training data

**Root causes:** Class imbalance, low validation samples, 512px resolution destroying fine structural details.

See [`docs/error_analysis.md`](docs/error_analysis.md) for full analysis.

---

## Governance & Licensing

- **Safety:** False Negatives are exponentially more dangerous than False Positives in AECO. This model is a monitoring aid only — NOT for automated safety-critical shutdowns without human oversight.
- **Privacy:** Face and license plate blurring required before any deployment (GDPR). EU AI Act may classify construction safety monitoring as "high-risk AI" under Annex III.
- **Operational limits:** Not validated for nighttime, >100m distance, heavy dust/rain, or across different geographies.
- **Code license:** MIT
- **Dataset:** Roboflow Universe (public, with attribution)
- **Framework:** Ultralytics AGPL-3.0 (commercial use requires Enterprise license)

See [`docs/governance_checklist.md`](docs/governance_checklist.md) for full governance documentation.

---

## Reproducibility Proof

This notebook was tested on February 27, 2026. A fresh Colab runtime with T4 GPU successfully reproduced all training, validation, and inference results using only `Runtime → Run All` with zero manual intervention.
