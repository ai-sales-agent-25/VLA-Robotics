https://www.arxiv.org/abs/2506.08388

**Paper:** Reinforcement Learning Teachers of Test Time Scaling

### 1. Summary and Rating

This paper introduces a novel framework for training language models (LMs) for reasoning tasks, called Reinforcement-Learned Teachers (RLTs). The authors identify a fundamental mismatch in existing reinforcement learning (RL) reasoning pipelines: models are trained with sparse rewards to solve problems from scratch, a task plagued by exploration challenges, yet their primary use is often to generate reasoning traces to distill knowledge into other "student" models.

To resolve this, the RLT framework reframes the task. Instead of solving a problem, the RLT is given both the question and the solution and is tasked with generating a high-quality explanation connecting them. It is trained via RL with a dense reward function that directly optimizes for the explanation's utility for a downstream student. This reward measures both the student's ability to predict the solution given the explanation and the logical plausibility of the explanation itself from the student's perspective.

The empirical results are compelling. The authors show that a small 7B parameter RLT can produce raw reasoning traces that, when used for distillation, create student models that outperform those trained on heavily post-processed traces from orders-of-magnitude larger LMs (like DeepSeek-R1). This superiority holds when distilling to larger students (32B), cold-starting traditional RL, and even in zero-shot transfer to out-of-distribution tasks. The work suggests a more efficient, scalable, and effective paradigm for generating synthetic reasoning data, reducing the reliance on massive models and costly post-processing.

**Rating: 9/10**

The paper presents a conceptually elegant and highly effective solution to a well-known and critical problem in applying RL to LMs—the exploration bottleneck. The reframing of the problem from "solver" to "teacher" is a clever and powerful insight. The experimental validation is rigorous, with strong comparisons to state-of-the-art baselines, thoughtful ablations, and demonstrations across multiple use cases (distillation, RL cold-starting, OOD transfer). The potential impact on democratizing the creation of powerful reasoning models is significant. It stands as a strong contribution that could shift how the community approaches synthetic data generation for reasoning.

### 2. Main Ideas

1.  **Reframing the RL Task from Solving to Explaining:** The central idea is to circumvent the exploration problem inherent in sparse-reward RL. Instead of training a model to find a correct answer from scratch, the framework provides the model (the RLT) with both the question and the solution. The model's task is then simplified to generating an instructive explanation, which is more amenable to learning with dense rewards.

2.  **A Dense Reward Function Optimized for Distillation:** The quality of an RLT's explanation is measured by a novel, dense reward function designed specifically for the end goal of student distillation. The reward has two key components:
    *   **Explanation Usefulness (r_SS):** Measures how much the student model's log-probability of generating the correct solution increases after being conditioned on the RLT's explanation.
    *   **Explanation Clarity (r_KL):** A regularizer that ensures the explanation is a logical and "natural" continuation from the student's perspective by minimizing the KL divergence between the teacher's and student's probability distributions over the explanation tokens.

3.  **Efficient Generation of Superior-Quality Reasoning Traces:** A primary finding is that a small 7B RLT can produce raw (un-postprocessed) reasoning traces that are more effective for distillation than traces from much larger models (e.g., DeepSeek-R1, QwQ-32B) that require expensive generation and heuristic-driven post-processing. This demonstrates a path toward creating high-quality synthetic data for reasoning more efficiently and at a lower cost.

### 3. 10 Most Important Citations

1.  **Guo et al. (2025).** Deepseek-r1: Incentivizing reasoning capability in llms via reinforcement learning.
    *   This paper is a key milestone that popularizes the RL reasoning paradigm which the RLT framework aims to improve upon and serves as a major point of comparison.
    *   Link: https://arxiv.org/abs/2501.12948

2.  **Li et al. (2025).** Llms can easily learn to reason from demonstrations structure, not content, is what matters!
    *   This work is used as a strong baseline for distillation, and its dataset of challenging problems is used for training and evaluation in the RLT paper.
    *   Link: https://arxiv.org/abs/2502.07374

3.  **Muennighoff et al. (2025).** s1: Simple test-time scaling.
    *   This is a significant recent baseline for scaling reasoning via distillation, against which the authors compare the performance of students trained on RLT traces.
    *   Link: https://arxiv.org/abs/2501.19393

4.  **Bespoke Labs. (2025).** Bespoke-stratos: The unreasonable effectiveness of reasoning distillation.
    *   This blog post details the strongest baseline pipeline, which uses post-processed traces from the large DeepSeek-R1 model, making it a crucial benchmark for the RLT's performance.
    *   Link: www.bespokelabs.ai/blog/bespoke-stratos-the-unreasonable-effectiveness-of-reasoning-distillation

5.  **Shao et al. (2024).** Deepseekmath: Pushing the limits of mathematical reasoning in open language models.
    *   This paper introduced Grouped-Reward Policy Optimization (GRPO), the specific RL algorithm used to train the Reinforcement-Learned Teachers.
    *   Link: https://arxiv.org/abs/2402.03300

6.  **Yue et al. (2025).** Does reinforcement learning really incentivize reasoning capacity in llms beyond the base model?
    *   This citation provides a critical perspective that motivates the RLT framework by questioning whether standard RL for reasoning truly extrapolates beyond a model's initial abilities.
    *   Link: https://arxiv.org/abs/2502.19395

7.  **Hinton et al. (2015).** Distilling the knowledge in a neural network.
    *   This is the foundational paper on knowledge distillation, the core "teacher-student" concept that the RLT framework is designed to optimize for.
    *   Link: https://arxiv.org/abs/1503.02531

8.  **Ecoffet et al. (2019).** Go-explore: a new approach for hard-exploration problems.
    *   This paper is cited as a key example of work tackling the hard exploration problems in RL, a challenge that the RLT framework directly addresses and circumvents.
    *   Link: https://arxiv.org/abs/1901.10995

9.  **Kojima et al. (2022).** Large language models are zero-shot reasoners.
    *   This is a seminal paper that introduced Chain-of-Thought prompting, setting the foundation for research into inducing complex reasoning in LMs, which this work builds upon with RL.
    *   Link: https://proceedings.neurips.cc/paper_files/paper/2022/hash/8bb0d291acd4acf06ef112099c16db32-Abstract-Conference.html

10. **Shen et al. (2025).** Satori: Reinforcement learning with chain-of-action-thought enhances llm reasoning via autoregressive search.
    *   This is cited as a recent, alternative approach to enhancing LM reasoning with RL, providing important context for the current research landscape in which the RLT framework operates.
    *   Link: https://arxiv.org/abs/2502.02508
