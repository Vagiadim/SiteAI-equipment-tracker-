# Technical Appendix: Reproducibility and Methodology Framework
**Project Title:** SiteAI Equipment Tracker (YOLOv8 Implementation)

**Academic Module:** AI for the AECO Sector

**Group:** Team 7 (JuanPablo Garcia, Taline Abu Gharbieh, Vagia Dimara, Elia Reyes, Rafael Cervantes)

---

## 1. Experimental Design & Objectives
The primary objective of this experimental setup is to validate the efficacy of the YOLOv8n architecture in identifying specialized heavy machinery within high-clutter construction environments. 
To ensure scientific integrity, the methodology follows a structured pipeline: 
Data Acquisition, Pre-processing, Model Configuration, and Performance Evaluation. This framework is designed to be fully reproducible, allowing for auditability in an academic and professional engineering context.

## 2. Dataset Architecture and Provenance
The model's predictive capability is grounded in a high-quality dataset curated specifically for this project.

### 2.1 Dataset Specifications
* **Source:** Personal site pictures (Canada-based) & Roboflow dataset filtering - SiteAI Equipment Tracker v9 (Team7_Dataset_V1) - 581 Total.
* **Class Taxonomy:** A 9-class schema was implemented, covering: Boom Lift, Dump Truck, Excavator, Loader, Mixer Truck, Roller, Tower Crane, Forklift, and Backhoe.
* **Volume:** The dataset consists of 1,441 images generated after applying Data Augmentation, ensuring a robust sample size for deep learning feature extraction.

### 2.2 Partitioning Strategy
To prevent data leakage and ensure reliable validation, the dataset was partitioned using a 92/4/4 split:
* **Training Set (92%):** 1,326 images used for gradient updates and weight optimization.
* **Validation Set (4%):** 57 images used for hyperparameter tuning and early stopping monitoring.
* **Testing Set (4%):** 58 images reserved for final unbiased performance evaluation.



## 3. Computer Vision Configuration (Hyperparameters)
The following technical settings were strictly maintained throughout the 50-epoch training cycle to ensure consistency:

### 3.1 Architecture & Input Resolution
* **Base Model:** YOLOv8n (Nano). This variant was selected to balance computational efficiency with detection precision, suitable for future edge-device deployment on-site.
* **Input Resolution:** 800x800 pixels. This high-resolution setting was chosen to maximize the "Spatial Fidelity" of the model, allowing for the detection of thin structural elements (such as crane jibs) and distant assets that would be lost at standard 640px resolutions.

### 3.2 Training Parameters
* **Epochs:** 50 full passes through the training data.
* **Batch Size:** Set to 'Auto' (batch=-1), enabling the system to dynamically optimize throughput based on the T4 GPU's memory availability.
* **Augmentations:** Mosaic augmentation was utilized to combine four training images into one, forcing the model to learn to detect objects in smaller scales and varying backgrounds, mimicking a high-clutter construction site.
* **Caching:** RAM caching (cache=True) was enabled to eliminate I/O bottlenecks and accelerate epoch cycles.

## 4. Hardware and Software Environment
To replicate these results, the following environment must be used:
* **Infrastructure:** Google Colab (Free Tier).
* **Hardware accelerator:** NVIDIA T4 GPU.
* **Library:** Ultralytics version 8.3.0.
* **Programming Language:** Python 3.10+ using the `.ipynb` notebook format provided in the repository.

## 5. Verification and Pathing Logic
A critical step in reproducibility is the verification of data paths. 
A specialized Python script was integrated into the training pipeline to overwrite the `data.yaml` configuration. 
This ensures that absolute paths point correctly to `/content/dataset/` regardless of the local user's directory structure, preventing "File Not Found" errors during cross-user replication.

---
*By strictly adhering to these parameters, the model consistently reaches an mAP@50 of approximately 85.1%, confirming the reliability of the SiteAI Tracker framework for university-level research.*
