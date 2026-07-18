# Volumetric Cardiac Segmentation using Mamba U-Net Architectures on the ACDC Dataset

An advanced deep learning framework utilizing **State Space Models (SSMs)**, specifically the **Mamba** architecture, adapted into a U-Net topology for multi-class cardiac structure segmentation. This system accurately delineates the Right Ventricle (RV), Myocardium (MYO), and Left Ventricle (LV) from cardiac MRI volumes.

This repository documents the research benchmarks for both the 2D Slice-by-Slice approach and the 3D Volumetric sequence modeling pipeline, geared toward a functional mobile application deployment.

---

## 📊 Performance Benchmark Summary

Through rigorous architectural optimization (Learning Rate scheduling, Class-Weighted Losses, and Gradient Clipping), the following benchmarks were achieved on the ACDC validation set:

| Architecture | Mean Dice | RV Dice | MYO Dice | LV Dice | Status & Deployment Strategy |
| :--- | :---: | :---: | :---: | :---: | :--- |
| **2D Mamba U-Net** | **0.9450** | 0.9310 | 0.9420 | 0.9620 | **Production Ready** (Deployed via Flutter + Supabase Stack) |
| **3D Mamba U-Net (V2.2)** | **0.7612** | 0.6978 | 0.7447 | 0.8467 | **Research Benchmark** (Retained for sequence consistency studies) |

### 🚀 The 3D Breakthrough Journey (V2.2 Update)
Initial 3D volumetric iterations suffered from structural optimization bottlenecks (~0.61 Mean Dice). The final **Ultimate Push V2.2** successfully achieved a peak **0.7612 Mean Dice** by integrating:
* **Bidirectional Mamba Bottleneck** preserving critical spatial Z-axis slice relationships.
* **Class-Weighted Cross Entropy** to explicitly boost underrepresented cardiac structures (RV & MYO).
* **Gradient Norm Clipping (max_norm=1.0)** to stabilize sequence processing trajectories and eliminate gradient explosions.

---

## 🏗️ Core System Architecture & Mobile Integration

To ensure clinical utility, high precision, and system stability, the project transitions from raw training notebooks into a mobile-ready production pipeline:

1. **Frontend UI (Flutter):** A minimalist, medical-grade mobile interface tailored for clinicians to manage patients, upload raw `.h5` files, and interactively scroll through segmented slices.
2. **Backend Storage & Coordination (Supabase):** PostgreSQL manages secure patient metadata, while Supabase Storage handles volumetric file transfers.
3. **AI Inference Server (Python Backend):** A dedicated script processes incoming files using the high-precision **2D Mamba U-Net** (`>0.94` Dice), computes clinical metrics, and saves the output masks.

---

## 📁 Repository Structure

* `mamba segmentation image 2d.ipynb`: The end-to-end training pipeline, validation logs, and configuration yielding the production-ready 0.945 Dice score.
* `mamba segmentation image 3d.ipynb`: The optimization notebook containing the Ultimate Push V2.2 training execution logs.
* `inference_pipeline.py`: A clean, production-ready inference utility designed to bridge the raw model weights with the Supabase cloud backend.
* `requirements.txt`: Python environment dependencies.
* `.gitignore`: Built-in rules to protect the repository from committing heavy dataset arrays or model weight files (`.pth`).

---

## 🛠️ Requirements & Installation

Clone the repository and install the necessary dependencies:

```bash
git clone [https://github.com/your-username/mamba-cardiac-segmentation.git](https://github.com/your-username/mamba-cardiac-segmentation.git)
cd mamba-cardiac-segmentation
pip install -r requirements.txt
