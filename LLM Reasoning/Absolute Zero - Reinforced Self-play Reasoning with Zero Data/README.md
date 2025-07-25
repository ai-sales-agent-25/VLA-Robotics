https://arxiv.org/abs/2505.03335

Absolute Zero: Reinforced Self-play Reasoning with Zero Data

**1. Summary and Rating**

This paper introduces "Absolute Zero," a novel paradigm for training large language models (LLMs) in reasoning tasks without relying on any external, human-curated data. The authors argue that current Reinforcement Learning with Verifiable Rewards (RLVR) methods, even in "zero-setting" scenarios, still depend on manually curated question-answer pairs, posing scalability challenges and limitations for superintelligent AI. The Absolute Zero paradigm addresses this by enabling a single LLM to autonomously propose tasks that maximize its own learning progress and then improve its reasoning by solving these self-generated tasks.

The paper presents the Absolute Zero Reasoner (AZR), an instantiation of this paradigm. AZR uses a code executor as a unified environment to both validate the integrity of proposed coding tasks (across abduction, deduction, and induction modes) and verify the correctness of the LLM's solutions, thereby providing a grounded, verifiable reward signal. Despite being trained entirely without external data, AZR achieves state-of-the-art performance on various coding and mathematical reasoning benchmarks, outperforming models trained on tens of thousands of in-domain human-curated examples. The authors also demonstrate AZR's scalability across model sizes and compatibility with different model classes, highlighting its potential to enable self-sufficient and continuously improving AI reasoning capabilities. Key findings include the amplification of reasoning by code priors, pronounced cross-domain transfer, natural emergence of intermediate planning in solutions, and distinct cognitive behaviors per reasoning mode.

**Rating: 9.5/10**

For a PhD-level audience, this paper is highly compelling. It tackles a fundamental and forward-looking problem in AI: how to enable models to learn and improve reasoning capabilities beyond the limits of human-generated data and supervision. The "Absolute Zero" paradigm is a bold and innovative proposal, and the AZR system provides a concrete and well-reasoned instantiation. The empirical results are particularly impressive, demonstrating state-of-the-art performance from literally zero external training examples for the reasoning fine-tuning stage. The methodology is clearly explained, and the connection to concepts like self-play (AlphaZero) and the use of a verifiable environment (code execution) is well-grounded. The discussion of emergent behaviors and the "uh-oh moment" regarding safety adds a layer of nuanced observation. The work opens up significant avenues for future research into self-sufficient AI. The slight deduction is only because, while pioneering, the long-term implications and robustness of such a self-sufficient learning loop will require further extensive exploration across more diverse domains and potential failure modes.

**2. Main Ideas**

The main ideas discussed in this paper are:

1.  **The "Absolute Zero" Paradigm:** This is a novel training paradigm where a reasoning agent (an LLM) learns and improves its capabilities entirely through self-play, without relying on any external human-curated datasets, questions, or answers. The agent autonomously generates its own learning tasks to maximize its progress and learns by solving them and receiving feedback from an environment.
2.  **The Absolute Zero Reasoner (AZR) System:** AZR is a practical implementation of the Absolute Zero paradigm. It uses a single LLM that acts as both a "proposer" of coding tasks (spanning deduction, abduction, and induction) and a "solver" of these tasks. A code executor serves as the verifiable environment, validating proposed tasks and verifying solutions to provide reward signals for reinforcement learning.
3.  **Achieving State-of-the-Art Reasoning from Zero External Data:** The paper demonstrates that AZR, trained exclusively on self-generated coding tasks without any in-domain human data, can achieve state-of-the-art performance in code generation and competitive performance in mathematical reasoning, outperforming models fine-tuned on large, expertly-curated datasets. This highlights the potential for LLMs to autonomously bootstrap and significantly enhance their reasoning abilities.

**3. 10 Most Important Citations**

