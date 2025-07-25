https://huggingface.co/papers/2506.03295

https://x.com/WenhuChen/status/1930447298527670662

Unleashing the Reasoning Potential of Pre-trained LLMs by Critique Fine-Tuning on One Problem

**1. Summary and Rating**

**Summary:**
This paper introduces "one-shot Critique Fine-Tuning (CFT)," a novel and compute-efficient method to enhance the reasoning capabilities of pre-trained Large Language Models (LLMs). The core idea is that fine-tuning an LLM using critiques generated from diverse solutions to just a single problem can significantly unlock its inherent reasoning potential. The authors argue that existing methods like Reinforcement Learning (RL), particularly RL with Verifiable Rewards (RLVR), are often resource-intensive and unstable, while Supervised Fine-Tuning (SFT) typically requires large, high-quality datasets.

The proposed one-shot CFT method involves:
1.  Generating a diverse set of candidate solutions to a single seed problem using multiple open-source LLMs.
2.  Employing strong teacher LLMs to provide detailed critiques for each generated solution, focusing on correctness and step-by-step reasoning.
3.  Fine-tuning the base LLM on this compact dataset of (problem, candidate solution) -> critique pairs.

The authors conduct experiments on Qwen and Llama family models (1.5B to 14B parameters), evaluating them on mathematical and logical reasoning benchmarks. Their results demonstrate that one-shot CFT leads to substantial performance improvements. For instance, Qwen-Math-7B-CFT showed an average improvement of 15% on six math benchmarks and 16% on three logic reasoning benchmarks with only 5 GPU hours of training. This performance is comparable to or even surpasses one-shot RLVR, but with approximately 20 times less computational cost. Ablation studies confirm the robustness of the method across different seed problems and highlight the benefit of diverse candidate solutions. The paper posits one-shot CFT as a simple, general, and efficient approach for unlocking LLM reasoning, especially in scenarios with limited compute or data.

**Rating: 9/10**

For a PhD-level audience, this paper is rated 9/10.
*   **Novelty and Significance:** The concept of "one-shot" fine-tuning to elicit complex reasoning is highly relevant, and extending this to critique-based learning (CFT) is a novel and logical step. The paper addresses a significant challenge in LLM development: efficiently improving reasoning without massive computational overhead or data requirements.
*   **Methodological Soundness:** The methodology is clearly articulated and appears sound. The construction of the critique dataset is systematic, and the experimental design includes appropriate baselines (base models, SFT with full and one example, one-shot RLVR) and relevant benchmarks for both mathematical and logical reasoning. The use of "sober" baselines and consideration of training efficiency are commendable.
*   **Results and Impact:** The reported results are impressive, particularly the substantial performance gains coupled with a significant reduction in compute (20x less than one-shot RLVR). If these results generalize, one-shot CFT could be a very practical and impactful technique for practitioners.
*   **Clarity and Rigor:** The paper is well-written and clearly presents its contributions. The ablation studies on seed problem choice and solution diversity add to the rigor of the findings. The authors also acknowledge limitations, such as mixed results on already strong reasoning-oriented LLMs.

The paper makes a strong case for one-shot CFT as an efficient and effective method. While building on existing ideas like general CFT and one-shot RL, its specific focus and compelling efficiency gains make it a valuable contribution to the field of LLM post-training. The ".1" is held back mainly because, while highly efficient and effective for its stated scope, it's an improvement technique rather than a foundational paradigm shift, and its effectiveness is noted to be less consistent on already heavily optimized models.

**2. Main Ideas Discussed**

The main ideas discussed in this paper are:

1.  **One-Shot Critique Fine-Tuning (CFT) as an Effective Method for Unleashing LLM Reasoning:** The central thesis is that fine-tuning an LLM on detailed critiques of diverse, model-generated solutions to *only one problem* can significantly enhance its reasoning abilities across a range of mathematical and logical tasks. This suggests that LLMs possess latent reasoning capabilities that can be activated with highly targeted and critique-rich supervision.
2.  **Superior Compute-Efficiency and Comparability to Alternatives:** One-shot CFT is presented as a substantially more compute-efficient alternative to methods like one-shot Reinforcement Learning with Verifiable Rewards (RLVR), achieving comparable or even superior performance with significantly less training time (e.g., 20x less compute). It also outperforms standard Supervised Fine-Tuning (SFT), even when SFT uses much larger datasets, by encouraging deeper error analysis rather than mere imitation of solutions.
3.  **The Importance of Diverse Candidate Solutions and Teacher Critiques:** The effectiveness of one-shot CFT relies on constructing a rich training signal from a single problem. This is achieved by (a) generating a diverse set of candidate solutions (from multiple generator models) to expose the model being fine-tuned to various reasoning pathways and error types, and (b) using powerful teacher LLMs to provide detailed critiques, which guide the learning process more effectively than simple correct/incorrect labels or reference solutions alone.

