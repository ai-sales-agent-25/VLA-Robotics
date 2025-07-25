https://huggingface.co/papers/2507.18071

**Paper:** Group Sequence Policy Optimization

### 1. Summary and Rating

This paper introduces Group Sequence Policy Optimization (GSPO), a novel reinforcement learning (RL) algorithm designed to improve the stability and efficiency of training large language models (LLMs). The authors identify a fundamental flaw in the prior state-of-the-art method, Group Relative Policy Optimization (GRPO). They argue that GRPO’s use of token-level importance sampling is theoretically unsound, as it is based on single samples rather than an expectation over a distribution, leading to high-variance gradients that cause training instability and model collapse, especially in long-sequence generation and for Mixture-of-Experts (MoE) models.

The core innovation of GSPO is to redefine the importance ratio and perform optimization at the sequence level. This aligns the unit of optimization with the unit of reward, which is granted to the entire sequence. By using sequence likelihood for the importance ratio, GSPO eliminates the source of instability found in GRPO. Empirical results demonstrate that GSPO achieves superior performance, stability, and training efficiency. Notably, GSPO stabilizes the RL training of large MoE models without requiring complex workarounds like "Routing Replay" that were necessary for GRPO, thus simplifying the training process and infrastructure. The authors credit GSPO for significant improvements in their latest Qwen3 models.

**Rating: 9/10**

For a PhD-level audience, this paper is excellent. It presents a clear, well-motivated, and theoretically-grounded solution to a significant and timely problem in applied AI research—the stable fine-tuning of massive LLMs. The criticism of the previous method (GRPO) is sharp and precise, and the proposed solution (GSPO) is an elegant and direct fix. The experimental evidence is strong, demonstrating clear superiority over the baseline on large-scale models and highlighting a particularly impactful benefit for MoE architectures. While not introducing a new foundational paradigm in RL, its practical contribution, technical clarity, and demonstrable impact on state-of-the-art models make it a high-quality and important piece of work.

### 2. Main Ideas

1.  **Sequence-Level vs. Token-Level Importance Sampling:** The central idea is that for off-policy RL in language models where reward is given for an entire sequence, the importance sampling correction should also be performed at the sequence level. The paper argues that GRPO's token-level approach is a misapplication of importance sampling, introducing high-variance noise that accumulates over a sequence and causes instability. GSPO corrects this by defining the importance ratio based on the likelihood of the entire sequence, which naturally aligns the optimization objective with the sequence-level reward.
2.  **Stabilizing RL for Mixture-of-Experts (MoE) Models:** A key contribution is that GSPO inherently solves the "expert-activation volatility" issue that plagues MoE model training under GRPO. Because GSPO's importance ratio depends on the overall sequence likelihood, it is robust to minor changes in which experts are activated for individual tokens between policy updates. This eliminates the need for complex and constraining workarounds like "Routing Replay," thereby simplifying the training process and allowing the MoE model to leverage its full capacity.
3.  **Matching the Unit of Optimization with the Unit of Reward:** This core principle motivates the shift to sequence-level calculations. The paper highlights the mismatch in GRPO, where a sequence-level advantage is applied to gradients weighted by token-level importance ratios. GSPO restores this consistency by ensuring that both the advantage calculation and the importance-sampling-based clipping and optimization operate on the same unit: the complete generated sequence.

### 3. Important Citations

The paper lists only eight references. The most important ones are listed below.

1.  **Shao et al. (2024)** Deepseekmath: Pushing the limits of mathematical reasoning in open language models.
    *   This paper is cited as the source of the GRPO algorithm, which serves as the primary baseline and the direct predecessor that GSPO aims to improve upon.

2.  **Schulman et al. (2017)** Proximal policy optimization algorithms.
    *   This is the foundational paper for Proximal Policy Optimization (PPO), the RL algorithm whose core principles, such as the clipped surrogate objective, are adapted by both GRPO and GSPO.

3.  **Zheng et al. (2023)** Click: Controllable text generation with sequence likelihood contrastive learning.
    *   This work is directly credited for providing the formulation of the sequence-level importance ratio based on sequence likelihood, which is a cornerstone of the GSPO algorithm.
    *   Link: [https://aclanthology.org/2023.findings-acl.65/](https://aclanthology.org/2023.findings-acl.65/)

4.  **Team Qwen (2025a)** Qwen3 technical report.
    *   This citation provides evidence of GSPO's real-world impact, as the authors state their algorithm contributed to "exceptional performance improvements in the latest Qwen3 models."

5.  **OpenAI (2024)** Learning to reason with LLMs.
    *   This is cited to establish the context and motivation for the paper, highlighting that large-scale RL is a pivotal paradigm for advancing LLM capabilities.
    *   Link: [https://openai.com/index/learning-to-reason-with-llms/](https://openai.com/index/learning-to-reason-with-llms/)

6.  **DeepSeek-AI (2025)** Deepseek-rl: Incentivizing reasoning capability in llms via reinforcement learning.
    *   This paper is used as another example of how RL is being successfully applied to scale the reasoning abilities of LLMs, further justifying the need for robust RL algorithms like GSPO.

7.  **MiniMax (2025)** Minimax-m1: Scaling test-time compute efficiently with lightning attention.
    *   This reference is used to support the claim that existing state-of-the-art RL algorithms can suffer from "catastrophic and irreversible model collapse," establishing the problem that GSPO is designed to solve.

8.  **Team Qwen (2025b)** Qwq-32b: Embracing the power of reinforcement learning, March 2025b.
    *   This blog post by the authors' team further illustrates their commitment to and work on RL, providing additional background for the development of GSPO.
    *   Link: [https://qwenlm.github.io/blog/qwq-32b/](https://qwenlm.github.io/blog/qwq-32b/)
