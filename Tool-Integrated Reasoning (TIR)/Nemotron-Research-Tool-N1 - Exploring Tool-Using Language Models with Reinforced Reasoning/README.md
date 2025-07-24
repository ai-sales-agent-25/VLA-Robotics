https://arxiv.org/abs/2505.00024?utm_source=chatgpt.com

Nemotron-Research-Tool-N1: Exploring Tool-Using Language Models with Reinforced Reasoning

### 1. Summary and Rating

This paper introduces Nemotron-Research-Tool-N1 (Tool-N1), a series of large language models designed for enhanced tool-calling capabilities. The authors challenge the prevailing method of supervised fine-tuning (SFT) on tool-use trajectories distilled from more powerful models, arguing that it often leads to "imitative reasoning" and limits generalization. Instead, they employ a rule-based reinforcement learning (RL) strategy based on the GRPO algorithm. The core of their method is a lightweight, binary reward signal that only assesses the structural format and functional correctness of the final tool invocation. This approach forgoes explicit supervision of intermediate reasoning steps, allowing the model to develop its own reasoning strategies.

Through extensive experiments on benchmarks like BFCL, APIBank, and ACEBench, the paper demonstrates that their Tool-N1 models (7B and 14B) outperform strong closed-source models like GPT-4o and specialized SFT models. A key contribution is a systematic study comparing SFT, RL, and the common SFT-then-RL pipeline. Their findings compellingly suggest that a pure RL approach, even without distilled reasoning data, can achieve superior performance, questioning the utility of the widely adopted SFT-then-RL paradigm for this task.

**Rating: 9/10**

The paper earns a high rating for several reasons. It addresses a highly relevant and critical problem in the development of agentic LLMs: moving beyond brittle, imitative behavior in tool use. The methodological contribution, while building on prior "R1-style" RL, is its simple and effective application to the complex, general tool-calling domain. The most significant contribution is the rigorous experimental investigation into training recipes (SFT vs. RL). The finding that pure RL can outperform the SFT-then-RL pipeline is a potent, paradigm-questioning result that provides immediate, actionable insight for practitioners in the field. The thorough ablations on reward design and data composition further strengthen the paper's conclusions, making it a valuable and impactful piece of research for the LLM community.

### 2. Main Ideas

1.  **Reinforced Reasoning with Lightweight Supervision:** The central idea is to train tool-using LLMs with reinforcement learning using a simple, binary reward. Instead of providing dense supervision on the step-by-step reasoning process (as in SFT on distilled trajectories), the reward function only verifies that the output follows a correct format (i.e., contains `<think>` and `<tool_call>` tags) and that the generated tool call is functionally correct (correct tool name and arguments). This lightweight supervision encourages the model to learn *how* to reason for itself to achieve the correct tool invocation, rather than just mimicking the surface patterns of a teacher model.

2.  **Pure Reinforcement Learning Can Outperform SFT-then-RL:** A key finding of the paper is that the widely adopted "SFT-then-RL" pipeline is not necessarily optimal for tool-learning. Through a controlled study using a curated dataset of 5,518 reasoning trajectories, the authors show that a pure RL approach achieves the best performance, surpassing both SFT alone and the SFT+RL combination. This suggests that the initial SFT phase on distilled data may not provide significant benefits and might even hinder performance by biasing the model towards imitation, while pure RL allows for more effective and robust learning.

3.  **Binary Rewards and Structured Formatting are Critical:** The paper's ablation studies emphasize the importance of specific design choices in the RL framework. They find that a strict, binary reward (1 for a perfect tool call, 0 otherwise) leads to better performance than fine-grained rewards that give partial credit for correct formatting or function names. This suggests that partial rewards can lead to "reward hacking," where the model learns to satisfy superficial criteria without achieving full functional correctness. Furthermore, enforcing a structured reasoning format via prompting is shown to be crucial for reliable and generalizable tool use.

### 3. 10 Most Important Citations

1.  **Guo et al. 2025. Deepseek-r1: Incentivizing reasoning capability in llms via reinforcement learning.** This paper is the primary inspiration for the "R1-style" rule-based reinforcement learning approach that forms the core of the authors' methodology.
2.  **Chen et al. 2025. Acebench: Who wins the match point in tool learning?** This work is cited for identifying the problem of "pseudo reasoning" from SFT on distilled trajectories and for providing the ACEBench benchmark used for evaluation.
3.  **Yan et al. 2024. Berkeley function calling leaderboard.** This citation provides the main benchmark, the Berkeley Function Call Leaderboard (BFCL), which is used for the paper's primary performance evaluations and comparisons.
    *   Link: `https://gorilla.cs.berkeley.edu/blogs/8_berkeley_function_calling_leaderboard.html`
4.  **Liu et al. 2024. Toolace: Winning the points of llm function calling.** This paper introduced the ToolACE dataset, which is a major source of training data and a key specialized baseline model that Tool-N1 is compared against.
5.  **Zhang et al. 2024. xlam: A family of large action models to empower ai agent systems.** This work introduced the xLAM dataset, the other primary source of training data used to train the Tool-N1 models.
6.  **Wei et al. 2022. Chain-of-thought prompting elicits reasoning in large language models.** This foundational paper is cited to establish the importance of step-by-step reasoning for solving complex tasks, motivating the authors' focus on explicitly encouraging a reasoning phase before tool invocation.
7.  **Shao et al. 2024. Deepseekmath: Pushing the limits of mathematical reasoning in open language models.** This paper is referenced as a successful application of R1-style RL and for its use of the GRPO algorithm, which is also employed in this work.
8.  **Li et al. 2023. Api-bank: A comprehensive benchmark for tool-augmented llms.** This paper provides the APIBank benchmark, which the authors use to demonstrate the generalization capabilities of their method on an additional tool-use task.
9.  **Yao et al. 2023. React: Synergizing reasoning and acting in language models.** This is cited as a seminal work in combining reasoning and action, representing an alternative prompting-based approach to the training-based method explored in the paper.
10. **Touvron et al. 2023. Llama: Open and efficient foundation language models.** This paper introduced the LLaMA models, which are used as an alternative backbone in experiments to test the generalizability of the proposed RL training paradigm across different model families.
