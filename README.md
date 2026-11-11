# NSCH-Flourishing-ML (NSCH 2023)

Curated machine-learning benchmark derived from the **2023 National Survey of Children's Health (NSCH)** for school-age child flourishing. This release corresponds to the revised manuscript's analytical dataset: **32,934 observations**, **150 selected predictors**, and 5 additional columns (`child_id`, `flourishing_all4`, `FWC`, `STRATUM`, `FIPSST`) for a total of **155 columns**.

## Files included

- `dataset/nsch_2023_ml_ready_strict.csv`: final benchmark dataset (32,934 rows and 155 columns).
- `codebook/codebook_ml_dataset.csv`: variable names, data types, missing counts, and cardinalities. This is a structural codebook, not a full survey-question dictionary.
- `results/analysis_split_assignments.csv`: frozen 70/30 stratified train/test assignments (23,053 / 9,881 records, random seed 42).
- `results/baseline_model_results_summary.csv` and `results/cross_validation_results.csv`: reported model metrics.
- `results/mutual_information_scores.csv`, `results/feature_selection_diagnostics.csv`, and `results/sample_flow_summary.csv`: feature-selection and sample-construction artifacts.
- `scripts/00_setup_paths.py` through `scripts/06_export_paper_tables.py`: preparation, benchmarking, and reporting scripts.
- `environment.yml`: Conda environment specification.

## Install

From the extracted `NSCH-Flourishing-ML` folder:

```bash
conda env create -f environment.yml
conda activate childrens_health_ml
```

## Reproduce the baseline models using the included final dataset

The supplied strict dataset and split assignments allow the baseline model experiments to run **without downloading the raw survey**:

```bash
python scripts/04_train_models.py
```

This command writes model results and cross-validation metrics under `results/`. Training includes a 500-tree random forest and five-fold cross-validation; it may require substantial CPU time.

## Rebuild the final dataset from the original NSCH survey

The raw NSCH 2023 CAHMI topical CSV is **not included** in this ZIP. Obtain the source data through the Data Resource Center, subject to its access and reuse terms:

https://www.childhealthdata.org

Save the raw CSV as:

`dataset/NSCH_2023e_Topical_CAHMI_DRC.csv`

Then run:

```bash
python scripts/00_setup_paths.py
python scripts/01_prepare_dataset.py
python scripts/02_build_feature_sets.py
python scripts/03_feature_selection.py
python scripts/04_train_models.py
python scripts/05_export_descriptives.py
python scripts/06_export_paper_tables.py
```

The scripts create intermediate datasets, descriptive outputs, figures, and LaTeX tables as needed. Generated intermediate files, tables and figures are not included in this minimal release.

## Preprocessing details

Predictors are retained using numerical NSCH survey codes; the baseline scripts do **not** apply one-hot encoding. During model training, blank strings and values coded as `90`, `95`, `97`, `98`, or `99` are converted to missing values, then imputed with `-1`. These transformations are applied when running the scripts; the released CSV preserves its survey-coded feature values. Consult the original NSCH documentation for the intended meaning of each response code, including codes that are not recoded by this pipeline.

The benchmark uses only observations aged 6--17 with valid responses on four flourishing items. The binary target is `flourishing_all4`; 18,990 rows have target 1 and 13,944 have target 0.

## Data provenance and use

Source: 2023 National Survey of Children's Health (NSCH), distributed through the Child and Adolescent Health Measurement Initiative (CAHMI) Data Resource Center. The derived benchmark does not replace the official survey data or documentation. Users should consult the original provider's data-access, citation, and redistribution requirements before using or further sharing the derived CSV.

## Citation

Please cite the source NSCH 2023 survey and the associated NSCH-Flourishing-ML research article when using this benchmark. Consult the published article for its definitive bibliographic information.
