https://huggingface.co/papers/2505.22312

https://huggingface.co/Skywork/Skywork-OR1-32B

Skywork Open Reasoner 1 Technical Report

1.  **Summary and Rating:**

    This paper introduces Skywork-OR1, a reinforcement learning (RL) framework designed to enhance the reasoning capabilities of large language models (LLMs), particularly for long Chain-of-Thought (CoT) generation. Built upon the DeepSeek-R1-Distill model series, the Skywork-OR1 pipeline, termed MAGIC (Multi-stage Adaptive entropy scheduling for GRPO In Convergence), incorporates several key components including a specialized data mixture, multi-stage training, high-temperature sampling, on-policy training, adaptive entropy control, and the omission of KL loss. The authors demonstrate significant performance improvements on mathematical reasoning (AIME24, AIME25) and coding (LiveCodeBench) benchmarks, with their 32B model outperforming comparable models like DeepSeek-R1 and Qwen3-32B. A substantial portion of the paper is dedicated to comprehensive ablation studies validating their design choices and an in-depth investigation into the phenomenon of policy entropy collapse, identifying contributing factors and effective mitigation strategies. Crucially, the authors fully open-source their model weights, training code, and curated datasets to foster further research.

    **Rating: 8.5/10**

    For a PhD-level audience, this paper serves as an excellent technical report detailing a robust and effective methodology for applying RL to enhance complex reasoning in LLMs. The strengths lie in:
    *   **Empirical Rigor:** The extensive ablation studies on data, training strategies, loss components, and entropy collapse factors are highly valuable for researchers looking to implement or improve similar systems.
    *   **Significant Results:** The reported performance gains on challenging benchmarks are substantial and position Skywork-OR1 китайcompetitive state-of-the-art.
    *   **Openness and Reproducibility:** The commitment to open-sourcing models, code, and data is a major contribution to the community, facilitating reproducibility and further innovation.
    *   **Focused Investigation:** The deep dive into entropy collapse, a practical and often problematic issue in RL, offers valuable insights and actionable strategies.
    While it's a technical report focusing on an engineering pipeline and empirical findings rather than proposing a fundamentally new RL algorithm, its detailed exposition of a successful, scalable system for long CoT reasoning is of high practical and research value. The insights into managing long-sequence RL training and entropy dynamics are particularly insightful. The paper is well-structured and clearly presents its methods and findings.

2.  **Main Ideas Discussed:**

    1.  **The MAGIC RL Pipeline for Long CoT Models:** The paper details the "Multi-stage Adaptive entropy scheduling for GRPO In Convergence" (MAGIC) pipeline, a modified version of Group Relative Policy Optimization (GRPO). This includes specific strategies for data collection and filtering, multi-stage training (progressively increasing context length), high-temperature sampling for better exploration, primarily on-policy updates, and a refined loss function featuring adaptive entropy control and no KL divergence penalty, all tailored for effectively training LLMs on long reasoning tasks.
    2.  **Investigation and Mitigation of Policy Entropy Collapse:** A core focus is the empirical study of premature policy entropy collapse during RL training. The paper identifies factors influencing entropy dynamics (such as rollout diversity, off-policy updates, and entropy loss coefficients) and demonstrates that mitigating this collapse—through techniques like on-policy training, adaptive entropy control, or careful use of tricks like clip-higher—is critical for achieving improved and stable test performance.
    3.  **Open-Sourced Advancements in LLM Reasoning:** The work emphasizes full reproducibility and community research by open-sourcing the Skywork-OR1 model weights (7B and 32B variants), the training codebase, and the curated training datasets. This, combined with extensive ablation studies, provides a transparent and replicable path to achieving state-of-the-art reasoning capabilities.

3.  **10 Most Important Citations:**

    1.  Guo et al. 2025. Deepseek-r1: Incentivizing reasoning capability in llms via reinforcement learning.
        This citation is crucial as Skywork-OR1 builds upon the DeepSeek-R1-Distill model series and its RL approach for enhancing LLM reasoning.
    2.  Shao et al. 2024. Deepseekmath: Pushing the limits of mathematical reasoning in open language models.
        This paper introduces Group Relative Policy Optimization (GRPO), the core RL algorithm modified and used in the Skywork-OR1's MAGIC training pipeline.
    3.  Schulman et al. 2017. Proximal policy optimization algorithms.
        This paper introduces PPO, and the Skywork-OR1 policy loss is described as PPO-style, making this a foundational RL method for the work.
    4.  Sutton et al. 2018. Reinforcement learning: An introduction.
        This is the seminal textbook on reinforcement learning, providing the fundamental concepts and theories underpinning the RL methodologies used in the paper.
    5.  Luo et al. 2025. Deepscaler: Surpassing ol-preview with a 1.5b model by scaling rl. ([https://pretty-radio-b75.notion.site/DeepScaleR-Surpassing-01-Preview-with-a-1-5B-Model-by-Scaling-RL-19681902c1468005bed8ca303013a4e2](https://pretty-radio-b75.notion.site/DeepScaleR-Surpassing-01-Preview-with-a-1-5B-Model-by-Scaling-RL-19681902c1468005bed8ca303013a4e2))
        This work inspired the multi-stage training approach adopted in Skywork-OR1 and is relevant prior art in scaling RL for long CoT models.
    6.  Schulman et al. 2015. High-dimensional continuous control using generalized advantage estimation.
        The paper mentions using GAE (Generalized Advantage Estimation) to estimate token-level advantage (page 6), a common technique for PPO-style algorithms like theirs.
    7.  Jain et al. 2024. Livecodebench: Holistic and contamination free evaluation of large language models for code.
        LiveCodeBench is one of the primary benchmarks used to evaluate the coding capabilities and performance improvements of the Skywork-OR1 models.
    8.  Li et al. 2024. Numinamath. ([https://huggingface.co/AI-MO/NuminaMath-1.5](https://huggingface.co/AI-MO/NuminaMath-1.5) and [https://github.com/project-numina/aimo-progress-prize/blob/main/report/numina_dataset.pdf](https://github.com/project-numina/aimo-progress-prize/blob/main/report/numina_dataset.pdf))
        This dataset is a primary source for the math problems used in training and constructing the data mixture for Skywork-OR1.
    9.  Yu et al. 2025. Dapo: An open-source llm reinforcement learning system at scale.
        This paper is cited in relation to the "clip-higher" trick (page 26), an entropy control method investigated in Skywork-OR1's study on mitigating entropy collapse.
    10. Wen et al. 2025. Light-r1: Curriculum sft, dpo and rl for long cot from scratch and beyond.
        Light-R1 is cited as a recent work making preliminary progress toward efficient RL optimization for long CoT models (page 3), representing related contemporary research.
