# Results

This folder contains the measured outcome data for the study, computed under the nested cross-validation protocol described in `../folds/README.md`. All results are for 3 outer folds x 5 training seeds = 15 fold-seed evaluations per condition and architecture, unless noted otherwise.

Inferential/statistical testing of these results (LMM contrasts, factorial analysis, bootstrap significance checks) is kept separately in `../statistical_analysis/`.

## Primary result tables

- **`primary_augmentation_utility_rq1.csv`**
  RQ1: primary augmentation-utility and imbalance-control experiment. Minority-class F1 (mean, SD, 95% CI), macro-F1, PR-AUC, ROC-AUC, precision/recall/specificity, and the baseline-relative delta for every condition (WRS baseline, class-weighted BCE, focal loss, GPT-35, Nano-35, Mixed-70, ROS-35/70, RUS-35/70; the latter four evaluated without WRS, under uniform sampling) and both architectures.

- **`source_budget_rq2.csv`**
  RQ2: generator source and augmentation-budget comparison. Minority-F1, macro-F1, and PR-AUC (each with mean, SD, and 95% CI), ROC-AUC, precision/recall/specificity, and the baseline-relative delta and paired-t p-value for every metric, for GPT/Nano at N=10/30/35 and the pooled Mixed-source conditions at N=20/60/70 (mixed budgets are twice the corresponding per-generator budget, not equal-total-count comparisons).

- **`expert_filtered_rq3.csv`**
  RQ3: downstream utility of expert-filtered augmentation. WRS baseline vs. the expert-filtered GPT Image 1 (N=15) and Nano Banana 2 (N=29) subsets, both architectures.

## Secondary metrics

- **`secondary_metrics_confusion_matrix.csv`**
  Accuracy and ROC-AUC (mean, SD) and confusion-matrix counts (mean TP/FP/TN/FN, validation-optimal threshold) for every condition in the tables above, both architectures.

- **`calibration_brier.csv`, `calibration_reliability.csv`**
  Brier score and 10-bin reliability tables (seed-averaged per-patient probabilities), both architectures, all primary/source-budget/expert-filtered conditions.

## Sensitivity and audit results

- **`severe_imbalance_summary.csv`**
  Supplementary severe class-imbalance experiment (DenseNet-121). Within each outer-fold training partition, the real impacted class was subsampled to approximately 5:1 and 10:1 non-impacted:impacted (51 and 26 real impacted patients, from 143–144), while the validation and outer-test partitions were left unchanged at the natural ratio. The subsample is fixed per outer fold × seed and shared by all conditions, and the 10:1 subset is nested in the 5:1 subset. WRS, GPT-35, Nano-35, and ROS-35 (uniform sampling, as in the primary analysis) were re-trained with the same fold-specific hyperparameters and protocol. Minority-F1, macro-F1, and PR-AUC (mean, SD; 15 outer-fold × seed evaluations) and `n_minority_train` (median minority-class training samples after balancing, i.e. real impacted plus synthetic images or ROS duplicates) are reported for each training ratio, with the natural-ratio (1.78:1) results from the primary analysis included as a reference. At 10:1, ROS-35 can duplicate at most the 26 available real impacted patients.

- **`resolution_sensitivity.csv`**
  DenseNet-121 minority-F1, macro-F1, and PR-AUC (mean, SD) at the primary 256x256 setting (n=15) and at 384x768 with true aspect-preserving letterbox padding (n=9), for WRS, GPT-10, GPT-35, ROS-70, and Mixed-70.

- **`memorization_audit_gpt.csv`, `memorization_audit_nano.csv`, `memorization_audit_real_pairs.csv`**
  Leakage/memorization audit: real-image near-duplicate screening (perceptual hash and embedding cosine similarity) and synthetic-to-real nearest-neighbor cosine similarity, LPIPS distance, and perceptual-hash distance, computed per outer-fold train/val/test partition. See `memorization_audit_methodology.md` for the full methodology and the verified reference numbers (real-real cosine p95 threshold, near-duplicate check, train-vs-test comparison) behind these files.
