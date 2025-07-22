https://arxiv.org/abs/2505.09577

VTLA: Vision-Tactile-Language-Action Model with Preference Learning for Insertion Manipulation

### 1. Summary and Rating

This paper introduces the Vision-Tactile-Language-Action (VTLA) model, a framework designed to improve robotic manipulation in contact-rich tasks, such as peg-in-hole insertion. The authors identify that existing Vision-Language-Action (VLA) models are limited by their reliance on visual data, which is often insufficient for tasks requiring precise force and contact feedback. To address this, VTLA integrates vision, tactile, and language inputs into a single policy.

The model is trained on a simulated dataset generated in NVIDIA Isaac Gym, which includes visual, tactile, and action data for various peg shapes. The authors propose two main technical contributions. First, they introduce Vision-Guided Temporally Enhanced Tokens (VGTE) to better process sequences of tactile images, mitigating the temporal reasoning limitations of current Vision-Language Models (VLMs). Second, they employ Direct Preference Optimization (DPO) to fine-tune the model. This reframes the continuous control problem, which is typically regression-based, into a preference learning task more suitable for the next-token-prediction nature of Large Language Models (LLMs). This is achieved by generating multiple action candidates, ranking them against the ground truth, and training the model to prefer the better actions.

Experiments demonstrate that VTLA significantly outperforms existing methods, including diffusion policies and unimodal (VLA, TLA) baselines, in both simulated and real-world peg-in-hole tasks. The model shows strong generalization to unseen shapes and achieves a high success rate (over 95%) in real-world experiments, despite being trained solely on simulation data.

**Rating: 9/10**

The paper tackles a significant and challenging problem in robotics: contact-rich manipulation. The approach of integrating tactile sensing into a large-scale VLA model is both timely and logical. The two primary technical contributions are strong: the VGTE method is a thoughtful solution to the temporal limitations of VLMs for low-level sensor data, and the application of DPO to bridge the gap between classification-based LLM training and continuous robot control is particularly novel and clever. The experimental validation is comprehensive, including rigorous comparisons against state-of-the-art baselines, detailed ablation studies, and impressive Sim2Real transfer to a real robot, which validates the effectiveness of the proposed framework. The paper is well-written, the contributions are clear, and the results are compelling.

### 2. Main Ideas

1.  **Multimodal Integration for Contact-Rich Tasks:** The central idea is to enhance the capabilities of VLA models by incorporating tactile feedback. While vision provides global context for a task (e.g., the general location of the hole), tactile data offers crucial local information about contact and forces. By fusing vision, tactile imagery, and language instructions into a single model (specifically, by fine-tuning a Qwen2-VL model), VTLA can generate actions that are informed by both seeing the environment and "feeling" the contact, which is essential for succeeding in precise insertion tasks.

2.  **Preference Learning for Continuous Control:** A key innovation is the use of Direct Preference Optimization (DPO) to fine-tune the action generation policy. Standard LLM fine-tuning uses a next-token prediction loss, which is inherently classification-based and can lead to overfitting on ground-truth actions in a continuous control setting. The paper reframes the problem by first using a supervised fine-tuned model to generate a diverse set of possible actions. These actions are then programmatically labeled as "chosen" (closer to the ground truth) or "rejected" (further from the ground truth). The model is then optimized using the DPO loss, which trains it to prefer the "chosen" actions. This effectively provides a regression-like learning signal, improving the model's generalization and performance on the continuous robotic control task.

3.  **Temporally-Aware Tokenization for Tactile Data:** The authors recognized that pretrained VLMs are not inherently optimized for the short-term, fine-grained temporal sequences typical of tactile sensing during manipulation. To address this, they propose Vision-Guided Temporally Enhanced Tokens (VGTE). This involves encoding the sequence of tactile images into a more compact, temporally-aware representation using a Vision Transformer (ViT) before feeding it to the main language model. This pre-processing step helps the model better reason about the temporal evolution of contact states.

### 3. 10 Most Important Citations

1.  **Brohan et al. 2023. Rt-2: Vision-language-action models transfer web knowledge to robotic control.** This paper is foundational to the VLA paradigm, demonstrating that large models pre-trained on web-scale data can be effectively fine-tuned to become robotic control policies, which is the direct paradigm VTLA builds upon.
    *   Link: `https://arxiv.org/abs/2307.15818`

2.  **Rafailov et al. 2023. Direct preference optimization: Your language model is secretly a reward model.** This paper introduces Direct Preference Optimization (DPO), the key algorithm leveraged by the authors to fine-tune their model for a continuous control task by aligning it with preferred outcomes.
    *   Link: `https://arxiv.org/abs/2305.18290` (Note: The link in the paper is to NeurIPS, but the arXiv link is more direct)

3.  **Hao et al. 2025. Tla: Tactile-language-action model for contact-rich manipulation.** This is a direct baseline and predecessor to VTLA that uses only tactile and language inputs, highlighting the specific contribution of adding the vision modality in the current work.
    *   Link: `https://arxiv.org/abs/2503.08548`

4.  **Wang et al. 2024. Qwen2-vl: Enhancing vision-language model's perception of the world at any resolution.** This is the base Vision-Language Model that the authors chose to fine-tune, making it a critical dependency for the VTLA architecture.
    *   Link: `https://arxiv.org/abs/2409.12191`

5.  **Chi et al. 2023. Diffusion policy: Visuomotor policy learning via action diffusion.** This work represents a prominent, alternative state-of-the-art approach to imitation learning and is used as a key non-LLM baseline for experimental comparison.
    *   Link: `https://arxiv.org/abs/2303.04137`

6.  **Lee et al. 2020. Making sense of vision and touch: Learning multimodal representations for contact-rich tasks.** This is a highly cited paper on learning multimodal vision-tactile representations, establishing the importance and challenges of fusing these two modalities for the kind of contact-rich tasks the VTLA paper addresses.
    *   Link: `https://arxiv.org/abs/1910.05738`

7.  **Jones et al. 2025. Beyond sight: Finetuning generalist robot policies with heterogeneous sensors via language grounding.** This is a highly relevant contemporary work that also explores grounding generalist robot policies with non-visual sensors, situating VTLA within the current research frontier.
    *   Link: `https://arxiv.org/abs/2501.04693`

8.  **Calandra et al. 2018. More than a feeling: Learning to grasp and regrasp using vision and touch.** This is an influential earlier work demonstrating the benefits of combining vision and touch for robotic manipulation, setting the stage for more advanced fusion techniques like those in VTLA.
    *   Link: `https://arxiv.org/abs/1710.08253`

9.  **Kim et al. 2024. Openvla: An open-source vision-language-action model.** This citation represents the broader movement towards open-source, powerful VLA models that the research community, including the VTLA authors, is leveraging and contributing to.
    *   Link: `https://arxiv.org/abs/2406.09246`

10. **Zhang et al. 2023. Gelstereo 2.0: An improved gelstereo sensor with multimedium refractive stereo calibration.** This paper describes the specific visuotactile sensor used in the real-world experiments, making it crucial for understanding the hardware implementation and reproducibility of the results.
    *   Link: `https://ieeexplore.ieee.org/document/9910404`
