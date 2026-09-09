# Dataset

The underwater polarization dataset used in this project is publicly available from the ZeroDiff-Net repository:

https://github.com/weifeng827/ZeroDiff-Net

In our experiments, 362 original four-angle underwater polarization image groups were used. We randomly selected 72 original image groups as the independent test subset before data augmentation. The remaining 290 original groups were augmented by flipping, resulting in 1160 samples. Among them, 928 samples were used for training and 232 samples were used for validation.

No image group or augmented version from the independent test subset was used during training or validation.
