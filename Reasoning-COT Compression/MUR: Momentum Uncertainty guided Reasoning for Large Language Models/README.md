https://huggingface.co/papers/2507.14958

MUR: Momentum Uncertainty guided Reasoning for Large Language Models

### 1. Summary and Rating

This paper introduces Momentum Uncertainty-guided Reasoning (MUR), a novel, training-free algorithm designed to improve the computational efficiency of Large Language Models (LLMs) during reasoning tasks. The authors identify that existing Test-Time Scaling (TTS) methods, which enhance reasoning by allocating more computational resources (e.g., generating multiple solutions), often suffer from "overthinking," where they waste resources on simple, straightforward steps of a problem.

The core idea of MUR is to selectively and dynamically apply these resource-intensive TTS methods only when the model shows significant uncertainty. To achieve this, the paper proposes a new metric called "momentum uncertainty," which is an exponentially weighted moving average of step-level uncertainties from the reasoning process. Inspired by the concept of momentum in physics, this metric provides a more stable and context-aware assessment of the model's confidence compared to instantaneous, step-level uncertainty. A reasoning step is scaled only if its uncertainty significantly deviates from the aggregated momentum uncertainty. The framework also includes a `γ-control` hyperparameter, allowing users to flexibly manage the trade-off between performance and computational cost. The authors provide theoretical proofs demonstrating the stability and superior convergence properties of momentum uncertainty. Through extensive experiments on challenging benchmarks like MATH and AIME with the Qwen3 model family, they show that MUR can reduce computational token usage by over 50% on average while simultaneously improving reasoning accuracy by 0.62% to 3.37%.

**Rating: 9/10**

This paper is excellent. It addresses a highly relevant and practical problem in LLM inference: the trade-off between reasoning quality and computational cost. The proposed solution, MUR, is both elegant and intuitive, cleverly adapting the well-established concept of momentum to create a stable uncertainty metric. The method's strength lies in its simplicity and its nature as a training-free, orthogonal improvement that can be layered on top of various existing reasoning techniques. The authors support their proposal with a solid theoretical analysis of the metric's properties (variance, bias, convergence) and back it up with comprehensive empirical results that demonstrate significant gains in both efficiency and effectiveness. For a PhD-level audience, this work stands out for its clear motivation, technical rigor, and impactful results.

### 2. Main Ideas

The three main ideas of this paper are:

1.  **Adaptive Reasoning with Momentum Uncertainty:** The central contribution is the concept of "momentum uncertainty." Instead of relying on the noisy, fluctuating uncertainty of a single reasoning step, the paper proposes tracking an exponentially weighted average of uncertainties over the entire reasoning trajectory. This provides a smoothed, more stable baseline of the model's confidence, allowing the system to robustly detect when a new step is a significant outlier that requires more careful thought.
2.  **Selective Test-Time Scaling (TTS) to Mitigate "Overthinking":** The paper posits that applying TTS methods to every single step of a reasoning chain is inefficient and leads to computational waste on simple steps. MUR uses the momentum uncertainty metric to create an adaptive framework that applies TTS only to "critical" steps, thereby drastically reducing the total computational cost (token usage) without harming, and in many cases improving, overall performance.
3.  **Flexible Budget Control via `γ-control`:** MUR introduces a single hyperparameter, `γ`, that modulates the sensitivity of the uncertainty detector. This mechanism provides a simple and flexible knob for users to control the trade-off between computational budget and reasoning accuracy at inference time, without any need for model retraining.

### 3. 10 Most Important Citations

1.  **Qian et al. (1999)** On the momentum term in gradient descent learning algorithms.
    *   This paper is the primary inspiration for the core mechanism in MUR, providing the foundational concept of using momentum to smooth updates and stabilize a process.

2.  **Chen et al. (2024b)** Do not think that much for 2+ 3=? on the overthinking of o1-like llms.
    *   This citation is crucial as it formally identifies and discusses the problem of "overthinking" in LLMs, which is the central problem MUR aims to solve.

3.  **Brown et al. (2020)** Language models are few-shot learners.
    *   This is the foundational paper on GPT-3 that demonstrated the power of large-scale language models and set the stage for subsequent research on their reasoning capabilities.

4.  **Yao et al. (2023)** Tree of thoughts: Deliberate problem solving with large language models.
    *   This paper introduced a highly influential Test-Time Scaling (TTS) method for complex reasoning, representing a key class of methods that MUR can be applied to in order to improve efficiency.

5.  **Yang et al. (2025a)** Qwen3 technical report.
    *   This report details the Qwen3 models that are used exclusively for the experiments in this paper, making it essential for the reproducibility and context of the empirical results.

6.  **Kim et al. (2025)** Guiding reasoning in small language models with llm assistance.
    *   This work introduced the "SMART" baseline, a competing method for adaptive reasoning that MUR is systematically compared against in the experimental results.

7.  **Hendrycks et al. (2021)** Measuring mathematical problem solving with the math dataset.
    *   This paper introduced the MATH dataset, a primary and challenging benchmark used in the evaluation to demonstrate MUR's effectiveness in a difficult domain.

8.  **Lightman et al. (2023)** Let's verify step by step.
    *   This work on stepwise verification is a prominent example of sequential reasoning methods that can be made more efficient by MUR's selective scaling approach.

9.  **Ren et al. (2022)** Out-of-distribution detection and selective generation for conditional language models.
    *   This paper is cited as a baseline approach that uses a simple average of uncertainty, which MUR's momentum-based approach is theoretically and empirically shown to outperform.

10. **Rein et al. (2024)** GPQA: A graduate-level google-proof q&a benchmark.
    *   This citation provides the GPQA dataset, which is used to validate the generalization of MUR's approach to the science domain beyond just mathematics.
    *   Link: https://openreview.net/forum?id=Ti67584b98
