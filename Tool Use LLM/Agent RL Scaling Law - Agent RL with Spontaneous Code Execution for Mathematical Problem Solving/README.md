https://arxiv.org/abs/2505.07773

**Agent RL Scaling Law: Spontaneous Code Execution for Mathematical Problem Solving**

1.  **Brief Summary and Rating:**

    This paper investigates how Large Language Models (LLMs) can be trained using reinforcement learning (RL) from outcome-based rewards to spontaneously learn to generate and execute Python code for solving mathematical problems, a method termed ZeroTIR (Zero-shot Tool-Integrated Reasoning). The central contribution is the identification and empirical characterization of an "Agent RL Scaling Law," which describes predictable improvements in key metrics—spontaneous code execution frequency, average response length, and final task accuracy—as RL training progresses. The authors implement a robust framework featuring a decoupled code execution environment and validate their findings using standard RL algorithms (PPO, Reinforce++) on base LLM models (Qwen 2.5 Base 7B/32B). Experiments demonstrate that ZeroTIR significantly surpasses non-tool ZeroRL baselines and supervised fine-tuning (SFT)-based tool-integrated reasoning methods on challenging math benchmarks like AIME and MATH500. The study also reveals that while a larger budget for tool interactions (N_max) generally improves performance, agents often converge to strategies involving a small number of high-utility code calls.

    **Rating: 8.5/10**

    For a PhD-level audience, this paper presents a solid and timely contribution. Its strengths lie in:
    *   **Novelty of "Agent RL Scaling Law":** Systematically characterizing the learning dynamics of spontaneous tool acquisition via RL as a scaling phenomenon is a valuable conceptual framing.
    *   **Focus on Spontaneous Tool Use from Base Models:** The ZeroRL approach, avoiding SFT on tool-use trajectories, is important for understanding emergent capabilities and potentially fostering more generalizable problem-solving.
    *   **Robust Experimental Setup and Evaluation:** The use of standard benchmarks, comparison against relevant baselines (including contemporaneous work like TORL), and ablations (e.g., N_max, RL algorithms, model sizes) lend credibility to the findings. The engineering efforts for a stable and efficient training environment (decoupled execution, asynchronous pipeline) are also commendable.
    *   **Practical Insights:** The observation that models tend to converge to single, high-utility code calls despite being allowed more interactions is an interesting finding regarding learned efficiency.

    The paper is generally well-written and clearly presents its methodology and results. While the "scaling law" is currently characterized empirically and qualitatively, its formal mathematical definition is rightly noted as future work. The work advances the understanding of how LLM agents can autonomously learn complex behaviors like tool use, providing a reproducible benchmark.

2.  **Main Ideas Discussed:**

    1.  **Agent RL Scaling Law for Spontaneous Tool Acquisition:** The core idea is that as a base LLM undergoes RL training with outcome-based rewards (ZeroTIR), its ability to spontaneously and effectively use external tools (like a Python code interpreter for math problems) improves in a predictable, scalable manner. This scaling is observed through correlated increases in the frequency of tool use, the length of generated responses (accommodating code and reasoning), and overall task success rate with increased training steps.
    2.  **Efficacy of Outcome-Based RL for Emergent Tool Use:** The paper demonstrates that LLMs can learn to leverage tools for complex reasoning tasks purely from outcome-based rewards, without needing supervised examples of tool invocation or specific prompt engineering to trigger tool use. This "ZeroRL" approach fosters an environment where the agent explores and discovers the utility of tools, leading to performance surpassing non-tool baselines and even some SFT-based methods. The findings suggest agents learn efficient strategies, often relying on a few high-utility tool calls.
    3.  **Robust Framework for Training Tool-Using LLM Agents:** The authors propose and validate a practical framework for enabling spontaneous tool use in LLMs. This includes a decoupled code execution environment (enhancing stability and scalability) and efficient interaction mechanisms during RL rollout (e.g., dynamic stop tokens for iterative reasoning and code generation, asynchronous pipelining for training speed), which are crucial for effectively training these agentic systems.

3.  **10 Most Important Citations:**

    1.  **Guo et al. 2025.** Deepseek-r1: Incentivizing reasoning capability in llms via reinforcement learning. This paper is crucial as it highlights the success of ZeroRL (RL directly from base models using outcome-based rewards) for enhancing LLM reasoning, a foundational concept upon which the current paper builds by extending it to spontaneous tool use.
        *   Link: `arXiv:2501.12948`

    2.  **Li et al. 2025.** Torl: Scaling tool-integrated rl. This is a significant contemporaneous work that also explores ZeroRL for tool-integrated mathematical reasoning, providing a direct point of comparison and validating the general approach explored in the reviewed paper.
        *   Link: `arXiv:2503.23383`

    3.  **Hu et al. 2025a.** Open-reasoner-zero: An open source approach to scaling up reinforcement learning on the base model. This work (and its associated dataset ORZ-57k) is important as it provides a framework and dataset used by the authors for their ZeroRL experiments, underpinning their implementation.
        *   Link: `arXiv:2503.24290`

    4.  **Schick et al. 2023.** Toolformer: Language Models Can Teach Themselves to Use Tools. This paper is foundational for the idea of LLMs learning to use tools, though it relies on an SFT approach, offering a contrast to the RL-based spontaneous tool use explored in the reviewed paper.
        *   Link: `arXiv:2302.04761`

    5.  **Schulman et al. 2017.** Proximal policy optimization algorithms. This paper introduces PPO, one of the key reinforcement learning algorithms employed and evaluated by the authors for training their ZeroTIR models.
        *   Link: `arXiv:1707.06347`

    6.  **Hendrycks et al. 2021.** Measuring mathematical problem solving with the math dataset. This paper introduces the MATH dataset, a critical benchmark used extensively in the reviewed paper to evaluate the mathematical reasoning capabilities of their trained models.
        *   Link: `https://arxiv.org/abs/2103.03874`

    7.  **Gao et al. 2022b.** PAL: Program-Aided Language Models. This paper is an influential early work showing how LLMs can leverage external code execution (programs) to improve reasoning, particularly in mathematical domains, setting a precedent for tool-augmented LLMs.
        *   (No direct arXiv link in paper, but this is a well-known NeurIPS paper: `https://arxiv.org/abs/2211.10435`)

    8.  **Yang et al. 2024.** Qwen2.5-math technical report: Toward mathematical expert model via self-improvement. This paper introduces the Qwen2.5-Math model, a specialized math model whose base version is used and TIR capabilities are compared against, making it a relevant baseline and context for the Qwen models used.
        *   Link: `arXiv:2409.12122`

    9.  **Nakano et al. 2022.** WebGPT: Browser-assisted Question-Answering with Human Feedback. This is a seminal work demonstrating the effectiveness of outcome-based RL (with human feedback) for teaching LLMs to use external tools (a web browser), influencing the broader field of agentic RL.
        *   Link: `arXiv:2112.09332`

    10. **Wei et al. 2022.** Chain-of-thought prompting elicits reasoning in large language models. This paper is foundational for improving LLM reasoning by prompting them to generate intermediate steps, a capability that tool use, as explored in the reviewed paper, aims to further enhance and verify computationally.
        *   (No direct arXiv link in paper, but this is a well-known NeurIPS paper: `https://arxiv.org/abs/2201.11903`)
