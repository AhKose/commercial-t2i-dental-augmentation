# Expert-Validated Synthetic Images

This folder documents the expert-validation step applied to the technically screened synthetic image pool.

The technically screened synthetic images are stored in:

- `../synthetic_images/gpt_image/`
- `../synthetic_images/nano_banana_2/`

This folder does not duplicate the image files. Instead, this README provides filename-level expert-validation information identifying which technically screened images were retained or rejected after expert review.

## Purpose

After image generation and technical screening, an experienced dentist reviewed the retained synthetic image pool to create expert-validated subsets for a separate quality-control analysis.

This expert-validation step was not applied as a prerequisite for all augmentation experiments. Instead, it was used to test whether expert filtering of commercially generated synthetic radiographs improves downstream performance compared with count-matched random subsets from the technically screened pool.

## Scope of Expert Validation

The expert-validation step should not be interpreted as full clinical validation.

The review was used to identify visually acceptable synthetic panoramic radiographs for the expert-validation analysis. It did not establish diagnostic correctness, clinical validity, pathology-level accuracy, or suitability for patient-level decision-making.

## Expert Review Criteria

Three exclusion criteria were applied during expert review:

1. Images judged to be duplicates or near-duplicates of previously retained synthetic samples were removed to avoid artificially amplifying repeated generated instances within the same source augmentation pool.
2. Images were excluded if their visual content was inconsistent with the intended minority-class label, namely impacted teeth.
3. Images were discarded when they contained anatomically implausible, incoherent, or clinically unrealistic dental structures, even if the image still resembled a panoramic radiograph.

Images that did not meet these exclusion criteria were retained in the expert-validated subset.

## GPT Image Expert Review

The GPT Image technically screened pool contained 35 impacted-tooth synthetic panoramic radiographs.

### Expert-Validated GPT Image Samples

The following GPT Image samples were retained after expert review:

```text
gpt_impacted_1
gpt_impacted_2
gpt_impacted_3
gpt_impacted_4
gpt_impacted_5
gpt_impacted_7
gpt_impacted_18
gpt_impacted_19
gpt_impacted_20
gpt_impacted_22
gpt_impacted_23
gpt_impacted_24
gpt_impacted_27
gpt_impacted_28
gpt_impacted_29
```

Total expert-validated GPT Image samples: **15**

### Expert-Rejected GPT Image Samples

The following GPT Image samples were rejected after expert review:

```text
gpt_impacted_6
gpt_impacted_8
gpt_impacted_9
gpt_impacted_10
gpt_impacted_11
gpt_impacted_12
gpt_impacted_13
gpt_impacted_14
gpt_impacted_15
gpt_impacted_16
gpt_impacted_17
gpt_impacted_21
gpt_impacted_25
gpt_impacted_26
gpt_impacted_30
gpt_impacted_31
gpt_impacted_32
gpt_impacted_33
gpt_impacted_34
gpt_impacted_35
```

Total expert-rejected GPT Image samples: **20**

### Expert Note on GPT Image Sample 29

`gpt_impacted_29` was considered visually realistic. However, the expert noted that a clearly impacted tooth was not directly visible. The tooth corresponding to position 38 may represent a tooth with a decayed crown and a root remaining below the gingival level, or it may be interpreted as a coronectomy-related impacted-tooth case. Therefore, it was retained in the expert-validated subset.

### Similarity Assessment for GPT Image Samples

No duplicate or near-duplicate GPT Image samples were identified by the expert.

## Nano Banana 2 Expert Review

The Nano Banana 2 technically screened pool contained 35 impacted-tooth synthetic panoramic radiographs.

### Expert-Validated Nano Banana 2 Samples

The following Nano Banana 2 samples were retained after expert review:

```text
nano_banana_2_impacted_1
nano_banana_2_impacted_2
nano_banana_2_impacted_3
nano_banana_2_impacted_4
nano_banana_2_impacted_5
nano_banana_2_impacted_6
nano_banana_2_impacted_7
nano_banana_2_impacted_12
nano_banana_2_impacted_13
nano_banana_2_impacted_14
nano_banana_2_impacted_15
nano_banana_2_impacted_16
nano_banana_2_impacted_17
nano_banana_2_impacted_18
nano_banana_2_impacted_19
nano_banana_2_impacted_20
nano_banana_2_impacted_21
nano_banana_2_impacted_22
nano_banana_2_impacted_23
nano_banana_2_impacted_24
nano_banana_2_impacted_25
nano_banana_2_impacted_26
nano_banana_2_impacted_27
nano_banana_2_impacted_28
nano_banana_2_impacted_29
nano_banana_2_impacted_30
nano_banana_2_impacted_31
nano_banana_2_impacted_34
nano_banana_2_impacted_35
```

Total expert-validated Nano Banana 2 samples: **29**

### Expert-Rejected Nano Banana 2 Samples

The following Nano Banana 2 samples were rejected after expert review:

```text
nano_banana_2_impacted_8
nano_banana_2_impacted_9
nano_banana_2_impacted_10
nano_banana_2_impacted_11
nano_banana_2_impacted_32
nano_banana_2_impacted_33
```

Total expert-rejected Nano Banana 2 samples: **6**

### Similarity Assessment for Nano Banana 2 Samples

No duplicate images were identified by the expert. Some images showed visual similarity, but they differed by minor image-level or anatomical variations and were therefore treated as distinct samples.

## Use in Experiments

The expert-validated subsets were used only in the expert-validation experiment.

The experiment compared:

- GPT Image expert-filtered N = 15 vs. three random N = 15 subsets
- Nano Banana 2 expert-filtered N = 29 vs. three random N = 29 subsets

The random subsets were count-matched and sampled from the corresponding technically screened synthetic pools using three random seeds.

## Relation to Technical Screening

The random comparison subsets used in the expert-validation experiment did not represent the raw generation stream.

They were sampled from technically screened synthetic images that had already passed a limited non-clinical screening step for obvious presentation-level failures, such as visible text artifacts, non-panoramic image structure, or visibly invalid radiographic appearance.

Therefore, the expert-validation experiment evaluates the additional value of clinical expert filtering beyond simple technical screening, rather than comparing expert-filtered images with completely unfiltered raw generations.

## Important Notice

The expert-validation information is provided for research transparency and methodological inspection.

The corresponding synthetic images should not be interpreted as clinically valid radiographs, diagnostic references, or substitutes for real patient images.

They should not be used for clinical decision-making, diagnosis, or treatment planning.
