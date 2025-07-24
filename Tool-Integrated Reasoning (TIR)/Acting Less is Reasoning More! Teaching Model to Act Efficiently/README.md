https://arxiv.org/abs/2504.14870

Acting Less is Reasoning More ! Teaching Model to Act Efficiently

**1. Summary and Rating**

This paper addresses the issue of "cognitive offloading" in tool-integrated reasoning (TIR) with large language models (LLMs), where models tend to overuse external tools even when not strictly necessary. This excessive tool use incurs high computational costs, increases latency, and hinders the development of the models' internal reasoning capabilities. To mitigate this, the authors propose Optimal Tool Call-controlled Policy Optimization (OTC-PO), a reinforcement learning (RL) framework. OTC-PO modifies the reward function to jointly optimize for answer correctness and the efficiency of tool use, aiming to achieve correct answers with the minimal number of tool calls. A key component is the introduction of a "tool productivity" metric, defined as the ratio of correct answers to the total number of tool calls, which serves as a more holistic measure of a model's agentic reasoning efficiency. The framework is instantiated with Proximal Policy Optimization (PPO) and Group Relative Preference Optimization (GRPO), resulting in OTC-PPO and OTC-GRPO. Experiments on question-answering benchmarks using search and code interpreter tools show that OTC-PO significantly reduces tool calls (by up to 68.3%) and improves tool productivity (by up to 215.4%) while maintaining comparable answer accuracy to baseline RL methods that only optimize for correctness. The paper also highlights that minimizing external tool reliance can foster the LLM's internal reasoning capabilities.

**Rating: 8.5/10**

For a PhD-level audience, this paper is a strong contribution.
*   **Novelty (High):** The explicit focus on optimizing *tool use efficiency* alongside correctness within an RL framework for LLMs is a novel and important direction. The proposed "tool productivity" metric is a sensible and useful evaluation measure. The concept of actively penalizing excessive tool use to combat cognitive offloading and potentially enhance internal reasoning is well-articulated.
*   **Significance (High):** The problem of inefficient tool use is highly relevant for the practical deployment of agentic LLMs, impacting cost, latency, and the development of more autonomous reasoning. The paper tackles a tangible challenge in the field.
*   **Methodology (Solid):** The OTC-PO framework is conceptually straightforward and leverages established RL algorithms (PPO, GRPO). The reward shaping mechanism to incorporate tool use cost is logical. The approach of approximating the optimal number of tool calls is a practical solution to an otherwise challenging problem.
*   **Experimental Validation (Thorough):** The experiments are comprehensive, covering different models (Qwen series), tool types (search, code), and datasets (NQ, HotpotQA, AIME). The inclusion of in-domain and out-of-domain evaluations, along with comparisons to strong baselines (Search-R1, ToRL), strengthens the findings. The reported improvements in tool call reduction and productivity are substantial.
*   **Clarity and Presentation (Good):** The paper is generally well-written, with clear motivation and explanation of the proposed method. The case studies effectively illustrate the benefits of the approach.
*   **Potential Impact (High):** This work could significantly influence how future tool-using LLM agents are trained, encouraging a shift towards more resource-efficient and potentially more "thoughtful" models.

A minor point that could be explored further in future work (and doesn't detract significantly from this paper's core contribution) is a deeper analysis of *how* the reduced tool use translates to changes in internal reasoning patterns, though the case studies provide initial qualitative evidence. The unusual "2025" dating on the arXiv preprint and some references is noted but doesn't affect the scientific content assessment.

**2. Main Ideas Discussed**

1.  **Cognitive Offloading and Inefficient Tool Use in LLMs:** The paper identifies that current tool-integrated LLMs, often trained with RL focused solely on final answer correctness, tend to overuse external tools. This phenomenon, termed "cognitive offloading," leads to high operational costs and, more importantly, may hinder the development and utilization of the LLMs' internal reasoning capabilities. The paper argues for the need to explicitly encourage models to "act less" (use fewer tools) to "reason more" (rely on and develop internal knowledge).

2.  **Optimal Tool Call-controlled Policy Optimization (OTC-PO):** To address inefficient tool use, the paper proposes OTC-PO, an RL framework that trains LLMs to produce accurate answers with a minimal number of tool calls. This is achieved by introducing a novel tool-integrated reward function that jointly considers answer correctness and the efficiency of tool usage (i.e., the number of tool calls). This shifts the optimization objective from mere correctness to "tool productivity"—the ratio of correct answers to total tool calls.

