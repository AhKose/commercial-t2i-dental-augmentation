# Commercial T2I Dental Augmentation

This repository contains supplementary materials for the study:

**Commercial Text-to-Image Systems for Synthetic Augmentation of Impacted Teeth Classification in Class-Imbalanced Panoramic Dental Radiographs**

Dataset

The original real panoramic radiographs are not redistributed in this repository.

This repository provides fold split files and metadata required to reproduce the experimental setup, subject to access to the original dataset.

The task is a patient-level binary impacted-teeth classification problem:

Impacted: 254 patients
Non-impacted: 451 patients
Imbalance ratio: 1.78:1
Synthetic Image Generation

Synthetic minority-class panoramic radiographs were generated using:

OpenAI GPT Image
Google Gemini Nano Banana 2

Images were generated using simple class-conditional zero-shot prompts without medical-domain fine-tuning, prompt optimization, or task-specific generator adaptation.

Technical Screening

Generated images were technically screened to remove obvious presentation-level failures, including:

Non-panoramic outputs
Visible text artifacts
Clearly invalid radiographic appearance

This screening step was not a clinical validation or pathology-level review.

Expert Validation

A separate expert-validation analysis was performed after technical screening.

An experienced dentist reviewed the technically screened synthetic images and excluded images based on:

Duplicates or near-duplicates
Label inconsistency
Anatomical implausibility or clinically unrealistic structures

The expert-validated subsets were:

GPT Image: 15 images
Nano Banana 2: 29 images

These subsets were used only for the expert-validation experiment.

Experiments

The study includes three experimental analyses.

1. Primary augmentation-utility experiment

Evaluates whether the largest practically available synthetic sets improve performance relative to the no-augmentation baseline.

Conditions:

GPT-35
Nano-35
Mixed-70
2. Matched-budget source comparison

Evaluates generator source, source composition, and augmentation budget under equal total synthetic sample counts.

Conditions:

N=10: GPT-10, Nano-10, Mixed-10
N=30: GPT-30, Nano-30, Mixed-30

Random subset selection was repeated with three seeds.

3. Expert-validation experiment

Compares expert-filtered subsets against count-matched random subsets from the technically screened synthetic pool.

Conditions:

GPT Image: Filtered N=15 vs random N=15
Nano Banana 2: Filtered N=29 vs random N=29

Random subset selection was repeated with three seeds.

Models

Two pretrained classification architectures were evaluated:

DenseNet-121
Swin-Tiny

Both models were trained and evaluated using fixed patient-level stratified three-fold cross-validation.

Metrics

Primary metrics:

Minority-class F1
Macro-F1

Secondary metrics:

ROC AUC
Accuracy
Majority-class F1
Notes on Data Redistribution

The original dataset images are not included. Users must obtain access to the original dataset from its official source.

Synthetic images and metadata are provided only for research reproducibility and should not be interpreted as clinically valid radiographs.

Citation

Citation information will be added after publication.

@article{placeholder,
  title   = {Commercial Text-to-Image Systems for Synthetic Augmentation of Impacted Teeth Classification in Class-Imbalanced Panoramic Dental Radiographs},
  author  = {Köse, Abdullah Huzeyfe and Yılmaz, Rahime and Yılmaz, Elif and Ekşioğlu, Ender Mete},
  journal = {TBD},
  year    = {TBD}
}

License

License information will be added.
