https://arxiv.org/abs/2505.10832

**Learning When to Think: Shaping Adaptive Reasoning in R1-Style Models via Multi-Stage RL**

**1. Summary and Rating**

This paper addresses the "over-thinking" problem in Large Reasoning Models (LRMs), where models generate extensive, computationally expensive reasoning steps even for simple tasks. The authors propose **AutoThink**, a multi-stage reinforcement learning (RL) framework designed to equip R1-style models (which use a <think> then <answer> format) with adaptive reasoning capabilities. The core idea begins with an "ellipsis prompt" ("...") which, when inserted after the <think> tag, stochastically triggers either a thinking or no-thinking mode in the LRM without further training. AutoThink then leverages this emergent controllability through a three-stage RL process: Stage 1 stabilizes these dual modes using batch reward balancing; Stage 2 reinforces correct behavior within each mode to improve accuracy; and Stage 3 prunes redundant reasoning steps using a length-aware reward. Experiments on mathematical benchmarks show that AutoThink achieves a favorable trade-off between accuracy and computational efficiency (token usage) compared to standard prompting, no-thinking prompts, and other RL-based pruning methods. Notably, it improves accuracy while significantly reducing token usage on models like DeepSeek-R1-Distill-Qwen-1.5B.

**Rating: 8.5/10**

This paper presents a novel and practical approach to a well-recognized problem in LLM reasoning. The discovery of the "ellipsis prompt" effect is an interesting empirical finding that provides a simple yet effective mechanism for inducing controllable reasoning modes. The multi-stage RL framework is a well-thought-out strategy to progressively shape this behavior, balancing exploration of different reasoning modes with exploitation of efficient and accurate pathways. The experimental results are convincing, demonstrating clear improvements in the accuracy-efficiency frontier. The methodology is sound, and the paper is clearly written. For a PhD-level audience, the work is valuable for its clever use of an emergent model property and its structured RL approach to fine-tuning complex behaviors. The introduction of the E-F1 metric is also a useful contribution for evaluating this specific trade-off. The slight deduction is for the reliance on an empirically discovered prompt behavior, which might vary across different model architectures or scales, and the potential for reward hacking (acknowledged by the authors). However, the staged refinement process seems robust.

**2. Main Ideas Discussed**

The main ideas discussed in this paper are:

1.  **Ellipsis Prompt for Stochastic Reasoning Control:** The paper identifies that a minimal prompt modification—inserting a simple ellipsis ("...") after the <think> tag in R1-style models—can stochastically trigger either an explicit step-by-step thinking mode or a more direct, no-thinking (concise answer) mode. This reveals a latent controllability in these models without requiring architectural changes or extensive initial fine-tuning for this specific behavior.
2.  **Multi-Stage Reinforcement Learning (AutoThink) for Adaptive Reasoning:** The core contribution is AutoThink, a three-stage RL framework that progressively shapes the model's reasoning policy.
    *   **Stage 1 (Stabilize Dual Modes):** Prevents the model from collapsing into a single mode (always thinking or never thinking) by using batch-level reward balancing to encourage exploration of both.
    *   **Stage 2 (Reinforce Correct Behavior):** Improves the accuracy of both thinking and no-thinking modes by rewarding correct answers, allowing the model to learn when each mode is most effective.
    *   **Stage 3 (Prune Redundant Reasoning):** Introduces a length-aware reward to penalize overly long reasoning paths (especially for correct answers) and encourage conciseness, particularly in the no-thinking mode or for simpler problems.
3.  **Achieving Task-Adaptive Reasoning Efficiency:** By learning *when* to engage in detailed reasoning versus providing a succinct answer based on problem complexity, AutoThink enables LRMs to allocate computational resources more effectively. This leads to significant reductions in token usage (and thus latency/cost) while maintaining or even improving accuracy on complex reasoning tasks.

**3. List of 10 Most Important Citations**

1.  **Guo et al. 2025.** Deepseek-r1: Incentivizing reasoning capability in llms via reinforcement learning. arXiv preprint arXiv:2501.12948, 2025.
    *   This citation is crucial as DeepSeek-R1 and its distilled variants are the primary "R1-style models" upon which AutoThink is built and evaluated, defining the <think>/<answer> paradigm the paper addresses.
2.  **Wei et al. 2022.** Chain-of-thought prompting elicits reasoning in large language models. Advances in neural information processing systems, 35:24824-24837, 2022.
    *   This paper introduced Chain of Thought (CoT) prompting, which is the foundational reasoning scheme (explicit step-by-step generation) that R1-style models and AutoThink aim to make more adaptive and efficient.
3.  **Luo et al. 2025.** Deepscaler: Surpassing o1-preview with a 1.5b model by scaling rl, 2025. Notion Blog.
    *   DeepScaleR is another key R1-style model used for evaluation, representing a state-of-the-art smaller reasoning model that AutoThink demonstrates improvements upon, showing its applicability to already optimized models.
4.  **Sui et al. 2025.** Stop overthinking: A survey on efficient reasoning for large language models. arXiv preprint arXiv:2503.16419, 2025.
    *   This survey highlights the "over-thinking" problem that AutoThink directly aims to solve, providing context for the importance and timeliness of the research.
5.  **Hou et al. 2025.** Thinkprune: Pruning long chain-of-thought of llms via reinforcement learning. arXiv preprint arXiv:2504.01296, 2025.
    *   ThinkPrune is a key RL-based baseline method for efficient reasoning that AutoThink is compared against, representing a competing approach to reducing reasoning verbosity.
6.  **Ma et al. 2025.** Reasoning models can be effective without thinking. arXiv preprint arXiv:2504.09858, 2025.
    *   This paper explores the "no-thinking" prompt strategy, which serves as an important baseline and a conceptual counterpoint to the adaptive thinking enabled by AutoThink.
7.  **Zhang et al. 2025.** Grpo-lead: A difficulty-aware reinforcement learning approach for concise mathematical reasoning in language models. arXiv preprint arXiv:2504.09696, 2025.
    *   This citation (GRPO-LEAD) is directly inspirational for Stage 3 of AutoThink (length-aware reward shaping) and employs the GRPO algorithm, which AutoThink also utilizes.
8.  **Yu et al. 2025.** Dapo: An open-source llm reinforcement learning system at scale. arXiv preprint arXiv:2503.14476, 2025.
    *   DAPO introduces key RL techniques like dynamic group sampling (used in GRPO, which AutoThink employs), relevant to the RL methodology of the paper.
9.  **Fatemi et al. 2025.** Concise reasoning via reinforcement learning. arXiv preprint arXiv:2504.05185, 2025.
    *   This is cited as "Concise-RL," another RL-trained baseline that aims to shorten reasoning traces, providing a point of comparison for AutoThink's efficiency gains.
10. **Anthropic. 2025.** Claude 3.7 sonnet, 2025. URL https://www.anthropic.com/claude/sonnet.
    *   This citation is mentioned for introducing a controllable reasoning framework in industry models, showing parallel efforts and motivating the need for academic exploration of adaptive reasoning.
