# Leakage and Memorization Audit: Methodology and Verified Results

This documents the methodology behind `memorization_audit_gpt.csv`, `memorization_audit_nano.csv`, and `memorization_audit_real_pairs.csv`, referenced in the manuscript as the leakage and memorization audit.

## Methodology

### Part A: real-image uniqueness check

- Embeddings: ImageNet-pretrained DenseNet-121 (same backbone family as the classifier), classifier head replaced with identity, images resized to 256x256 and normalized with ImageNet mean/std, penultimate-layer features L2-normalized.
- Perceptual hash: 16x16 (256-bit) phash computed on grayscale images.
- For each of the 705 real panoramic radiographs, cosine similarity to every other real image was computed (full 705x705 pairwise embedding matrix, diagonal excluded), and the single highest match per image was retained as that image's nearest-neighbor reference.
- The perceptual-hash Hamming distance to the nearest neighbor was likewise computed for every real image.

### Part B: synthetic-to-real nearest-neighbor check

- For each of the 35 GPT Image 1 and 35 Nano Banana 2 technically screened synthetic images, cosine similarity to real images was computed separately against each outer fold's train/val/test partition (the same `outer_{0,1,2}.json` partitions used for classifier training), and the maximum similarity within each partition (plus the matching real image) was recorded. This gives the `o{0,1,2}_{train,val,test}_maxcos` / `_nn` columns in the per-generator CSVs.
- The overall nearest real image across the full 705-image pool, its cosine similarity, perceptual-hash Hamming distance, and LPIPS distance (AlexNet backbone) to the closest match were also recorded (`nn_real`, `nn_cos`, `nn_phash_hamming`, `nn_lpips`).
- A paired comparison of each synthetic image's fold-averaged max-cosine similarity to the train partition versus the test partition was used to check whether synthetic images were disproportionately similar to held-out test images.

### Reference threshold

The 95th percentile of the real-real nearest-neighbor cosine-similarity distribution (all 705 images) was used as the reference threshold for flagging a synthetic image as a possible memorization case.

## Verified results

- **Real-image near-duplicate check** (705 images): perceptual-hash nearest-neighbor Hamming distance, min=50/256, median=78/256. Zero pairs at Hamming <=5, zero pairs at Hamming <=10. No evidence of direct or near-duplicate real-image pairs under this criterion.
- **Real-real cosine-similarity reference**: mean=0.9222, 95th percentile=0.9383, max=0.9500.
- **Synthetic-to-real nearest-neighbor cosine similarity**: GPT Image 1 mean=0.8867 (max=0.9153, n=35); Nano Banana 2 mean=0.8987 (max=0.9214, n=35). Neither generator's maximum nearest-neighbor similarity exceeded the 0.9383 reference threshold (0/35 GPT, 0/35 Nano images exceed it).
- **Train-vs-test partition comparison**: average max-cosine similarity to the train partition exceeded that to the test partition for both generators (GPT: 0.8844 vs. 0.8815, delta=+0.0029; Nano: 0.8966 vs. 0.8938, delta=+0.0028; paired t-test p<.0001 for both, n=35 synthetic images per generator). The direction indicates synthetic images were marginally more similar to training images than to held-out test images, i.e., no evidence of preferential similarity to the test partition.

## Software

- Embeddings: `torchvision.models.densenet121` with `DenseNet121_Weights.IMAGENET1K_V1`.
- Perceptual hash: `imagehash.phash`, `hash_size=16`.
- Perceptual distance: `lpips`, AlexNet backbone (`net="alex"`).

## File contents

- `memorization_audit_real_pairs.csv`: the 10 highest-cosine real-real image pairs (illustrative closest matches, not the full 705x705 pairwise comparison).
- `memorization_audit_gpt.csv`, `memorization_audit_nano.csv`: per-synthetic-image nearest-neighbor statistics against each outer fold's train/val/test partition, plus the overall nearest real image, cosine similarity, perceptual-hash distance, and LPIPS distance.
