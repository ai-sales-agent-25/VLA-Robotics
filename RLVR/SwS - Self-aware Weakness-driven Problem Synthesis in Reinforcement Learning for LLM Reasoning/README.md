https://huggingface.co/papers/2506.08989

**SwS: Self-aware Weakness-driven Problem Synthesis in Reinforcement Learning for LLM Reasoning**

### 1. Summary and Rating

**Summary:**
This paper introduces "Self-aware Weakness-driven problem Synthesis" (SwS), a novel framework for improving the reasoning capabilities of Large Language Models (LLMs) through Reinforcement Learning with Verifiable Rewards (RLVR). The core issue addressed is the scarcity of high-quality, appropriately difficult training data for RL. SwS tackles this by first running a preliminary RL phase to identify a model's specific weaknesses—problems it consistently fails to learn. It then extracts the core mathematical concepts from these failure cases and synthesizes new, targeted problems designed to address these deficiencies. These synthetic problems undergo rigorous quality filtering, including verification of answers and difficulty-level screening, to ensure they provide a useful learning signal. The model is then further trained on an augmented dataset combining the original problems with these newly synthesized ones. The authors demonstrate that this weakness-driven approach leads to significant performance gains (average absolute improvements of 7.7% to 10.0%) across various model sizes (3B to 32B) and eight standard mathematical reasoning benchmarks, outperforming baseline models and other RL methods.

**Rating: 9/10**
This is an excellent paper with a novel and intuitive core idea. The methodology is sound, well-structured, and addresses a critical bottleneck in scaling RL for LLM reasoning—the generation of effective training data. The "self-aware" aspect, where the model's own failures guide the data synthesis process, is a clever and efficient alternative to generic data augmentation. The experimental evaluation is comprehensive, using multiple model sizes, strong baselines, and a wide array of difficult benchmarks, lending significant weight to the claimed performance improvements. The paper is clearly written, and the ablation studies and extensions (e.g., to weak-to-strong generalization and self-evolving paradigms) are thoughtful and further demonstrate the robustness and potential of the SwS framework. It represents a significant and practical contribution to the field.

---

### 2. Main Ideas

1.  **Self-aware Weakness Identification:** The central idea is to use the model's own performance during a preliminary RL training phase to pinpoint its weaknesses. A "weakness" is defined as a problem that the model consistently fails to solve and shows no learning progress on. This model-centric approach dynamically identifies the most relevant areas for improvement, moving beyond static datasets or generic difficulty heuristics.

2.  **Targeted Problem Synthesis and Augmentation:** Instead of simply rephrasing questions or augmenting data indiscriminately, SwS synthesizes entirely new problems that are specifically tailored to the model's identified weaknesses. This is achieved by extracting the underlying concepts from the "failed" problems, strategically recombining them, and then using a powerful instruction model to generate new questions. The process is made more efficient by allocating the problem synthesis budget based on the failure rates across different problem categories, focusing efforts where they are most needed.

3.  **Rigorous Multi-Stage Data Filtering for RL:** The paper emphasizes that the effectiveness of RLVR hinges on the quality of the training problems. The SwS framework incorporates a robust pipeline to ensure data quality. This includes (i) quality verification of the generated problem's text and rationale, (ii) generating and verifying a correct answer using self-consistency from a strong reasoning model, and (iii) difficulty filtering to select problems that are neither too easy nor too hard for the target model, thereby maximizing the gradient signal during RL training.

---

### 3. Top 10 Most Important Citations

1.  **Shao et al. 2024.** Deepseekmath: Pushing the limits of mathematical reasoning in open language models. This paper is cited for introducing Group Relative Policy Optimization (GRPO), the core reinforcement learning algorithm utilized throughout the SwS framework.

2.  **Guo et al. 2025.** Deepseek-r1: Incentivizing reasoning capability in llms via reinforcement learning. This is a foundational paper on applying RLVR to enhance LLM reasoning at scale, providing crucial context and motivation for the work.

3.  **Yu et al. 2025.** Dapo: An open-source llm reinforcement learning system at scale. The DAPO system's dataset is used for the initial training of larger models in the experiments, and the paper is referenced for methodological choices like omitting the KL term in RL.

4.  **Burns et al. 2023.** Weak-to-strong generalization: Eliciting strong capabilities with weak supervision. This citation is crucial as the authors directly extend their SwS framework to a weak-to-strong generalization setting, a key analysis in the paper.

5.  **Cobbe et al. 2021.** Training verifiers to solve math word problems. This pioneering work introduced the widely-used GSM8K dataset and demonstrated the viability of using outcome-based rewards (verifiable answers) for improving mathematical reasoning.

6.  **Hendrycks et al. 2021.** Measuring mathematical problem solving with the math dataset. This paper introduced the MATH dataset, which is a primary resource for both initial training (to find weaknesses) and evaluation in the experiments.

7.  **Zhao et al. 2025.** Promptcot: Synthesizing olympiad-level problems for mathematical reasoning in large language models. This work inspired the core synthesis mechanism in SwS, particularly the idea of recombining concepts to generate new, complex problems.

8.  **Huang et al. 2024.** Key-point-driven data synthesis with its enhancement on mathematical reasoning. This is a key piece of related work on data synthesis via concept combination, which helps to position the novelty of SwS's "weakness-driven" approach.

9.  **Luo et al. 2023.** Wizardmath: Empowering mathematical reasoning for large language models via reinforced evol-instruct. This paper presents a well-known method for improving problem difficulty and complexity (Evol-Instruct), which is cited as a potential future direction to enhance the SwS pipeline.

10. **Lightman et al. 2023.** Let's verify step by step. This paper is a key reference for process-level rewards and verification, which is a major alternative to the outcome-based reward paradigm used in SwS and is discussed in the related work section.
