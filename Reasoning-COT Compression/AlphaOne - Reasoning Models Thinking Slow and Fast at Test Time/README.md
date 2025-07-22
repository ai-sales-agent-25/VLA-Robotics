https://huggingface.co/papers/2505.24863

ALPHAONE: Reasoning Models Thinking Slow and Fast at Test Time

**1. Summary and Rating**

This paper introduces ALPHAONE (α1), a novel and universal framework for modulating reasoning progress in Large Reasoning Models (LRMs) at test time. It addresses the common LRM challenge of suboptimally balancing "slow" (deep, deliberate) and "fast" (efficient, superficial) thinking, which can lead to issues like overthinking or underthinking. α1 operates by first defining an "alpha moment" (α), a universal parameter that scales the thinking phase budget for an LRM. In the phase leading up to this α moment (pre-α moment), α1 dynamically schedules slow thinking transitions by stochastically inserting "wait" tokens (or similar cues for deliberation) based on a Bernoulli process with a time-varying probability. This allows for flexible control, such as initiating with slow thinking and gradually transitioning towards faster processing. After the α moment (post-α moment), α1 deterministically terminates prolonged slow thinking by replacing any further "wait" tokens with an "end-of-thinking" token (e.g., "</think>"). This crucial step actively encourages a shift to fast reasoning and efficient answer generation, combating what the authors term "slow thinking inertia."

The authors conduct extensive empirical studies across mathematical, coding, and scientific reasoning benchmarks using various o1-style LRMs (e.g., variants of DeepSeek-R1 and Qwen). The results demonstrate that α1 generally outperforms existing monotonic scaling methods (like s1 for increasing slow thinking, or CoD for decreasing it) in both reasoning capability and efficiency. α1 not only achieves higher accuracy but often does so with a reduced or comparable number of generated tokens. The framework is shown to effectively unify and generalize prior sparse modulation techniques by enabling more dense and flexible control. A key finding is that a "slow thinking first, then fast thinking" schedule, implemented via an annealing probability for "wait" token insertion, yields the best results.

**Rating: 9/10**

For a PhD-level audience, this paper is a strong contribution.
*   **Novelty and Significance:** It offers a comprehensive and principled framework for an important, practical problem in LRM deployment—managing the cognitive load and efficiency of reasoning processes at test time. The concept of the 'alpha moment' as a universal scaling factor, combined with distinct pre- and post-moment modulation strategies, is novel and addresses limitations of prior, simpler approaches.
*   **Methodology:** The proposed mechanisms (stochastic pre-alpha scheduling, deterministic post-alpha termination) are well-defined and intuitively address different aspects of reasoning control. The framework's ability to unify existing methods is a plus.
*   **Empirical Rigor:** The experimental validation is thorough, spanning multiple diverse benchmarks, different model sizes, and including crucial ablation studies that support the design choices (e.g., necessity of post-alpha modulation, effectiveness of linear annealing for scheduling). The introduction of the REP metric for efficiency-performance trade-off is also valuable.
*   **Clarity:** While introducing new concepts, the paper explains them clearly, supported by illustrative figures (e.g., Fig 1, Fig 2). The problem statement, proposed solution, and results are well-articulated.

The paper tackles a specific niche (test-time scaling for o1-style LRMs) but does so with a robust and generalizable approach that could influence future work on dynamic LRM inference. The only slight hesitation for a perfect score might stem from the reliance on specific tokens like "wait," which could vary in future LRM architectures, a limitation acknowledged by the authors. However, the underlying principles of dynamically budgeted and scheduled deliberation phases are broadly applicable.

**2. Main Ideas Discussed**

1.  **A Universal Framework for Test-Time Reasoning Modulation (ALPHAONE):** The central idea is the ALPHAONE (α1) framework itself, which provides a universal method to control the reasoning process of LRMs at test time. It introduces the "alpha moment" (α) to scale the overall thinking budget, uses stochastic insertion of "wait" tokens (pre-α moment) to dynamically encourage or schedule slow thinking, and employs deterministic replacement of "wait" tokens with an "end-of-thinking" token (post-α moment) to ensure a transition to efficient, fast answer generation.
2.  **Flexible Slow-to-Fast Reasoning Scheduling:** Unlike prior methods that often apply monotonic adjustments to reasoning depth, α1 allows for dynamic and flexible scheduling of slow thinking. Specifically, the paper demonstrates that a "slow thinking first, then fast thinking" strategy, implemented via an annealing schedule for the probability of inserting "wait" tokens, is more effective. This allows the model to deliberate more when needed (typically earlier in the reasoning process) and then become more direct.
3.  **Overcoming "Slow Thinking Inertia" for Efficiency:** The paper identifies "slow thinking inertia"—where LRMs, once engaged in deep thought, struggle to efficiently switch back to fast thinking for answer generation. The post-α moment modulation in α1 directly tackles this by deterministically terminating further slow thinking, thereby improving not only the quality of reasoning but also the overall efficiency (e.g., reducing unnecessary token generation).

**3. List of 10 Most Important Citations**

1.  **Kahneman, D.** 2011. Thinking, fast and slow.
    *   This book provides the foundational psychological concept of System 1 (fast) and System 2 (slow) thinking in humans, which the paper uses as an analogy to frame the reasoning processes in LRMs.
2.  **Jaech et al.** 2024. Openai o1 system card.
    *   This paper describes OpenAI's o1 model, establishing the "o1-style" LRM paradigm (thinking-then-answering, use of tokens like `</think>`) that ALPHAONE is designed to modulate.
3.  **DeepSeek-AI et al.** 2025. Deepseek-r1: Incentivizing reasoning capability in llms via reinforcement learning.
    *   Describes a key o1-style LRM used as a base model in ALPHAONE's experiments and highlights the use of reinforcement learning to train for slow thinking capabilities.
4.  **Muennighoff et al.** 2025. s1: Simple test-time scaling.
    *   This paper introduces the "s1" method, a significant baseline for test-time scaling that ALPHAONE compares against and aims to generalize by offering more flexible and dense modulation.
5.  **Xu et al.** 2025. Chain of draft: Thinking faster by writing less.
    *   This paper proposes "Chain of Draft" (CoD), another important baseline method focused on reducing the thinking budget, which ALPHAONE is benchmarked against.
6.  **Wei et al.** 2022. Chain-of-thought prompting elicits reasoning in large language models.
    *   This seminal work introduced chain-of-thought prompting, which is fundamental to the "thinking phase" of LRMs that ALPHAONE modulates.
7.  **Yang, Wang, et al.** 2025c. Speculative thinking: Enhancing small-model reasoning with large model guidance at inference time. (The paper cites this as Yang et al., 2025c; the full first author from the bib is Wang Yang).
    *   This citation is noted as inspiring the mechanism of appending "wait" tokens after structural delimiters (`\n\n`) due to their observed co-existence, informing a design choice in ALPHAONE's pre-α moment modulation.
8.  **Lightman et al.** 2024. Let's verify step by step.
    *   This work is relevant to the development of advanced LRMs through process-based reward models and is associated with the MATH benchmark, one of the evaluation datasets.
9.  **Wang et al.** 2023. Self-consistency improves chain of thought reasoning in language models.
    *   Describes self-consistency, an important parallel scaling technique for improving LRM reasoning, providing context for the broader area of test-time enhancements.
10. **Chen et al.** 2024b. Do NOT think that much for 2+3=? on the overthinking of o1-like llms.
    *   This paper directly addresses the "overthinking" problem in o1-like LRMs, which is one of the core issues ALPHAONE aims to mitigate by providing better control over the reasoning process.
