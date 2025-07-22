https://www.arxiv.org/abs/2507.14049

**Paper:** EdgeVLA: Efficient Vision-Language-Action Models

### 1. Summary and Rating

This paper introduces EdgeVLA, a novel Vision-Language-Action (VLA) model architecture designed to address the significant challenge of deploying large-scale visuomotor models on resource-constrained hardware, such as mobile robots. The core problem is that state-of-the-art models like OpenVLA, while powerful, are too large and slow for real-time inference on edge devices.

EdgeVLA achieves substantial gains in efficiency through two primary innovations. First, it abandons the standard autoregressive approach for predicting robot end-effector positions, where each dimension of the action is generated sequentially. Instead, it predicts the entire action jointly in a single forward pass, which the authors show results in a 7x inference speedup without compromising the model's encoding capabilities. Second, it replaces the large language model (LLM) backbone with a much smaller, yet highly capable, Small Language Model (SLM), specifically Qwen2-0.5B. This modification, combined with pretrained visual encoders (SigLIP and DINOv2), reduces the model's total parameter count to 1 billion, a fraction of OpenVLA's 7.5 billion.

Early results on the BridgeData V2 and OpenX datasets demonstrate that EdgeVLA maintains training performance comparable to its larger counterpart, OpenVLA, while achieving a 4x reduction in memory usage and the aforementioned 7x speedup in inference time. The paper presents a clear and practical path toward making powerful, general-purpose robotic manipulation models deployable in real-world scenarios.

**Rating: 8.5/10**

This paper receives a high rating for its direct and effective approach to solving a critical, practical problem in robotics. The proposed architectural changes are simple, well-motivated, and yield significant, quantifiable improvements in speed and memory efficiency. By showing that neither autoregressive action generation nor massive language models are strictly necessary for high-performing VLAs, the work opens important new avenues for research into efficient model design. While the results are presented as "early," the direct comparison against a strong baseline like OpenVLA on large-scale datasets provides compelling evidence for the method's viability. The paper is well-written, and its contribution is clear and impactful for the field.

### 2. Main Ideas

1.  **Joint (Non-Autoregressive) Action Prediction:** The primary architectural innovation is the elimination of the autoregressive requirement for end-effector position prediction. Instead of generating the action token-by-token (e.g., x, then y, then z), EdgeVLA predicts the entire action vector simultaneously. This parallel prediction is the main driver of the 7x inference speedup, making real-time control on edge devices feasible.

2.  **Leveraging Small Language Models (SLMs) for Robotic Control:** The paper successfully demonstrates that large, multi-billion parameter LLMs can be substituted with much smaller SLMs (in this case, Qwen2-0.5B) without a significant drop in performance for visuomotor control tasks. This challenges the "bigger is better" trend and provides a clear strategy for reducing the computational and memory footprint of VLA models, making them more accessible.

### 3. 10 Most Important Citations

1.  **Kim et al. (2024) Openvla: An open-source vision-language-action model.** This paper introduces OpenVLA, the primary state-of-the-art model that EdgeVLA is benchmarked against and designed to make more efficient.
    *   Link: [https://arxiv.org/abs/2405.09228](https://arxiv.org/abs/2405.09228)

2.  **Embodiment Collaboration et al. (2024) Open x-embodiment: Robotic learning datasets and rt-x models.** This citation refers to the large-scale OpenX dataset, which is used for training and evaluating EdgeVLA on a diverse set of robotic manipulation tasks.
    *   Link: [https://arxiv.org/abs/2403.09337](https://arxiv.org/abs/2403.09337)

3.  **Yang et al. (2024) Qwen2 technical report.** This report details the Qwen2 model, the specific Small Language Model (SLM) whose 0.5B-parameter version is used as the language backbone in EdgeVLA, making the model highly efficient.
    *   Link: [https://arxiv.org/abs/2406.04832](https://arxiv.org/abs/2406.04832)

4.  **Karamcheti et al. (2024) Prismatic vlms: Investigating the design space of visually-conditioned language models.** The paper follows the "recipe" from this work, which provides a foundational framework for constructing and understanding Vision-Language Models like EdgeVLA.
    *   Link: [https://arxiv.org/abs/2311.08241](https://arxiv.org/abs/2311.08241)

5.  **Oquab et al. (2024) Dinov2: Learning robust visual features without supervision.** This paper introduces DINOv2, one of the two pretrained visual encoders used in the EdgeVLA architecture to extract powerful image representations.
    *   Link: [https://arxiv.org/abs/2304.07193](https://arxiv.org/abs/2304.07193)

6.  **Zhai et al. (2023) Sigmoid loss for language image pre-training.** This work introduces SigLIP, the second pretrained visual encoder used in EdgeVLA, which is crucial for aligning visual information with the language model's token space.
    *   Link: [https://arxiv.org/abs/2303.15343](https://arxiv.org/abs/2303.15343)

7.  **Brohan et al. (2023) Rt-2: Vision-language-action models transfer web knowledge to robotic control.** This is a foundational paper that demonstrated the effectiveness of transferring knowledge from large-scale, web-based vision-language models to robotic control, paving the way for approaches like OpenVLA and EdgeVLA.
    *   Link: [https://arxiv.org/abs/2307.15818](https://arxiv.org/abs/2307.15818)

8.  **Walke et al. (2024) Bridgedata v2: A dataset for robot learning at scale.** This is one of the two key datasets used to train and validate EdgeVLA's performance, particularly for showing its training characteristics against OpenVLA.
    *   Link: [https://bridgedata-v2.github.io/](https://bridgedata-v2.github.io/)

9.  **Dao, T. (2023) Flashattention-2: Faster attention with better parallelism and work partitioning.** This citation is important contextually, as the baseline model (OpenVLA) uses this highly optimized attention mechanism, making EdgeVLA's reported speedups (achieved without it) even more notable.
    *   Link: [https://arxiv.org/abs/2307.08691](https://arxiv.org/abs/2307.08691)

10. **Abdin et al. (2024) Phi-3 technical report: A highly capable language model locally on your phone.** This paper is cited as another example of a powerful SLM, strengthening the core argument that efficient yet capable language models are a viable foundation for next-generation robotics models.
    *   Link: [https://arxiv.org/abs/2404.14219](https://arxiv.org/abs/2404.14219)
