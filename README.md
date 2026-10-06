## Reproduction & Modifications

This repository contains modifications made while reproducing the original MRLHGNN implementation for the BTP project.

### Issues Found and Changes Made

#### 1. Missing `load_D3()` Function

The original `main.py` imported and called `load_D3()`.

The function was not present in `load_data.py`.

The implementation was changed to use the available `load()` function instead.

#### 2. Missing Dataset3 Input

`main.py` expected:

    dataset/Dataset3/mat_Drug_Disease.csv

This file was not present in the repository.

The existing `dataset/KFCdataset_baseline.csv` was used to create the required file:

    dataset/Dataset3/mat_Drug_Disease.csv

No new dataset was generated.

#### 3. Incorrect Model Function Call

The original training code passed additional arguments to the model:

    model(g, feature, metapath_list, epoch, fold)

However, `SeHG_bio.forward()` accepts:

    model(g, feature, metapath_list)

The extra arguments were removed.

### Environment

The reproduction was performed using:

- WSL2 Ubuntu
- Python 3.10.12
- PyTorch 2.0.1+cu118
- DGL 1.1.0+cu118
- NVIDIA RTX 3050 Laptop GPU (4 GB)

CUDA execution and the MRLHGNN forward pass were successfully verified.

### Baseline Reproduction

A complete 5-fold training run was successfully executed.

| Metric      | Result |
|  ---        |   ---  |
| AUC         | 0.9574 |
| AUPR        | 0.5743 |
| F1          | 0.6530 |
| Accuracy    | 0.9948 |
| Recall      | 0.7396 |
| Specificity | 0.9965 |
| Precision   | 0.5845 |

The reproduced AUC (0.9574) is close to the AUC reported in the original paper (0.9585).

### Planned Extension

The reproduced MRLHGNN model will be used as the baseline for the BTP extension.

Planned work includes:

- Similarity leakage analysis
- Time-aware extension
- Conformal Prediction for uncertainty quantification
- Calibration comparison
- Reliability and coverage evaluation

