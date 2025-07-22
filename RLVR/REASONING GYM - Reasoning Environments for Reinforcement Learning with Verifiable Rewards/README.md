https://arxiv.org/abs/2505.24760

https://x.com/_OliverStanley/status/1929487448783933897

REASONING GYM: Reasoning Environments for Reinforcement Learning with Verifiable Rewards

**1. Summary and Rating**

This paper introduces REASONING GYM (RG), a comprehensive and open-source library featuring over 100 procedurally generated reasoning environments. These environments are specifically designed for training and evaluating Large Language Models (LLMs) using Reinforcement Learning with Verifiable Rewards (RLVR). RG aims to address the critical bottleneck of data scarcity and quality in developing advanced reasoning capabilities in LLMs. Its core innovation lies in the procedural generation of tasks across diverse domains (algebra, arithmetic, computation, cognition, geometry, graph theory, logic, and games), which allows for virtually infinite training data with parametrically adjustable complexity and algorithmically verifiable rewards. This approach mitigates concerns of dataset memorization and enables dynamic curriculum learning.

The authors conduct extensive experiments demonstrating RG's efficacy. They show that frontier LLMs exhibit low zero-shot performance on many RG tasks, especially those involving visual-spatial concepts represented textually, and that performance often drops sharply with increasing task difficulty (a "difficulty cliff"). Crucially, training models with RLVR on RG tasks leads to significant improvements not only on the trained tasks but also shows strong intra-domain generalization, surprising cross-domain transfer (e.g., algorithmic training improving math skills), and improved performance on established external benchmarks like MATH and GSM8K. The paper also highlights the benefits of curriculum learning within the RG framework.

**Rating: 9/10**

For a PhD-level audience, this paper is a strong contribution.
*   **Significance:** It addresses a timely and critical problem in LLM research – the need for scalable, diverse, and controllable data for advancing reasoning capabilities. The proposed solution, REASONING GYM, offers a valuable tool and testbed for the community.
*   **Novelty:** While procedural generation and RL environments are not new in themselves, the scale, diversity of reasoning tasks, focus on LLMs and RLVR, and the systematic design for verifiable rewards and difficulty control make RG a novel and substantial contribution.
*   **Methodology & Evaluation:** The design principles of RG are sound, and the experimental evaluation is comprehensive. The authors test multiple state-of-the-art models, explore various generalization scenarios (intra-domain, cross-domain, external benchmarks), and investigate curriculum learning. The commitment to open-sourcing the library and configurations significantly enhances its value.
*   **Impact Potential:** RG has high potential to facilitate more rigorous and scalable research into LLM reasoning, enabling deeper understanding of current model limitations and fostering the development of more capable models.
*   **Clarity:** The paper is well-written, clearly articulating the motivations, design, and empirical findings. The "2025" date on the preprint is unusual but doesn't detract from the content's quality.

The paper makes a solid engineering and empirical contribution that should be highly valuable to researchers working on LLM reasoning and reinforcement learning.

**2. Main Ideas Discussed**

1.  **REASONING GYM (RG) as a Scalable and Controllable Framework for RLVR:** The paper introduces RG, a library of over 100 procedurally generated reasoning tasks. Its key features—algorithmic verifiability, large solution spaces, and parametric difficulty control—are designed to provide a robust and infinitely scalable data source for training and evaluating LLM reasoning through Reinforcement Learning with Verifiable Rewards, overcoming limitations of fixed datasets.
2.  **Systematic Evaluation of LLM Reasoning and Identification of "Difficulty Cliffs":** RG serves as a challenging benchmark that reveals significant limitations in current frontier LLMs. The experiments highlight that performance often degrades sharply as task complexity increases (the "difficulty cliff phenomenon"), particularly in areas like visual-spatial reasoning presented textually, and that even reasoning-focused models struggle with many RG configurations.
3.  **Demonstration of Generalizable Skill Acquisition via RLVR on RG:** The paper empirically shows that training LLMs on RG tasks using RLVR leads to substantial improvements in reasoning abilities. This improvement is not limited to the specific tasks trained on but also generalizes effectively within the same domain, across different reasoning domains (e.g., algorithmic training benefiting mathematical domains), and to established external benchmarks like MATH and GSM8K.

**3. 10 Most Important Citations**

1.  Cobbe et al. 2021. Training verifiers to solve math word problems.
    *   This paper introduced the GSM8K dataset, a key benchmark for grade school math word problems, which REASONING GYM uses for evaluating the external generalization of models trained on its tasks.
2.  Hendrycks et al. 2021. Measuring mathematical problem solving with the math dataset.
    *   This paper introduced the MATH dataset, a challenging benchmark for advanced mathematical problem solving, used by REASONING GYM to assess the transfer of learned skills to complex external mathematical tasks.
3.  Lambert et al. 2024. T\" ulu 3: Pushing frontiers in open language model post-training. arXiv preprint arXiv:2411.15124.
    *   URL: (No URL provided in paper for main link, but arXiv: https://arxiv.org/abs/2411.15124)
    *   This work on the Tülu model series highlights progress and methodologies in post-training LLMs, including RL techniques, providing context for the RLVR approach facilitated by REASONING GYM.
4.  Guo et al. 2025. Deepseek-r1: Incentivizing reasoning capability in llms via reinforcement learning. arXiv preprint arXiv:2501.12948.
    *   URL: https://arxiv.org/abs/2501.12948
    *   DeepSeek-R1 is a prominent model that leverages RLVR for enhancing reasoning, and its development underscores the importance of verifiable rewards and diverse reasoning tasks, which REASONING GYM aims to provide systematically.
5.  Cobbe et al. 2020. Leveraging procedural generation to benchmark reinforcement learning.
    *   This paper demonstrates the value of procedural content generation for creating diverse and challenging environments for benchmarking reinforcement learning agents, a core principle adopted by REASONING GYM for LLM reasoning.
6.  OpenAI et al. 2024. Openai 01 system card.
    *   URL: https://arxiv.org/abs/2412.16720
    *   The OpenAI model (referred to as 03-mini in the paper, likely from this series) is a state-of-the-art LLM whose reasoning capabilities are evaluated using REASONING GYM, serving as a key baseline for performance.
7.  Bengio et al. 2009. Curriculum learning. In *Proceedings of the 26th Annual International Conference on Machine Learning (ICML '09)*.
    *   This is a foundational paper on curriculum learning, a training strategy where models learn from easier examples before harder ones, which REASONING GYM supports through its adjustable difficulty and shows to be beneficial.
8.  Shao et al. 2024. Deepseekmath: Pushing the limits of mathematical reasoning in open language models. arXiv preprint arXiv:2402.03300.
    *   URL: https://arxiv.org/abs/2402.03300
    *   The GRPO algorithm, referenced as being from this work (or associated with it), is used in the REASONING GYM paper for conducting RLVR experiments, making this citation relevant to their training methodology.
9.  OpenThoughts Team. 2025. Open Thoughts.
    *   URL: https://www.open-thoughts.ai/
    *   This project is cited as being the closest to REASONING GYM's work in curating reasoning datasets across various domains, highlighting it as a significant related effort in the field.
10. Villalobos et al. 2022. Will we run out of data? limits of Ilm scaling based on human-generated data. arXiv preprint arXiv:2211.04325.
    *   URL: https://arxiv.org/abs/2211.04325
    *   This paper discusses the potential limits of scaling LLMs due to finite human-generated data, reinforcing the motivation for REASONING GYM's procedural generation approach to create virtually infinite training instances.
