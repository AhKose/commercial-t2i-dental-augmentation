# Commercial T2I Dental Augmentation

Supplementary repository for the study:

**Commercial Text-to-Image Systems for Synthetic Augmentation of Impacted Teeth Classification in Class-Imbalanced Panoramic Dental Radiographs**

This repository contains supplementary materials used to support the transparency and reproducibility of the study, including synthetic images, patient-level fold partitions, representative prompt examples, expert-validation records, supplementary statistical summaries, and source code to be released after manuscript acceptance.

## Overview

The study evaluates whether commercially available general-purpose text-to-image systems can provide useful synthetic augmentation for patient-level impacted-teeth classification in class-imbalanced panoramic dental radiographs.

Synthetic minority-class panoramic radiographs were generated using:

- OpenAI GPT Image
- Google Gemini Nano Banana 2

The generated images were added only to the training partitions. Validation and test partitions remained entirely real.

## Repository Structure

```text
.
├── synthetic_images/
│   ├── README.md
│   ├── gpt_image/
│   │   └── technically screened GPT Image outputs
│   ├── nano_banana_2/
│   │   └── technically screened Nano Banana 2 outputs
│   └── expert_validated/
│       └── README.md
├── folds/
│   ├── README.md
│   ├── impacted_partition_1.json
│   ├── impacted_partition_2.json
│   └── impacted_partition_3.json
├── prompts/
│   └── README.md
├── statistical_analysis/
│   └── supplementary statistical summaries
├── code/
│   └── README.md
└── README.md
```

## Folder Descriptions

### `synthetic_images/`

Contains the technically screened synthetic panoramic dental radiographs generated for the study.

- `gpt_image/` contains technically screened images generated using GPT Image.
- `nano_banana_2/` contains technically screened images generated using Nano Banana 2.
- `expert_validated/` documents the expert-validation decisions at the filename level.

The synthetic images were used only as additional training samples. They were not included in validation or test partitions.

### `folds/`

Contains the fixed patient-level stratified fold partitions used in the impacted-teeth classification experiments.

Each JSON file corresponds to one partition/fold and includes train, validation, and test image lists together with class-distribution information and selected source annotations.

The real DENTEX panoramic radiographs are not redistributed in this repository. The fold files are provided to document the patient-level experimental partitioning used in the study.

### `prompts/`

Contains representative English prompt examples documenting the short class-conditional zero-shot prompting workflow used for synthetic image generation.

The prompt examples are representative rather than exhaustive. They are provided to improve transparency regarding the generation procedure.

### `statistical_analysis/`

Contains supplementary statistical summaries for the study, including the primary fold-seed results, planned mixed-effects and Bayesian contrasts, pairwise summaries for the source, budget, and expert-validation analyses, and auxiliary image-quality metrics.

See `statistical_analysis/README.md` for a description of each file.

### `code/`

Contains the source code associated with the manuscript.

The source code associated with this study will be made available in this repository after manuscript acceptance.

## Experimental Design

### 1. Primary Augmentation-Utility and Imbalance-Control Experiment

This experiment evaluates whether the largest practically available commercial T2I augmentation settings improve classification performance relative to the no-synthetic WRS baseline and additional non-synthetic imbalance-handling controls.

Conditions:

- WRS baseline
- Class-weighted BCE
- Focal loss
- GPT-35
- Nano-35
- Mixed-70
- ROS-35 and ROS-70
- RUS-35 and RUS-70

The Mixed-70 condition combines 35 GPT Image samples and 35 Nano Banana 2 samples. It should be interpreted as a pooled higher-budget condition rather than a strictly matched source-comparison condition.

The ROS and RUS conditions are count- and ratio-matched resampling controls. ROS-35 and ROS-70 add the same number of duplicated real minority images as the corresponding synthetic conditions, while RUS-35 and RUS-70 reduce the majority class so that the resulting class ratio matches the corresponding synthetic condition. These controls isolate the contribution of synthetic image content from a change in sample count or class ratio alone.

All conditions shared an identical preprocessing and train-time augmentation pipeline. Conditions differed only in the sampler, the loss function, and the added or removed training data.

The primary results were evaluated using three predefined patient-level folds and five random seeds, resulting in 15 fold-seed runs per backbone.

### 2. Matched-Budget Source Comparison

This experiment evaluates the effects of generator source, source composition, and augmentation budget under equal total synthetic sample counts.

Conditions:

- GPT-10
- Nano-10
- Mixed-10
- GPT-30
- Nano-30
- Mixed-30

The mixed-source conditions use balanced contributions from the two generators:

- Mixed-10: 5 GPT Image + 5 Nano Banana 2
- Mixed-30: 15 GPT Image + 15 Nano Banana 2

Random subset selection was repeated with three seeds.

### 3. Expert-Validation Experiment

This experiment evaluates whether expert-filtered synthetic images provide measurable downstream benefit compared with count-matched random subsets drawn from the technically screened synthetic pool.

Conditions:

- GPT Image: expert-filtered N = 15 vs. three random N = 15 subsets
- Nano Banana 2: expert-filtered N = 29 vs. three random N = 29 subsets

Random subsets were sampled from the corresponding technically screened synthetic pools using three random seeds.

## Code Availability

The source code associated with this study will be made available in this repository after manuscript acceptance.

## Dataset Notice

The original real DENTEX panoramic radiographs are not redistributed in this repository.

Users must obtain the original dataset from its official source:

S. Er, "DENTEX Challenge 2023," Zenodo, 2023, doi: 10.5281/zenodo.7812323.

This repository provides supplementary materials, including synthetic images, patient-level fold partition files, representative prompt examples, expert-validation records, supplementary statistical summaries, and source code to be released after manuscript acceptance.

## Synthetic Image Notice

The synthetic images are provided for research transparency and reproducibility support.

They should not be interpreted as clinically valid radiographs, diagnostic references, or substitutes for real patient images.

They should not be used for clinical decision-making, diagnosis, or treatment planning.

## Citation

Citation information will be added after publication.

