https://arxiv.org/abs/2505.13988

The Hallucination Tax of Reinforcement Finetuning

1.  **Brief Summary and Rating (1-10):**

    This paper identifies and addresses a significant side effect of Reinforcement Finetuning (RFT) in Large Language Models (LLMs), termed the "hallucination tax." The authors systematically demonstrate that while RFT enhances LLM reasoning capabilities, it concurrently degrades their refusal behavior, leading them to confidently produce hallucinated answers to unanswerable questions. To investigate and mitigate this, they introduce SUM (Synthetic Unanswerable Math), a novel dataset of high-quality, implicitly unanswerable math problems designed to require reasoning for abstention. The core finding is that augmenting RFT training data with a small proportion (e.g., 10%) of SUM examples substantially restores appropriate refusal behavior (reducing refusal drops by over 80% in some cases) with only minimal trade-offs in accuracy on solvable tasks. Crucially, this improved ability to recognize unanswerable questions and abstain generalizes beyond mathematical problems to other domains like factual question answering, indicating that the model learns to better leverage inference-time compute to reason about its own knowledge boundaries.

    **Rating: 9/10**

    For a PhD-level audience, this paper is a strong contribution. It clearly defines a pertinent and previously underexplored problem (the "hallucination tax") in the increasingly important area of RFT for LLMs. The introduction of the SUM dataset is a valuable resource, and the methodology for its generation is well-described. The experimental design is comprehensive, testing across multiple models and a diverse set of benchmarks for both answerable and unanswerable questions. The findings are significant, offering a practical and effective solution to improve model trustworthiness and epistemic humility without substantial performance costs. The demonstration of generalization is particularly compelling. The paper is well-written, clearly structured, and the arguments are well-supported by empirical evidence. It addresses a nuanced aspect of LLM alignment that is critical for reliable deployment.

2.  **Main Ideas Discussed:**

    1.  **The Hallucination Tax of RFT:** The primary idea is the identification and systematic study of a "hallucination tax" associated with standard Reinforcement Finetuning. While RFT improves reasoning on solvable tasks, it inadvertently increases an LLM's propensity to hallucinate confident answers to unanswerable or ambiguous questions, rather than refusing to answer.
    2.  **Mitigation through Synthetic Unanswerable Data (SUM):** The paper proposes and demonstrates an effective mitigation strategy by introducing SUM (Synthetic Unanswerable Math). By augmenting the RFT training process with a small percentage of these carefully constructed unanswerable math problems, LLMs can be taught to recognize situations requiring abstention due to insufficient or contradictory information.
    3.  **Generalizable Uncertainty Reasoning:** Training with SUM not only improves refusal on in-domain (math) unanswerable questions but also enables LLMs to better reason about their own uncertainty and knowledge boundaries. This improved refusal capability generalizes to out-of-domain tasks, such as factual question answering, suggesting a more fundamental improvement in the model's epistemic awareness.

3.  **List of 10 Most Important Citations:**

    1.  **OpenAI.** 2024. Openai o1 system card.
        This citation represents prominent RFT-enhanced models and is used to highlight both the capabilities RFT brings and the observed issue of increased hallucination in reasoning-oriented models, setting the context for the paper's investigation.
    2.  **Guo et al.** 2025. Deepseek-r1: Incentivizing reasoning capability in llms via reinforcement learning.
        Cited as a key example of recent RFT work focused on enhancing reasoning, which the paper argues can inadvertently lead to the "hallucination tax."
    3.  **Luo et al.** 2025. Deepscaler: Surpassing o1-preview with a 1.5b model by scaling rl. Notion Blog. [https://github.com/PraMamba/DeepScaleR](https://github.com/PraMamba/DeepScaleR)
        The DeepScaleR dataset, introduced in this work, forms the basis from which the authors generate their novel SUM (Synthetic Unanswerable Math) dataset, making it foundational to their methodology.
    4.  **Schulman et al.** 2017. Proximal policy optimization algorithms.
        This paper introduces Proximal Policy Optimization (PPO), the reinforcement learning algorithm used by the authors for their Reinforcement Finetuning experiments.
    5.  **Sun et al.** 2024. Benchmarking hallucination in large language models based on unanswerable math word problem.
        This work inspired the criteria for defining unanswerable questions used in the creation of the SUM dataset and its UWMP dataset is used as a key evaluation benchmark for unanswerable math problems.
    6.  **Yin et al.** 2023. Do large language models know what they don't know?
        This paper introduces the SelfAware dataset, a benchmark for factual unanswerable questions, which is crucial for evaluating the generalization of the refusal behavior learned from the SUM dataset.
    7.  **Cobbe et al.** 2021. Training verifiers to solve math word problems.
        This paper introduces the GSM8K dataset, a standard benchmark for grade school math problems, used extensively in this work to evaluate the performance on answerable tasks and assess accuracy trade-offs when introducing SUM.
    8.  **Yang et al.** 2024. Alignment for honesty.
        The rule-based reward function designed in "The Hallucination Tax of Reinforcement Finetuning" to encourage both accurate solutions and appropriate refusals follows the approach presented in this paper.
    9.  **Tonmoy et al.** 2024. A comprehensive survey of hallucination mitigation techniques in large language models.
        This survey provides a broad context for the problem of LLM hallucination, which the current paper specifically addresses in the context of RFT.
    10. **Huang et al.** 2024b. O1 replication journey-part 2: Surpassing o1-preview through simple distillation, big progress or bitter lesson?
        Cited for providing anecdotal evidence of degraded refusal behavior in LLMs after RFT, motivating the systematic investigation undertaken in this paper.
