# License

Copyright (C) 2023 Li Peng (plpeng@hnu.edu.cn), Cheng Yang (yangchengyjs@163.com)

This program is free software; you can redistribute it and/or
modify it under the terms of the GNU General Public License
as published by the Free Software Foundation; either version 3
of the License, or (at your option) any later version.

This program is distributed in the hope that it will be useful,
but WITHOUT ANY WARRANTY; without even the implied warranty of
MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.  See the
GNU General Public License for more details.

You should have received a copy of the GNU General Public License
along with this program; if not, see <http://www.gnu.org/licenses/>.



# MRLHGNN
MRLHGNN is effective tool for drug repositioning and we are thankful that [Gu et al.](https://www.sciencedirect.com/science/article/pii/S0010482522008356) have published part of their data which can be used directly.



# Environment Requirement
+ torch version (GPU) == 2.0.1
+ CUDA version == 12.0
+ numpy == 1.34.3
+ matplotlib == 3.5.1
+ dgl-cu118 == 1.1.0
+ pandas == 1.5.3
+ scikit-learn == 1.2.2
+ torch-cluster == 1.6.1+pt20cu118
+ torch-scatter == 2.1.1+pt20cu118
+ torch-sparse == 0.6.17+pt20cu118
+ torch-spline-conv == 1.2.2+pt20cu118
+ torchaudio ==2.0.2
+ torchvision == 0.15.2



# Model
+ load_data.py: Constructing heterogeneous graph.
+ SeHG.py: the core model proposed in the paper.



# Compare_models
 
* NTSIM (2017)
    * Proposed in [Predicting drug-disease associations based on the known association bipartite network](https://ieeexplore.ieee.org/abstract/document/8217698/), BIBM 2017.

* BNNR (2019)
    * Proposed in [Drug repositioning based on bounded nuclear norm regularization](https://doi.org/10.1093/bioinformatics/btz331), Bioinformatics 2019.

* HGIMC (2020)
    * Proposed in [Heterogeneous graph inference with matrix completion for computational drug repositioning](https://doi.org/10.1093/bioinformatics/btaa1024), Bioinformatics 2020.

* NIMCGCN (2020)
    * Proposed in [Neural inductive matrix completion with graph convolutional networks for miRNA-disease association prediction](https://doi.org/10.1093/bioinformatics/btz965), Bioinformatics 2020.

* LAGCN (2021)
    * Proposed in [Predicting drug–disease associations through layer attention graph convolutional network](https://doi.org/10.1093/bib/bbaa243), Briefings in Bioinformatics 2021.

* DRHGCN (2021)
    * Proposed in [Drug repositioning based on the heterogeneous information fusion graph convolutional network](https://doi.org/10.1093/bib/bbab319), Briefings in Bioinformatics 2021.

* DRWBNCF (2022)
    * Proposed in [A weighted bilinear neural collaborative filtering approach for drug repositioning](https://doi.org/10.1093/bib/bbab581), Briefings in Bioinformatics 2022.

* REDDA (2022)
    * Proposed in [REDDA: Integrating multiple biological relations to heterogeneous graph neural network for drug-disease association prediction](https://www.sciencedirect.com/science/article/pii/S0010482522008356), Computers in Biology and Medicine 2022.

* MilGNet (2022)
    * Proposed in [MilGNet: a multi-instance learning-based heterogeneous graph network for drug repositioning](https://ieeexplore.ieee.org/abstract/document/9995152/), BIBM 2022.



# Question
+ If you have any problems or find mistakes in this code, please contact with us: 
Cheng Yang: yangchengyjs@163.com ; Li Peng: plpeng@hnu.edu.cn

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

| Metric | Result |
|---|---:|
| AUC | 0.9574 |
| AUPR | 0.5743 |
| F1 | 0.6530 |
| Accuracy | 0.9948 |
| Recall | 0.7396 |
| Specificity | 0.9965 |
| Precision | 0.5845 |

The reproduced AUC (0.9574) is close to the AUC reported in the original paper (0.9585).

### Planned Extension

The reproduced MRLHGNN model will be used as the baseline for the BTP extension.

Planned work includes:

- Similarity leakage analysis
- Time-aware extension
- Conformal Prediction for uncertainty quantification
- Calibration comparison
- Reliability and coverage evaluation

