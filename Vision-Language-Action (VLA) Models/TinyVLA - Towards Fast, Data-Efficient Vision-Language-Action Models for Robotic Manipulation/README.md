https://arxiv.org/abs/2409.12514

**TinyVLA: Towards Fast, Data-Efficient Vision-Language-Action Models for Robotic Manipulation**

### 1. Summary and Rating

This paper introduces TinyVLA, a new family of compact Vision-Language-Action (VLA) models designed to address two critical bottlenecks in robotic manipulation: the slow inference speeds and extensive data requirements of current state-of-the-art models. The authors propose a framework that diverges from the trend of using massive, auto-regressive models like OpenVLA. Instead, TinyVLA is built by (1) initializing a policy with a compact, pre-trained multimodal vision-language model (VLM) with fewer than 1.4 billion parameters, thereby leveraging general world knowledge without needing pre-training on huge robotics datasets, and (2) attaching a diffusion policy decoder to generate continuous robot actions directly, which is significantly faster than the token-by-token generation of auto-regressive models.

Through extensive experiments in both simulation (MetaWorld) and the real world (single-arm Franka and bimanual UR5 robots), the paper demonstrates that TinyVLA substantially outperforms OpenVLA in inference speed (up to 20x faster) and data efficiency (it requires no robot data pre-training). Despite its smaller size, TinyVLA achieves comparable or superior task success rates and shows robust generalization across novel instructions, objects, viewpoints, and environmental conditions. The work presents a compelling case for building smaller, more efficient models for practical robotic deployment.

**Rating: 9/10**

This is a high-quality, impactful paper. Its primary strength lies in pragmatically addressing a major obstacle for the real-world application of large robotic models—inference speed and training cost. Rather than proposing a complex new architecture, the authors intelligently combine existing, powerful concepts (compact VLMs, diffusion policies, and LoRA) into an elegant and highly effective solution. The experimental validation is thorough and convincing, with direct comparisons to a strong baseline (OpenVLA) across a wide array of generalization axes and both simulated and real-world tasks. The inclusion of bimanual experiments, where the data-specialized OpenVLA fails completely, provides powerful evidence for the flexibility of their approach. The paper makes a significant engineering and systems-level contribution, offering a valuable and practical alternative to the "bigger is better" paradigm that currently dominates the field.

### 2. Main Ideas

The two main ideas of the paper are:

1.  **Compact Pre-trained Models as a Data-Efficient Backbone:** The paper challenges the necessity of using massive (e.g., 7B+ parameter) VLA models that require pre-training on large-scale robotics datasets (like OpenX). It demonstrates that a much smaller (<1.4B parameter) vision-language model, pre-trained on general web-scale image and text data, can serve as a highly effective and data-efficient foundation for a robot policy. This approach leverages the rich world knowledge embedded in the VLM to achieve strong generalization without the computational and data cost of robotics-specific pre-training.

2.  **Diffusion Policy for Fast, Direct Action Generation:** Instead of relying on slow, auto-regressive decoders that predict discretized action tokens one at a time, TinyVLA integrates a diffusion policy head. This module is conditioned on the VLM's multimodal embedding and directly generates the full, continuous action vector for the robot in a non-autoregressive manner. This architectural choice is the key driver behind the model's 20x inference speedup, making it suitable for real-time control where low latency is crucial.

### 3. 10 Most Important Citations

1.  **Kim et al. 2024. Openvla: An open-source vision-language-action model.**
    This is the primary state-of-the-art VLA model that TinyVLA is benchmarked against to demonstrate its superior speed, data efficiency, and performance.

2.  **Chi et al. 2023. Diffusion policy: Visuomotor policy learning via action diffusion.**
    This paper introduces the core "Diffusion Policy" architecture which TinyVLA adopts as its action decoder to enable fast and direct generation of continuous robot actions.

3.  **Brohan et al. 2023. Rt-2: Vision-language-action models transfer web knowledge to robotic control.**
    This is a seminal paper that demonstrated a VLM could be directly co-fine-tuned into a robotic policy, establishing the VLA paradigm and setting the context for subsequent work like TinyVLA.

4.  **Hu et al. 2022. LORA: Low-rank adaptation of large language models.**
    This work provides the parameter-efficient fine-tuning technique (LoRA) used by TinyVLA to adapt the pre-trained VLM to robotic tasks using only a small number of trainable parameters, which is key to its data efficiency.
    *   Link: https://openreview.net/forum?id=nZeVKeeFYf9

5.  **Padalkar et al. 2023. Open x-embodiment: Robotic learning datasets and rt-x models.**
    This citation describes the large-scale robotics dataset (OpenX) used to pre-train models like OpenVLA, which TinyVLA's methodology successfully avoids, thereby drastically reducing its data dependency.

6.  **Liu et al. 2023. Visual instruction tuning.**
    The authors state they followed the training pipeline from this paper (LLaVA) to create the compact vision-language models that serve as the backbone for TinyVLA.
    *   Link: https://openreview.net/forum?id=w0H2xGHlkw

7.  **Ho et al. 2020. Denoising diffusion probabilistic models.**
    This is the foundational paper on Denoising Diffusion Probabilistic Models (DDPMs), which provides the theoretical basis for the diffusion policy decoder used in TinyVLA.

8.  **Brohan et al. 2022. Rt-1: Robotics transformer for real-world control at scale.**
    This paper introduced a large transformer model for robotics and demonstrated its effectiveness at scale, influencing the development of subsequent VLA models like RT-2 and OpenVLA.

9.  **Biderman et al. 2023. Pythia: A suite for analyzing large language models across training and scaling.**
    This work introduces the Pythia family of language models, which the authors used as the language backend when training their compact VLM backbone for TinyVLA.

10. **Yu et al. 2020. Meta-world: A benchmark and evaluation for multi-task and meta reinforcement learning.**
    This paper introduces the MetaWorld simulation benchmark, which was used to conduct a large-scale evaluation of TinyVLA's multi-task learning capabilities across 50 different tasks.
