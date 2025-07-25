https://arxiv.org/abs/2505.08311

AM-Thinking-v1: Advancing the Frontier of Reasoning at 32B Scale

**1. Brief Summary and Rating**

This paper introduces AM-Thinking-v1, a 32B dense large language model specifically optimized for advanced reasoning tasks, particularly in mathematics and code generation. Built upon the open-source Qwen2.5-32B base model and trained using publicly available queries, AM-Thinking-v1 demonstrates impressive performance, outperforming the 671B MoE model DeepSeek-R1 and rivaling other leading, much larger Mixture-of-Experts (MoE) models like Qwen3-235B-A22B and Seed1.5-Thinking on benchmarks such as AIME 2024 (85.3), AIME 2025 (74.4), and LiveCodeBench (70.3). The authors attribute this success to a meticulously crafted post-training pipeline that combines Supervised Fine-Tuning (SFT) to encourage a "think-then-answer" pattern and Reinforcement Learning (RL) using an adapted Group Relative Policy Optimization (GRPO) with difficulty-aware query selection and a two-stage training process. The paper also details significant optimizations to the RL rollout phase for efficiency. By achieving these results with a moderately sized dense model, the work highlights the potential of accessible, open-source models to reach state-of-the-art reasoning capabilities, offering a practical alternative to massive MoE architectures. The model and its training insights are open-sourced.

**Rating: 8.5/10**

For a PhD-level audience, this paper presents a valuable contribution. It successfully demonstrates that a well-curated dataset and a sophisticated post-training pipeline can significantly boost the reasoning capabilities of a mid-sized (32B) dense model to levels competitive with, or even exceeding, much larger and more complex MoE models in specific reasoning domains. The detailed methodology, including data processing, SFT strategy, the two-stage RL approach, and particularly the RL rollout speed optimizations, offers practical insights. The open-sourcing of the model and the emphasis on using publicly available data further enhance its impact. While not introducing a novel fundamental architecture, the paper's strength lies in its rigorous engineering, strong empirical results, and its contribution to making high-performance reasoning models more accessible. The discussion on "SFT pattern shift" and the subsequent training adjustments is also an interesting practical finding.

**2. Main Ideas Discussed**

1.  **Achieving State-of-the-Art Reasoning with Mid-Scale Dense Models:** The primary idea is that a 32B dense language model can achieve exceptional reasoning performance, rivaling or surpassing significantly larger Mixture-of-Experts (MoE) models on challenging mathematical and coding benchmarks. This is achieved through a meticulously designed post-training pipeline built entirely from open-source components (Qwen2.5-32B base, publicly available queries), demonstrating a practical path to high performance without relying on private data or massive MoE architectures.
2.  **Meticulously Crafted Post-Training Pipeline:** The success of AM-Thinking-v1 hinges on a detailed post-training strategy comprising:
    *   **Data Curation:** Strict preprocessing of open-source queries, including deduplication, quality filtering, decontamination, and for mathematical data, a rigorous ground-truth verification process.
    *   **Supervised Fine-Tuning (SFT):** Using a "cold-start" dataset to encourage a "think-then-answer" reasoning pattern and specific SFT configurations (larger learning rate and batch size) to handle "pattern shifts" observed in long-form reasoning tasks.
    *   **Reinforcement Learning (RL):** Employing an adapted Group Relative Policy Optimization (GRPO) with difficulty-aware query selection (filtering based on SFT model pass rates), a two-stage training approach with adjusted learning rates and response lengths, and handling of overlong responses to ensure stable and progressive improvement.
3.  **Optimization of RL Training Efficiency:** The paper details significant efforts to optimize the rollout speed in their RL framework (verl), which is often a bottleneck. They implement static load balancing by distributing prompt sampling and dynamic instance allocation via a custom load-balancer aware of real-time system metrics, detaching the rollout worker from the inference engine. This "detached" design significantly improves throughput and GPU utilization during the lengthy rollout phase.

**3. List of 10 Most Important Citations**

1.  **DeepSeek-AI et al. 2025.** Deepseek-r1: Incentivizing reasoning capability in llms via reinforcement learning.
    *   This paper introduces DeepSeek-R1, a key high-performing MoE model that AM-Thinking-v1 is benchmarked against and outperforms in several reasoning tasks.
2.  **Qwen Team. 2025.** Qwen3, April 2025.
    *   This reference pertains to the Qwen3 models, including the Qwen3-235B-A22B MoE model, which is a state-of-the-art open-source model used as a strong baseline for comparison.
3.  **Qwen Team. 2024.** Qwen2.5: A party of foundation models, September 2024.
    *   This work introduces the Qwen2.5 series, from which the Qwen2.5-32B base model used for AM-Thinking-v1 originates, making it a foundational citation.
4.  **ByteDance Seed et al. 2025.** Seed1.5-thinking: Advancing superb reasoning models with reinforcement learning.
    *   Introduces Seed1.5-Thinking, another top-tier MoE reasoning model that AM-Thinking-v1 is shown to rival, highlighting its competitive performance.
5.  **MAA. 2024.** American invitational mathematics examination aime. `https://maa.org/math-competitions/american-invitational-mathematics-examination-aime`
    *   Describes the AIME benchmark (specifically AIME2024 results are used), a challenging mathematical reasoning competition dataset crucial for evaluating AM-Thinking-v1's math capabilities.
6.  **Jain, N et al. 2024.** Livecodebench: Holistic and contamination free evaluation of large language models for code. `arXiv preprint arXiv:2403.07974`
    *   This paper introduces LiveCodeBench, a key benchmark used to evaluate AM-Thinking-v1's code generation and understanding abilities.
7.  **Schulman, J et al. 2017.** Proximal policy optimization algorithms.
    *   This paper introduces Proximal Policy Optimization (PPO), the foundational algorithm upon which Group Relative Policy Optimization (GRPO), used in AM-Thinking-v1's RL stage, is based.
8.  **Shao, Z et al. 2024.** Deepseekmath: Pushing the limits of mathematical reasoning in open language models.
    *   While this paper introduces DeepSeekMath, it is cited in AM-Thinking-v1 as the source where Group Relative Policy Optimization (GRPO) is effectively used for mathematical reasoning, which AM-Thinking-v1 adapts for its RL training.
9.  **Sheng, G et al. 2024.** Hybridflow: A flexible and efficient rlhf framework. `arXiv preprint arXiv: 2409.19256`
    *   This paper introduces the 'verl' framework, an open-source RL framework that AM-Thinking-v1's training pipeline is built upon and extended.
10. **Kwon, W et al. 2023.** Efficient memory management for large language model serving with pagedattention. In *Proceedings of the ACM SIGOPS 29th Symposium on Operating Systems Principles*.
    *   This paper likely refers to vLLM (as pagedattention is its core mechanism), a fast inference framework mentioned as being integrated into 'verl' and crucial for optimizing the rollout speed during AM-Thinking-v1's RL training.
