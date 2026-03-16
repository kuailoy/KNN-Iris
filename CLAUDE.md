# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

KNN-based classification model for the Iris dataset. The pipeline covers preprocessing, data splitting, model training/tuning, and evaluation.

**Deadlines:**
- Development: 22/3/2026
- Report: 27/3/2026 (Dong & All)
- Presentation: 31/3/2026 (Yiming & All)

## Running Notebooks

Run notebooks in this order — each depends on outputs from the previous:

```bash
jupyter notebook          # open Jupyter in browser
# or
jupyter nbconvert --to notebook --execute preprocessing.ipynb --inplace
jupyter nbconvert --to notebook --execute data_splitting.ipynb --inplace
jupyter nbconvert --to notebook --execute main.ipynb --inplace
```

## Pipeline Architecture

All work is in Jupyter notebooks. Data flows sequentially:

1. **`preprocessing.ipynb`** — loads `data/iris_with_missing.csv`, handles missing values (mean imputation for numerics, mode for categoricals), label-encodes the `class` column (setosa=0, versicolor=1, virginica=2), standardizes features with `StandardScaler`, saves `data/iris_preprocessed.csv` (standardized features + `label` column).

2. **`data_splitting.ipynb`** — loads `data/iris_preprocessed.csv`, splits into train/test (currently 80/20 stratified; README specifies 70/15/15 train/val/test — this needs updating), saves `data/X_train.csv`, `data/X_test.csv`, `data/y_train.csv`, `data/y_test.csv`.

3. **`main.ipynb`** — (empty, to be implemented) KNN training with k∈{3,5,7}, distance metrics (Euclidean, Manhattan), evaluation with accuracy/precision/recall/F1/ROC-AUC, and leave-one-out cross-validation.

## Data

- `data/iris_with_missing.csv` — raw 150-sample Iris dataset with 2 introduced missing values (sepal length, sepal width)
- `data/iris_preprocessed.csv` — standardized features with integer label column

## Key Implementation Notes

- The split in `data_splitting.ipynb` is currently 80/20; the spec requires **70% train / 15% validation / 15% test** — needs a second split to create a validation set.
- `main.ipynb` is empty and needs the full KNN implementation per the README spec.
- Feature columns in preprocessed data: `sepal length_std`, `sepal width_std`, `petal length_std`, `petal width_std`, `label`.
