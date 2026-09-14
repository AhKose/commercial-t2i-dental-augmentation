# Commercial T2I Dental Augmentation

Supplementary repository for the study:

**Text-to-Image–Based Synthetic Data Augmentation Using Commercial Models for Addressing Class Imbalance in Impacted Teeth Classification**

This repository contains supplementary materials used to support the transparency and reproducibility of the study, including synthetic images, patient-level nested fold partitions, representative prompt examples, expert-validation records, a complete set of statistical and sensitivity-analysis outputs, and source code to be released after manuscript acceptance.

## Overview

The study evaluates whether commercially available general-purpose text-to-image (T2I) systems can provide useful synthetic augmentation for patient-level impacted-teeth classification in class-imbalanced panoramic dental radiographs.

Synthetic minority-class panoramic radiographs were generated using:

- OpenAI GPT Image 1
- Google Gemini Nano Banana 2

via short class-conditional zero-shot prompting, without medical-domain fine-tuning or task-specific adaptation. The generated images were added only to the training partitions; validation and test partitions remained entirely real.

Under a nested patient-level cross-validation protocol with repeated training seeds, the primary commercial T2I augmentation conditions did **not** demonstrate a consistent or statistically supported advantage over the no-synthetic WeightedRandomSampler (WRS) baseline. Generator source, augmentation budget, and expert filtering produced configuration-dependent numerical differences without a uniformly superior setting. See the manuscript and `statistical_analysis/` for the complete results.

## Repository Structure

```text
.
├── synthetic_images/
│   ├── README.md
│   ├── gpt_image/            technically screened GPT Image 1 outputs (N=35)
│   ├── nano_banana_2/        technically screened Nano Banana 2 outputs (N=35)
│   └── expert_validated/     README documenting expert retain/reject decisions
├── folds/
│   ├── README.md
│   ├── outer_fold_{0,1,2}.json                       outer test folds + inner-CV split
│   └── hp_search_{densenet121,swin_tiny}_outer{0,1,2}.json   selected hyperparameters
├── prompts/
│   └── README.md             representative zero-shot prompt examples
├── statistical_analysis/
│   ├── README.md
│   └── ...                   full statistical/sensitivity result tables (see below)
├── figures/
│   ├── README.md
│   └── figure4_forest_primary_lmm_contrasts.{png,pdf}
├── code/
│   └── README.md             released after manuscript acceptance
└── README.md
```

## Folder Descriptions

### `synthetic_images/`

Contains the technically screened synthetic panoramic dental radiographs generated for the study.

- `gpt_image/` contains technically screened images generated using GPT Image 1 (43 raw generations, 8 rejected at technical screening, 35 retained).
- `nano_banana_2/` contains technically screened images generated using Nano Banana 2 (49 raw generations, 14 rejected at technical screening, 35 retained).
- `expert_validated/` documents the expert-validation decisions at the filename level, including the disjoint expert-approved (N=15) vs. expert-rejected (N=20) GPT Image 1 groups used in the RQ3 secondary analysis.

Generation targeted a minimum technically screened pool of 35 images per generator; see `synthetic_images/README.md` for full generation/rejection counts and screening criteria.

The synthetic images were used only as additional training samples. They were not included in validation or test partitions.

### `folds/`

Contains the fixed patient-level **nested** cross-validation partitions used in the study's experiments: 3 outer test folds, each with an isolated 2-fold inner-CV hyperparameter search and a fixed 399/71 final train/validation split. See `folds/README.md` for the full protocol description and file schema.

The real DENTEX panoramic radiographs are not redistributed in this repository.

### `prompts/`

Contains representative English prompt examples documenting the short class-conditional zero-shot prompting workflow used for synthetic image generation.

### `statistical_analysis/`

Contains the complete supplementary statistical and sensitivity-analysis outputs: the RQ1/RQ2/RQ3 result tables, LMM contrasts (minority-F1, macro-F1, PR-AUC), the RQ2 source × budget × backbone factorial analysis, the RQ3 disjoint expert-approved-vs-rejected comparison, patient-level bootstrap results, resolution/preprocessing sensitivity (256×256 vs. 384×768 direct-resize vs. 384×768 true aspect-preserving), calibration, and the leakage/memorization audit. See `statistical_analysis/README.md` for a description of each file.

### `figures/`

Supplementary figure files, including the forest plot of the primary LMM contrasts (manuscript Figure 4).

### `code/`

The source code associated with this study will be made available in this repository after manuscript acceptance.

## Experimental Design

### 1. Primary Augmentation-Utility and Imbalance-Control Experiment (RQ1)

Evaluates whether the largest practically available commercial T2I augmentation settings affect classification performance relative to the no-synthetic WRS baseline and additional non-synthetic imbalance-handling controls, under the original imbalanced real-data distribution.

Conditions: WRS baseline · class-weighted BCE · focal loss · GPT-35 · Nano-35 · Mixed-70 · ROS-35/ROS-70 · RUS-35/RUS-70.

Mixed-70 combines 35 GPT Image 1 and 35 Nano Banana 2 samples and should be interpreted as a pooled higher-budget condition rather than a strictly matched source comparison. ROS/RUS are evaluated **without** WRS, under uniform sampling, so that data-level resampling is not combined with an additional class-balanced sampling mechanism.

### 2. Source and Augmentation-Budget Comparison (RQ2)

Evaluates generator source, augmentation budget, and mixed-source composition under controlled per-generator synthetic counts: GPT/Nano at N=10, N=30, N=35, and the corresponding pooled Mixed-source conditions at N=20, N=60, N=70 (twice the per-generator budget, not an equal-total-count comparison). A controlled source × budget × backbone factorial analysis is reported for the single-source conditions.

### 3. Expert-Filtered Augmentation (RQ3)

Evaluates the downstream utility of expert-filtered commercial T2I augmentation: the expert-filtered GPT Image 1 (N=15) and Nano Banana 2 (N=29) subsets vs. the no-synthetic WRS baseline. As a secondary/disjoint analysis, it also checks whether the expert-approved GPT Image 1 subset (N=15) outperforms a count-matched, fully disjoint expert-rejected subset (N=15) drawn from the technically screened but expert-rejected images.

All three experiments use the same 3 outer folds × 5 training seeds = 15 fold-seed evaluations per condition and architecture (DenseNet-121, Swin-Tiny).

### 4. Robustness and Sensitivity Analyses

- **Patient-level bootstrap** (B=5,000, fixed 0.5 decision threshold) addressing the fact that the five training seeds within an outer fold share the same held-out test patients.
- **Resolution/preprocessing sensitivity** (DenseNet-121, 384×768) under both direct resizing and true aspect-preserving letterbox padding, including a direct paired comparison between the two resizing strategies.
- **Leakage and memorization audit**: real-image near-duplicate screening and synthetic-to-real nearest-neighbor similarity, per outer-fold train/val/test partition.
- **Calibration**: Brier score and reliability tables.

See `statistical_analysis/README.md` for the complete list of result files.

## Code Availability

The source code associated with this study will be made available in this repository after manuscript acceptance.

## Dataset Notice

The original real DENTEX panoramic radiographs are not redistributed in this repository.

Users must obtain the original dataset from its official source:

S. Er, "DENTEX Challenge 2023," Zenodo, 2023, doi: 10.5281/zenodo.7812323.

## Synthetic Image Notice

The synthetic images are provided for research transparency and reproducibility support.

They should not be interpreted as clinically valid radiographs, diagnostic references, or substitutes for real patient images, and should not be used for clinical decision-making, diagnosis, or treatment planning.

## Citation

Citation information will be added after publication.
