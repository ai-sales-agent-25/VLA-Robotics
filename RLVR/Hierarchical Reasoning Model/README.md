https://arxiv.org/abs/2506.21734

https://x.com/Dorialexander/status/1951954826545238181

https://x.com/omarsar0/status/1951751651729060081

https://x.com/makingAGI/status/1947286324735856747

https://x.com/casper_hansen_/status/1951656675250684163

https://x.com/Dorialexander/status/1951781342632394886

https://www.youtube.com/watch?v=DvZ8jZ-laj4

Hierarchical Reasoning Model

### 1. Summary and Rating

This paper introduces the Hierarchical Reasoning Model (HRM), a novel, brain-inspired recurrent architecture designed to overcome the limitations of standard Transformers in complex reasoning tasks. The authors argue that the fixed, shallow computational depth of models like LLMs prevents them from solving problems requiring algorithmic execution, forcing reliance on brittle and data-intensive Chain-of-Thought (CoT) prompting. The HRM addresses this by featuring two interdependent recurrent modules operating at different timescales: a high-level module for slow, abstract planning and a low-level module for fast, detailed computations. This design enables significant computational depth while maintaining training stability through a process termed "hierarchical convergence," where the fast module reaches local equilibria before the slow module updates, preventing the premature convergence that plagues typical RNNs.

Remarkably, the HRM is trained from scratch without BPTT, using an efficient one-step gradient approximation and a deep supervision scheme. The model also incorporates an adaptive computational time (ACT) mechanism to dynamically adjust processing steps based on task complexity. With only 27 million parameters and trained on just 1000 examples, HRM achieves near-perfect accuracy on tasks intractable for large LLMs, such as solving complex Sudoku puzzles and finding optimal paths in large mazes. It also substantially outperforms larger models on the Abstraction and Reasoning Corpus (ARC). A key finding is that the trained HRM develops an emergent dimensionality hierarchy—with the high-level module operating in a much higher-dimensional space than the low-level one—that strikingly mirrors organizational principles observed in the mouse cortex.

**Rating: 9.5/10**

This is an exceptional paper that presents a compelling alternative to the dominant Transformer-based paradigm for reasoning. Its novelty lies not just in the architecture itself but in the synthesis of ideas from neuroscience, dynamical systems, and deep learning to solve a fundamental problem. The empirical results are striking, demonstrating a massive leap in data efficiency and performance on tasks that are canonical examples of algorithmic reasoning. The analysis of the emergent dimensionality hierarchy provides strong, falsifiable evidence for the model's underlying mechanism and its correspondence to biological computation, elevating the work beyond a simple demonstration of performance. For a PhD-level audience, the paper is highly stimulating, challenging prevailing assumptions about scale vs. architecture and providing a well-executed, rigorously evaluated, and potentially transformative research direction.

### 2. Main Ideas

1.  **Hierarchical, Multi-Timescale Recurrence for Deep Reasoning:** The central idea is that complex reasoning requires deep, iterative computation, which is ill-suited to the fixed-depth nature of standard Transformers. The HRM's architecture, inspired by the brain's cortical hierarchy, implements this with two coupled recurrent modules: a "slow" high-level planner and a "fast" low-level executor. This structure enables "hierarchical convergence," allowing the model to perform long, stable reasoning sequences within a single forward pass, effectively overcoming the depth limitations of Transformers and the instability of traditional RNNs.
2.  **Efficient, BPTT-Free Training for Deep Recurrence:** The paper introduces a practical and efficient training regime that avoids the memory-intensive and biologically implausible Backpropagation Through Time (BPTT). It uses a one-step gradient approximation, theoretically grounded in the mathematics of Deep Equilibrium Models, combined with a deep supervision strategy. This allows the model to receive frequent gradient feedback during training, enabling it to learn complex, multi-step algorithms from only a few thousand input-output examples, without any intermediate supervision like CoT traces.
3.  **Emergent Functional Specialization Mirroring the Brain:** A key finding is that the hierarchical architecture, when trained, gives rise to an emergent functional organization that parallels the brain. The paper shows that the high-level module learns to operate in a high-dimensional representation space (high Participation Ratio), allowing for flexible, context-dependent processing, while the low-level module operates in a more constrained, low-dimensional space. This dimensionality hierarchy, which does not exist in the untrained model, suggests the model autonomously discovers a fundamental principle of neural computation and provides a mechanistic explanation for its powerful reasoning capabilities.

### 3. 10 Most Important Citations

1.  **Wei et al. (2022) Chain-of-thought prompting elicits reasoning in large language models.**
    This citation is critical as it defines the "Chain-of-Thought" (CoT) paradigm, which the HRM paper identifies as the dominant but flawed method for reasoning in current LLMs and aims to provide an alternative to.
2.  **Chollet. (2019) On the measure of intelligence (abstraction and reasoning corpus).**
    This paper introduced the Abstraction and Reasoning Corpus (ARC), a key benchmark used to demonstrate HRM's superior generalization and inductive reasoning capabilities compared to much larger models.
3.  **Murray et al. (2014) A hierarchy of intrinsic timescales across primate cortex.**
    This is a foundational neuroscientific citation providing evidence for the hierarchical and multi-timescale processing in the brain that directly inspires the core design of the HRM's high-level and low-level modules.
4.  **Bai et al. (2019) Deep equilibrium models.**
    This work is central to the theoretical justification of HRM's training method, as the paper explicitly grounds its one-step gradient approximation in the concepts of Deep Equilibrium Models (DEQ) and the Implicit Function Theorem.
5.  **Lillicrap et al. (2019) Backpropagation through time and the brain.**
    This citation articulates the computational expense and biological implausibility of Backpropagation Through Time (BPTT), reinforcing the significance of HRM's proposed BPTT-free approximate gradient training method.
6.  **Vaswani et al. (2017) Attention is all you need.**
    This is the foundational paper for the Transformer, the architecture dominant in modern AI, whose computational limitations in reasoning the HRM is explicitly designed to address and overcome.
7.  **Graves et al. (2016) Adaptive computation time for recurrent neural networks.**
    This paper introduced Adaptive Computation Time (ACT), a mechanism for dynamically allocating computational steps, which the HRM successfully incorporates to manage reasoning complexity and improve efficiency.
8.  **Posani et al. (2025) Rarely categorical, always high-dimensional: how the neural code changes along the cortical hierarchy.**
    This paper provides the direct comparative data from the mouse cortex on dimensionality hierarchy (Figure 8), which the HRM's trained modules are shown to replicate, forming the basis of the "Brain Correspondence" section.
9.  **Dehghani et al. (2018) Universal transformers.**
    This is a significant piece of related work that also attempted to make Transformers Turing-complete by adding recurrence; it serves as an important benchmark for comparison regarding HRM's claims of computational universality and practical performance.
10. **Kahneman et al. (2011) Thinking, fast and slow.**
    This work provides the highly influential cognitive framework of "System 1" (fast, automatic) and "System 2" (slow, deliberate) thinking, which the paper uses as an analogy for the interaction between its low-level and high-level modules.