3.  **Balancing Accuracy and Efficiency for Enhanced Autonomy:** The core of OTC-PO is to find a balance where the model uses tools only when necessary, thereby reducing costs and latency while maintaining high accuracy. The paper demonstrates that by discouraging excessive tool calls, models can be prompted to leverage their internal knowledge more effectively, potentially leading to more robust and autonomous reasoning. The framework is designed to be adaptable to different RL algorithms like PPO and GRPO.

**3. List of 10 Most Important Citations**

1.  **LeCun.** 2022. A path towards autonomous machine intelligence version 0.9. 2, 2022-06-27. Open Review, 62(1):1–62, 2022.
    *   This citation provides the motivating vision for autonomous machine intelligence to minimize actions, aligning with the paper's core goal of teaching models to act efficiently by reducing tool calls.
    *   Link: (No direct link in paper, general search for OpenReview can find it)

2.  **Wei et al.** 2023. Chain-of-thought prompting elicits reasoning in large language models, 2023.
    *   This paper introduced Chain-of-Thought prompting, which is fundamental to the advanced reasoning capabilities of LLMs that tool-integrated reasoning aims to augment and, in this paper's case, make more efficient.

3.  **Risko and Gilbert.** 2016. Cognitive offloading. Trends in cognitive sciences, 20(9):676-688, 2016.
    *   This citation defines and explains the concept of "cognitive offloading," which is a central problem this paper aims to address in the context of LLMs over-relying on external tools.

4.  **Schulman et al.** 2017. Proximal policy optimization algorithms. arXiv preprint arXiv:1707.06347, 2017.
    *   This paper introduces Proximal Policy Optimization (PPO), one of the two key reinforcement learning algorithms upon which the proposed OTC-PO framework (specifically OTC-PPO) is built.
    *   Link: https://arxiv.org/abs/1707.06347

5.  **Shao et al.** 2024. Deepseekmath: Pushing the limits of mathematical reasoning in open language models. arXiv preprint arXiv:2402.03300, 2024.
    *   This paper is cited as the source for the Group Relative Preference Optimization (GRPO) algorithm, which is the other RL backbone for the proposed OTC-GRPO variant.
    *   Link: https://arxiv.org/abs/2402.03300

6.  **Jin et al.** 2025. Search-r1: Training llms to reason and leverage search engines with reinforcement learning, 2025.
    *   Search-R1 is a primary baseline method that the paper extensively compares against, particularly for tasks requiring search tool integration; it represents the standard RL approach optimizing for correctness only.
    *   Link: (Likely an arXiv paper, specific ID not in this reference format but findable given authors/title)

7.  **Li et al.** 2025. Torl: Scaling tool-integrated rl, 2025.
    *   ToRL is another significant baseline for tool-integrated RL that this paper compares against, especially in the context of code generation tools, highlighting the effectiveness of OTC-PO.
    *   Link: (Likely an arXiv paper)

8.  **Gou et al.** 2024. ToRA: A tool-integrated reasoning agent for mathematical problem solving. In The Twelfth International Conference on Learning Representations, 2024.
    *   This paper presents ToRA, an example of a tool-integrated reasoning agent, illustrating the broader field of TIR to which the current work contributes by focusing on efficiency.

9.  **Qian et al.** 2025. Smart: Self-aware agent for tool overuse mitigation. arXiv preprint arXiv:2502.11435, 2025.
    *   This citation is relevant as it discusses tool overuse mitigation, similar to the problem tackled by the current paper, though SMART uses supervised fine-tuning rather than RL. It highlights the importance of addressing tool efficiency.
    *   Link: https://arxiv.org/abs/2502.11435 (Year in reference is 2025, link has 2024, using ref year) - The bib entry seems to have a typo in the arxiv id itself, it should likely be 2402.11435. The link provided in the paper is "arXiv:2502.11435".

10. **Arora and Zanette.** 2025. Training language models to reason efficiently, 2025.
    *   This work is cited for providing theoretical justification for the multiplicative reward design used in OTC-PO, which combines correctness rewards with a tool-use efficiency coefficient.
