# Synthetic Images

This folder contains the technically screened synthetic panoramic radiographs generated using:

- `gpt_image_1/`
- `nano_banana_2/`

The images were generated using short class-conditional zero-shot prompts targeting the minority class, namely impacted teeth.

Only technically screened images are included. Outputs with obvious presentation-level failures, such as visible text artifacts, non-panoramic appearance, or clearly invalid radiographic structure, were removed or regenerated during dataset construction.

Expert-filtered images are documented under `expert_validated/`. This folder identifies which technically screened images were retained after expert review.
