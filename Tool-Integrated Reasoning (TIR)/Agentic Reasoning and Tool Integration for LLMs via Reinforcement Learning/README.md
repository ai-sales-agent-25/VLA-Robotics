https://arxiv.org/abs/2505.01441

**Agentic Reasoning and Tool Integration for LLMs via Reinforcement Learning**

### 1. Summary and Rating

This paper introduces ARTIST (Agentic Reasoning and Tool Integration in Self-improving Transformers), a unified framework designed to enhance Large Language Models (LLMs) by integrating agentic reasoning, tool use, and reinforcement learning (RL). The authors identify a core limitation of existing LLMs: their reliance on static, internal knowledge and text-only reasoning, which hinders performance on tasks requiring dynamic interaction, multi-step planning, and precise computation.

ARTIST addresses this by enabling an LLM to autonomously decide when, how, and which external tools (like code interpreters or web search) to use within its reasoning process. The framework structures the model's output as an interleaved sequence of internal thought, tool calls, and tool outputs. This entire process is trained end-to-end using an outcome-based RL algorithm, Group Relative Policy Optimization (GRPO), which rewards the model based on the final outcome's correctness without requiring step-by-step supervision. This approach allows the model to learn robust and adaptive strategies for tool invocation.

The authors conduct extensive experiments on two challenging domains: complex mathematical reasoning (on benchmarks like AIME, AMC, and Olympiad) and multi-turn function calling (on BFCL v3 and T-bench). The results show that ARTIST significantly outperforms a wide range of baselines, including powerful frontier models like GPT-4o, prompt-based methods, and other tool-augmented models. Notably, the paper demonstrates that the framework fosters emergent agentic capabilities such as iterative self-correction and self-refinement.

**Rating: 9/10**

ARTIST presents a compelling and well-executed solution to a significant, well-known problem in LLM research. The novelty lies in the tight, synergistic coupling of agentic reasoning and dynamic tool use, optimized via a scalable, outcome-based RL algorithm. The experimental design is rigorous, featuring comprehensive comparisons on difficult benchmarks and insightful metric analyses that effectively demonstrate the superiority of this integrated approach over prompting or supervised methods. The paper is well-written, clearly articulating its contribution and placing it firmly within the context of related work. The demonstrated emergent capabilities and the strong empirical gains, even over much larger proprietary models, establish this work as a significant step toward more autonomous and capable AI systems.

### 2. Main Ideas

1.  **Unified Framework of Reasoning, Tools, and RL:** The central thesis is that reasoning, tool use, and learning should not be treated as separate modules. ARTIST proposes a unified framework where tool interaction is a "first-class operation" within the LLM's reasoning chain. The model learns to interleave internal reasoning (`<think>`) with tool invocations (`<tool_name>`) and their resulting outputs (`<output>`), creating a dynamic feedback loop that is trained end-to-end. This tight integration allows the model to learn not just *to use* tools, but to strategize *how and when* to use them in a context-aware manner.

2.  **Outcome-Based RL for Agentic Strategy Learning:** The framework avoids the need for expensive, step-by-step supervised data on how to use tools. Instead, it employs Group Relative Policy Optimization (GRPO), an RL algorithm that guides the model based on simple outcome-based rewards (e.g., is the final answer correct?). By optimizing for the final result, the model is free to explore and learn complex, multi-step strategies for problem-solving, leading to more robust and generalizable tool-use behaviors.

3.  **Emergent Agentic Capabilities:** A key finding is that sophisticated agentic behaviors—such as **self-correction** (diagnosing and fixing tool errors), **self-refinement** (iteratively improving an approach based on intermediate results), and **self-reflection** (evaluating and explaining its own reasoning)—arise naturally from the ARTIST framework. These capabilities are not explicitly supervised but emerge from the model learning to maximize its outcome-based reward within the structured reasoning-and-action loop, highlighting the power of the approach to foster deeper reasoning.

### 3. 10 Most Important Citations

