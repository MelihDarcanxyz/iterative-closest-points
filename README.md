# Iterative Closest Point (ICP) Implementation

This repository contains a Python implementation of the Iterative Closest Point (ICP) algorithm for aligning a [SMPL-X model](https://smpl-x.is.tue.mpg.de/) to a 3D point cloud with unknown correspondences. It utilizes [Chamfer Distance](https://pytorch3d.readthedocs.io/en/latest/_modules/pytorch3d/loss/chamfer.html) as loss function, which is a two-way point-to-point distance function. Please check out `main.ipynb` for more descriptive explanation.

## File Structure

```
iterative-closest-points/

├── environment.yml # Conda environment file (see Setup below)
├── main.ipynb
├── models/ # Directory for the body models
│   └── smplx/
│       └── SMPLX_NEUTRAL.npz # SMPL-X neutral pose model file (download from https://smpl-x.is.tue.mpg.de/)
├── outputs/    # example outputs
│   └── icp-convergence-0.gif
│   └── icp-convergence-1.gif
│   └── icp-convergence-2.gif
└── README.md   # This document
```

## Setup

1.  **Clone the Repository:**

    ```bash
    git clone https://github.com/MelihDarcanxyz/iterative-closest-points.git
    cd iterative-closest-points
    ```

2.  **Create Conda Environment:**

    It is highly recommended to use a Conda environment for managing dependencies. This ensures reproducibility and avoids conflicts with other Python projects.

    ```bash
    conda env create -f environment.yml
    conda activate icp
    ```

## Results

### Successful Convergences

![ICP Convergence Example](outputs/icp-convergence-0.gif)
![ICP Convergence Example](outputs/icp-convergence-1.gif)
![ICP Convergence Example](outputs/icp-convergence-2.gif)

### Failed Convergences

Experimenting with more sophisticated learning rate scheduling techniques, such as cyclical learning rates or adaptive learning rates, could lead to faster and more stable convergence.

Additionally, incorporating surface normals into the loss function, where we can understand the orientation of points, can provide valuable geometric information and potentially improve alignment accuracy, encouraging the aligned point clouds to not only be close in position but also in orientation.

![ICP Convergence Example](outputs/icp-convergence-3.gif)
![ICP Convergence Example](outputs/icp-convergence-4.gif)

## Future Work

- [ ] Point to plane distance implementation
- [ ] Experiment with normal distances
- [ ] Failed convergence detection (loss > `$THRESHOLD`) and restarting with different learning rate schedules. `$THRESHOLD` is empirically `5e-5`.
