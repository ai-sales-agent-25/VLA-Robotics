https://arxiv.org/abs/2505.02142

# Exploring the Potential of Offline RL for Reasoning in LLMs: A Preliminary Study

## 1. Summary and Rating

This paper investigates the efficacy of Offline Reinforcement Learning (RL) methods, specifically Direct Preference Optimization (DPO) and its length-desensitized variant (LD-DPO), for enhancing the reasoning capabilities of Large Language Models (LLMs). The authors argue that common Online RL approaches (like PPO or GRPO) are computationally expensive and complex to implement. In contrast, Offline RL offers a simpler, more economical alternative by leveraging pre-collected datasets.

The study conducts experiments using the DeepDistill-32B model as a baseline and evaluates performance on several reasoning benchmarks (AIME2024, GPQA-Diamond, LiveCodeBench, IFEval, Arena-Hard). The results demonstrate that LD-DPO significantly improves model performance, achieving an average enhancement of 3.3% across benchmarks, with a notable 10.1% increase on the challenging Arena-Hard benchmark. A key contribution is the analysis of DPO's sensitivity to output length; the paper highlights that merely increasing reasoning length can be detrimental if not aligned with semantic richness. LD-DPO is shown to mitigate this issue, leading to more stable and meaningful improvements. The paper provides detailed descriptions of data processing and training methodologies, offering practical insights for developing cost-effective Offline RL approaches for LLM reasoning.

**Rating: 8.0/10**

**Reasoning for Rating:**
The paper provides a focused and timely investigation into a practical alternative (Offline RL) for a significant challenge (cost and complexity of Online RL for LLM reasoning). The empirical validation of LD-DPO's benefits, particularly its handling of length sensitivity and its strong performance on challenging benchmarks like Arena-Hard, is a valuable contribution. While termed a "preliminary study," it offers solid empirical evidence and clear insights that can guide future research and development in more economical LLM alignment techniques for reasoning. The methodology is sound, the data processing is well-described, and the paper is well-articulated for its target audience, effectively highlighting the potential of simpler offline methods. The analysis comparing DPO and LD-DPO regarding output length and performance stability is particularly insightful.

## 2. Main Ideas Discussed

1.  **Efficacy of Offline RL for LLM Reasoning:** The primary idea is that simpler, more economical Offline RL methods, particularly Length-Desensitized DPO (LD-DPO), can substantially improve the reasoning capabilities of LLMs. These methods offer a viable alternative to computationally intensive Online RL techniques, achieving significant performance gains (e.g., +3.3% average, +10.1% on Arena-Hard) with lower complexity.
2.  **Addressing Length Sensitivity in DPO:** The paper highlights a critical issue with standard DPO: its tendency to favor longer responses, which can lead to verbosity and redundancy without necessarily improving semantic quality, sometimes even degrading performance (as seen in IFEval for DPO). LD-DPO effectively mitigates this by introducing a length-decoupling hyperparameter, encouraging more concise yet semantically rich outputs, leading to more stable and consistent performance improvements across diverse reasoning tasks. The study emphasizes that meaningful increases in response length (semantic richness) are crucial, not just length itself.

## 3. 10 Most Important Citations

1.  **Rafailov et al. 2023. Direct preference optimization: Your language model is secretly a reward model.**
    This paper introduces DPO, the foundational offline RL algorithm that this study builds upon and aims to improve for reasoning tasks.
    (No direct link in paper, typically found on arXiv or conference proceedings like NeurIPS)

2.  **Liu et al. 2024. Length desensitization in direct preference optimization.**
    This paper introduces LD-DPO, the specific offline RL variant extensively evaluated and shown to be effective in the current study, particularly for addressing DPO's length bias.
    URL: `https://arxiv.org/abs/2409.06411`

3.  **Schulman et al. 2017. Proximal policy optimization algorithms.**
    This citation refers to PPO, a prominent Online RL algorithm often used for LLM fine-tuning, which serves as a contrasting example of the more complex methods the current paper seeks to find alternatives for.
    URL: `https://arxiv.org/abs/1707.06347`

4.  **Ouyang et al. 2022. Training language models to follow instructions with human feedback.**
    This is the InstructGPT paper, foundational for demonstrating the effectiveness of RLHF (often using PPO) for aligning LLMs, setting the context for why RL is important for LLMs.
    URL: `https://arxiv.org/abs/2203.02155`

5.  **DeepSeek-AI et al. 2025. Deepseek-r1: Incentivizing reasoning capability in llms via reinforcement learning.**
    This paper describes DeepSeek-R1, a state-of-the-art reasoning model whose distilled outputs are used to create the training dataset for the Offline RL methods in the current study, highlighting the source of preference data.
    URL: `https://arxiv.org/abs/2501.12948`

6.  **Tian et al. 2025. Deepdistill: Enhancing llm reasoning capabilities via large-scale difficulty-graded data training.**
    This paper introduces DeepDistill-32B, the base model upon which the DPO and LD-DPO experiments are conducted, and also describes the data processing methodology followed.
    URL: `https://arxiv.org/abs/2504.17565`

7.  **Rein et al. 2023. Gpqa: A graduate-level google-proof q&a benchmark.**
    This is one of the key reasoning benchmarks (GPQA-Diamond) used to evaluate the performance of the models, testing challenging multi-step reasoning.
    URL: `https://arxiv.org/abs/2311.12022`

8.  **Li et al. 2024. From crowdsourced data to high-quality benchmarks: Arena-hard and benchbuilder pipeline.**
    This citation refers to the Arena-Hard benchmark, where the LD-DPO method showed particularly significant improvements, underscoring its utility for complex general reasoning.
    URL: `https://arxiv.org/abs/2406.11939` (paper for pipeline, blog for original data: `https://lmsys.org/blog/2024-04-19-arena-hard/`)

9.  **Zhou et al. 2023. Instruction-following evaluation for large language models.**
    This paper introduces IFEval, a benchmark used to evaluate instruction-following capabilities, where LD-DPO demonstrated more stable performance compared to standard DPO.
    URL: `https://arxiv.org/abs/2311.07911`

10. **Jain et al. 2024. Livecodebench: Holistic and contamination free evaluation of large language models for code.**
    This is the LiveCodeBench, a benchmark used for evaluating code generation reasoning, on which LD-DPO showed notable enhancement.
    URL: `arXiv preprint arXiv:2403.07974`
