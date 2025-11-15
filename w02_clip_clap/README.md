## Week 02 — CLIP/CLAP

### Lecture 2: CLIP

  Lecture briefly introduces contrastive learning as a way to learn representations in a shared embedding space, then uses CLIP as the main case study: image–text architecture, InfoNCE-style training on web-scale image-caption pairs, and zero-shot transfer to downstream tasks. It also touches on modern CLIP-style models and CLAP audio-text pretraining as extensions of the same contrastive recipe.

### Seminar 2: CLIP Hands-on Notebook
  
[![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](
https://colab.research.google.com/github/AlbinaBurlova/hse-fcs-multimodal-course/blob/main/w02_clip_clap/sem2_CLIP.ipynb
)

  Seminar notebook demonstrates CLIP in practice: loading the ViT-B/32 model, preprocessing images, and computing image/text embeddings with the original OpenAI implementation. Students visualize cosine-similarity heatmaps on `skimage` samples, run zero-shot classification on CIFAR-100, and then reproduce the workflow with HuggingFace `CLIPModel` / `CLIPProcessor` on a COCO image to build intuition about CLIP’s embedding space and zero-shot behavior.

### References and materials

- Radford et al., *Learning Transferable Visual Models From Natural Language Supervision (CLIP)* - [arXiv:2103.00020](https://arxiv.org/abs/2103.00020)  
- Chopra et al., *Learning a Similarity Metric Discriminatively, with Application to Face Verification* - [PDF](http://yann.lecun.com/exdb/publis/pdf/chopra-05.pdf)  
- Chen et al., *A Simple Framework for Contrastive Learning of Visual Representations (SimCLR)* - [PMLR](https://proceedings.mlr.press/v119/chen20j/chen20j.pdf)  
- Amit Chaudhary, *The Illustrated SimCLR Framework* - [blog post](https://amitness.com/posts/simclr)  
- Chuang et al., *Debiased Contrastive Learning* - [arXiv:2007.00224](https://arxiv.org/abs/2007.00224)  
- Khosla et al., *Supervised Contrastive Learning* - [arXiv:2004.11362](https://arxiv.org/abs/2004.11362)  
- Kong et al., *PANNs: Large-Scale Pretrained Audio Neural Networks for Audio Pattern Recognition* (CNN14 backbone for audio encoders) - [arXiv:1912.10211](https://arxiv.org/abs/1912.10211)  
- Wu et al., *Large-scale Contrastive Language-Audio Pretraining with Feature Fusion and Keyword-to-Caption Augmentation (CLAP)* - [arXiv:2211.06687](https://arxiv.org/abs/2211.06687)  
- OpenAI CLIP code and docs - [github.com/openai/CLIP](https://github.com/openai/CLIP)
- CLAP - [github.com/microsoft/CLAP](https://github.com/microsoft/CLAP)
- LAION CLAP implementation - [github.com/LAION-AI/CLAP](https://github.com/LAION-AI/CLAP)
