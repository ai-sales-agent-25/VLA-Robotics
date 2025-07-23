https://arxiv.org/abs/2501.16664

https://itcanthink.substack.com/p/paper-notes-improving-vision-language

**Paper:** Improving Vision-Language-Action Model with Online Reinforcement Learning

### 1. Summary and Rating

This paper addresses the challenge of improving large Vision-Language-Action (VLA) models for robotics beyond initial supervised fine-tuning (SFT). The authors observe that directly applying standard online reinforcement learning (RL) to these billion-parameter models is often unstable and computationally demanding, leading to performance degradation. To overcome this, they propose **iRe-VLA**, an iterative framework that alternates between two stages. In the first stage (Online RL), the large VLM backbone is frozen, and only a lightweight action head is trained via RL on new tasks. This stabilizes the learning process and keeps it computationally tractable for local machines. In the second stage (Supervised Learning), the entire model is fine-tuned using a combination of the original expert dataset and the new, successful trajectories collected during the RL stage. This step leverages the full expressive power of the VLM and mitigates catastrophic forgetting. The authors demonstrate through experiments in simulated benchmarks (MetaWorld, Franka-Kitchen) and a real-world Panda robot setup that iRe-VLA effectively improves performance on both expert-level and novel tasks, while also enhancing the model's overall generalization ability.

**Rating: 8.5/10**

The paper tackles a timely and significant problem in robotics: how to enable large foundation models to continuously learn and adapt through environmental interaction. The proposed iRe-VLA method is an elegant and practical solution to the documented instability of RL when applied to large transformer models. The two-stage iterative design is well-motivated, addressing the dual challenges of training stability and computational burden. The experimental validation is comprehensive, with clear results in multiple domains, a relevant ablation study, and a successful real-world deployment that underscores the method's practicality. While the core idea of iterating between exploration and supervised distillation is not entirely novel, its specific formulation and application to modern, large-scale VLAs for low-level control is a strong and valuable contribution to the field.

### 2. Main Ideas

1.  **Direct Online RL is Unstable for Large VLA Models:** The paper's primary motivation stems from the empirical finding that applying standard online RL algorithms (like PPO) to fine-tune an entire large VLA model leads to training instability and performance drops. This is attributed to noisy RL gradients disrupting the carefully pre-trained representations within the massive VLM backbone.
2.  **Iterative Two-Stage Learning (iRe-VLA):** The core contribution is a novel framework, iRe-VLA, that separates exploration from representation learning. It iterates between:
    *   **Stage 1 (Stable RL Exploration):** Freezing the VLM backbone and training only a small, lightweight action head with RL. This allows the agent to safely and efficiently explore and learn new tasks without corrupting the base model.
    *   **Stage 2 (Supervised Knowledge Consolidation):** Fine-tuning the entire model (using efficient methods like LoRA) on a combined dataset of the original expert data and newly gathered successful trajectories. This step distills the new knowledge into the VLM, improving its core representations and preventing catastrophic forgetting.
3.  **Distributing Computational Load:** The iRe-VLA framework is designed to be computationally practical. The lightweight RL stage can be run on local hardware with limited resources (e.g., a single GPU), while the more demanding supervised fine-tuning stage can be offloaded to more powerful remote servers, making the approach accessible for real-world robotics research.

### 3. 10 Most Important Citations

1.  **Ouyang et al. (2022)** Training language models to follow instructions with human feedback.
    *   This paper introduced Reinforcement Learning from Human Feedback (RLHF), establishing the paradigm of using RL to align large models with desired behaviors, which inspired the RL-based fine-tuning approach in this work.
    *   Link: [https://arxiv.org/abs/2203.02155](https://arxiv.org/abs/2203.02155)

2.  **Brohan et al. (2023)** RT-2: Vision-language-action models transfer web knowledge to robotic control.
    *   This paper introduced a state-of-the-art VLA model that is trained via supervised fine-tuning, representing the powerful baseline models that the authors of iRe-VLA aim to improve with online interaction.
    *   Link: [https://arxiv.org/abs/2307.15818](https://arxiv.org/abs/2307.15818)

3.  **Parisotto et al. (2020)** Stabilizing transformers for reinforcement learning.
    *   This work provides direct evidence for the central problem statement: transformer-based policies are inherently difficult to train with RL, motivating the authors' decision to freeze the VLM during the RL phase.
    *   Link: [http://proceedings.mlr.press/v119/parisotto20a.html](http://proceedings.mlr.press/v119/parisotto20a.html)

4.  **Hu et al. (2021)** LoRA: Low-rank adaptation of large language models.
    *   This citation is methodologically crucial as the iRe-VLA framework uses LoRA for parameter-efficient fine-tuning of the entire VLM during the supervised learning stage.
    *   Link: [https://arxiv.org/abs/2106.09685](https://arxiv.org/abs/2106.09685)

5.  **Li et al. (2023)** Blip-2: Bootstrapping language-image pre-training with frozen image encoders and large language models.
    *   This paper introduces the specific VLM (BLIP-2) used as the backbone in the experiments, making it a critical citation for the implementation of the VLA model.
    *   Link: [https://arxiv.org/abs/2301.12597](https://arxiv.org/abs/2301.12597)

6.  **Padalkar et al. (2023)** Open x-embodiment: Robotic learning datasets and rt-x models.
    *   This work is cited to emphasize that high-quality expert datasets for robotics are expensive and difficult to obtain, which motivates the development of methods like iRe-VLA that can learn from online interaction.
    *   Link: [https://arxiv.org/abs/2310.08864](https://arxiv.org/abs/2310.08864)

7.  **McCloskey et al. (1989)** Catastrophic interference in connectionist networks: The sequential learning problem.
    *   This classic paper provides the theoretical context for "catastrophic forgetting," a key problem that iRe-VLA addresses by replaying both expert and online-collected data during its supervised learning stage.
    *   Link: [https://www.sciencedirect.com/science/article/pii/B9780125433247500095](https://www.sciencedirect.com/science/article/pii/B9780125433247500095)

8.  **Schulman et al. (2017)** Proximal policy optimization algorithms.
    *   PPO is the standard RL algorithm used as a baseline for comparison, demonstrating that a naive application performs poorly compared to the proposed iRe-VLA framework.
    *   Link: [https://arxiv.org/abs/1707.06347](https://arxiv.org/abs/1707.06347)

9.  **Yu et al. (2020)** Meta-world: A benchmark and evaluation for multi-task and meta reinforcement learning.
    *   This paper introduces one of the main simulated benchmarks (Metaworld) used to empirically validate the effectiveness of the iRe-VLA method across a diverse set of manipulation tasks.
    *   Link: [https://arxiv.org/abs/1910.10897](https://arxiv.org/abs/1910.10897)

10. **Luo et al. (2024)** SERL: A software suite for sample-efficient robotic reinforcement learning.
    *   This work provides the software suite and experimental setup used for the real-world manipulation experiments, demonstrating the practicality and sample-efficiency of iRe-VLA.
    *   Link: [https://arxiv.org/abs/2401.16013](https://arxiv.org/abs/2401.16013)
