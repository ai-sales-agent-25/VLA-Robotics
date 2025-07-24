https://arxiv.org/abs/2503.23383

TORL: Scaling Tool-Integrated RL

1.  **Summary and Rating:**

    This paper introduces TORL (Tool-Integrated Reinforcement Learning), a framework designed to train large language models (LLMs) to autonomously utilize computational tools by applying reinforcement learning directly from base models, circumventing the need for prior supervised fine-tuning (SFT) on tool-use trajectories. The core idea is that by enabling unrestricted exploration via RL from scratch, models can discover more optimal and nuanced strategies for tool integration than those learned by imitating predefined SFT datasets or incrementally improving SFT-trained models.

    Experiments conducted with Qwen2.5-Math base models demonstrate TORL's efficacy, showing substantial performance improvements on mathematical reasoning benchmarks like AIME24. For instance, TORL-7B surpasses RL without tool integration by 14% and the best existing Tool-Integrated Reasoning (TIR) model (presumably SFT-based or SFT+RL) by 17% on AIME24. A key contribution highlighted is the emergence of sophisticated cognitive behaviors—such as strategic tool invocation based on problem characteristics, self-regulation where the model learns to avoid ineffective code patterns, and dynamic adaptation between computational tool use and analytical reasoning—all learned implicitly through reward-driven optimization rather than explicit instruction. The authors also analyze design choices like tool call frequency control and the impact of reward shaping (e.g., penalties for non-executable code, which surprisingly did not improve performance).

    **Rating: 9/10**

    The paper presents a well-motivated and clearly articulated approach to a significant problem in LLM reasoning: effective and flexible tool integration. The methodological shift towards RL directly from base models for tool use is a valuable contribution, offering a pathway to potentially more general and robust tool-using agents. The empirical results are strong, demonstrating clear improvements over relevant baselines. The analysis of emergent cognitive behaviors is particularly insightful and elevates the paper beyond a simple performance demonstration, providing qualitative evidence of sophisticated learning. The ablation studies on design choices (like the maximum tool calls `C` and reward structure) are useful. The open-sourcing of implementations, datasets, and models further strengthens its contribution to the research community. It's a solid piece of engineering and research that pushes the boundaries of LLM capabilities in a practical and scalable manner.

2.  **Main Ideas Discussed:**

    1.  **Direct Reinforcement Learning for Tool Integration from Base Models:** The central idea is that LLMs can learn to effectively use tools (like a Python interpreter for calculations) through reinforcement learning applied directly to "raw" base models, without requiring prior supervised fine-tuning on tool-use examples. This allows for more unrestricted exploration and discovery of optimal tool-use strategies compared to methods that rely on SFT or incrementally improve SFT-trained models.
    2.  **Emergence of Complex Cognitive Behaviors:** Through reward-driven learning alone, TORL-trained models develop sophisticated, uninstructed behaviors. These include strategic tool invocation (deciding when and how to use tools), self-regulation (e.g., identifying and reducing the generation of ineffective or erroneous code), and dynamic adaptation between computational reasoning (using tools) and analytical reasoning (natural language steps), sometimes even cross-validating results from one mode with the other.
    3.  **Scalable Performance Improvements in Mathematical Reasoning:** The TORL framework leads to significant performance gains on challenging mathematical reasoning benchmarks (AIME24, MATH500, etc.) across different model sizes (1.5B and 7B parameters). This demonstrates the scalability of the approach and its effectiveness in tasks requiring precise computation and complex reasoning steps, outperforming both non-tool-integrated RL models and existing SFT-based tool-integrated models.

3.  **10 Most Important Citations:**

    1.  **Yang et al. 2024.** Qwen2.5-math technical report: Toward mathematical expert model via self-improvement.
        *   This paper provides the Qwen2.5-Math base models that TORL experiments are built upon, and also describes Qwen2.5-Math-Instruct-TIR, a key comparative model that uses SFT before RL for tool integration.
    2.  **Wei et al. 2022.** Chain-of-thought prompting elicits reasoning in large language models.
        *   This foundational paper introduces Chain-of-Thought prompting, a standard natural language reasoning technique whose limitations in precise computation motivate the need for tool-integrated approaches like TORL.
    3.  **Gou et al. 2023.** Tora: A tool-integrated reasoning agent for mathematical problem solving.
        *   Represents a significant existing Tool-Integrated Reasoning (TIR) approach, often relying on SFT, which TORL aims to improve upon by enabling more flexible strategy discovery through direct RL.
    4.  **Hendrycks et al. 2021.** Measuring mathematical problem solving with the math dataset.
        *   This paper introduced the MATH dataset, one of the challenging mathematical benchmarks used extensively in this paper to evaluate TORL's performance.
    5.  **Shao et al. 2024.** Deepseekmath: Pushing the limits of mathematical reasoning in open language models.
        *   The GRPO (Generalized Reinforcement Learning from Online Human-Preference Optimization) algorithm, used for training in TORL, is associated with the authors/work of Deepseek, highlighting a state-of-the-art RL technique for LLMs.
    6.  **Li et al. 2025.** Limr: Less is more for rl scaling.
        *   Introduces LIMR, the reinforcement learning data distillation technique explicitly used by the authors to construct their high-quality, difficulty-balanced dataset for training TORL models.
    7.  **Sheng et al. 2024.** Hybridflow: A flexible and efficient rlhf framework.
        *   Provides the veRL (Hybridflow) framework, which is the specific software infrastructure used to conduct all of TORL's reinforcement learning experiments.
    8.  **Gao et al. 2023.** Pal: Program-aided language models.
        *   This is an influential early work demonstrating how LLMs can leverage external programs (code execution) to improve reasoning, setting the stage for more advanced tool-integration methods like TORL.
    9.  **Hu et al. 2025.** Open-reasoner-zero: An open source approach to scaling reinforcement learning on the base model.
        *   This work represents a contemporaneous open-source effort in scaling RL directly on base models, aligning with TORL's philosophy and highlighting a broader trend in the field. Link: https://github.com/Open-Reasoner-Zero/Open-Reasoner-Zero
    10. **Luo et al. 2025.** Deepscaler: Surpassing o1-preview with a 1.5b model by scaling rl.
        *   This paper contributes the DeepScaleR dataset, which is one of the sources for TORL's training data, and also showcases another successful effort in scaling RL for LLMs. Link: https://pretty-radio-b75.notion.site/DeepScaleR-Surpassing-01-Preview-with-a-1-5B-Model-by-Scaling-RL-19681902c1468005bed8
