https://arxiv.org/abs/2504.13837

**Does Reinforcement Learning Really Incentivize Reasoning Capacity in LLMs Beyond the Base Model?**

**1. Summary and Rating**

This paper critically re-evaluates the widely held assumption that Reinforcement Learning with Verifiable Rewards (RLVR) enhances the fundamental reasoning capabilities of Large Language Models (LLMs) beyond their pre-trained base models. Using the pass@k metric with large values of *k* across various models, benchmarks (math, code, vision), and RL algorithms, the authors find that while RLVR improves performance at low *k* (sampling efficiency), base models consistently match or even surpass their RL-trained counterparts at large *k*. This suggests RLVR primarily biases the model's sampling distribution towards known, high-reward reasoning paths already present within the base model's capabilities, rather than discovering novel reasoning patterns. This biasing enhances efficiency but narrows the model's exploration capacity and ultimate reasoning boundary, which remains fundamentally limited by the base model. The study contrasts this with distillation, which they show *can* introduce new knowledge and expand the reasoning boundary. The findings challenge the view of RLVR as a mechanism for continuous self-improvement in reasoning and suggest its current form may be insufficient to push reasoning frontiers significantly beyond the base model's inherent potential.

**Rating: 9/10**

*   **Justification:** This paper receives a high rating for a PhD-level audience due to its significant and potentially controversial contribution. It directly challenges a prevailing narrative about the benefits of RL for LLM reasoning using a rigorous and appropriate methodology (large-k pass@k, perplexity analysis, controlled comparisons). The core finding – that RLVR improves efficiency but narrows the *scope* of reasoning relative to the base model – is counter-intuitive, important, and well-supported by extensive experiments across diverse tasks and models. The distinction drawn between RLVR and distillation further strengthens the argument. The work is highly relevant, addresses a critical question in LLM development, and forces a re-evaluation of RL's role in enhancing reasoning. While dense, the paper is clearly argued, and the results have significant implications for future research directions in LLM training paradigms.

**2. Main Ideas**

1.  **RLVR Limits Reasoning Capacity:** Contrary to common belief, RLVR training does not expand the fundamental reasoning capacity of LLMs beyond their base models. While RL-trained models excel at low sampling counts (pass@1), base models demonstrate comparable or superior performance when allowed extensive sampling (pass@k with large *k*), indicating a broader, albeit less efficiently sampled, reasoning potential in the base model.
2.  **RLVR as Biasing, Not Knowledge Infusion:** The primary effect of RLVR is to increase the sampling efficiency of correct reasoning paths that are *already present* within the base model's distribution. It biases the model towards rewarded outputs but does not fundamentally introduce new reasoning strategies or knowledge, ultimately leading to a narrower exploration space and reasoning boundary compared to the base model.
3.  **Distillation vs. RLVR:** Unlike RLVR, knowledge distillation from a more capable teacher model *can* genuinely introduce new reasoning patterns and knowledge, demonstrably expanding the reasoning capacity of a student model beyond its original base capabilities. This highlights a fundamental difference in how these two techniques impact LLM reasoning potential.

**3. 10 Most Important Citations**

1.  **Guo et al. 2025.** Deepseek-r1: Incentivizing reasoning capability in llms via reinforcement learning.
    *   *Relevance:* Represents a state-of-the-art RLVR-trained model (DeepSeek-R1) whose success motivates the investigation, and is also used as an example of distillation potential. [https://arxiv.org/abs/2501.12948](https://arxiv.org/abs/2501.12948) (Link inferred from citation context, not explicit in OCR text for this ref)
2.  **Chen et al. 2021.** Evaluating large language models trained on code.
    *   *Relevance:* Introduced the pass@k metric for code generation, which this paper adapts and extends as the primary evaluation method for reasoning capacity boundary. [https://arxiv.org/abs/2107.03374](https://arxiv.org/abs/2107.03374)
3.  **Lambert et al. 2024.** T\" ulu 3: Pushing frontiers in open language model post-training.
    *   *Relevance:* Discusses recent advancements in LLM post-training, including RLVR, providing context for the techniques being analyzed. [https://arxiv.org/abs/2411.15124](https://arxiv.org/abs/2411.15124)
4.  **Brown et al. 2024.** Large language monkeys: Scaling inference compute with repeated sampling.
    *   *Relevance:* Explores the effectiveness of repeated sampling (large *k*) for LLM inference, directly related to the pass@k methodology used in this paper to probe model capacity limits. [https://arxiv.org/abs/2407.21787](https://arxiv.org/abs/2407.21787)
5.  **Schulman et al. 2017.** Proximal policy optimization algorithms.
    *   *Relevance:* Introduced PPO, a foundational RL algorithm commonly used in RLVR and included in this paper's analysis of different RL algorithms. [https://arxiv.org/abs/1707.06347](https://arxiv.org/abs/1707.06347)
6.  **Cobbe et al. 2021.** Training verifiers to solve math word problems.
    *   *Relevance:* Introduced the GSM8K benchmark dataset, a key evaluation benchmark used extensively in this paper's mathematical reasoning experiments. [https://arxiv.org/abs/2110.14168](https://arxiv.org/abs/2110.14168)
7.  **Hendrycks et al. 2021.** Measuring mathematical problem solving with the math dataset.
    *   *Relevance:* Introduced the MATH dataset, another crucial benchmark used for evaluating mathematical reasoning capabilities in the experiments.
8.  **Jaech et al. 2024.** Openai ol system card.
    *   *Relevance:* Describes OpenAI's o1 model, cited as a prominent example of a large-scale reasoning model improved via RL, setting the stage for the paper's investigation. [https://arxiv.org/abs/2412.16720](https://arxiv.org/abs/2412.16720)
9.  **Shao et al. 2024.** Deepseekmath: Pushing the limits of mathematical reasoning in open language models.
    *   *Relevance:* Introduced the GRPO algorithm (used in the paper's RL algorithm comparison) and presented another strong math reasoning model trained with RL. [https://arxiv.org/abs/2402.03300](https://arxiv.org/abs/2402.03300)
10. **Ouyang et al. 2022.** Training language models to follow instructions with human feedback.
    *   *Relevance:* Foundational work on instruction tuning and RLHF (a precursor/relative to RLVR), establishing the paradigm of using RL to align LLMs, providing context for RLVR's development.
