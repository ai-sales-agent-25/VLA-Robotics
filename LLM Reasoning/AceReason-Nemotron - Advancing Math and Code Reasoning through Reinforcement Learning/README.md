https://arxiv.org/abs/2505.16400

https://x.com/_weiping/status/1925730974827991072

AceReason-Nemotron: Advancing Math and Code Reasoning through Reinforcement Learning

**1. Summary and Rating**

This paper demonstrates that large-scale reinforcement learning (RL) can significantly enhance the mathematical and code reasoning capabilities of strong, pre-existing small- and mid-sized supervised fine-tuned (SFT) models, enabling them to surpass state-of-the-art distillation-based models. The authors propose a sequential RL training strategy: first training on math-only prompts, then on code-only prompts. Notably, math-only RL is shown to improve performance not only on math benchmarks but also on code reasoning tasks, indicating cross-domain generalization. Subsequent code-only RL further boosts code performance with minimal degradation to math capabilities. The work emphasizes the importance of a robust data curation pipeline for collecting challenging problems with verifiable solutions and introduces key experimental insights, including curriculum learning with progressively increasing response lengths and the stabilizing effect of strict on-policy parameter updates. The authors find that RL elicits foundational reasoning capabilities and pushes models to solve problems previously beyond their reach. The resulting AceReason-Nemotron models (7B and 14B) achieve competitive or superior results on benchmarks like AIME and LiveCodeBench.

**Rating: 9/10**

This paper receives a high rating for several reasons.
*   **Significant Contribution:** It compellingly challenges the prevailing notion that distillation is unequivocally superior to RL for smaller/mid-sized reasoning models, demonstrating RL's potential when carefully applied. The performance improvements are substantial.
*   **Novel Methodology Aspect:** The sequential math-then-code RL approach is simple yet effective, and the finding of math-RL benefiting code reasoning is a noteworthy insight into cross-domain generalization through RL.
*   **Rigorous Experimentation:** The paper includes extensive ablation studies (e.g., on-policy updates, length extension, prompt difficulty, interplay of math/code RL) and detailed analysis, lending strong support to its conclusions.
*   **Practical Insights:** It provides valuable, actionable insights into the RL training recipe for complex reasoning tasks, such as data curation strategies, curriculum learning, and handling noisy rewards, which are often missing from reports on frontier models.
*   **Clarity and Reproducibility:** The paper is well-written and clearly presents its methods and findings. The authors also plan to release the model and dataset, which is commendable for reproducibility and further research.
The work is a solid piece of engineering and empirical research that pushes the boundaries of RL for reasoning in LLMs, making a valuable contribution to a sophisticated audience. A point could potentially be argued if the core RL algorithm (GRPO) itself isn't novel to this paper, but its specific application, sequencing, and the surrounding meticulous training regime for reasoning tasks provide substantial novelty.

**2. Main Ideas Discussed**

1.  **Sequential Domain-Specific RL for Enhanced Reasoning:** The core methodological proposal is to first apply RL using math-only prompts, followed by RL using code-only prompts. This staged approach is shown to be highly effective, with math-only RL unexpectedly boosting both math and code reasoning abilities, and subsequent code-only RL further improving code performance without significant catastrophic forgetting in math.
2.  **RL Surpassing Distillation for Mid-Sized Models:** The paper demonstrates that with a carefully curated dataset and a refined RL training process, RL can significantly improve strong SFT (distilled) models, achieving performance that surpasses state-of-the-art distillation-based models of similar sizes, particularly for the 14B parameter scale. This suggests RL can unlock capabilities beyond what SFT/distillation alone can achieve from a given base model.
3.  **Criticality of Data Curation and RL Training Recipe:** The success of the RL approach hinges on a robust data curation pipeline (generating high-quality, verifiable problems) and specific RL training strategies. These include curriculum learning (progressively increasing maximum response length and problem difficulty) and strict on-policy updates to maintain training stability and prevent entropy collapse, which are crucial for eliciting and expanding the model's reasoning abilities.

**3. 10 Most Important Citations**

1.  Guo et al. 2025. Deepseek-R1: Incentivizing reasoning capability in LLMs via reinforcement learning.
    This paper introduced DeepSeek-R1, whose open-sourcing and RL-based success significantly influenced the research direction, and the current work builds upon distilled versions of DeepSeek-R1-Qwen models and follows its evaluation protocols.
2.  Shao et al. 2024. DeepseekMath: Pushing the limits of mathematical reasoning in open language models.
    This work introduced the GRPO algorithm, which is the specific reinforcement learning algorithm adopted and adapted by AceReason-Nemotron for its training framework.
3.  OpenAI. 2024. Learning to reason with LLMS.
    The release of models like OpenAI's o1 is cited as a key event that attracted significant attention to building reasoning models using large-scale reinforcement learning, setting the context for this research.
4.  Liu et al. 2024. AceMath: Advancing frontier math reasoning with post-training and reward modeling.
    The rule-based Python verification function for math problems used in this paper is built on top of sympy, following the approach detailed in AceMath.
5.  Jain et al. 2024. Livecodebench: Holistic and contamination free evaluation of large language models for code.
    LiveCodeBench is a primary benchmark used for evaluating the code reasoning capabilities of AceReason-Nemotron, and its repository's code execution tools are used for coding problem verification.
6.  Bercovich et al. 2025. Llama-Nemotron: Efficient Reasoning Models.
    Llama-Nemotron represents a state-of-the-art distillation-based reasoning model that this paper compares against, particularly challenging its finding that distillation outperforms RL for smaller models.
7.  Luo et al. 2025. Deepcoder: A fully open-source 14b coder at o3-mini level.
    DeepCoder-14B is a state-of-the-art open-source code generation model used as a key performance comparison point in the code evaluation benchmarks.
8.  Moshkov et al. 2025. Aimo-2 winning solution: Building state-of-the-art mathematical reasoning models with openmathreasoning dataset.
    This paper presents OpenMath-Nemotron models, which are strong SOTA specialized distilled math models that AceReason-Nemotron is benchmarked against.
9.  Ahmad et al. 2025. Opencodereasoning: Advancing data distillation for competitive coding.
    This work introduces OpenCodeReasoning models, which are state-of-the-art distilled models for code reasoning that AceReason-Nemotron compares its performance against.
10. Yang et al. 2024. Qwen2.5 technical report.
    The initial SFT models (DeepSeek-R1-Distill-Qwen-7B/14B) used as the starting point for RL in this paper are based on the Qwen2.5 model family, making this report relevant for understanding the base architecture.
