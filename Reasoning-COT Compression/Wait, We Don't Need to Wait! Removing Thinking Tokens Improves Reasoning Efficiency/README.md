https://huggingface.co/papers/2506.08343

**Wait, We Don't Need to “Wait”! Removing Thinking Tokens Improves Reasoning Efficiency**

### 1. Summary and Rating

**Summary:**
This paper investigates the efficiency of large reasoning models (LRMs), particularly the "R1-style" models that exhibit explicit, step-by-step Chain-of-Thought (CoT) reasoning. The authors observe that these models often engage in "overthinking," characterized by verbose and redundant reasoning steps marked by self-reflection tokens like "Wait," "Hmm," and "Alternatively." This verbosity increases computational overhead and latency. To address this, the paper proposes NOWAIT, a simple, training-free, inference-time intervention. The method works by identifying a list of self-reflection keywords and using a logit processor to suppress the generation of their corresponding tokens. This steers the model away from redundant validation loops and towards more direct reasoning paths. The authors conduct extensive experiments across ten textual, visual, and video reasoning benchmarks using five different R1-style models. The results demonstrate that NOWAIT can reduce the length of CoT trajectories by 27% to 51% while largely preserving, and in some cases even slightly improving, task accuracy. The paper concludes that explicit self-reflection is not essential for the reasoning capabilities of these models and that suppressing it is a highly effective strategy for improving inference efficiency.

**Rating: 8.5/10**
This is a strong, practical paper that addresses a highly relevant problem in the deployment of large reasoning models: inference efficiency. Its core idea is simple, elegant, and surprisingly effective. The empirical evaluation is thorough, covering multiple modalities, diverse benchmarks of varying difficulty, and several state-of-the-art models. The inclusion of comparisons against other efficiency methods (both training-free and training-based) and the analysis of the differential impact on RL-based versus distilled models adds significant depth and provides valuable insights. While the core technique (logit processing) is not novel, its specific application to surgically remove "overthinking" tokens is a clever and well-motivated contribution. The paper is well-written, the results are clearly presented, and the method is immediately useful as a plug-and-play solution. It falls slightly short of a 9+ because the contribution is more of a clever engineering/empirical finding than a fundamental breakthrough in our understanding of model reasoning, but it is an excellent example of impactful, targeted research.

### 2. Main Ideas

1.  **Explicit Self-Reflection Tokens are a Major Source of Inefficiency:** The paper's central premise is that the "Aha Moment" in R1-style models, signaled by tokens like "Wait" and "Hmm," often leads to "overthinking"—redundant, verbose reasoning loops that significantly increase generation length and latency without contributing positively to the final answer. The paper argues that this behavior is often a form of "behavioral mimicry" rather than a necessary component of complex reasoning.

2.  **Inference-Time Token Suppression (NOWAIT) is an Effective Solution:** The core contribution is NOWAIT, a simple method that intervenes at inference time to improve efficiency. It identifies a predefined list of reflection-related keywords and suppresses their generation by setting their corresponding logits to a large negative value. This training-free approach effectively prunes unnecessary reasoning paths, significantly shortening the output while maintaining model utility.

3.  **Reasoning Robustness Varies by Training Paradigm:** The paper provides an insightful analysis showing that the NOWAIT method has a different impact on models trained with Reinforcement Learning (RL) versus those trained via distillation on CoT data. RL-based models prove to be more robust, maintaining performance even when reflection tokens are suppressed. In contrast, distilled models show significant performance degradation on harder tasks, suggesting their reasoning capabilities are more rigidly tied to the specific CoT structures seen during training, making them more brittle to this kind of intervention.

### 3. 10 Most Important Citations

1.  **Guo et al. 2025.** Deepseek-r1: Incentivizing reasoning capability in llms via reinforcement learning.
    This paper introduces DeepSeek-R1, a prime example of the "R1-style" reasoning models that are the main target of the NOWAIT intervention.

2.  **Chen et al. 2025b.** An empirical study on eliciting and improving r1-like reasoning models.
    This work is cited for identifying the "Aha Moment" phenomenon, where models use tokens like "Wait" to signal self-reflection, which is the core behavior this paper aims to control.

3.  **Sui et al. 2025.** Stop overthinking: A survey on efficient reasoning for large language models.
    This citation helps establish the broader context and problem of "overthinking" in LLMs, which the NOWAIT method is designed to mitigate.

4.  **Ma et al. 2025a.** Reasoning models can be effective without thinking.
    This paper introduces the "NoThink" strategy, a key prompt-based baseline used in the experiments to compare against NOWAIT's effectiveness.

5.  **Luo et al. 2025.** O1-pruner: Length-harmonizing fine-tuning for o1-like reasoning pruning.
    This paper presents a training-based method (O1-Pruner) for improving efficiency, serving as an important point of comparison for the training-free NOWAIT approach.

6.  **Wei et al. 2022.** Chain-of-thought prompting elicits reasoning in large language models.
    This is the foundational paper that introduced Chain-of-Thought (CoT) prompting, the general reasoning paradigm within which this paper operates.

7.  **Yue et al. 2024a.** Mmmu: A massive multi-discipline multimodal understanding and reasoning benchmark for expert agi.
    This is one of the key and most challenging multimodal benchmarks used to validate the effectiveness and robustness of NOWAIT across different data types.

8.  **Yue et al. 2025.** Does reinforcement learning really incentivize reasoning capacity in llms beyond the base model?
    This citation is crucial for the analysis in Section 4.3, as it underscores the significant differences between RL-based and distilled reasoning models, which the paper shows respond differently to the NOWAIT intervention.

9.  **Zhao et al. 2025.** Mmvu: Measuring expert-level multi-discipline video understanding.
    This paper provides the MMVU benchmark, which was essential for demonstrating that NOWAIT's efficiency gains extend to complex video reasoning tasks.

10. **Qwen Team. 2025.** Qwen3: Think Deeper, Act Faster.
    The Qwen3 series of models are used extensively throughout the paper's experiments, making this a critical citation for understanding the specific models being evaluated.
