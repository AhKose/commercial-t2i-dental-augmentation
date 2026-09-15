# Statistical Analysis

This folder provides the inferential statistical analyses for the study, computed under the nested cross-validation protocol described in `../folds/README.md`. Descriptive result tables (the measured metrics themselves) are kept separately in `../results/`.

All results are for 3 outer folds x 5 training seeds = 15 fold-seed evaluations per condition and architecture, unless noted otherwise (the resolution-sensitivity file uses 3 seeds x 3 folds = 9).

## Primary contrasts

- **`lmm_contrasts_f1minor.csv`, `lmm_contrasts_f1macro.csv`, `lmm_contrasts_prauc.csv`**
  Linear mixed-model (LMM) contrasts for minority-F1, macro-F1, and PR-AUC respectively. Model: `metric ~ condition + (1 | outer_fold x seed)`. Each row reports one contrast's LMM coefficient, 95% CI, LMM p-value, and a paired-t sensitivity p-value, organized in blocks: (A) the three pre-specified primary T2I contrasts vs. WRS, (B) exploratory budget/source contrasts vs. WRS, (C) GPT-family/Nano-family/Mixed-family pooled contrasts vs. WRS. Each block is reported separately for DenseNet-121, Swin-Tiny, and the combined (both-architecture) model.

- **`rq3_disjoint_gpt_approved_vs_rejected.csv`**
  RQ3 secondary/disjoint analysis: the expert-approved GPT Image 1 subset (N=15) vs. a count-matched, fully disjoint expert-rejected subset (N=15) sampled from the 20 technically screened images the expert did not retain, plus each subset vs. the WRS baseline. Reported for minority-F1, macro-F1, and PR-AUC (DenseNet-121; LMM contrast with 95% CI and paired-t sensitivity check).

- **`single_source_budget_contrasts.csv`**
  Condition-specific exploratory contrasts vs. WRS for each single-source budget condition (GPT-10/30/35, Nano-10/30/35) individually, minority-F1, DenseNet-121/Swin-Tiny/combined. Each row reports the LMM delta and 95% CI, the raw LMM p-value, a Holm-adjusted p-value, and the patient-level bootstrap delta/CI/p as an independence-robust cross-check. GPT-10 is the one condition with a raw and Holm-adjusted p below .05 (DenseNet-121 only); it is reported in the manuscript as a non-replicating exploratory finding, since it is not significant in Swin-Tiny and does not hold up under the patient-level bootstrap. Holm correction for GPT-10/GPT-30/Nano-10/Nano-30 is applied within that 4-condition exploratory family; GPT-35/Nano-35 are the pre-specified primary contrasts, already Holm-corrected within their own 3-condition family (see Table VII / `lmm_contrasts_f1minor.csv` block A). No pooled/aggregate baseline is used in this file; every row is a single named condition vs. WRS.

## RQ2 factorial analysis

- **`rq2_factorial_source_budget_backbone.csv`**
  Controlled source x budget x backbone factorial analysis (single-source GPT/Nano conditions at N=10/30/35 only; mixed-source excluded because its total budget is not matched to the single-source levels). Likelihood-ratio tests between nested mixed-effects models for the 3-way interaction, each 2-way interaction, and each main effect.

- **`rq2_factorial_full_model_coefficients.csv`**
  Coefficients of the full model `delta ~ source * budget * arch` (every main effect and interaction term), with 95% CI and p-values.

- **`rq2_factorial_additive_model_coefficients.csv`**
  Coefficients of the additive model `delta ~ source + budget + backbone` (the reduced model retained by the factorial analysis above, since no interaction term was significant), with 95% CI and p-values for each term.

## Sensitivity analyses

- **`patient_level_bootstrap.csv`**
  Patient-level paired bootstrap (B=5,000 resamples of the 705 patients, seed-averaged probabilities per patient, fixed 0.5 decision threshold, no per-condition threshold optimization). Reports minority-F1, macro-F1, and PR-AUC with bootstrap 95% CIs, and baseline-relative deltas with bootstrap two-sided p-values, for every condition and both architectures. This directly addresses the pseudoreplication concern that the five training seeds within an outer fold share the same held-out test patients.

- **`outer_fold_level_aggregation.csv`**
  Outer-fold-level aggregation: the five training-seed values within each outer fold are averaged into a single fold-level value per condition, giving 3 genuinely independent-patient observations per architecture (6 combined) instead of 15 pseudo-replicated fold-seed units. Paired-t comparison against WRS for GPT-35, Nano-35, Mixed-70, and GPT-10, all three primary metrics. None of these contrasts, including GPT-10, are significant at the fold level, consistent with the patient-level bootstrap above.

- **`resolution_sensitivity_padaspect_contrasts.csv`**
  LMM contrasts vs. the WRS baseline under the 384x768 true aspect-preserving preprocessing (DenseNet-121).

## Notes on the statistical protocol

- The primary outcome is minority-class F1; macro-F1 and PR-AUC are reported as complementary outcomes using the same comparison structure.
- The pre-specified primary contrasts are GPT-35, Nano-35, and Mixed-70 vs. the no-synthetic WRS baseline, analyzed separately (not pooled into a single aggregate "AUG" contrast, since they differ in generator source and synthetic-data budget).
- The primary inferential model is a linear mixed-effects model with a random intercept for the matched outer-fold x training-seed evaluation unit. Multiple comparisons are controlled with Holm's sequential procedure, applied separately to the pre-specified primary contrasts and to the exploratory comparisons.
- Because the five training-seed repetitions within an outer fold share the same held-out patients, they are not independent patient-level samples. This dependence is examined using the patient-level bootstrap above (fixed threshold, no per-condition threshold search) as the primary sensitivity check.
- Given the limited dataset size, statistical power is inherently limited; results should be interpreted using effect sizes and confidence intervals alongside p-values rather than a single significance threshold.
