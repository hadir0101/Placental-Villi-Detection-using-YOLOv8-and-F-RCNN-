# Placental Villi Detection using YOLOv8 and Faster R-CNN

A medical-imaging object detection project that automates placental villi analysis on high-resolution histopathology slides.

This work compares **YOLOv8s** (fast, one-stage detector) and **Faster R-CNN** (precision-oriented, two-stage detector) for detecting three villi types:
- **Terminal villi**
- **Intermediate villi**
- **Stem villi**

> Based on the bachelor thesis: **"Object Detection Techniques in Medical Imaging"** (Budapest University of Technology and Economics, 2025).

---

## Why this project matters

Manual placental slide analysis is slow, expert-dependent, and difficult to scale. This project demonstrates that **bounding-box detection** can be a practical and scalable alternative to segmentation for placental microscopy, even under:
- class imbalance,
- dense overlapping structures,
- very large whole-slide images (WSIs).

---

## What was built

### 1) End-to-end dataset pipeline
- Converted polygon annotations (XML) to object detection labels.
- Tiled large microscopy slides for memory-efficient training/inference.
- Applied augmentation and oversampling to address rare classes (especially Stem villi).

### 2) Two complete detection workflows
- **YOLOv8s pipeline** on **1024×1024** tiles with overlap.
- **Faster R-CNN pipeline** on **2048×2048** tiles with overlap and post-processing.

### 3) Evaluation framework
- Quantitative metrics: Precision, Recall, mAP@0.5, mAP@0.5:0.95.
- Qualitative analysis: confusion matrices, prediction behavior, class-wise strengths/limitations.

---

## Key results (test set)

### YOLOv8s
| Class | Precision | Recall | mAP@0.5 | mAP@0.5:0.95 |
|---|---:|---:|---:|---:|
| Terminal | 0.752 | 0.794 | 0.819 | 0.707 |
| Intermediate | 0.694 | 0.662 | 0.694 | 0.537 |
| Stem | 0.556 | 0.577 | 0.596 | 0.337 |
| **Overall** | **0.667** | **0.678** | **0.703** | **0.527** |

### Faster R-CNN
| Class | Precision | Recall | mAP@0.5 | mAP@0.5:0.95 |
|---|---:|---:|---:|---:|
| Terminal | 0.7294 | 0.6764 | 0.700 | 0.490 |
| Intermediate | 0.6713 | 0.5555 | 0.610 | 0.410 |
| Stem | 0.4210 | 0.4571 | 0.440 | 0.280 |
| **Overall** | **0.6072** | **0.5630** | **0.583** | **0.393** |

### Interpretation
- **YOLOv8s**: stronger recall-oriented behavior and faster detection throughput.
- **Faster R-CNN**: cleaner class separation and more conservative predictions.
- Together, results support a strong case for **hybrid/ensemble approaches** in medical object detection.

---

## Highlights

- Built and evaluated **two production-relevant CV pipelines** on a real medical dataset.
- Solved practical ML engineering challenges: annotation conversion, WSI tiling, imbalance handling, and post-processing.
- Delivered measurable results with clear trade-off analysis (speed vs precision, sensitivity vs false positives).
- Demonstrated domain transfer: adapting general-purpose detectors to **digital pathology**.

---

## Repository contents

- `Yolov8WithTiling (3).ipynb` — YOLOv8 data prep, tiling, training, and evaluation workflow.
- `Final F_Rcnn (1).ipynb` — Faster R-CNN training/evaluation workflow (+ fusion experiments).
- `thesis_hadir_clean (2).pdf` — full thesis with methodology, experiments, and discussion.

---

## How to use this repository

This repository is notebook-driven.

1. Open `Yolov8WithTiling (3).ipynb` to reproduce the YOLOv8 pipeline.
2. Open `Final F_Rcnn (1).ipynb` to reproduce the Faster R-CNN pipeline.
3. Update dataset paths in notebook cells to your environment (many paths are set for Google Drive/Colab).
4. Run cells sequentially for preprocessing, training, and evaluation.

> Note: The notebooks were originally developed in Google Colab and include Google Drive-based paths.

---

## Future direction

- Resolution-aware training by villus morphology.
- Better rare-class handling for Stem villi.
- Hybrid architecture combining YOLOv8 speed with Faster R-CNN precision.

---

## Author

**Hadir Helali**
