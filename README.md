# DDAG-Net

**DDAG-Net: A novel Dual-Domain Adaptive Decoupling and Arterial Axis-Guided Network for Pulmonary Embolism Detection Segmentation**

> A topology-aware pulmonary embolism segmentation framework with dual-domain adaptive decoupling, vascular skeleton-guided attention, and cross-layer functional gating.

---

## 📌 Overview

DDAG-Net is a 3D medical image segmentation framework designed for **pulmonary embolism (PE) segmentation** in **CT pulmonary angiography (CTPA)**.

The network is built upon an improved 3D U-Net style architecture and introduces four complementary innovations to address the major challenges of PE analysis:

- Small embolism targets
- Complex pulmonary vascular structures
- Severe class imbalance
- Structural inconsistency in segmentation
- Weak boundary representation

The proposed framework integrates vascular structural priors, topology-aware learning, dual-domain feature disentanglement, and task-guided skip modulation into a unified end-to-end segmentation network.

---

## 🧠 Network Architecture

The overall architecture of DDAG-Net is illustrated below:

```text
Input CTPA
   │
Encoder
   ├── Stage 1: Standard Feature Extraction
   ├── Stage 2: Dual-Domain Adaptive Decoupling
   ├── Stage 3: Dual-Domain Adaptive Decoupling
   └── Stage 4: Dual-Domain Adaptive Decoupling
            ├── Frequency Decomposition
            ├── Vessel Diameter Awareness
            └── Task-Oriented Feature Decoupling
   │
Bottleneck
   └── Early Coarse PE Prediction
   │
Decoder
   ├── Cross-Layer Functional Gating
   ├── Multi-scale Feature Recovery
   └── Skip Feature Refinement
   │
ASPP Multi-scale Fusion
   │
Topology-Aware Deformation
   │
Vessel Segmentation Branch
   │
Skeleton Extraction
   │
Skeleton-Guided Attention
   │
Final PE Segmentation
```

---

## ✨ Key Innovations

### 1️⃣ Vascular Skeleton-Guided Attention (AGAWithSkeleton)

A vascular skeleton-guided attention mechanism is introduced to explicitly incorporate pulmonary artery structural priors.

- Extracts 3D vascular skeletons from vessel segmentation predictions
- Guides embolism feature refinement along vascular centerlines
- Enhances localization of small emboli within thin pulmonary branches

---

### 2️⃣ Topology-Aware Consistency Constraint

A topology-aware deformation strategy is designed to preserve structural consistency under feature perturbations.

- Applies controlled feature-space deformation
- Encourages topological stability during training
- Reduces anatomically implausible segmentation artifacts

Loss formulation:

```math
L_{total} = L_{seg} + \lambda_{ortho} L_{ortho} + \lambda_{topo} L_{topo}
```

---

### 3️⃣ Dual-Domain Adaptive Feature Decoupling

A dual-domain feature disentanglement module is proposed to improve representation learning for PE segmentation.

**Components**

**Frequency Decomposition**

- Separates low-frequency global structure features
- Separates high-frequency detail-sensitive features

**Vessel Diameter-Aware Learning**

- Dynamically adjusts receptive fields according to vessel scale

**Task-Oriented Decoupling**

- Learns PE-specific features
- Learns vessel-specific features
- Learns shared representations

**Soft Orthogonal Constraint**

Encourages feature disentanglement between PE and vascular representations.

---

### 4️⃣ Cross-Layer Functional Gating

A task-guided skip modulation mechanism is introduced to improve semantic consistency in encoder-decoder fusion.

- Generates early coarse PE predictions
- Uses coarse predictions to guide skip-feature selection
- Suppresses irrelevant low-level responses

---

## 📂 Project Structure

The following is a **GitHub project layout** for this model:

```bash
DDAG-Net/
├── models/
│   ├── DDAG_Net.py
│   ├── StdBlocks.py
│   ├── topology_consistency.py
│   └── attention_modules.py
│
├── datasets/
│   ├── dataset.py
│   └── transforms.py
│
├── utils/
│   ├── losses.py
│   ├── metrics.py
│   └── visualization.py
│
├── checkpoints/
├── results/
├── train.py
├── test.py
├── inference.py
├── requirements.txt
└── README.md
```

---

## ⚙️ Requirements

### Environment

- Python >= 3.9
- PyTorch >= 2.0
- CUDA >= 11.8

### Install Dependencies

```bash
pip install -r requirements.txt
```

### Main Dependencies

```text
torch
numpy
scikit-image
scipy
SimpleITK
tqdm
```

---

## 🚀 Training

If you organize the repository with a standard training entry script, training can be started as:

```bash
python train.py
```

Example:

```bash
python train.py \
  --batch_size 2 \
  --lr 1e-4 \
  --epochs 300
```

---

## 🧪 Inference

```bash
python inference.py \
  --ckpt checkpoints/ddag_net.pth
```

---

## 📊 Evaluation Metrics

The following metrics are commonly used for this framework:

- Dice Similarity Coefficient (DSC)
- Sensitivity
- AUC
- Froc-score
- 95% Hausdorff Distance (HD95)

---

## 🗃️ Dataset

The framework is designed for **CT pulmonary angiography (CTPA)** datasets.

Typical preprocessing includes:

- Resampling
- Intensity normalization
- Lung region cropping
- Patch extraction
- Elastic deformation augmentation

---

## 🔥 Features

- 3D end-to-end segmentation
- Pulmonary artery prior modeling
- Frequency-aware feature learning
- Topology-consistent regularization
- Small-target sensitive design
- Multi-task representation disentanglement

---

## 🔭 Future Work

Potential future directions include:

- Multi-modal clinical information fusion
- Transformer-enhanced global context modeling
- Semi-supervised pulmonary embolism learning
- Topology-preserving graph reasoning

---

## 📤 Model Outputs

The current network `forward()` returns:

```python
{
    "segs": seg,
    "segvs": segv,
    "segs_deform": seg_deform,
    "ortho_loss": ortho_loss_total,
}
```

Where:

- `segs` denotes the final PE segmentation
- `segvs` denotes the vessel segmentation branch output
- `segs_deform` denotes the topology-aware auxiliary prediction during training
- `ortho_loss` denotes the soft orthogonal regularization term


---
## 📦 Code Availability

This repository currently serves as the **official project page** for DDAG-Net.

> 🚧 **The full source code, pretrained models, and training scripts will be released after the paper is officially accepted.**

This ensures compliance with journal and conference submission policies.



## ⭐ Acknowledgements

This project is built upon the PyTorch deep learning framework and open-source medical image segmentation project.

Special thanks to the medical imaging research community for their valuable contributions.

