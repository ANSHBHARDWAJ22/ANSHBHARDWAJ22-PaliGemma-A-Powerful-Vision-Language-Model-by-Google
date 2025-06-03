# PaliGemma: A Powerful Vision-Language Model by Google

##  Overview

**PaliGemma** is a cutting-edge **Vision-Language Model (VLM)** developed by Google that combines the capabilities of both image understanding and natural language generation. It can take an **image + text as input** and produce **text as output**, making it ideal for tasks like **image captioning**, **visual question answering (VQA)**, **object detection**, and **referring expression segmentation**.

It leverages:
- **SigLIP-So400m** as the **image encoder**
- **Gemma-2B** as the **text decoder**

This powerful combination, connected via a **linear adapter**, forms the foundation of the PaliGemma model.

---

##  Architecture Details
![Screenshot 2025-05-25 040119](https://github.com/user-attachments/assets/80b93a8e-62a0-4d2e-9299-f83f54655045)


### 🔹 Image Encoder: SigLIP

**SigLIP (Sigmoid Language-Image Pretraining)** is an advanced vision-language model that, like CLIP, learns joint representations of images and text. It uses a **contrastive learning objective** but replaces softmax with **sigmoid**, allowing it to generalize better in certain cases.

### 🔹 Text Decoder: Gemma

**Gemma** is a **decoder-only language model** similar in structure to GPT-based models. The variant used here is **Gemma-2B**, which is responsible for generating the output text from visual and textual input.

### 🔹 Linear Adapter

A **learned linear projection layer** connects the SigLIP image encoder output to the input of the Gemma decoder. This acts as a bridge between vision and language modalities, enabling end-to-end learning and inference.

---

##  Checkpoint Types

Google has released multiple types of PaliGemma models optimized for different usage scenarios:

| Type | Description | Use Case |
|------|-------------|----------|
| **PT (Pretrained)** | Trained on large-scale image-text data | Ideal for custom fine-tuning |
| **Mix** | PT models fine-tuned on a **mixture of tasks** (captioning, VQA, etc.) | Ready-to-use for general inference |
| **FT (Fine-Tuned)** | Task-specific models fine-tuned on academic benchmarks | High-performance for specific datasets |

---

##  Resolutions & Precisions

Each model is available in **three resolutions**:
- `224x224`: Suitable for most use cases, optimized for speed and memory
- `448x448`: Balanced quality vs cost
- `896x896`: High-detail, used for fine-grained tasks (e.g., OCR), but memory intensive

And in **three precisions**:
- `float32`: Default and most stable
- `bfloat16` and `float16`: Faster and more memory-efficient, suitable for GPUs/TPUs

> Note: High-resolution models significantly increase memory and compute cost with only marginal accuracy gains for general tasks.

---

## ⚙️ Integration with Hugging Face

All PaliGemma models are released on the [Hugging Face Hub](https://huggingface.co/collections/google/paligemma-664c3241e85bb67f93cb429e) with full support for the `transformers` library. Models are also available for the original JAX framework.

- Transformers support:
  - Model loading
  - Tokenizer & image processor
  - Inference pipeline
  - Fine-tuning utilities

---

##  Core Capabilities

PaliGemma is **not designed for multi-turn conversation**. Instead, it performs **single-turn tasks** — one image and one prompt per prediction.

You configure the task using **task-specific prefixes**, such as:

### 1.  Image Captioning
```text
caption
