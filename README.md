# Hi-Fi Hands 20/20: A Benchmark for Viewpoint-Invariant Hand Gesture Recognition

Hi-Fi Hands 20/20 is a **high-fidelity hand gesture recognition dataset** designed for evaluating **spatio-temporal gesture recognition models under real-world distribution shifts**.

The dataset introduces **structured variability across viewpoint, environment, and subject demographics**, enabling rigorous evaluation of gesture recognition models beyond traditional benchmarks.

This repository contains the **Hi-Fi Hands 20/20 dataset, sample clips, and supporting resources**.

---

## Dataset Overview

Hi-Fi Hands 20/20 is designed to address limitations in existing gesture recognition datasets by focusing on:

- High temporal fidelity
- Dual-modality data
- Structured distribution shifts
- Viewpoint diversity

Key characteristics:

- **20 gesture classes**
- **20 participants**
- **4800+ gesture videos**
- **1080p resolution**
- **60 FPS**
- **RGB video + 3D skeletal annotations**
- **Indoor and outdoor environments**

Each gesture sequence contains approximately **100–150 frames (~2 seconds)** enabling models to capture fine-grained motion dynamics and subtle finger articulation.

---

## Dataset Statistics

| Property | Value |
|--------|------|
| Total videos | 4800+ |
| Gesture classes | 20 |
| Participants | 20 |
| Frame rate | 60 fps |
| Resolution | 1920 × 1080 |
| Average frames per video | ~120 |
| Keypoints per frame | 21 |
| Viewpoints | Egocentric + Allocentric |
| Environments | Indoor + Outdoor |

---

## Gesture Vocabulary

The dataset contains **20 gesture classes** grouped into four categories.

```
### Single-hand Static Gestures
    Thumbs Up
    Thumbs Down
    Victory
    Okay
    Point


### Single-hand Dynamic Gestures
    Swipe Right
    Swipe Left
    Swipe Up
    Swipe Down
    Rotate CW
    Rotate CCW
    Come
    Snap


### Double-hand Static Gestures
    Heart
    Box
    Book


### Double-hand Dynamic Gestures
    Pinch In
    Pinch Out
    Clap
    Drive
```


## Dataset Structure

```
Example repository structure:
    HiFiHands_20_20
    │
    ├── sf_clips/
    │ ├── User_01/
    │ ├── User_02/
    │ ├── User_03/
    │ └── ...
    │
    ├── samples/
    │ └── example_frames
    │
    ├── scripts/
    │ ├── frame_extraction.py
    │ └── preprocessing.py
    │
    ├── segmentation/
    │ └── hand_segmentation.py
    │
    ├── paper/
    │ └── HiFiHands_2020_paper.pdf
    │
    ├── requirements.txt
    │
    └── README.md
```

## Data Collection

The dataset was recorded using **Samsung Galaxy S23 Ultra and S24 Ultra smartphones**.
```
Recording conditions:
    
    - **1080p resolution**
    - **60 FPS frame rate**
    - **Indoor and outdoor environments**
    - **Natural illumination variations**
    - **Handheld camera motion**

Participants performed gestures naturally without strict posture or camera placement constraints to increase **intra-class variability and realism**.


## Modalities

### RGB Modality

  Raw RGB gesture videos captured at:  
      Resolution: 1920 × 1080
      Frame rate: 60 FPS
  
  
  Videos preserve natural recording conditions including:
      - motion blur
      - illumination changes
      - background variation

### 3D Skeletal Modality
  
  Each frame contains:
      21 hand keypoints in 3D
      These skeletal sequences enable modeling using:
        - Graph Neural Networks
        - Spatio-temporal Transformers
        - Multimodal fusion architectures
```
## Models Used

We evaluated representative architectures from two categories: **skeleton-based** and **RGB-based** gesture recognition models.

| Model | Type | Description |
|------|------|-------------|
| ST-GCN | Skeleton-based | Graph convolution network modeling spatial-temporal relationships between 21 hand joints |
| STGT | Skeleton-based | Transformer-based model capturing long-range spatial and temporal dependencies |
| 3D ResNet | RGB-based | 3D convolution network learning spatio-temporal features from video clips |
| SlowFast | RGB-based | Dual-pathway architecture capturing both slow and fast motion dynamics |


Skeleton models operate on **21 3D hand keypoints**, while RGB models use **video clips sampled from gesture sequences**.

---

## Training Configuration

| Parameter | Value |
|----------|------|
| Optimizer | Adam |
| Learning Rate | 1e-4 |
| Batch Size | 32 |
| Training Epochs | 80 |
| RGB Clip Length | 64 frames |

---

## Evaluation Protocols

We evaluate models under the following settings:

| Protocol | Description |
|--------|-------------|
| Cross-Subject (LOSO) | Train on 15 subjects, test on 5 unseen subjects |
| Cross-Viewpoint | Train on allocentric gestures, test on egocentric gestures |
| OOD Kinematic | Train on male participants, test on female participants |

---

## Model Performance

| Model | Type | Cross-Subject | Cross-Viewpoint |
|------|------|------|------|
| ST-GCN | Skeleton-based | 91.3 | 68.4 |
| STGT | Skeleton-based | 93.5 | 71.2 |
| 3D ResNet | RGB-based | 89.7 | 60.5 |
| SlowFast | RGB-based | 92.8 | 62.7 |
| **STGT  (Ours)** | Both | **94.1** | **76.5** |

---

## Final Model Used

For training and evaluation of the **Hi-Fi Hands 20/20 dataset**, we primarily used the following model:

```
Spatial Temporal Graph Transformer (STGT)
```

This model operates on **21 3D hand skeletal keypoints** and captures long-range spatial and temporal dependencies between joints, making it suitable for modeling complex hand gesture dynamics.
