SiteAI Equipment Tracker
YOLOv8 construction equipment detection for automated site monitoring
MAICEN M4U3 Assignment — Team 7
Show Image

Problem Statement
Construction sites require continuous monitoring of heavy equipment for safety, logistics, and progress tracking. Manual monitoring is time-consuming and error-prone. This project uses YOLOv8 object detection to automatically identify and locate construction equipment in site images, providing a proof-of-concept for automated site monitoring.
Success criteria: Achieve mAP@50 > 50% across all classes with a fully cloud-reproducible pipeline.

Dataset

Source: Roboflow (SiteAI-equipment-tracker, Team 7)
Format: YOLOv8 (exported from Roboflow)
Split: 80/20 (train/val)
Image size: 512×512
Download: Automatically downloaded from GitHub Release v1.0

Classes (7)
ClassDescriptionboom_liftAerial work platform with articulating or telescoping boomdump_truckTruck with open-box bed for transporting loose materialexcavatorTracked machine with bucket arm for diggingloaderWheeled machine with front-mounted bucketmixer_truckTruck with rotating drum for transporting concreterollerCompaction machine for flattening surfacestower_craneFixed crane with horizontal jib mounted on tall mast

Results
Results from training YOLOv8n for 50 epochs at 512×512 resolution on a Tesla T4 GPU.
Overall Metrics
MetricValuePrecisionUPDATE AFTER RUNRecallUPDATE AFTER RUNmAP@50UPDATE AFTER RUNmAP@50-95UPDATE AFTER RUN
Per-Class Performance (mAP@50)
ClassmAP@50Statusboom_liftUPDATEdump_truckUPDATEexcavatorUPDATEloaderUPDATEmixer_truckUPDATErollerUPDATEtower_craneUPDATE
Key Takeaways

Best performing classes: UPDATE AFTER RUN
Weakest classes: UPDATE AFTER RUN
The model serves as a viable proof-of-concept for automated construction equipment detection
Weak classes can be improved with more training data and better annotation coverage


How to Reproduce

One-click reproduction: Click the Colab badge above, select T4 GPU, and hit Run All. No manual uploads needed.

Step-by-step:

Click the Open in Colab badge above (or open the notebook from notebooks/)
Go to Runtime → Change runtime type → T4 GPU
Click Runtime → Run all
The notebook will automatically:

Install dependencies
Download the dataset from GitHub Release v1.0
Extract and configure dataset paths
Remove Roboflow metadata for independence
Train YOLOv8n for 50 epochs (512×512)
Evaluate and display metrics + training curves
Show a visual performance dashboard
Run predictions on 10 validation images
Display a 6×6 evidence grid with class coverage
Download and run predictions on 5 new unseen images from GitHub
Print a reproducibility summary


Total runtime: ~30–50 minutes on T4 GPU


Reproducibility Checklist
ParameterValueModelYOLOv8n (Nano)FrameworkUltralyticsEpochs50Image size512Batch sizeautoEarly stoppingpatience=15CacheRAMGPUTesla T4 (Google Colab)DatasetGitHub Release v1.0 (auto-download)New test imagesGitHub repo (auto-download)Manual uploadsNone (fully cloud-based)

Repository Structure
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

Notebook Structure
CellWhat It Does1Environment setup — installs Ultralytics, checks GPU2Downloads dataset.zip from GitHub Release v1.03Unzips dataset and inspects folder structure4Locates and displays data.yaml configuration5Fixes dataset paths for Colab (auto-detects valid/val)6Removes Roboflow metadata for platform independence7Trains YOLOv8n — 50 epochs, 512px, auto batch, patience=158Evaluates model — regenerates validation plots9Lists training output files9.aDisplays training visualizations (styled dark theme)9.bVisual metrics dashboard (bar chart)10Saves best weights for download10.aDownloads 5 new test images from GitHub (no manual upload)11Runs predictions on new test images and displays results11.a6×6 evidence grid with class coverage12Prints reproducibility summary

Trained Weights
Download from GitHub Release v1.0:

dataset.zip — Full dataset (YOLOv8 format)
best.pt — Trained model weights


Documentation

docs/error_analysis.md — False positives, false negatives, and data improvement plan
docs/governance_checklist.md — Privacy, limitations, and risk assessment
docs/class_definitions.md — Label rules for all 7 classes


Deliverables

deliverables/slides.pdf — Presentation slides (6–8 slides)
deliverables/mini_report.pdf — 2-page summary report


License
This project is licensed under the MIT License.

Team
Team 7 — MAICEN Module 4, Unit 3
Zigurat Institute of Technology