1.  **Shao et al. 2024. Deepseekmath: Pushing the limits of mathematical reasoning in open language models.**
    This paper introduces Group Relative Policy Optimization (GRPO), the core reinforcement learning algorithm that ARTIST adopts to train its models using outcome-based rewards.

2.  **Schulman et al. 2017. Proximal policy optimization algorithms.**
    This work introduced Proximal Policy Optimization (PPO), a foundational RL algorithm upon which GRPO is based, making it critical for understanding the underlying optimization method.

3.  **Wei et al. 2023. Chain-of-thought prompting elicits reasoning in large language models.**
    This paper introduced chain-of-thought (CoT) prompting, a foundational technique for improving LLM reasoning that ARTIST builds upon by integrating external tool use into the thought process.

4.  **Schick et al. 2023. Toolformer: Language models can teach themselves to use tools.**
    This is a seminal paper demonstrating that LLMs can learn to use external tools via self-supervised learning, establishing a key area of research that ARTIST significantly advances with its RL-based approach.

5.  **Gao et al. 2023. Pal: Program-aided language models.**
    This paper introduced an influential method for using LLMs to generate code (for a Python interpreter) to solve reasoning problems, a technique directly related to ARTIST's mathematical reasoning case study and used as a baseline for comparison.
    *   **Link:** https://arxiv.org/abs/2211.10435

6.  **Ouyang et al. 2022. Training language models to follow instructions with human feedback.**
    This paper popularized the use of Reinforcement Learning from Human Feedback (RLHF) to align LLMs, establishing RL as a critical method for improving model behavior, a paradigm that ARTIST extends to the domain of tool-integrated reasoning.
    *   **Link:** https://arxiv.org/abs/2203.02155

7.  **DeepSeek-AI et al. 2025. Deepseek-r1: Incentivizing reasoning capability in llms via reinforcement learning.**
    This work is cited as a powerful frontier model that also successfully utilizes the GRPO algorithm for reasoning, serving as a key state-of-the-art baseline in ARTIST's experiments.
    *   **Link:** https://arxiv.org/abs/2501.12948

8.  **Sutton et al. 1998. Reinforcement learning: An introduction, volume 1.**
    This is the foundational textbook for reinforcement learning, cited by the paper to ground its use of RL as a powerful and effective method for amplifying the reasoning abilities of LLMs.

9.  **Gou et al. 2024. Tora: A tool-integrated reasoning agent for mathematical problem solving.**
    This paper presents a strong tool-augmented model for math reasoning and is used as a primary open-source baseline, representing a state-of-the-art approach that ARTIST is directly compared against and outperforms.
    *   **Link:** https://arxiv.org/abs/2309.17452

10. **Hendrycks et al. 2021. Measuring mathematical problem solving with the math dataset.**
    This paper introduced the MATH dataset, a challenging and widely used benchmark for mathematical reasoning that is central to the experimental evaluation of ARTIST's capabilities.
    *   **Link:** https://arxiv.org/abs/2103.03874
==

**Agentic Reasoning and Tool Integration for LLMs via Reinforcement Learning**

---

### 1  Brief summary and rating (1–10)

The paper introduces **ARTIST (Agentic Reasoning and Tool Integration in Self‑improving Transformers)**, a training framework that lets large language models decide *when*, *how* and *which* external tools to invoke while they reason.  ARTIST interleaves natural‑language “thought” tokens with executable tool calls (e.g., Python, web search, domain APIs) inside a single trajectory and learns the entire policy with **Group‑Relative Policy Optimisation (GRPO)**—an outcome‑based reinforcement‑learning algorithm that needs no step‑level supervision.  Loss masking ensures the model learns the *decision* to call a tool rather than merely copying its deterministic output.  Experiments on competition‑level mathematics (MATH‑500, AIME, AMC, Olympiad) and multi‑turn function‑calling benchmarks (τ‑bench, BFCL v3) show up to **22 % absolute accuracy gains** over tool‑augmented baselines and even beat GPT‑4o on several tasks .  Qualitative analyses reveal emergent behaviours such as self‑correction and adaptive tool selection .

