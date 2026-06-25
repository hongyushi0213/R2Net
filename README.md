# R2Net
R2Net: Dual Rectification and Hierarchical Reconstruction for Multi-Modal Crowd Counting

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)
[![PyTorch](https://img.shields.io/badge/PyTorch-%3E%3D2.0-EE4C2C?style=flat&logo=pytorch)](https://pytorch.org/)
[![Status](https://img.shields.io/badge/Status-Under_Review-blue.svg)]()

This is the official PyTorch implementation of the paper **"Dual Rectification and Hierarchical Reconstruction Network for Multi-Modal Crowd Counting"** ($R^2Net$).

> **Note:** This repository is currently anonymized for double-blind review. Full source code, pre-trained weights, and the detailed dataset processing pipeline will be made completely public upon paper acceptance.

---

## 📌 Key Highlights

- **Dual Feature Rectification:** Introduces Deformable Cross-Modal Alignment (DCMA) and Density-Aware Asymmetric Spatial Gating (DASG) to fundamentally overcome cross-modal spatial misalignment and semantic contamination.
- **Hierarchical Density Reconstruction:** Features the Modality-Aware Cross-Level Differential Recovery (MACL) Decoder, precisely restoring high-frequency tiny-target details lost during downsampling through differential mathematical modeling.
- **Geometry-Aware Composite Loss:** A synergistic optimization pipeline integrating Optimal Transport (OT), Total Variation (TV), Local Relative Density (LRD) regularization, and Modality-Swap Consistency (MSFC) to strictly enforce topological stability and eliminate MSE-induced over-smoothing.

---

## 🛠️ Environment Setup

We recommend using Anaconda to create an isolated virtual environment. The codebase has been extensively tested on Ubuntu 22.04 with PyTorch 2.x and NVIDIA GeForce RTX 5090 GPUs.

```bash
# Create and activate the environment
conda create -n r2net python=3.10 -y
conda activate r2net

# Install PyTorch (CUDA 12.x recommended for high-performance GPUs)
pip install torch torchvision --index-url [https://download.pytorch.org/whl/cu121](https://download.pytorch.org/whl/cu121)

# Install other essential dependencies
pip install -r requirements.txt
