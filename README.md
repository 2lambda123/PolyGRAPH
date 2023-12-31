# Graph neural networks for efficient learning of mechanical properties of polycrystals

<img src="title.png" width=100% height=100%>

This repository holds the data and code required to reproduce results presented in *"Graph neural networks for efficient learning of
mechanical properties of polycrystals"*.

```
@article{HESTROFFER2023,
title = {Graph neural networks for efficient learning of mechanical properties of polycrystals},
journal = {Computational Materials Science},
volume = {217},
pages = {111894},
year = {2023},
issn = {0927-0256},
doi = {https://doi.org/10.1016/j.commatsci.2022.111894},
url = {https://www.sciencedirect.com/science/article/pii/S092702562200605X},
author = {Jonathan M. Hestroffer and Marie-Agathe Charpagne and Marat I. Latypov and Irene J. Beyerlein},
}
```

## Setup
Install dependencies. Please note that installing [PyTorch](https://pytorch.org/get-started/locally/) and [PyTorchGeometric](https://pytorch-geometric.readthedocs.io/en/latest/notes/installation.html) will be more involved and custom to your machine/GPU. See links provided.
```bash
pip install -r requirements.txt
```

## Create Graphs
Generate microstructure graphs for all representative volume elements (RVEs).
```bash
python create_graphs.py
```

## Prepare Data
Assemble graphs and rve mechanical response into PyTorch datalists.
```bash
python write_data.py
```

## Run Model Evaluations
The different evaluations presented in the original paper are:
  1. 10-fold cross-validation of texture groups (A-G)
  2. Train (A-G) / Test (A-G)
  3. Train (A-G) / Test (H-L)
  4. 5-fold reduced data 'psuedo cross-validation', Train (A-G) / Test (H-L)
  
For each evaluation, loss histories, parity plots, and model checkpoints are outputted.

```
Usage: python model.py [OPTIONS]
Options:
  --eval INT                   Evaluation number (e.g., 1 - 4, default: 1)
  --prop STRING                Material property of interest (stiffness/strength, default: stiffness)
  --config INT                 Hyper-parameter configuration number (default: 0)
  --config_dir PATH            Directory with hyper-parameter configuration .jsons (default: ./config/)
  --output_dir PATH            Output directory (default: ./config/)
  --seed INT                   Random seed (default: 42)
```