*Rating: **9 / 10*** – The work is conceptually clear, experimentally thorough, and pushes the state of the art in agentic LLMs.  A point is deducted only because long‑horizon safety and failure modes are not deeply analysed.

---

### 2  Key ideas

1. **Unified agentic roll‑outs** – Reasoning tokens, tool calls, and tool outputs are treated as first‑class elements in one sequence, allowing the model to plan, act, observe, and revise within a single context .
2. **Outcome‑based RL with GRPO** – By masking tool‑output tokens and grouping multiple roll‑outs, GRPO steers the policy using final‑answer rewards plus auxiliary format and execution rewards, avoiding a value network and reducing compute .
3. **Cross‑domain efficacy** – The same policy‑training recipe transfers from symbolic maths (via a Python interpreter) to real‑world task automation (via function APIs) without extra supervision, consistently outperforming prompt‑engineering baselines .

---

### 3  Two or three main themes

* **Tool use as reasoning, not post‑processing** – Tool invocation is embedded in the chain of thought, so the model learns *when* external computation truly helps.
* **Reinforcement learning without dense labels** – Outcome‑only rewards, augmented with light structure/format signals, suffice to teach sophisticated multi‑step strategies.
* **Generalisable agent behaviour** – The same architecture and training pipeline work for fundamentally different domains, hinting at a domain‑agnostic path toward practical AI agents.

---

### 4  Ten most important citations

| #  | Citation                                                                                                                                                                                                                                                             | Relation to this paper |
| -- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------- |
| 1  | **Wei et al. 2023. *Chain‑of‑thought prompting elicits reasoning in large language models*.** [https://arxiv.org/abs/2201.11903](https://arxiv.org/abs/2201.11903) – Establishes the value of explicit reasoning traces that ARTIST augments with tool use.          |                        |
| 2  | **Schick et al. 2023. *Toolformer: Language models can teach themselves to use tools*.** [https://arxiv.org/abs/2302.04761](https://arxiv.org/abs/2302.04761) – Early self‑supervised approach to API calling; ARTIST surpasses it with RL and richer tool ecology.  |                        |
| 3  | **Gao et al. 2023. *PAL: Program‑Aided Language Models*.** – Shows code‑generation for reasoning; ARTIST generalises the idea to multiple tools and RL.                                                                                                              |                        |
| 4  | **Shao et al. 2024. *DeepSeekMath: Pushing the limits of mathematical reasoning in open language models*.** [https://arxiv.org/abs/2402.03300](https://arxiv.org/abs/2402.03300) – Demonstrates GRPO’s effectiveness; ARTIST builds on the same RL core.             |                        |
| 5  | **Schulman et al. 2017. *Proximal Policy Optimization Algorithms*.** [https://arxiv.org/abs/1707.06347](https://arxiv.org/abs/1707.06347) – Foundational RL algorithm that GRPO extends.                                                                             |                        |
| 6  | **Ouyang et al. 2022. *Training language models to follow instructions with human feedback*.** [https://arxiv.org/abs/2203.02155](https://arxiv.org/abs/2203.02155) – Baseline RLHF paradigm contrasted with ARTIST’s outcome‑only RL.                               |                        |
| 7  | **Sutton et al. 1998. *Reinforcement Learning: An Introduction*.** – Classic textbook grounding the paper’s RL framing.                                                                                                                                              |                        |
| 8  | **Yan et al. 2024. *BFCL v3: A Benchmark for Function Calling in LLMs*.** – Supplies one of ARTIST’s evaluation suites for multi‑turn API workflows.                                                                                                                 |                        |
| 9  | **Yao et al. 2024. *τ‑Bench: Conversational Evaluation of Tool‑Using Agents*.** – Another key benchmark showing ARTIST’s gains in realistic dialogues.                                                                                                               |                        |
| 10 | **Hendrycks et al. 2021. *Measuring Mathematical Problem Solving With the MATH Dataset*.** – Provides the competition‑style math tasks on which ARTIST is tested.                                                                                                    |                        |

---

*Prepared for a technically literate audience; all links reproduced exactly as cited in the paper.*
