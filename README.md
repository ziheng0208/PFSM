# PFSM

PFSM is a PyTorch implementation of a polarization-aware frequency-decoupled state space model for underwater polarization image restoration.

The model takes four RGB polarization observations as a 12-channel tensor and restores the corresponding four-angle polarization images. The main components include:

- Spatial polarization transformation for Stokes-, DoLP-, and AoP-related feature extraction.
- Wavelet-based frequency decomposition for low-frequency appearance recovery and high-frequency structure restoration.
- State-space feature modeling for efficient long-range contextual interaction.
- Dual-domain adaptive fusion for spatial-frequency feature alignment.

## Environment

Install the dependencies with:

```bash
pip install -r requirements.txt
```

The state-space branch requires `mamba-ssm`. Please install a version compatible with your CUDA and PyTorch environment.


## Dataset

The underwater polarization dataset used in this paper is publicly available from the ZeroDiff-Net repository:

https://github.com/weifeng827/ZeroDiff-Net/blob/main/README.md

In this work, we use the complete tank scene dataset with ground-truth references provided in the  dataset link of ZeroDiff-Net. The dataset contains 362 original four-angle polarization image groups. We randomly select 72 original image groups as the independent test subset before data augmentation. The remaining 290 image groups are used for training and validation. Horizontal and vertical flipping are applied only to the non-test samples, producing 1160 augmented samples, among which 928 and 232 samples are used for training and validation, respectively. No test image or its augmented variants are included in the training or validation subsets.

Please organize the downloaded dataset according to the folder structure below before training and testing.

The training and validation data are expected to follow this folder structure:

```text
data/
├── train/
│   ├── I1/
│   ├── I2/
│   ├── I3/
│   ├── I4/
│   ├── T1/
│   ├── T2/
│   ├── T3/
│   └── T4/
└── test/
    └── validation/
        ├── I1/
        ├── I2/
        ├── I3/
        ├── I4/
        ├── T1/
        ├── T2/
        ├── T3/
        └── T4/
```

`I1` to `I4` are degraded four-angle polarization observations, and `T1` to `T4` are the corresponding reference images.

## Training

```bash
python train.py --dataset_path ./data/train --img_width 512 --img_height 512 --batch_size 4
```

Checkpoints and validation results are saved under `experiments/PFSM/`.

## Testing

```bash
python test.py --dataset_path ./data/test --sub_dir validation --checkpoint ./checkpoints/pfsm.pth --save_dir ./results/pfsm_test
```

## Complexity Analysis

```bash
python scripts/compute_model_complexity.py --input-channels 12 --height 512 --width 512
```


