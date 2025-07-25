https://arxiv.org/abs/2504.16891

**Paper:** AIMO-2 Winning Solution: Building State-of-the-Art Mathematical Reasoning Models with OpenMathReasoning dataset

**1. Summary and Rating**

This paper details the NVIDIA team's first-place solution for the AI Mathematical Olympiad - Progress Prize 2 (AIMO-2). Their approach centers on three main contributions: First, the creation of "OpenMathReasoning," a large-scale dataset containing 540K unique mathematical problems (including Olympiad-level) and 3.2 million long-reasoning Chain-of-Thought (CoT) solutions. Second, they introduce a novel method for Tool-Integrated Reasoning (TIR), iteratively training models to combine natural language reasoning with Python code execution, resulting in 1.7 million high-quality TIR solutions. This iterative process involves generation, aggressive quality filtering, and retraining. Third, they developed "GenSelect," a pipeline to train models to identify the most promising solution from multiple candidates, showing improvements over majority voting baselines. By combining these pillars, they trained a series of OpenMath-Nemotron models (from 1.5B to 32B parameters) that achieve state-of-the-art results on mathematical reasoning benchmarks. The paper also describes the specific training recipes, inference optimizations (including TensorRT-LLM and speculative decoding), and strategies used for their AIMO-2 submission. Crucially, the authors release their code, models, and the entire OpenMathReasoning dataset to foster further research.

**Rating: 9/10**

This paper presents a significant and well-executed piece of research in the challenging domain of advanced mathematical reasoning. The contributions are substantial: the OpenMathReasoning dataset is a valuable resource, the iterative refinement process for Tool-Integrated Reasoning is a novel and effective technique, and the GenSelect pipeline offers a promising direction for improving solution selection. The empirical validation, crowned by winning the AIMO-2 competition, is strong. The detailed methodology, including data curation, model training, and Kaggle-specific optimizations, provides a clear and reproducible account of their success. The open-sourcing of all artifacts (dataset, models, code) is highly commendable and will undoubtedly benefit the research community. The paper is well-written and clearly articulates complex ideas, making it accessible despite the inherent technical depth. While many individual components (CoT, tool use, solution selection) are known, their sophisticated integration, the scale of data generation, and the iterative refinement loops represent a state-of-the-art engineering and research effort. A potential area for even greater impact in future work could be deeper analysis into the failure modes or the generalization capabilities beyond the specific style of problems encountered in AIMO/AoPS.

**2. Main Ideas Discussed**

The paper's approach to building state-of-the-art mathematical reasoning models is built on three main ideas:

1.  **Large-Scale High-Quality Dataset Creation (OpenMathReasoning):** A core pillar is the development of an extensive dataset (540K unique problems, 3.2M CoT solutions) by collecting problems (primarily from Art of Problem Solving forums) and using LLMs (DeepSeek-R1, QwQ-32B) to generate detailed, long-reasoning solutions. This dataset serves as the foundation for training their models.
2.  **Iterative Tool-Integrated Reasoning (TIR):** Recognizing the limitations of pure CoT, the authors developed a novel method to integrate code execution (Python) with long reasoning. This involves an iterative pipeline:
    *   Initial TIR data generation using an instruction-following model.
    *   Aggressive quality filtering to retain only high-impact code usage.
    *   Fine-tuning reasoning models on this filtered TIR data.
    *   Using the improved model to generate more, higher-quality TIR data, and repeating the process. This resulted in 1.7M high-quality TIR solutions and models adept at using tools effectively.
3.  **Generative Solution Selection (GenSelect):** To move beyond the limitations of simple majority voting for selecting the best solution from multiple candidates (pass@k), they developed a pipeline to train models to perform this selection. The model is prompted with multiple solution summaries and reasons in natural language to pick the most promising one. This showed significant improvements over baselines, especially for a smaller number of generations.

**3. 10 Most Important Citations**

1.  **Wei et al. 2022. Chain-of-thought prompting elicits reasoning in large language models.** [35]
    This citation is foundational for the paper's approach to generating multi-step solutions by prompting models to produce intermediate reasoning steps (CoT), which forms a large part of their OpenMathReasoning dataset.
2.  **Guo et al. 2025. DeepSeek-R1: Incentivizing Reasoning Capability in LLMs via Reinforcement Learning.** [10]
    DeepSeek-R1 is a key open-weight model extensively used by the authors for generating a significant portion of their initial CoT solutions and served as an important baseline model in their experiments.
3.  **Yang et al. 2025. Qwen2.5 Technical Report.** [39] (and **Yang et al. 2024. Qwen2.5-Math Technical Report.** [40])
    Qwen2.5 models (both base and math-specific versions) are the primary architecture the authors fine-tune to create their OpenMath-Nemotron series, and Qwen models are also used in data processing and generation steps.
4.  **Chen et al. 2023. Program of Thoughts Prompting: Disentangling Computation from Reasoning for Numerical Reasoning Tasks.** [3]
    This work introduced Program of Thoughts (PoT), which is a key precursor and conceptual basis for integrating code execution with LLM reasoning, directly relevant to the paper's Tool-Integrated Reasoning (TIR) pillar. Link: (TMLR)
5.  **Toshniwal et al. 2024. OpenMathInstruct-1: A 1.8 Million Math Instruction Tuning Dataset.** [31]
    This is significant prior work by some of the authors on creating large-scale math instruction tuning datasets focused on tool integration, showing a consistent research direction and providing context for the current dataset's development. Link: (NeurIPS Datasets and Benchmarks)
6.  **Zhang et al. 2024. Generative Verifiers: Reward Modeling as Next-Token Prediction.** [45]
    This paper is highly influential for their GenSelect pipeline, as it proposes training models to generate evaluative reasoning about solutions rather than just classifying them, a principle adopted by the authors. Link: `arXiv:2408.15240`
7.  **Ye et al. 2025. LIMO: Less is More for Reasoning.** [42]
    This citation informs the authors' strategy for effectively fine-tuning instruction-following models (like LIMO-Qwen-32B) on smaller, high-quality reasoning datasets to enable capabilities like TIR without degrading instruction-following. Link: `arXiv:2502.03387`
8.  **Wang et al. 2023. Self-Consistency Improves Chain of Thought Reasoning in Language Models.** [34]
    Majority voting, a technique related to self-consistency, serves as a strong baseline against which the authors evaluate their GenSelect approach; self-consistency itself is a widely recognized method for enhancing LLM reasoning. Link: (ICLR)
9.  **Frieder et al. 2024. Ai mathematical olympiad progress prize 2.** [7]
    This is the official citation for the AIMO-2 competition, which the authors' work won, providing the primary validation and context for their research and development efforts. Link: [https://kaggle.com/competitions/ai-mathematical-olympiad-progress-prize-2](https://kaggle.com/competitions/ai-mathematical-olympiad-progress-prize-2)
10. **Toshniwal et al. 2025. OpenMathInstruct-2: Accelerating AI for Math with Massive Open-Source Instruction Data.** [30]
    This is another recent and relevant work by the authors on a large-scale math instruction dataset, from which they reuse components like judge prompts and checkpoint averaging techniques, demonstrating a continuous and iterative research effort. Link: (ICLR)
