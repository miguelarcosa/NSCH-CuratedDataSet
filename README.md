# Child Flourishing Prediction (NSCH 2023)

This repository contains a curated machine-learning-ready dataset derived from the 2023 National Survey of Children's Health (NSCH).

The project builds a binary target variable, `flourishing_all4`, indicating whether a child meets four flourishing indicators based on NSCH survey items.

## Repository structure

- `dataset/`: raw and processed datasets
- `scripts/`: reproducible preprocessing, feature selection, training, and descriptive analysis scripts
- `results/`: model performance metrics, feature rankings, and summary statistics
- `figures/`: generated figures
- `codebook/`: dataset documentation
- `notebooks/`: exploratory notebook version of the workflow

## Main outputs

- Cleaned survey-derived dataset
- Machine-learning-ready dataset versions
- Mutual information feature ranking
- Logistic regression and random forest baselines
- Weighted vs. unweighted model comparison
- Cross-validation performance
- Descriptive statistics and target distribution
- Correlation heatmap
- Codebook for released variables

## Reproducibility

Run the scripts in the following order:

1. `python scripts/01_prepare_dataset.py`
2. `python scripts/02_build_feature_sets.py`
3. `python scripts/02_feature_selection.py`
4. `python scripts/03_train_models.py`
5. `python scripts/05_export_descriptives.py`

## Environment

Create the environment with:

```bash
conda env create -f environment.yml
conda activate childrens_health_ml