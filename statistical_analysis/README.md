# Statistical Analysis

This folder provides the complete supplementary statistical outputs for the study, computed under the **nested cross-validation protocol** described in `../folds/README.md`.

All results are for **3 outer folds × 5 training seeds = 15 fold-seed evaluations** per condition and architecture, unless noted otherwise (the resolution-sensitivity files use 3 seeds × 3 folds = 9).

## Core result tables (per research question)

- **`primary_augmentation_utility_rq1.csv`**
  RQ1: primary augmentation-utility and imbalance-control experiment. Minority-class F1 (mean, SD, 95% CI), macro-F1, PR-AUC, ROC-AUC, precision/recall/specificity, and the baseline-relative delta for every condition (WRS baseline, class-weighted BCE, focal loss, GPT-35, Nano-35, Mixed-70, ROS-35/70, RUS-35/70; the latter four evaluated **without** WRS, under uniform sampling) and both architectures.

- **`source_budget_rq2.csv`**
  RQ2: generator source and augmentation-budget comparison. Same metrics as above for GPT/Nano at N=10/30/35 and the pooled Mixed-source conditions at N=20/60/70 (mixed budgets are **twice** the corresponding per-generator budget, not equal-total-count comparisons).

- **`expert_filtered_rq3.csv`**
  RQ3: downstream utility of expert-filtered augmentation. WRS baseline vs. the expert-filtered GPT Image 1 (N=15) and Nano Banana 2 (N=29) subsets, both architectures.

- **`rq3_disjoint_gpt_approved_vs_rejected.csv`**
  RQ3 secondary/disjoint analysis: the expert-**approved** GPT Image 1 subset (N=15) vs. a count-matched, fully disjoint expert-**rejected** subset (N=15) sampled from the 20 technically screened images the expert did not retain, plus each subset vs. the WRS baseline. Reported for minority-F1, macro-F1, and PR-AUC (DenseNet-121; LMM contrast with 95% CI and paired-t sensitivity check).

## Inferential statistics

- **`lmm_contrasts_f1minor.csv`, `lmm_contrasts_f1macro.csv`, `lmm_contrasts_prauc.csv`**
  Linear mixed-model (LMM) contrasts for minority-F1, macro-F1, and PR-AUC respectively. Model: `metric ~ condition + (1 | outer_fold × seed)`. Each row reports one contrast's LMM coefficient, 95% CI, LMM p-value, and a paired-t sensitivity p-value, organized in blocks: (A) the three pre-specified primary T2I contrasts vs. WRS, (B) exploratory budget/source contrasts vs. WRS, (C) GPT-family/Nano-family/Mixed-family pooled contrasts vs. WRS. Each block is reported separately for DenseNet-121, Swin-Tiny, and the combined (both-architecture) model.

- **`rq2_factorial_source_budget_backbone.csv`**
  Controlled source × budget × backbone factorial analysis (single-source GPT/Nano conditions at N=10/30/35 only; mixed-source excluded because its total budget is not matched to the single-source levels). Likelihood-ratio tests between nested mixed-effects models for the 3-way interaction, each 2-way interaction, and each main effect.

- **`rq2_factorial_additive_model_coefficients.csv`**
  Coefficients of the additive model `delta ~ source + budget + backbone` (the reduced model retained by the factorial analysis above), with 95% CI and p-values for each term.

## Robustness / sensitivity analyses

- **`patient_level_bootstrap.csv`**
  Patient-level paired bootstrap (B=5,000 resamples of the 705 patients, seed-averaged probabilities per patient, **fixed 0.5 decision threshold**, no per-condition threshold optimization). Reports minority-F1, macro-F1, and PR-AUC with bootstrap 95% CIs, and baseline-relative deltas with bootstrap two-sided p-values, for every condition and both architectures. This directly addresses the pseudoreplication concern that the five training seeds within an outer fold share the same held-out test patients.

- **`resolution_sensitivity_summary_all.csv`**
  DenseNet-121 resolution/preprocessing sensitivity: mean ± SD for minority-F1, macro-F1, and PR-AUC at the primary 256×256 setting (n=15) and at 384×768 under two resize strategies, **direct resize / squash** (n=9) and **true aspect-preserving letterbox padding** (n=9), for WRS, GPT-10, GPT-35, ROS-70, and Mixed-70.

- **`resolution_sensitivity_padaspect_contrasts.csv`**
  LMM contrasts vs. the WRS baseline under the true aspect-preserving 384×768 preprocessing only (the literal reading of the aspect-preserving-resizing request).

- **`resolution_sensitivity_squash_vs_padaspect.csv`**
  Direct paired comparison between the two 384×768 resizing strategies (aspect-preserving − direct resize) for each condition, at the same seeds/folds. This isolates whether a condition's apparent resolution-sensitivity result depended on the resizing method itself.

- **`calibration_brier.csv`, `calibration_reliability.csv`**
  Brier score and 10-bin reliability tables (seed-averaged per-patient probabilities), both architectures, all primary/source-budget/expert-filtered conditions.

- **`memorization_audit_gpt.csv`, `memorization_audit_nano.csv`, `memorization_audit_real_pairs.csv`**
  Leakage/memorization audit: real-image near-duplicate screening (perceptual hash + embedding cosine similarity) and synthetic-to-real nearest-neighbor cosine similarity / LPIPS distance / perceptual-hash distance, computed per outer-fold train/val/test partition.

## Notes on the statistical protocol

- The primary outcome is **minority-class F1**; macro-F1 and PR-AUC are reported as complementary outcomes using the same comparison structure.
- The pre-specified primary contrasts are GPT-35, Nano-35, and Mixed-70 vs. the no-synthetic WRS baseline, analyzed **separately** (not pooled into a single aggregate "AUG" contrast, since they differ in generator source and synthetic-data budget).
- The primary inferential model is a linear mixed-effects model with a random intercept for the matched outer-fold × training-seed evaluation unit. Multiple comparisons are controlled with Holm's sequential procedure, applied separately to the pre-specified primary contrasts and to the exploratory comparisons.
- Because the five training-seed repetitions within an outer fold share the same held-out patients, they are not independent patient-level samples. This dependence is examined using the patient-level bootstrap above (fixed threshold, no per-condition threshold search) as the primary sensitivity check.
- Given the limited dataset size, statistical power is inherently limited; results should be interpreted using effect sizes and confidence intervals alongside p-values rather than a single significance threshold.

## Image-quality metrics

Auxiliary Kernel Inception Distance (KID, radiology-domain features) and LPIPS diversity metrics for the technically screened synthetic pools are reported in the manuscript (Table III); the underlying per-pair values are available on request.
