# Statistical Analysis

This folder provides supplementary statistical summaries for the study.

## Files

- **`primary_results.csv`**
  Primary experiment results: mean and standard deviation of minority-class F1, macro-F1, and AUC for every condition and backbone, computed over the 15 fold-seed runs (3 patient-level folds × 5 random seeds).

- **`planned_contrasts.csv`**
  Planned linear mixed-effects (LMM) and Bayesian comparisons for minority-class F1. Each contrast is reported separately for DenseNet-121, Swin-Tiny, and the combined (both-backbone) model, together with the mean difference, Cohen's *d*, LMM *p*, and the Bayesian posterior probability of superiority.

- **`source_budget_pairwise_summaries_rq2.csv`**
  Additional pairwise summaries for the matched-budget source and budget analyses (RQ2), including source comparisons, the N=10 versus N=30 budget effect, and mixed-source versus single-source contrasts.

- **`expert_validation_pairwise_summaries_rq3.csv`**
  Additional pairwise summaries for the expert-filtered versus count-matched random subset analyses (RQ3), reported per generator and for both generators pooled.

- **`auxiliary_kid_lpips_metrics.csv`**
  Auxiliary Kernel Inception Distance (KID) and LPIPS diversity metrics reported for the synthetic image pools.

## Notes on the statistical protocol

- The primary metric is **minority-class F1**; macro-F1 and AUC are reported as secondary measures.
- Results correspond to the **fold-seed evaluation protocol** described in the manuscript: three predefined patient-level folds combined with five random seeds, giving 15 runs per condition and backbone.
- Because repeated cross-validation produces correlated measurements, significance is reported with complementary approaches: a linear mixed-effects model with a random intercept per fold-seed run (the primary inferential model), effect sizes, and Bayesian posterior probabilities of superiority based on a correlated *t* posterior. Non-parametric tests and a conservative Nadeau-Bengio correction were additionally examined as sensitivity checks.
- Given the limited dataset size and the correlated nature of repeated cross-validation, statistical power is inherently limited. Results should therefore be interpreted using effect sizes and posterior probabilities alongside p-values rather than a single significance threshold.

## Image-quality metrics

`auxiliary_kid_lpips_metrics.csv` reports the Kernel Inception Distance (KID) between each synthetic image pool and the real impacted-class images, together with the LPIPS diversity within each pool.

KID is used because it remains unbiased at the small sample sizes involved here, and its embeddings are taken from a publicly available DenseNet-121 pretrained on public chest-radiograph collections (`torchxrayvision`). This embedding model is separate from the classifiers evaluated in the study.

These metrics are exploratory and are intended for comparison between image pools rather than as absolute quality scores.
