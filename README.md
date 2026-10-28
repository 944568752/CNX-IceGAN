# CNX-IceGAN

## Paper

**Monocular image segmentation and perspective-corrected load estimation for asymmetrically iced transmission lines**

Chengqi Liu, Zonghan Yang, Yali Wu, Xiaoyan Xiong, and Dongguang Zhang

This repository accompanies the manuscript and provides an overview of the proposed method and its reported results.

## Overview

Estimating transmission-line icing loads from a single image is challenging because longitudinal camera views introduce perspective-dependent scaling and asymmetric ice accretion produces overhanging icicles. This work combines semantic segmentation, vanishing-point calibration, and morphology-guided volume integration to estimate icing loads from monocular images.

The framework extracts the iced-conductor mask, compensates for spatial scale variation, and separately estimates the volumes of the main ice body and icicle branches. The resulting volume estimates are used to calculate the vertical load per unit length and equivalent icing thickness.

## Method

1. **Fine icing segmentation.** CNX-IceGAN uses CNX-IceNet as its generator, combining a ConvNeXt V2 encoder, Coordinate Attention, and PixelShuffle decoding. A conditional PatchGAN discriminator provides adversarial supervision to improve mask boundaries and slender icicle details.
2. **Perspective correction.** A position-dependent scale derived from the conductor vanishing point accounts for perspective variation in longitudinal views.
3. **Morphology-guided load estimation.** Skeleton analysis separates the main ice body from overhanging icicles. Slice integration estimates their volumes, while boundary truncation reduces double counting at their intersections. The estimated volumes are then converted into physical load and equivalent icing thickness.

## Reported Results

The following results are reported in the manuscript.

### Segmentation

The dataset contains **1,479 icing images**.

| Model | MPA (%) | mIoU (%) | F1-score (%) |
| --- | ---: | ---: | ---: |
| U-Net | 88.12 | 87.52 | 88.33 |
| MobileNet V3 | 91.32 | 90.21 | 90.63 |
| ResNet50 | 90.45 | 89.87 | 90.21 |
| DeepLabV3+ | 91.50 | 90.63 | 91.75 |
| **CNX-IceGAN** | **95.83** | **94.79** | **95.84** |

CNX-IceGAN improves mIoU over DeepLabV3+ by **4.16 percentage points** on the reported dataset.

### Load Estimation

The method was evaluated on **nine artificial-icing samples** and **ten observation-station cases**. Load estimates differed from reference values by **less than 10%** in these validation cases.

Load estimates depend on geometric calibration, cross-sectional assumptions, and ice density. The limited number of load-validation cases warrants further evaluation across additional icing events and camera configurations.

## Code Availability

This repository currently provides the project overview and reported results.

The code will be released as open source upon acceptance of the paper.
