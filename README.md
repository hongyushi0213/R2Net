# R2Net: Dual Rectification and Hierarchical Reconstruction for Multi-Modal Crowd Counting

---

## Introduction

Multi-modal crowd counting aims to estimate crowd distributions and total counts by using complementary information from different modalities, such as RGB, thermal, and depth images. However, existing methods still face several challenges, including cross-modal spatial misalignment, semantic degradation under adverse illumination, tiny-target information loss during downsampling, and over-smoothed density map supervision.

To address these issues, we propose **R2Net**, which builds a complete optimization pipeline from front-end feature rectification to back-end density reconstruction. Specifically, R2Net contains:

* **Three-branch feature extraction**, which extracts RGB-specific, thermal-specific, and cross-modal fusion features.
* **DCMA**, a Deformable Cross-Modal Alignment module for cross-modal spatial correction.
* **DASG**, a Density-Aware Asymmetric Spatial Gating module for robust asymmetric feature fusion.
* **MACL Decoder**, a Modality-Aware Cross-Level Differential Recovery Decoder for tiny-target detail reconstruction.
* **Geometry-Aware Composite Supervision**, which improves geometric localization and alleviates density map over-smoothing.

---

## Overall Framework

The overall architecture of R2Net consists of five main components:

1. U-Net-based front-end auxiliary fusion module.
2. Shared VGG19–ViT hybrid encoder.
3. Deformable Cross-Modal Alignment module.
4. Density-Aware Asymmetric Spatial Gating module.
5. Modality-Aware Cross-Level Differential Recovery Decoder.

The network first extracts multi-branch features from RGB and thermal inputs. Then, DCMA aligns RGB features with thermal spatial references, while DASG suppresses unreliable RGB noise and introduces useful texture cues. Finally, MACL Decoder recovers tiny-target details and generates the final density map.

---

## Main Modules

### DCMA: Deformable Cross-Modal Alignment

DCMA aims to reduce cross-modal spatial misalignment caused by physical baselines and imaging differences. It uses thermal features as stable spatial anchors and adaptively resamples RGB features through deformable convolution.

### DASG: Density-Aware Asymmetric Spatial Gating

DASG addresses semantic reliability gaps between RGB and thermal modalities. It uses density-aware spatial gates to suppress degraded RGB noise and selectively introduce reliable RGB texture cues, with thermal features serving as the stable fusion basis.

### MACL Decoder: Modality-Aware Cross-Level Differential Recovery Decoder

MACL Decoder recovers tiny-target details lost during downsampling. It purifies shallow features with modality-aware gating, computes deep-shallow differential responses, and restores high-frequency details for density map reconstruction.

### Geometry-Aware Composite Loss

The proposed loss function includes output-level geometric matching, feature-level local topology constraints, and cross-modal semantic consistency. It helps alleviate the over-smoothing problem of traditional MSE supervision.

---

## Requirements

The code is implemented with PyTorch.

Recommended environment:

```text
Python >= 3.8
PyTorch >= 1.10
CUDA >= 11.3
torchvision
numpy
opencv-python
scipy
tqdm
matplotlib
Pillow
PyYAML
```

Install dependencies:

```bash
conda create -n r2net python=3.9
conda activate r2net

pip install -r requirements.txt
```

---

## Datasets

We evaluate R2Net on three multi-modal crowd counting datasets:

* **RGBT-CC**
* **DroneRGBT**
* **ShanghaiTechRGBD**

Please download the datasets from their official sources and organize them as follows:

```text
datasets/
├── RGBT-CC/
│   ├── train/
│   ├── val/
│   └── test/
├── DroneRGBT/
│   ├── train/
│   ├── val/
│   └── test/
└── ShanghaiTechRGBD/
    ├── train/
    └── test/
```

Due to dataset license restrictions, this repository does not redistribute the original datasets. Please follow the official dataset licenses when using them.

---


## Evaluation Metrics

We use the following evaluation metrics:

* **RMSE**: Root Mean Square Error.
* **GAME(0)**: Equivalent to MAE, measuring global counting error.
* **GAME(1), GAME(2), GAME(3)**: Measuring local regional counting errors at different grid levels.

Lower values indicate better performance.

---

## Results

More detailed quantitative comparisons and ablation studies are provided in the paper.


## Visualization

This repository also supports visualization of:

* Predicted density maps.
* Cross-modal offset fields in DCMA.
* Spatial gating weights in DASG.
* Differential feature responses in MACL Decoder.
* Hyper-parameter sensitivity curves.


---

## Pretrained Models

Pretrained weights will be released after the paper is accepted.

| Dataset          | Checkpoint  |
| ---------------- | ----------- |
| RGBT-CC          | Coming soon |
| DroneRGBT        | Coming soon |
| ShanghaiTechRGBD | Coming soon |

---


## Acknowledgements

This project is built upon PyTorch and related open-source libraries. We sincerely thank the authors of RGBT-CC, DroneRGBT, and ShanghaiTechRGBD for providing public multi-modal crowd counting benchmarks.

---

## Contact

For questions about the paper or code, please contact:

```text
Ziyi Zhao
Email: zhaoziyi.000@gmail.com
```

