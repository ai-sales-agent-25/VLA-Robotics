https://arxiv.org/abs/2505.18116

Bridging Supervised Learning and Reinforcement Learning in Math Reasoning

1.  **Brief Summary and Rating (1-10 for a PhD-level audience):**

    This paper introduces Negative-aware Fine-Tuning (NFT), a novel supervised learning (SL) approach designed to enable Large Language Models (LLMs) to self-improve in math reasoning tasks by learning from their own mistakes. Traditionally, self-improvement driven by binary verifier signals (correct/incorrect) has been dominated by Reinforcement Learning (RL) methods, as SL methods are typically seen as reliant on reference answers and unable to effectively utilize negative feedback. NFT challenges this by constructing an implicit negative policy, parameterized by the same LLM being trained, which allows the model to directly optimize its policy based on both positive and self-generated negative answers within an SL framework.
    The authors conduct experiments on 7B and 32B models, demonstrating that NFT significantly improves performance over SL baselines like Rejection sampling Fine-Tuning (RFT) and achieves results comparable to or even surpassing leading RL algorithms such as GRPO and DAPO. A key theoretical contribution is the demonstration that NFT and GRPO are equivalent under strict-on-policy training conditions, despite their distinct theoretical origins. This finding, along with the empirical results, suggests that NFT effectively bridges the gap between SL and RL paradigms for LLM fine-tuning in binary-feedback learning systems.

    **Rating: 9/10**

    *   **Justification:** This paper presents a compelling and timely contribution to the field of LLM fine-tuning. The novelty of NFT lies in its elegant formulation of an SL-based approach that successfully incorporates negative feedback, a domain traditionally handled by RL. The theoretical analysis establishing an equivalence with GRPO under specific conditions is a significant insight, offering a deeper understanding of the underlying mechanisms at play in both SL and RL approaches to self-improvement. The empirical results are strong, showing NFT's competitiveness with state-of-the-art RL methods on challenging math reasoning tasks. For a PhD-level audience, the paper offers valuable new perspectives on leveraging SL for self-correction, potentially simplifying training pipelines while maintaining or improving performance. The work is well-motivated, clearly presented, and addresses a relevant problem in LLM development. The direct comparison and bridging of SL and RL paradigms are particularly insightful. The complexity is handled well, and the theoretical underpinnings are adequately explained for the target audience.

2.  **What are 2 or 3 of the main ideas discussed in this paper?**

    *   **Negative-aware Fine-Tuning (NFT) for Self-Improvement:** The central idea is the introduction of NFT, a supervised learning method that enables LLMs to learn from their own incorrect generations (negative feedback). Unlike traditional SL, which often discards negative samples, NFT explicitly models them using an "implicit negative policy" derived from the main LLM, allowing for direct optimization using both positive and negative self-generated data.
    *   **Challenging RL's Exclusivity in Self-Correction:** The paper argues against the prevailing notion that self-improvement using binary verifier signals is exclusive to Reinforcement Learning. By showing that NFT, an SL method, can effectively learn from mistakes and achieve performance comparable or superior to sophisticated RL algorithms like GRPO and DAPO, it demonstrates that SL can also be a powerful tool for autonomous self-correction in LLMs.
    *   **Theoretical and Empirical Bridging of SL and RL:** A significant contribution is the establishment of a formal connection between NFT and the RL algorithm GRPO. The paper proves their equivalence in strict-on-policy training scenarios, despite their different theoretical foundations. This theoretical bridge, supported by strong empirical results, suggests that the performance gap previously observed between SL and RL in such settings might be due to SL's historical inability to leverage negative feedback, a gap NFT aims to close.

3.  **Please make a list of the 10 most important citations. Please format with first author’s last name followed by et al. Then year written. Then full title of the paper. Then one sentence description of how the citation relates to the paper. Please include links if links are given in the paper:**

    1.  Shao et al. 2024. Deepseekmath: Pushing the limits of mathematical reasoning in open language models.
        *   This paper introduces GRPO, a key RL algorithm that NFT is theoretically compared to and shown to be equivalent to under on-policy conditions, and is used as an experimental baseline.
    2.  Yu et al. 2025. Dapo: An open-source llm reinforcement learning system at scale.
        *   This paper introduces DAPO, a state-of-the-art RL algorithm used as a primary baseline for experimental comparison, and also provides the DAPO-Math-17k dataset used for training.
    3.  Dong et al. 2023. Raft: Reward ranked finetuning for generative foundation model alignment.
        *   This paper introduces RFT (Reward ranked Fine-Tuning), an important supervised learning baseline that NFT improves upon by effectively incorporating negative feedback.
    4.  Schulman et al. 2017. Proximal policy optimization algorithms.
        *   This paper introduces PPO, a foundational RL algorithm that influences methods like GRPO and is part of the broader context of policy gradient methods discussed in the paper.
    5.  Chu et al. 2025. Sft memorizes, rl generalizes: A comparative study of foundation model post-training.
        *   This citation represents the common view that supervised learning (SFT/SL) is primarily for memorization and less suited for self-reflective learning from mistakes, a notion this paper's NFT method challenges.
    6.  Williams 1992. Simple statistical gradient-following algorithms for connectionist reinforcement learning.
        *   This paper introduces the REINFORCE algorithm, a fundamental policy gradient method mentioned in the background as a basis for reinforcement learning optimization.
    7.  Rafailov et al. 2023. Direct preference optimization: Your language model is secretly a reward model.
        *   This paper introduces DPO, which involves an implicit reward model, and is cited in the related works section for conceptual similarities to NFT's implicit policy modeling for direct optimization.
    8.  DeepSeek-AI 2025. Deepseek-r1: Incentivizing reasoning capability in llms via reinforcement learning.
        *   This work is cited to highlight the central role of Reinforcement Learning in enhancing LLM reasoning abilities, providing context for the current paper's contribution of an alternative SL-based approach.
    9.  Yang et al. 2024. Qwen2.5-math technical report: Toward mathematical expert model via self-improvement.
        *   This paper describes the Qwen2.5-Math models, which are the base LLMs used in the experiments to evaluate NFT, demonstrating its practical application.
    10. Yuan et al. 2023. Scaling relationship on learning mathematical reasoning with large language models.
        *   This paper is cited as another example of Rejection sampling Fine-Tuning (RFT) and discusses its effectiveness, providing a baseline understanding that NFT aims to extend by leveraging negative data.
