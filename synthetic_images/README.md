# Synthetic Images

This folder contains the technically screened synthetic panoramic radiographs generated using:

- `gpt_image_1/`
- `nano_banana_2/`

The images were generated using short class-conditional zero-shot prompts targeting the minority class, namely impacted teeth.

Only technically screened images are included. Outputs with obvious presentation-level failures, such as visible text artifacts, non-panoramic appearance, or clearly invalid radiographic structure, were removed or regenerated during dataset construction.

## Generation and technical-screening counts

Generation targeted a minimum technically screened pool of 35 images per generator; raw outputs were generated (and rejected outputs regenerated) until this target was reached.

| Generator | Raw generations | Rejected at technical screening | Retained (technically screened) |
|---|---:|---:|---:|
| GPT Image 1 | 43 | 8 | 35 |
| Nano Banana 2 | 49 | 14 | 35 |

Rejections at this stage were due to obvious presentation-level failures only (visible text artifacts, non-panoramic image structure, or visibly invalid radiographic appearance) and did not involve clinical or anatomical judgment. Clinical/anatomical review of the technically screened pool is a separate, later step. See `expert_validated/`.

Expert-filtered images are documented under `expert_validated/`. This folder identifies which technically screened images were retained after expert review.
