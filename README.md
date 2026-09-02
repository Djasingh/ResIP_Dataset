# Researcher Influence Prediction (ResIP) — Dataset

This repository contains the dataset used to train and evaluate the models proposed in:

> **Researcher influence prediction (ResIP) using academic genealogy network**
> Dhananjay Kumar, Plaban Kumar Bhowmick, Jiaul H. Paik
> *Journal of Informetrics*, Volume 17, Issue 2, Article 101392 (2023)
> [https://doi.org/10.1016/j.joi.2023.101392](https://doi.org/10.1016/j.joi.2023.101392)

## Overview

The dataset supports the **Researcher Influence Prediction (ResIP)** task — predicting a researcher's future influence in an academic field by modelling the growth of their academic lineage (family graph/tree) over time. It was built from a subset of researchers drawn from the Mathematics Genealogy Project (MGP).

## Getting Started

Unzip the dataset archive:

```bash
tar -xvjf dataset.tar.bz2
```

The extracted folder contains multiple **NumPy** and **pickle** files, one set per method proposed in the paper.

## File Naming

File names indicate which method/dataset they correspond to:

| Method | Description |
|---|---|
| `ResIP-M1` | Single-point output prediction |
| `ResIP-M2` | Output sequence prediction |
| `ResIP-M3` | Identified by `"ResIP-M3"` in the file name |

## Data Format

### ResIP-M1 and ResIP-M2

The train and test data for these methods are stored as tuples containing:

- **Input** — sequence of embedding vectors for the researchers in the family graph/tree
- **Output**:
  - **ResIP-M1** — a single output value (single time-point prediction)
  - **ResIP-M2** — an output sequence (multi time-point prediction)

### ResIP-M3

Data files are identified by the `"ResIP-M3"` substring in their file name.

### Common Notes

- **Input:** A sequence of embedding vectors representing the researchers in the family graph/tree at a given time point.
- **Output:** The family size during the prediction period.
- **Scaling:** Output values are **not pre-scaled**. Apply a **log2 transformation** to the output before use.

## Loading the Data

Example of loading a NumPy or pickle file:

```python
import numpy as np
import pickle

# NumPy files
data = np.load("path/to/file.npy", allow_pickle=True)

# Pickle files
with open("path/to/file.pkl", "rb") as f:
    data = pickle.load(f)
```

Remember to apply the log2 transformation to output values before scoring or evaluation:

```python
transformed_output = np.log2(output)
```

## Citation

If you use this dataset, please cite:

```bibtex
@article{kumar2023resip,
  title   = {Researcher influence prediction ({ResIP}) using academic genealogy network},
  author  = {Kumar, Dhananjay and Bhowmick, Plaban Kumar and Paik, Jiaul H.},
  journal = {Journal of Informetrics},
  volume  = {17},
  number  = {2},
  pages   = {101392},
  year    = {2023},
  doi     = {10.1016/j.joi.2023.101392}
}
```

## License

Specify license here.