1.  **DeepSeek-AI et al. 2025.** Deepseek-r1: Incentivizing reasoning capability in llms via reinforcement learning. This paper introduced the "zero setting" for RLVR, which AZR directly builds upon and extends by removing the need for curated question-answer pairs. (Link: `https://doi.org/10.48550/arXiv.2501.12948`)
2.  **Silver et al. 2017.** Mastering chess and shogi by self-play with a general reinforcement learning algorithm. This work on AlphaZero is a key inspiration for the self-play approach in Absolute Zero, demonstrating superhuman performance from learning entirely through self-interaction without human data. (Link: `http://arxiv.org/abs/1712.01815`)
3.  **Lambert et al. 2024.** Tülu 3: Pushing frontiers in open language model post-training. This paper provides context on RLVR as a significant method for enhancing LLM reasoning, a field to which Absolute Zero contributes a new paradigm. (Link: `https://doi.org/10.48550/arXiv.2411.15124`)
4.  **Hughes et al. 2024.** Position: Open-endedness is essential for artificial superhuman intelligence. This citation supports the motivation for Absolute Zero by discussing the limitations of human-designed tasks if AI surpasses human intelligence and the importance of preventing issues like reward hacking in learned reward models. (Link: `https://openreview.net/forum?id=Bc4vZ2CX7E`)
5.  **Sukhbaatar et al. 2018.** Intrinsic motivation and automatic curricula via asymmetric self-play. The proposer reward in AZR, based on the solver's success rate, is conceptually similar to ideas in unsupervised environment design and asymmetric self-play explored in this paper. (Link: `https://openreview.net/forum?id=SkT5Yg-RZ`)
6.  **Yao et al. 2023.** React: Synergizing reasoning and acting in language models. The paper observes that AZR naturally develops intermediate planning steps in its solutions, akin to the ReAct prompting framework, suggesting an emergent complex reasoning behavior. (Link: `https://openreview.net/forum?id=WE_vluYUL-X`)
7.  **Ouyang et al. 2022.** Training language models to follow instructions with human feedback. This is a foundational paper on supervised fine-tuning (SFT) with human feedback, representing the type of data-intensive approach that Absolute Zero aims to complement or move beyond for frontier models. (No direct link given in paper, standard NeurIPS reference)
8.  **Villalobos et al. 2024.** Position: Will we run out of data? limits of LLM scaling based on human-generated data. This paper highlights the crucial problem of data scarcity and scalability limitations of relying on human-generated data for training LLMs, a core motivation for the Absolute Zero approach. (Link: `https://openreview.net/forum?id=ViZcgDQjyG`)
9.  **Aryabumi et al. 2024.** To code, or not to code? exploring impact of code in pre-training. This citation provides empirical evidence and rationale for using code-based tasks as the medium for AZR's self-improvement, as code training can enhance general reasoning abilities. (Link: `https://doi.org/10.48550/arXiv.2408.10914`)
10. **Zhang et al. 2025a.** 100 days after deepseek-r1: A survey on replication studies and more directions for reasoning language models. This paper is referenced in relation to the "uh-oh moment" observed with Llama3.1-8B, underscoring the critical need for ongoing safety research and oversight even in self-sufficient learning paradigms. (Link: `https://arxiv.org/abs/2505.00551`)



==

Absolute Zero: Reinforced Self-play Reasoning with Zero Data

**1. Brief Summary and Rating**

This paper introduces "Absolute Zero," a novel paradigm for training reasoning models using Reinforcement Learning with Verifiable Rewards (RLVR) that notably requires no external, human-curated data. The core idea is that a single language model learns to both *propose* learnable tasks and *solve* them, improving its reasoning capabilities entirely through self-play and interaction with an environment that provides verifiable feedback. The authors instantiate this paradigm with the Absolute Zero Reasoner (AZR), a system that focuses on code-based reasoning. AZR generates three types of coding tasks (abduction, deduction, and induction), uses a code executor to validate proposed tasks and verify solutions, and employs a tailored reinforcement learning algorithm for joint training of task proposal and solution. Despite being trained without any in-domain human-curated examples, AZR achieves state-of-the-art (SOTA) performance on several coding and mathematical reasoning benchmarks, outperforming models trained with tens of thousands of such examples. The paper argues that this approach addresses the scalability concerns of reliance on human-produced data and is a step towards more autonomous AI systems capable of self-improvement and potentially surpassing human intelligence. The work also highlights emergent behaviors, cross-domain generalization, and positive scaling with model size.

**Rating: 9.5/10**

For a sophisticated, PhD-level audience, this paper is highly compelling.
*   **Novelty and Ambition (Score: 10/10):** The "Absolute Zero" paradigm, where the model generates its own curriculum of tasks from scratch and learns without any external data, is exceptionally novel and ambitious. It pushes the boundaries of self-supervised and reinforcement learning for reasoning.
*   **Significance and Potential Impact (Score: 10/10):** If the results generalize and the paradigm can be extended to other domains, the implications are profound. It offers a path to overcoming the data bottleneck in training advanced AI reasoners and could lead to systems with truly autonomous learning capabilities.
*   **Methodology and Rigor (Score: 9/10):** The proposed AZR system, with its use of a code executor as a verifiable environment and the structured approach to task generation (abduction, deduction, induction) and reward design, is well-conceived for the target domain of code-based reasoning. The experiments are comprehensive, including comparisons to relevant baselines, ablation studies, and analyses of emergent behaviors and scaling properties. The use of Task-Relative REINFORCE++ for training is a sensible choice.
*   **Results and Claims (Score: 9/10):** The reported SOTA performance on multiple benchmarks, particularly outperforming models trained on extensive human-curated data, is a very strong result and supports the paper's main claims. The observed cross-domain transfer to mathematical reasoning from code-based self-play is particularly impressive.
*   **Clarity and Presentation (Score: 9/10):** The paper is generally well-written and clearly articulates a complex set of ideas and experiments. The distinction between existing RLVR and the proposed "Absolute Zero" setting is made effectively.

The slight deduction from a perfect 10 acknowledges that the current instantiation (AZR) is focused on the domain of code, where verifiability is more straightforward. Generalizing the "Absolute Zero" paradigm to domains with less clear-cut verification mechanisms remains a significant future challenge. The "uh-oh moment" regarding safety with Llama models, while candidly reported, also underscores the complexities of highly autonomous learning systems. However, these are areas for future work rather than fundamental flaws in the current paper's contribution, which is a significant conceptual and empirical step forward.

