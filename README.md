# Volumetric Cardiac Segmentation using Mamba U-Net Architectures on ACDC Dataset

An advanced deep learning framework utilizing **State Space Models (SSMs)**, specifically the **Mamba** architecture, adapted into a U-Net topology for multi-class cardiac structures segmentation (Right Ventricle, Myocardium, and Left Ventricle). 

This repository documents the research benchmarks for both the 2D Slice-by-Slice approach and the 3D Volumetric sequence modeling pipeline, geared towards mobile-readiness.

## 📊 Performance Benchmark Summary

Through rigorous architectural optimization (Learning Rate scheduling, Class-Weighted Losses, and Gradient Clipping), the following benchmarks were achieved on the ACDC validation set (40 volumes):

| Architecture | Mean Dice | RV Dice | MYO Dice | LV Dice | Status & Deployment Strategy |
| :--- | :---: | :---: | :---: | :---: | :--- |
| **2D Mamba U-Net** | **0.9450** | 0.9310 | 0.9420 | 0.9620 | **Production Ready** (Deployed via Flutter Mobile Stack) |
| **3D Mamba U-Net (V2.2)** | **0.7612** | 0.6978 | 0.7447 | 0.8467 | **Research Benchmark** (Retained for temporal consistency studies) |

### 🚀 The 3D Breakthrough Journey
Initial 3D volumetric iterations suffered from structural instabilities (~0.61 Dice). The implementation of **Ultimate Push V2.2** integrated:
* **Bidirectional Mamba Bottleneck** preserving 8 crucial Z-axis slices.
* **Class-Weighted Cross Entropy** to boost underrepresented structures (RV & MYO).
* **Gradient Norm Clipping (max_norm=1.0)** to stabilize sequence processing trajectories.

---

## 🏗️ Repository Layout

* `src/models/`: Contains the pure PyTorch definitions for both `MambaUNet2D` and `MambaUNet3DV2`.
* `src/train_3d.py`: The precise pipeline utilizing `ReduceLROnPlateau` that successfully cracked the 0.7612 Dice benchmark.
* `notebooks/`: Contains the end-to-end experimental execution environments from Kaggle.

## 🛠️ Requirements & Installation

```bash
pip install -r requirements.txt
