# Statistical Analysis

This folder provides the inferential statistical analyses for the study, computed under the nested cross-validation protocol described in `../folds/README.md`. Descriptive result tables (the measured metrics themselves) are kept separately in `../results/`.

All results are for 3 outer folds x 5 training seeds = 15 fold-seed evaluations per condition and architecture, unless noted otherwise (the resolution-sensitivity file uses 3 seeds x 3 folds = 9).

## Primary contrasts

- **`lmm_contrasts_f1minor.csv`, `lmm_contrasts_f1macro.csv`, `lmm_contrasts_prauc.csv`**
  Linear mixed-model (LMM) contrasts for minority-F1, macro-F1, and PR-AUC respectively. Model: `metric ~ condition + (1 | outer_fold x seed)`. Each row reports one contrast's LMM coefficient, 95% CI, LMM p-value, and a paired-t sensitivity p-value, organized in blocks: (A) the three pre-specified primary T2I contrasts vs. WRS, (B) exploratory budget/source contrasts vs. WRS, (C) GPT-family/Nano-family/Mixed-family pooled contrasts vs. WRS. Each block is reported separately for DenseNet-121, Swin-Tiny, and the combined (both-architecture) model.

- **`rq3_disjoint_gpt_approved_vs_rejected.csv`**
  RQ3 secondary/disjoint analysis: the expert-approved GPT Image 1 subset (N=15) vs. a count-matched, fully disjoint expert-rejected subset (N=15) sampled from the 20 technically screened images the expert did not retain, plus each subset vs. the WRS baseline. Reported for minority-F1, macro-F1, and PR-AUC (DenseNet-121; LMM contrast with 95% CI and paired-t sensitivity check).

## RQ2 factorial analysis

- **`rq2_factorial_source_budget_backbone.csv`**
  Controlled source x budget x backbone factorial analysis (single-source GPT/Nano conditions at N=10/30/35 only; mixed-source excluded because its total budget is not matched to the single-source levels). Likelihood-ratio tests between nested mixed-effects models for the 3-way interaction, each 2-way interaction, and each main effect.

- **`rq2_factorial_additive_model_coefficients.csv`**
  Coefficients of the additive model `delta ~ source + budget + backbone` (the reduced model retained by the factorial analysis above), with 95% CI and p-values for each term.

## Sensitivity analyses

- **`patient_level_bootstrap.csv`**
  Patient-level paired bootstrap (B=5,000 resamples of the 705 patients, seed-averaged probabilities per patient, fixed 0.5 decision threshold, no per-condition threshold optimization). Reports minority-F1, macro-F1, and PR-AUC with bootstrap 95% CIs, and baseline-relative deltas with bootstrap two-sided p-values, for every condition and both architectures. This directly addresses the pseudoreplication concern that the five training seeds within an outer fold share the same held-out test patients.

- **`resolution_sensitivity_padaspect_contrasts.csv`**
  LMM contrasts vs. the WRS baseline under the 384x768 true aspect-preserving preprocessing (DenseNet-121).

## Notes on the statistical protocol

- The primary outcome is minority-class F1; macro-F1 and PR-AUC are reported as complementary outcomes using the same comparison structure.
- The pre-specified primary contrasts are GPT-35, Nano-35, and Mixed-70 vs. the no-synthetic WRS baseline, analyzed separately (not pooled into a single aggregate "AUG" contrast, since they differ in generator source and synthetic-data budget).
- The primary inferential model is a linear mixed-effects model with a random intercept for the matched outer-fold x training-seed evaluation unit. Multiple comparisons are controlled with Holm's sequential procedure, applied separately to the pre-specified primary contrasts and to the exploratory comparisons.
- Because the five training-seed repetitions within an outer fold share the same held-out patients, they are not independent patient-level samples. This dependence is examined using the patient-level bootstrap above (fixed threshold, no per-condition threshold search) as the primary sensitivity check.
- Given the limited dataset size, statistical power is inherently limited; results should be interpreted using effect sizes and confidence intervals alongside p-values rather than a single significance threshold.