**2. Main Ideas Discussed**

The main ideas discussed in this paper are:

1.  **The Absolute Zero Paradigm:** This is a new reinforcement learning paradigm where a single agent learns to autonomously propose tasks that maximize its own learning progress and then improves its reasoning abilities by solving these self-generated tasks. Crucially, this process occurs *without relying on any external, human-curated data* (questions, answers, or reasoning traces), using only feedback from an environment that provides verifiable rewards (e.g., a code executor).
2.  **Absolute Zero Reasoner (AZR) Implementation:** AZR is presented as the first instantiation of the Absolute Zero paradigm. It utilizes a single large language model that plays dual roles: a *proposer* that generates coding tasks (categorized into abduction, deduction, and induction) and a *solver* that attempts to solve these tasks. A code executor serves as the environment, validating task integrity and providing verifiable rewards for both task proposal (based on learnability) and solution correctness.
3.  **Achieving SOTA Reasoning and Generalization from Zero External Data:** The paper demonstrates that AZR, despite being trained entirely through self-play on self-generated coding tasks without any external datasets, achieves state-of-the-art performance on established coding and mathematical reasoning benchmarks. This highlights the potential for strong reasoning capabilities and cross-domain generalization to emerge purely from grounded self-improvement, challenging the reliance on large, human-curated datasets.

**3. 10 Most Important Citations**

1.  **Lambert et al. 2024. Tülu 3: Pushing frontiers in open language model post-training.**
    *   This citation is important as it represents recent advancements in RLVR (Reinforcement Learning with Verifiable Rewards), the foundational technique upon which the "Absolute Zero" paradigm builds and extends by removing reliance on curated datasets. (Link: https://doi.org/10.48550/arXiv.2411.15124)
2.  **DeepSeek-AI et al. 2025. Deepseek-r1: Incentivizing reasoning capability in llms via reinforcement learning.**
    *   This work introduced a "zero" RLVR setting (R1 model) that AZR is explicitly compared against and aims to surpass by eliminating the need for even curated question-answer pairs for training initiation. (Link: https://doi.org/10.48550/arXiv.2501.12948)
3.  **Silver et al. 2017. Mastering chess and shogi by self-play with a general reinforcement learning algorithm.**
    *   This (AlphaZero) is a seminal paper on self-play, demonstrating superhuman performance by learning without human data or domain-specific knowledge beyond game rules, aligning with AZR's philosophy of learning entirely through self-interaction. (Link: http://arxiv.org/abs/1712.01815)
4.  **Villalobos et al. 2024. Position: Will we run out of data? limits of LLM scaling based on human-generated data.**
    *   This citation highlights the critical problem of data scarcity and the limitations of relying on human-generated data for scaling LLMs, which the "Absolute Zero" paradigm directly addresses. (Link: https://openreview.net/forum?id=ViZcgDQjyG)
5.  **Jaech et al. 2024. Openai o1 system card.**
    *   Referenced as "o1", this work is noted for deploying self-bootstrapping ideas on a large scale for reasoning, representing significant prior art in improving LLM reasoning that AZR's zero-data approach contrasts with. (Link: arXiv preprint arXiv:2412.16720 - Note: Link based on typical format, actual link from paper preferred if different.)
6.  **Ouyang et al. 2022. Training language models to follow instructions with human feedback.**
    *   This paper (InstructGPT) is foundational for supervised fine-tuning (SFT) and RLHF, representing the dominant paradigm that often requires human data, which AZR's "Absolute Zero" approach seeks to circumvent for reasoning improvement.
7.  **Sukhbaatar et al. 2018. Intrinsic motivation and automatic curricula via asymmetric self-play.**
    *   This work is relevant for its exploration of asymmetric self-play and learnability-based rewards for a proposer agent, similar to the reward design for AZR's proposer role. (Link: https://openreview.net/forum?id=SkT5Yg-RZ)
8.  **Hu 2025. REINFORCE++: A simple and efficient approach for aligning large language models.**
    *   The paper's reinforcement learning algorithm, Task-Relative REINFORCE++ (TRR++), is a variant of REINFORCE++ introduced in this citation, making it crucial for understanding AZR's training mechanism. (Link: https://doi.org/10.48550/arXiv.2501.03262)
9.  **Yao et al. 2023. React: Synergizing reasoning and acting in language models.**
    *   The emergent behavior of AZR, where it interleaves step-by-step plans (as comments) with code, is likened to the ReAct prompting framework, making this citation relevant for contextualizing AZR's reasoning process. (Link: https://openreview.net/forum?id=WE_vluYUL-X)
10. **Yuan et al. 2024. Self-rewarding language models.**
    *   This paper is part of the recent trend of models improving themselves via self-generated feedback or rewards, which aligns with the core self-improvement philosophy of the Absolute Zero paradigm. (Link: https://arxiv.org/abs/2401.10020)
