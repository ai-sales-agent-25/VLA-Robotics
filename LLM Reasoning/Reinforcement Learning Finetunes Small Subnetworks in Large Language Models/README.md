https://arxiv.org/abs/2505.11711

Reinforcement Learning Finetunes Small Subnetworks in Large Language Models

1.  **Summary and Rating:**
    This paper investigates the phenomenon of "parameter update sparsity" during the reinforcement learning (RL) finetuning of large language models (LLMs). The authors surprisingly find that substantial performance gains and alignment improvements from RL are achieved by updating only a very small subnetwork of the model's parameters, typically 5-30%, with the vast majority of parameters remaining effectively unchanged. This sparsity is shown to be an intrinsic property of RL finetuning, occurring across diverse RL algorithms (PPO, DPO, KTO, etc.) and LLM architectures, without explicit sparsity-promoting mechanisms.

    Crucially, the paper demonstrates that finetuning only this identified sparse subnetwork (while freezing other parameters) not only recovers the test accuracy of the fully finetuned model but also results in a model with parameter values nearly identical to those obtained via full finetuning. This finding extends beyond the Lottery Ticket Hypothesis. The identified subnetworks exhibit significant overlap even when training conditions like random seeds, training data, or RL algorithms are varied, suggesting a partially transferable underlying structure. The authors posit that this update sparsity is primarily driven by training on data that is close to the current policy distribution. Factors such as KL-divergence regularization and gradient clipping are found to have a limited impact on this sparsity. The updates, while sparse, are shown to be nearly full-rank, indicating that RL modifies a small set of parameters that span almost the full representational subspaces of the parameter matrices, rather than confining changes to low-rank subspaces.

    **Rating: 9/10**
    This paper presents a compelling and potentially highly impactful set of findings for the LLM research community. For a PhD-level audience, the discovery of intrinsic, high-degree parameter update sparsity in RL finetuning is a significant contribution, challenging common assumptions about the extent of changes RL induces. The empirical evidence across multiple models and state-of-the-art RL algorithms is thorough. The demonstration that finetuning only the emergent subnetwork can closely replicate the fully finetuned model (in both performance and parameter space) has profound implications for training efficiency, model understanding, and catastrophic forgetting. The investigation into the causes of sparsity, pointing towards in-distribution training, offers valuable insights. The distinction from LoRA (sparse full-rank updates vs. dense low-rank updates) is also a noteworthy clarification. The paper is well-structured and clearly articulates its findings. The primary strength lies in the novelty and potential practical utility of its core observations.

2.  **Main Ideas Discussed:**
    1.  **Intrinsic Parameter Update Sparsity in RL Finetuning:** The core finding is that RL finetuning inherently modifies only a small fraction (5-30%) of an LLM's parameters, leaving the rest unchanged. This "parameter update sparsity" is observed consistently across various RL algorithms and LLM families without any explicit sparsity-inducing techniques.
    2.  **Subnetwork Sufficiency for Performance and Parameter Replication:** Finetuning solely the identified sparse subnetwork (with other parameters frozen) is sufficient to achieve performance comparable to, or even better than, full RL finetuning. More strikingly, this subnetwork-only finetuning yields a model whose parameters are nearly identical to the fully finetuned model, going beyond the traditional Lottery Ticket Hypothesis which primarily focuses on performance matching.
    3.  **In-Distribution Training as the Primary Driver of Sparsity:** The paper argues that the primary reason for this update sparsity is training on data that is close to the model's current policy distribution (e.g., on-policy RL or SFT on data similar to what RL will use). Other common RL techniques like KL-divergence regularization towards a reference model or gradient clipping have a comparatively limited impact on the emergence of this sparsity.

3.  **10 Most Important Citations:**

    1.  Frankle et al. 2019. The lottery ticket hypothesis: Finding sparse, trainable neural networks.
        This citation is fundamental as it introduced the Lottery Ticket Hypothesis, a core concept related to the paper's investigation of sparse subnetworks, although the current paper extends this by showing near-identical parameter recovery, not just performance.
        (Link: https://openreview.net/forum?id=rJl-b3RcF7)

    2.  Ouyang et al. 2022. Training language models to follow instructions with human feedback.
        This paper is a key reference for modern RLHF in LLMs, establishing the paradigm that the current work investigates and showing the effectiveness of RL for alignment.
        (Link: https://arxiv.org/abs/2203.02155)

    3.  Schulman et al. 2017b. Proximal policy optimization algorithms.
        PPO is one of the widely-used RL algorithms tested in the paper to demonstrate the generalizability of the sparsity phenomenon, making this a crucial methodological citation.
        (Link: https://arxiv.org/abs/1707.06347)

    4.  Rafailov et al. 2023. Direct preference optimization: Your language model is secretly a reward model.
        DPO is another major RL algorithm extensively analyzed in the paper, whose update sparsity is a key piece of evidence for the paper's claims.
        (Link: https://openreview.net/forum?id=HPuSIXJaa9)

    5.  Cui et al. 2025. Process reinforcement through implicit rewards. (PRIME)
        PRIME is one of the RL algorithms highlighted and used in detailed experiments (e.g., Conjecture 1 validation, layerwise sparsity analysis), making its citation important for understanding the experimental setup.
        (Link: https://arxiv.org/abs/2502.01456)

    6.  Hu et al. 2022. LoRA: Low-rank adaptation of large language models.
        This paper is important as LoRA represents an alternative parameter-efficient finetuning approach (low-rank updates), which the current paper contrasts with its finding of sparse but full-rank updates.
        (Link: https://openreview.net/forum?id=nZeVKeeFYf9)

    7.  Chu et al. 2025. Sft memorizes, rl generalizes: A comparative study of foundation model post-training.
        This citation supports the paper's findings by providing context that RL might preserve pretrained capabilities better than SFT, which aligns with the observation of RL inducing sparser updates.
        (Link: https://arxiv.org/abs/2501.17161)

    8.  Shao et al. 2024. Deepseekmath: Pushing the limits of mathematical reasoning in open language models. (Implicitly GRPO as DeepSeek models use GRPO or similar RL techniques for math)
        The DeepSeek models (often trained with GRPO, another RL algorithm mentioned) are part of the experimental suite, showing high update sparsity, making this relevant. (The paper directly cites "Shao et al., 2024" for GRPO in Figure 1 and Table 1, with DeepSeek Math 7B).
        (Link: https://arxiv.org/abs/2402.03300)

    9.  Ethayarajh et al. 2024. Kto: Model alignment as prospect theoretic optimization.
        KTO is another RL algorithm included in the experiments (Table 1) demonstrating the parameter update sparsity phenomenon, making this citation relevant to the breadth of evidence.
        (Link: https://arxiv.org/abs/2402.01306)

    10. Sutton et al. 1998. Reinforcement learning: An introduction, volume 1.
        This is the foundational textbook for reinforcement learning, cited for establishing the basic principles and context of the RL methods being investigated.
