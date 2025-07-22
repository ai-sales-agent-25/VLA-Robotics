https://arxiv.org/abs/2504.13837

https://x.com/YangYue_THU/status/1929569066832060851

https://limit-of-rlvr.github.io/

**Does Reinforcement Learning Really Incentivize Reasoning Capacity in LLMs Beyond the Base Model?**

**1. Brief Summary and Rating**

This paper critically re-examines the widely held assumption that Reinforcement Learning with Verifiable Rewards (RLVR) endows Large Language Models (LLMs) with fundamentally new reasoning abilities beyond their pre-trained base models. Through extensive experiments across various model families, RL algorithms, and benchmarks (mathematics, coding, visual reasoning), the authors find that while RLVR-trained models outperform base models at low sampling counts (k in pass@k), base models often match or even surpass RL-trained models at large k values. This suggests that RLVR primarily enhances sampling efficiency by biasing the model's output distribution towards known correct reasoning paths already present in the base model's sampling distribution. However, this comes at the cost of reducing the model's exploration capacity and narrowing its overall reasoning boundary compared to the base model. The paper further demonstrates that, unlike RLVR, distillation can genuinely introduce new knowledge and expand the reasoning capabilities of a model. The authors conclude that RLVR, in its current form, does not elicit new reasoning patterns but rather refines the selection from existing ones, highlighting a critical limitation in advancing LLM reasoning and suggesting the need for new training paradigms.

**Rating: 9/10**

For a PhD-level audience, this paper is highly valuable.
*   **Novelty & Impact:** It challenges a significant and popular belief in the field regarding the role of RLVR in LLM reasoning. The findings have strong implications for future research directions in developing more capable reasoning models.
*   **Rigor:** The experimental setup is comprehensive, covering multiple model families (Qwen, LLaMA), sizes, tasks (math, code, visual reasoning), and RL algorithms. The use of pass@k at large k to probe the "reasoning boundary" is a sound methodological choice for their argument, and the manual CoT analysis adds depth.
*   **Clarity:** The paper is well-written, and its central argument is clearly articulated and consistently supported by the presented evidence. The distinction made between sampling efficiency and true reasoning capacity expansion is insightful.
*   **Contribution:** It provides a nuanced understanding of what RLVR achieves and, more importantly, what it doesn't. The comparison with distillation further clarifies the mechanisms of knowledge acquisition in LLMs.

The paper effectively "pours some cold water" on the hype surrounding RLVR as a mechanism for *creating* new reasoning, framing it more as an optimization or biasing technique. This critical perspective is essential for scientific progress. A point could potentially be deducted if one argues the core idea (RL as exploitation of existing knowledge) isn't entirely novel in a broader RL context, but its specific, rigorous demonstration for RLVR in LLMs and the implications drawn are significant.

**2. Main Ideas Discussed**

1.  **RLVR Enhances Sampling Efficiency but Reduces Overall Reasoning Capacity:** The primary finding is that RLVR makes LLMs more efficient at finding correct solutions (higher pass@1 or pass@k for small k) by biasing their output towards rewarded reasoning paths. However, this comes at the cost of exploration, leading to a narrower scope of solvable problems when allowed extensive sampling (lower pass@k for large k) compared to the base model, suggesting the base model has a wider, albeit less efficiently accessed, reasoning capacity.
2.  **Reasoning Paths in RLVR Models are Pre-existing in Base Models:** The paper argues through perplexity analysis and empirical results (RL-trained models' solvable problems being a subset of the base model's) that RLVR does not teach the model fundamentally new reasoning patterns or CoTs. Instead, the reasoning abilities manifested by RL-trained models are already latently present within the base model's distribution; RL training just makes them more probable to be sampled.
3.  **Distillation Fundamentally Differs from RLVR by Expanding Reasoning Capacity:** In contrast to RLVR, the paper shows that distillation from a more capable teacher model can genuinely introduce new knowledge and reasoning patterns not present in the student base model, thereby expanding its reasoning boundary beyond what the base model alone could achieve.

**3. List of 10 Most Important Citations**

1.  **Guo et al. 2025.** Deepseek-r1: Incentivizing reasoning capability in llms via reinforcement learning.
    *   This paper represents a key work demonstrating the success of RLVR (specifically the "zero" RL setting) in enhancing LLM reasoning, serving as a prime example of the prevailing belief that the current paper critically examines and refutes in terms of *new* capability generation. It is also used as an example for distillation. (Link: arXiv:2501.12948)
2.  **Brown et al. 2024.** Large language monkeys: Scaling inference compute with repeated sampling.
    *   This citation is crucial for the methodology, as the current paper uses the pass@k metric with large values of k, as explored by Brown et al., to define and evaluate the reasoning capability boundary of LLMs.
3.  **Chen et al. 2021.** Evaluating large language models trained on code.
    *   This paper introduced the pass@k metric, particularly its unbiased estimation method, which is a core evaluation technique adopted and extended by the current work to assess reasoning across various tasks. (Link: arXiv:2107.03374)
4.  **Lambert et al. 2024.** T\"ulu 3: Pushing frontiers in open language model post-training.
    *   Cited as evidence for Reinforcement Learning with Verifiable Rewards (RLVR) being a key driver behind recent advances in LLM reasoning capabilities, setting the context for the paper's investigation. (Link: arXiv:2411.15124)
5.  **Schulman et al. 2017.** Proximal policy optimization algorithms.
    *   PPO is a foundational RL algorithm frequently used in RLVR for LLMs, and it's one of the algorithms discussed and implicitly evaluated in the paper's experiments on different RL methods. (Link: arXiv:1707.06347)
6.  **Jaech et al. 2024.** Openai o1 system card.
    *   Cited as an example of a reasoning-centric LLM (OpenAI-o1) that advanced the frontier, with RLVR being a key component, thus representing the type of model whose training paradigm is being analyzed. (Link: arXiv:2412.16720)
7.  **Ouyang et al. 2022.** Training language models to follow instructions with human feedback.
    *   This is a foundational paper on applying reinforcement learning (RLHF) to LLMs, which paved the way for subsequent RL-based methods like RLVR for more specific capabilities like reasoning.
8.  **Zeng et al. 2025.** Simplerl-zoo: Investigating and taming zero reinforcement learning for open base models in the wild.
    *   The RLVR-trained models (Oat-Zero based on Qwen-2.5) from SimpleRLZoo are used in the paper's mathematical reasoning experiments, making this a direct source for their empirical study. (Link: arXiv:2503.18892)
9.  **Shao et al. 2024.** Deepseekmath: Pushing the limits of mathematical reasoning in open language models.
    *   Cited for the GRPO (Generalized Reward Policy Optimization) algorithm, which is a critic-free RL variant used in the experiments, and represents recent efforts in math reasoning with RL. (Link: arXiv:2402.03300)
10. **Liu et al. 2025b.** Understanding r1-zero-like training: A critical perspective.
    *   The RL model Oat-Zero-7B developed by Liu et al. is specifically analyzed, and their work provides a critical perspective on zero-RL training, aligning with the current paper's theme of scrutinizing RLVR's effects. (Link: Notion page via https://oatllm.notion.site/oat-zero, then to arXiv:2503.20783)
