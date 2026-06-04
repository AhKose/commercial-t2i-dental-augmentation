# Prompt Examples

This folder provides representative prompt examples used during the synthetic panoramic radiograph generation process.

The examples are included to document the conditional zero-shot prompting workflow used with the commercial text-to-image systems evaluated in this study.

## Purpose

The prompt examples are provided for transparency regarding how synthetic panoramic radiographs were generated.

They are not intended to represent the complete prompt history or the full set of prompts used in the study. Instead, they provide representative examples of the prompting style and generation workflow.

## Conditional Zero-Shot Prompting

In this study, conditional zero-shot prompting refers to the use of pre-trained commercial text-to-image systems without medical-domain fine-tuning, task-specific adaptation, or local generator training.

The generation requests were conditioned through natural-language prompts that specified:

- the target class, namely impacted teeth
- the intended image type, namely panoramic dental X-ray
- image-level requirements such as HEIGHT = 384 and WIDTH = 768
- absence of visible text on the image
- selected anatomical variations, such as missing molar or anterior teeth

Some images were generated from initial prompts, while others were generated using follow-up prompts in the same generation session. Therefore, follow-up prompts should be interpreted together with the preceding prompt context.

## Representative Prompt Examples

The following examples illustrate the prompting style used to generate synthetic impacted-tooth panoramic radiographs.

### Example 1: Nano Banana 2 Initial Prompt

**Generator:** Google Gemini Nano Banana 2  
**Generated image:** `nano_banana_2_impacted_1`

```text
Generate a panoramic X-ray image containing an impacted tooth with HEIGHT = 384 and WIDTH = 768. Do not include any text on the image. One molar tooth should be missing.
```

### Example 2: Nano Banana 2 Follow-up Prompt

**Generator:** Google Gemini Nano Banana 2  
**Generated image:** `nano_banana_2_impacted_2`

```text
Now generate one with missing anterior teeth.
```

**Note:**  
This was a follow-up prompt issued in the same generation session after the initial impacted-tooth panoramic X-ray prompt. Therefore, it depends on the previous prompt context.

### Example 3: GPT Image Initial Prompt

**Generator:** OpenAI GPT Image  
**Generated image:** `gpt_impacted_1`

```text
Generate a panoramic X-ray image containing an impacted tooth with HEIGHT = 384 and WIDTH = 768.
```

### Example 4: GPT Image Follow-up Prompt

**Generator:** OpenAI GPT Image  
**Generated image:** `gpt_impacted_2`

```text
Now make one with several missing molar teeth.
```

**Note:**  
This was a follow-up prompt issued in the same generation session after the initial impacted-tooth panoramic X-ray prompt. Therefore, it depends on the previous prompt context.

## Generation Workflow

The representative examples above show the general prompting logic used during synthetic image generation.

In practice, several follow-up prompts were sometimes used sequentially within the same generation session to obtain additional candidate images. After several variants were generated, a new generation context could be started again using an initial prompt such as:

```text
Generate a panoramic X-ray image containing an impacted tooth with HEIGHT = 384 and WIDTH = 768.
```

This initial prompt was then followed by additional variation-oriented prompts to generate further candidate images.

## Screening After Generation

Generated images were subjected to technical screening before inclusion in the synthetic image pool.

Images with obvious presentation-level failures were excluded or regenerated during dataset construction. These failures included, but were not limited to:

- visible text artifacts
- non-panoramic appearance
- clearly invalid radiographic structure
- severe anatomical implausibility
- low-quality or unusable image output

Only technically screened images were retained in the synthetic image folders.

## Scope of These Examples

The prompts listed here are representative examples rather than the complete set of prompts used in the study.

They are provided to improve transparency regarding the generation process and to illustrate how conditional zero-shot prompting was applied for minority-class synthetic augmentation.
