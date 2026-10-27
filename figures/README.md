# Figures

Supplementary figure(s) referenced in the manuscript and repository documentation.

- **`figure4_forest_primary_lmm_contrasts.png` / `.pdf`**
  Manuscript Figure 4. Forest plot of the LMM-estimated differences in minority-class F1 between the primary commercial T2I augmentation conditions (GPT-35, Nano-35, Mixed-70) and the no-synthetic WRS baseline, reported separately for DenseNet-121, Swin-Tiny, and the combined (both-architecture) model. Points show the coefficient estimate; horizontal bars show the 95% confidence interval; the vertical dashed line marks no difference from baseline. Values correspond to `../statistical_analysis/lmm_contrasts_f1minor.csv` (block A).

- **`dataset/`**
  Dataset visualizations: real and synthetic example radiographs, patient-level class distribution per outer fold, impacted-tooth counts and FDI positions, and a feature-space PCA of real vs. synthetic images. See `dataset/README.md`.

- **`severe_imbalance_minority_f1.png` / `.pdf`**
  Supplementary severe class-imbalance experiment (DenseNet-121). Minority-class F1 (mean ± SD over 15 outer-fold × seed evaluations) for WRS, GPT-35, Nano-35, and ROS-35 at the natural training imbalance (1.78:1) and after subsampling the real impacted class in the training partitions to approximately 5:1 and 10:1. Values correspond to `../results/severe_imbalance_summary.csv`.
