---
layout: post
date: 2024-12-15
inline: true
related_posts: false
---

[Getting free Bits Back from Rotational Symmetries in LLMs](https://jiajunhe98.github.io/assets/pdf/bits-back-llm_slides.pdf)\
*Workshop on Machine Learning and Compression at NeurIPS 2024*\
<sub>**Abstract:** Current methods for compressing neural network weights, such as decomposition, pruning, quantization, and channel simulation, often overlook the inherent symmetries within these networks and thus waste bits on encoding redundant information. We propose a format based on bits-back coding for storing rotationally symmetric Transformer weights more efficiently than the usual array layout at the same floating-point precision. We evaluate our method on Large Language Models (LLMs) pruned by SliceGPT (Ashkboos et al., 2024) and achieve a 3-5% reduction in total bit usage for free across different model sizes and architectures without impacting model performance within a certain numerical precision.</sub>