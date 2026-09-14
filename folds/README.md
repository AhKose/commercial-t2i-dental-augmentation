# Fold Partitions (Nested Cross-Validation Protocol)

This folder contains the fixed patient-level **nested** cross-validation partitions used in the impacted-teeth classification experiments.

## Protocol

Hyperparameter tuning is kept fully isolated from the outer test partitions through a **nested 3-fold cross-validation** scheme with a dedicated inner hyperparameter-search stage:

1. The 705 patients are partitioned into **3 mutually exclusive, stratified outer folds** (`outer_fold_0.json`, `outer_fold_1.json`, `outer_fold_2.json`). Each patient serves as an outer test case exactly once.
2. For each outer fold, hyperparameter optimization (Optuna, 25 trials) is performed **exclusively within that outer fold's development data**, using a 2-fold **inner** cross-validation split (the `inner` field inside each outer-fold file). The outer test partition is never accessed during this stage.
3. After hyperparameter selection, the same outer development set is further split with a fixed stratified 85/15 division into 399 training and 71 validation patients (`train` / `val` fields), used for final model fitting, early stopping, checkpoint selection, and decision-threshold selection. This split is fixed across all five training seeds within an outer fold.
4. The selected hyperparameters for each architecture and outer fold are recorded separately in `hp_search_<arch>_outer<k>.json`.

The outer test partition (`test` field) is never used for tuning, early stopping, checkpoint selection, or threshold optimization. It is used only for final evaluation.

## Files

- **`outer_fold_0.json`, `outer_fold_1.json`, `outer_fold_2.json`**
  One file per outer fold. Each contains:
  - `disease`: target condition used for the task (`Impacted`).
  - `outer_fold`: outer-fold index (0–2).
  - `master_seed`: seed used for the partitioning procedure.
  - `scheme`: short description of the nested protocol.
  - `train` / `val`: the fixed 399/71 final training/validation split for this outer fold (image lists + class distribution).
  - `test`: the held-out outer test partition for this fold (never used for tuning).
  - `inner`: the 2-fold inner cross-validation split of the outer development set, used exclusively for hyperparameter search.

  Each image entry includes:
  - `image_id`: original DENTEX image identifier.
  - `file_name`: original dataset file name.
  - `has_impacted`: binary label used in this study.
  - `has_caries`: additional annotation retained from the source metadata (not used in this task).

- **`hp_search_densenet121_outer{0,1,2}.json`, `hp_search_swin_tiny_outer{0,1,2}.json`**
  The Optuna hyperparameter-search outcome for each architecture and outer fold: the selected hyperparameters (`lr_backbone`, `lr_head`, `weight_decay`, `dropout`, `label_smooth`), the best mean inner-fold validation macro-F1, and the per-inner-fold validation scores.

## Training seeds

Within each outer fold, model training was repeated using five random seeds. Patient membership in the train/validation/test partitions above remains **fixed** across all five seeds; the seeds vary model initialization, minibatch sampling, training-time augmentation stochasticity, and (for synthetic conditions using fewer than the full synthetic pool) synthetic subset selection. This gives 3 outer folds × 5 seeds = 15 fold-seed evaluations per condition and architecture.

## Notice

The original DENTEX images are not redistributed in this repository. Obtain them from the official source: S. Er, "DENTEX Challenge 2023," Zenodo, 2023, doi: 10.5281/zenodo.7812323.
