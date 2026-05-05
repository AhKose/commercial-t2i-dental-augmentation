# Fold Partitions

This folder contains the fixed patient-level stratified partitions used in the impacted-teeth classification experiments.

Each JSON file corresponds to one partition/fold and includes:

- `disease`: target condition used for the task.
- `partition_id`: fold identifier.
- `random_seed`: seed used during partitioning.
- `split_ratios`: train/validation/test split ratios.
- `train`, `val`, `test`: image lists and class distributions.
- `image_id`: original image identifier.
- `file_name`: original dataset file name.
- `has_impacted`: binary label used in this study.
- `has_caries`: additional annotation retained from the source metadata.

The original DENTEX images are not included in this repository.
