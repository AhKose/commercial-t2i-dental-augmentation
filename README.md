# Commercial T2I Dental Augmentation

Supplementary repository for the study:

**Commercial Text-to-Image Systems for Synthetic Augmentation of Impacted Teeth Classification in Class-Imbalanced Panoramic Dental Radiographs**

This repository contains synthetic images, fold split information, metadata, and experimental results used to support transparency and reproducibility of the study.

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
│   ├── gpt_image/
│   │   └── technically screened GPT Image outputs
│   ├── nano_banana_2/
│   │   └── technically screened Nano Banana 2 outputs
│   └── expert_validated/
│       ├── gpt_image/
│       │   └── expert-approved GPT Image subset
│       └── nano_banana_2/
│           └── expert-approved Nano Banana 2 subset
├── folds/
│   └── patient-level train, validation, and test split files
├── metadata/
│   └── dataset, synthetic image, prompt, expert-review, and subset-selection metadata
├── results/
│   └── numerical results reported in the study
├── docs/
│   └── supplementary notes, prompt examples, and methodological details
└── README.md
```

## Folder Descriptions

### `synthetic_images/`

Contains the synthetic panoramic dental radiograph images generated for the study.

- `gpt_image/` contains the technically screened images generated using GPT Image.
- `nano_banana_2/` contains the technically screened images generated using Nano Banana 2.
- `expert_validated/` contains the expert-approved subsets used only in the expert-validation analysis.

### `folds/`

Contains patient-level fold split files used in the experiments.

The real DENTEX panoramic radiographs are not redistributed in this repository. The fold files are provided to document the patient-level experimental partitioning used in the study.

### `metadata/`

Contains metadata files related to:

- dataset summary
- synthetic image generation
- prompt information
- technical screening
- expert-validation decisions
- random subset selections
- experimental settings

### `results/`

Contains numerical result files corresponding to the experiments reported in the paper.

The study includes three experimental analyses:

1. Primary augmentation-utility experiment
2. Matched-budget source comparison
3. Expert-validation experiment

### `docs/`

Contains supplementary documentation, such as prompt examples, additional methodological notes, or repository-specific explanations.

## Experimental Design

### 1. Primary Augmentation-Utility Experiment

This experiment evaluates whether the largest practically available synthetic image sets improve classification performance relative to the no-augmentation baseline.

Conditions:

- GPT-35
- Nano-35
- Mixed-70

The Mixed-70 condition combines 35 GPT Image samples and 35 Nano Banana 2 samples. It should be interpreted as a pooled higher-budget condition rather than a strictly matched source-comparison condition.

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

- GPT Image: expert-filtered N=15 vs random N=15
- Nano Banana 2: expert-filtered N=29 vs random N=29

Random subset selection was repeated with three seeds.

## Dataset Notice

The original real DENTEX panoramic radiographs are not redistributed in this repository.

Users must obtain the original dataset from its official source. This repository provides only supplementary materials such as synthetic images, fold information, metadata, and results.

## Synthetic Image Notice

The synthetic images are provided for research transparency.

They should not be interpreted as clinically valid radiographs, diagnostic references, or substitutes for real patient images.

## Citation

Citation information will be added after publication.
