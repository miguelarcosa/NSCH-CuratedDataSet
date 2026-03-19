# Child Flourishing Prediction (NSCH 2023)

This repository provides a curated machine-learning-ready dataset derived from the 2023 National Survey of Children's Health (NSCH).

The original data are publicly available from the Data Resource Center for Child and Adolescent Health:
https://www.childhealthdata.org

## Overview

The NSCH is a nationally representative survey that collects information on child health, well-being, and family context in the United States.

However, the raw dataset contains skip patterns, categorical encodings, and survey-specific structures that limit its direct use in machine learning.

This project transforms the original survey data into a structured dataset suitable for predictive modeling and reproducible research.

## Main Contribution

- Construction of a binary flourishing indicator: `flourishing_all4`
- Creation of a clean, machine-learning-ready dataset
- Feature selection using mutual information
- Fully reproducible machine learning pipeline
- Baseline models for benchmarking
- Automatic generation of tables and figures for the associated paper
- Public release of processed data and code

The released dataset is **derived**, not raw, and includes:

- `child_id`
- Target variable (`flourishing_all4`)
- Selected predictor variables
- Survey weights
- Survey design variables

## Repository Structure

- `dataset/`: raw and processed datasets
- `scripts/`: reproducible Python pipeline
- `results/`: model metrics and descriptive outputs
- `figures/`: generated plots (ROC, distributions, heatmaps)
- `tables/`: LaTeX tables generated automatically
- `codebook/`: variable documentation
- `notebooks/`: exploratory analysis

## Dataset Versions

- Full cleaned dataset
- ML-ready dataset
- Strict feature subset (interpretable models)

## Reproducibility

The full pipeline is reproducible and should be executed in the following order:

```bash
python scripts/00_setup_paths.py
python scripts/01_prepare_dataset.py
python scripts/02_build_feature_sets.py
python scripts/03_feature_selection.py
python scripts/04_train_models.py
python scripts/05_export_descriptives.py
python scripts/06_export_paper_tables.py
python scripts/07_compare_weighted_models.py
python scripts/08_state_analysis.py
python scripts/09_export_state_table.py
python scripts/10_export_weighted_comparison_table.py
python scripts/11_export_dataset_flow_figure.py

These scripts perform:
dataset cleaning and preprocessing
construction of ML-ready feature sets
feature selection using mutual information
training of logistic regression and random forest models
descriptive statistics and target distribution analysis
automatic export of LaTeX tables for the paper
comparison between weighted and unweighted models
state-level (geographical) analysis
export of state-level summary tables
export of weighted model comparison tables
generation of the dataset processing flow figure

##Environment
Create the environment with:
conda env create -f environment.yml
conda activate childrens_health_ml

##Data Availability
The raw NSCH dataset is publicly available from:
https://www.childhealthdata.org
The processed machine-learning-ready dataset and all scripts used in this study are available in this repository.

##Citation
If you use this dataset, please cite:
The NSCH dataset (HRSA)
The associated research article (to be added upon publication)

##License
This project uses publicly available data. Please refer to the NSCH data usage terms for restrictions.