**3. 10 Most Important Citations**

Here is a list of 10 important citations from the paper, formatted as requested:

1.  **Wang et al. 2025a.** Reinforcement learning for reasoning in large language models with one training example.
    *   This paper introduces the "1-shot RLVR" concept, which serves as a key benchmark and motivation for the current work's exploration of "one-shot" learning paradigms for reasoning.
    *   Link: `https://arxiv.org/abs/2504.20571` (derived from preprint ID)

2.  **Wang et al. 2025b.** Critique fine-tuning: Learning to critique is more effective than learning to imitate.
    *   This citation provides the foundational "Critique Fine-Tuning (CFT)" methodology that the current paper adapts and specializes into a "one-shot" approach.
    *   Link: `https://arxiv.org/abs/2501.17703` (derived from preprint ID)

3.  **Guo et al. 2025.** Deepseek-r1: Incentivizing reasoning capability in llms via reinforcement learning.
    *   This paper is cited for its work on Reinforcement Learning with Verifiable Rewards (RLVR), a prominent post-training method for reasoning that the current paper compares against in terms of performance and efficiency.
    *   Link: `https://arxiv.org/abs/2501.12948` (derived from preprint ID)

4.  **Ouyang et al. 2022.** Training language models to follow instructions with human feedback.
    *   This is a foundational paper on instruction fine-tuning and aligning LLMs using human feedback, establishing the importance of post-training for model capabilities.
    *   (No direct link in references, but widely known as InstructGPT paper, often found on arXiv: `https://arxiv.org/abs/2203.02155`)

5.  **Achiam et al. 2023.** Gpt-4 technical report.
    *   Describes GPT-4, a powerful LLM used in this study as one of the "teacher models" for generating critiques, highlighting the capability of advanced models in providing supervision.
    *   Link: `https://arxiv.org/abs/2303.08774` (derived from preprint ID)

6.  **Hendrycks et al. 2021.** Measuring mathematical problem solving with the math dataset.
    *   This paper introduces the MATH dataset, a key benchmark used extensively in the current work to evaluate the mathematical reasoning capabilities of the fine-tuned LLMs.
    *   Link: `https://arxiv.org/abs/2103.03874` (derived from preprint ID)

7.  **Lewkowycz et al. 2022.** Solving quantitative reasoning problems with language models.
    *   Introduces Minerva, an LLM focused on quantitative reasoning, and its associated benchmark (Minerva Math), which is used for evaluation in this paper.
    *   (No direct link in references, but NIPS paper, often on arXiv: `https://arxiv.org/abs/2206.14858`)

8.  **Kazemi et al. 2025.** Big-bench extra hard.
    *   This paper defines the BIG-Bench Extra Hard (BBEH) benchmark, which is used to evaluate the logical reasoning capabilities of the models, testing generalization beyond mathematical tasks.
    *   Link: `https://arxiv.org/abs/2502.19187` (derived from preprint ID)

9.  **Hochlehnert et al. 2025.** A sober look at progress in language model reasoning: Pitfalls and paths to reproducibility.
    *   This work is cited for providing "sober baseline scores" and for its critical analysis of RLVR evaluation practices, lending credibility to the current paper's evaluation by using these more rigorous baselines.
    *   Link: `https://arxiv.org/abs/2504.07086` (derived from preprint ID)

10. **Shao et al. 2025.** Spurious rewards: Rethinking training signals in rlvr.
    *   This citation is important as it discusses the challenges of RLVR, such as reliance on spurious reward signals, which motivates the search for alternative, potentially more robust and generalizable methods like CFT.
    *   (Cited as "Notion Blog" in references; no standard academic link provided in the paper.)
