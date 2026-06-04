# Expert-Validated Synthetic Images

This folder documents the expert-validation step applied to the technically screened synthetic image pool.

The technically screened synthetic images are stored in:

- `../gpt_image/`
- `../nano_banana_2/`

This folder does not duplicate the image files. Instead, this README provides filename-level expert-validation information identifying which technically screened images were retained or rejected after expert review.

## Purpose

The expert-validation step was used to identify synthetic panoramic radiographs that were visually acceptable according to dental expert review.

The expert-approved subsets were used only in the expert-validation experiment, where expert-filtered synthetic images were compared with count-matched randomly selected subsets from the technically screened synthetic pool.

## Scope of Expert Validation

The expert-validation step should not be interpreted as full clinical validation.

The review was used to identify visually acceptable synthetic panoramic radiographs for the expert-validation analysis. It did not establish diagnostic correctness, clinical validity, pathology-level accuracy, or suitability for patient-level decision-making.

## GPT Image Expert Review

The GPT Image technically screened pool contained 35 impacted-tooth synthetic panoramic radiographs.

### Expert-Approved GPT Image Samples

The following GPT Image samples were considered realistic or visually acceptable after expert review:

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

Total expert-approved GPT Image samples: **15**

### Expert-Rejected GPT Image Samples

The following GPT Image samples were considered unrealistic or not visually acceptable after expert review:

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

`gpt_impacted_29` was considered visually realistic. However, the expert noted that a clearly impacted tooth was not directly visible. The tooth corresponding to position 38 may represent a tooth with a decayed crown and a root remaining below the gingival level, or it may be interpreted as a coronectomy-related impacted-tooth case. Therefore, it was retained in the expert-approved subset.

### Similarity Assessment for GPT Image Samples

No clearly duplicate or highly similar GPT Image samples were identified by the expert.

## Nano Banana 2 Expert Review

The Nano Banana 2 technically screened pool contained 35 impacted-tooth synthetic panoramic radiographs.

### Expert-Approved Nano Banana 2 Samples

The following Nano Banana 2 samples were considered realistic or visually acceptable after expert review:

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

Total expert-approved Nano Banana 2 samples: **29**

### Expert-Rejected Nano Banana 2 Samples

The following Nano Banana 2 samples were considered unrealistic or not visually acceptable after expert review:

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

The expert-approved subsets were used in the expert-validation experiment.

The experiment compared:

- GPT Image expert-filtered N = 15 vs. random N = 15
- Nano Banana 2 expert-filtered N = 29 vs. random N = 29

The random subsets were count-matched and sampled from the technically screened synthetic pool.

## Important Notice

The expert-approved filenames are provided for research transparency and methodological inspection.

The corresponding synthetic images should not be interpreted as clinically valid radiographs, diagnostic references, or substitutes for real patient images.

They should not be used for clinical decision-making, diagnosis, or treatment planning.
