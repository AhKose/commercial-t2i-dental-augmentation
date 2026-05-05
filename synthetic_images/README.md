# Synthetic Images

This folder contains the technically screened synthetic panoramic radiographs generated using:

- `gpt_image/`
- `nano_banana_2/`

The images were generated using class-conditional zero-shot prompts targeting the minority class, namely impacted teeth.

Only technically screened images are included. Outputs with obvious presentation-level failures, such as visible text artifacts, non-panoramic appearance, or clearly invalid radiographic structure, were removed or regenerated during dataset construction.

Expert-filtered images are not duplicated in a separate image folder. Instead, the expert-validation metadata in `expert_validation/` identifies which images were retained after expert review.
