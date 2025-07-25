https://arxiv.org/abs/2504.07086

A Sober Look at Progress in Language Model Reasoning: Pitfalls and Paths to Reproducibility

**1. Summary and Rating**

This paper conducts a comprehensive empirical study investigating the reproducibility and reliability of reported progress in language model (LM) reasoning, with a specific focus on mathematical reasoning benchmarks. The authors find that current evaluation practices often lack methodological rigor, transparency, and statistical grounding. Performance on these benchmarks is shown to be highly sensitive to subtle and often unreported implementation details, including decoding parameters, random seeds, prompt formatting, and even hardware/software configurations. This sensitivity, particularly problematic for small benchmarks, can lead to inflated or misleading claims of advancement.

To address these issues, the paper proposes a standardized evaluation framework and a set of best practices. Using this framework, the authors re-evaluate several recent reasoning-enhancement methods. Their findings are "sobering": Reinforcement Learning (RL) approaches, especially when applied to already distilled models, often yield only modest improvements—far below original claims—and are prone to overfitting. In contrast, Supervised Finetuning (SFT) methods demonstrate more consistent and generalizable performance gains. To foster more reliable future research, the authors release their complete experimental setup, including code, prompts, and model outputs, aiming to establish more rigorous foundations for evaluating progress in LM reasoning.

**Rating: 9.5/10**

For a PhD-level audience, this paper is exceptionally valuable. It tackles a critical and timely issue—the reliability of benchmark-driven progress in a fast-moving subfield of AI. The empirical investigation is thorough, and the "sobering" conclusions regarding the actual, reproducible gains from recent methods (especially RL-based ones) are important for the community to internalize. The paper’s strength lies not just in its critique but in its constructive approach: proposing concrete best practices and providing open-source tools to improve future evaluations. The detailed analysis of various sources of variance is insightful and educates researchers on potential pitfalls. The clarity of its arguments and the directness in addressing methodological shortcomings contribute significantly to its impact. It encourages a shift from "leaderboard chasing" to more robust and scientifically sound research practices. A near-perfect score is warranted due to its potential to significantly improve the rigor and reproducibility of future work in LM reasoning.

**2. Main Ideas Discussed**

1.  **Pervasive Reproducibility Issues in LLM Reasoning Benchmarking:** The paper argues that current progress in LLM reasoning, particularly for mathematics, is significantly clouded by a lack of methodological rigor in evaluations. It meticulously demonstrates how subtle, often unreported, variations in experimental setup (e.g., random seeds, decoding hyperparameters, hardware configurations, prompt formatting, evaluation frameworks) can drastically alter reported performance metrics, leading to unreliable and often overly optimistic claims of progress, especially on small or volatile benchmarks.
2.  **Standardized Re-evaluation Reveals Overstated Gains for RL and Robustness of SFT:** By applying a proposed standardized evaluation framework, the authors re-assess recent reasoning enhancement techniques. They find that many Reinforcement Learning (RL) methods, particularly those building upon strong, distilled base models, deliver substantially less improvement than originally reported, with gains often falling within experimental variance or exhibiting overfitting to specific benchmarks (like AIME'24). In contrast, Supervised Fine-Tuning (SFT) methods are shown to provide more consistent, stable, and generalizable performance improvements across various benchmarks.
3.  **A Call for Rigor and Provision of Tools for Transparent Research:** Beyond critique, the paper offers concrete "paths to reproducibility." It advocates for and details a set of best practices for evaluation, such as using multiple random seeds, reporting variance, performing model-specific hyperparameter optimization, ensuring sufficient context length, using robust answer-matching logic, and standardizing hardware/software stacks. Crucially, to facilitate this shift towards more rigorous research, the authors open-source their entire evaluation framework, including code, prompts, and model outputs.

**3. 10 Most Important Citations**

1.  **Henderson et al. 2018.** Deep reinforcement learning that matters.
    This foundational paper highlights the reproducibility crisis in deep RL research and advocates for more rigorous evaluation methodologies, a theme central to Hochlehnert et al.'s investigation into LLM reasoning.
2.  **Agarwal et al. 2021.** Deep reinforcement learning at the edge of the statistical precipice.
    This work critically examines the statistical robustness of RL evaluations, emphasizing sensitivity to factors like random seeds, which Hochlehnert et al. confirm is a significant issue in LLM reasoning benchmarks.
3.  **DeepSeek-AI et al. 2025.** DeepSeek-R1: Incentivizing Reasoning Capability in LLMs via Reinforcement Learning. (URL: `https://arxiv.org/abs/2501.12948`)
    This paper introduces the DeepSeek-R1 model, a key subject of re-evaluation in Hochlehnert et al.'s study, where its performance and the efficacy of subsequent RL fine-tuning are scrutinized under a standardized framework.
4.  **Liao et al. 2021.** Are we learning yet? A meta review of evaluation failures across machine learning.
    This meta-review discusses how flawed evaluation practices can distort the perception of progress in machine learning, providing a broader context for Hochlehnert et al.'s specific focus on LLM reasoning.
5.  **Hendrycks et al. 2021.** Measuring mathematical problem solving with the math dataset. (URL: `arXiv:2103.03874`)
    This paper introduces the MATH dataset, a prominent benchmark for mathematical reasoning, which Hochlehnert et al. utilize extensively in their empirical study to assess model performance and variability.
6.  **Fourrier et al. 2023.** LightEval: A lightweight framework for LLM evaluation. (URL: `https://github.com/huggingface/lighteval`)
    Hochlehnert et al. adopt and build upon the LightEval framework for their standardized evaluation procedure, ensuring consistency and facilitating the reproducibility of their findings.
7.  **Dang et al. 2025.** Reinforcement learning for reasoning in small llms: What works and what doesn't. (URL: `https://arxiv.org/abs/2503.16219`)
    This paper introduces the OpenRS models, which are among the recent RL-based reasoning methods that Hochlehnert et al. re-evaluate, finding their originally reported gains to be less substantial under standardized conditions.
8.  **Luo et al. 2025.** DeepScaleR: Surpassing O1-Preview with a 1.5B Model by Scaling RL. (Notion Blog reference in paper, specific paper not cited, but refers to the DeepScaleR model evaluated)
    DeepScaleR is highlighted by Hochlehnert et al. as one of the few RL-trained models that demonstrated robust and significant improvements in their standardized re-evaluation, contrasting with many other RL methods.
9.  **Yang et al. 2024b.** Qwen2.5-math technical report: Toward mathematical expert model via self-improvement. (URL: `arXiv:2409.12122`)
    The Qwen2.5-Math models are used by Hochlehnert et al. as important base models for evaluating the effectiveness of subsequent reinforcement learning and supervised fine-tuning strategies in the mathematical reasoning domain.
10. **Bowyer et al. 2025.** Position: Don't use the CLT in LLM evals with fewer than a few hundred datapoints. (URL: `arXiv:2503.01747`)
    This work calls for greater statistical rigor in LLM evaluations, particularly concerning small datasets and the reporting of uncertainty, aligning with and supporting Hochlehnert et al.'s empirical findings on evaluation instability and their proposed best practices.
