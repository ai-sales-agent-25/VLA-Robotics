https://huggingface.co/papers/2506.13585

https://x.com/natolambert/status/1934802793757311185

https://huggingface.co/MiniMaxAI/MiniMax-M1-80k

**MiniMax-M1: Scaling Test-Time Compute Efficiently with Lightning Attention**

### 1. Summary and Rating

This paper introduces MiniMax-M1, a 456-billion parameter open-weight large reasoning model featuring a novel hybrid architecture. This architecture combines a Mixture-of-Experts (MoE) design with "Lightning Attention," a form of I/O-aware linear attention, enabling a 1-million-token context window and highly efficient long-sequence generation. A key contribution is a new reinforcement learning algorithm called CISPO (Clipped IS-weight Policy Optimization), which stabilizes and accelerates RL training by clipping importance sampling weights rather than entire token updates, thus preserving gradients from crucial reasoning tokens. The authors provide a detailed methodology for training, including continual pre-training, supervised fine-tuning, and a sophisticated RL phase using a diverse curriculum of verifiable (e.g., math, software engineering) and non-verifiable tasks. They transparently discuss and provide solutions for practical training challenges, such as numerical precision mismatches and optimizer instability. Extensive benchmarks show MiniMax-M1 is highly competitive with leading open-weight models like DeepSeek-R1 and Qwen3-235B, with standout performance on complex software engineering, long-context understanding, and agentic tool-use tasks, validating its efficiency for next-generation, long-reasoning applications.

**Rating: 9/10**

This is an excellent paper that makes significant contributions on multiple fronts. The synthesis of MoE and a linear attention variant at this scale, released as an open-weight model, is a major advance for the community. The proposed CISPO algorithm is a novel and well-motivated improvement over existing PPO-style methods, supported by clear empirical evidence. The paper's strength lies in its combination of architectural innovation, algorithmic novelty, and rigorous, transparent reporting of the large-scale training process and its challenges. It serves as both a release of a powerful new model and a valuable technical document on how to build and train such systems efficiently.

### 2. Main Ideas

1.  **Hybrid Attention for Efficient Long-Context Reasoning:** The central architectural innovation is the use of a hybrid attention mechanism that mixes standard softmax attention with "Lightning Attention" (a linear attention variant). By using one standard attention block for every seven linear attention blocks, the model dramatically reduces the computational complexity (FLOPs) of processing and generating long sequences, enabling a 1M token context and 80K token generation length while being significantly more efficient than models relying solely on quadratic attention.

2.  **CISPO: An Efficient Reinforcement Learning Algorithm:** The paper proposes a novel RL algorithm, Clipped IS-weight Policy Optimization (CISPO). It addresses a key limitation in PPO-style algorithms where important but low-probability "reasoning fork" tokens (e.g., "However," "Recheck") get their updates clipped. CISPO instead clips the importance sampling (IS) weight, ensuring all tokens contribute to the gradient, which leads to more stable and faster RL training, demonstrated by a 2x speedup over the DAPO algorithm in a controlled experiment.

3.  **A Scalable Training and Data Curation Methodology:** The paper provides a comprehensive blueprint for developing a large-scale reasoning model. This includes a multi-stage training process (continual pre-training, SFT, RL) and a detailed strategy for curating a diverse data curriculum. This curriculum integrates rule-based verifiable environments (for math, coding, and software engineering) with model-based feedback for general tasks, and it outlines a curriculum learning approach to balance these domains, providing a valuable methodology for the field.

### 3. 10 Most Important Citations

1.  **Vaswani et al. 2017. Attention is all you need.**
    This foundational paper introduced the Transformer architecture, upon which nearly all modern LLMs, including MiniMax-M1, are built.

2.  **Schulman et al. 2017. Proximal policy optimization algorithms.**
    This work introduced the PPO algorithm, which is the foundational RL method that the paper's novel CISPO algorithm directly modifies and compares against.

3.  **Wei et al. 2022. Chain-of-thought prompting elicits reasoning in large language models.**
    This paper established the concept of Chain-of-Thought (CoT) reasoning, which is the core capability that MiniMax-M1 and other large reasoning models are optimized to perform and scale.

4.  **Qin et al. 2024b. Lightning attention-2: A free lunch for handling unlimited sequence lengths in large language models.**
    This work introduces the "Lightning Attention" mechanism that is the core component of MiniMax-M1's efficient hybrid architecture, enabling its long-context capabilities.

5.  **MiniMax et al. 2025. Minimax-01: Scaling foundation models with lightning attention.**
    This is the authors' own previous work on the base model, MiniMax-Text-01, which was further trained and developed into the MiniMax-M1 model presented in this paper.

6.  **DeepSeek-AI et al. 2025. Deepseek-r1: Incentivizing reasoning capability in llms via reinforcement learning.**
    This paper presents DeepSeek-R1, a key state-of-the-art open-weight reasoning model that serves as a primary benchmark for comparison throughout MiniMax-M1's evaluation.

7.  **Yu et al. 2025. Dapo: An open-source llm reinforcement learning system at scale.**
    This paper introduced the DAPO algorithm, which serves as a main point of comparison for the paper's proposed CISPO algorithm to demonstrate CISPO's superior training efficiency.

8.  **Jimenez et al. 2024. SWE-bench: Can language models resolve real-world github issues?**
    This paper provides the SWE-bench benchmark, which is used to highlight MiniMax-M1's particular strength in complex, execution-based software engineering tasks.
    Link: `https://openreview.net/forum?id=VTF8yNQM66`

9.  **Liu et al. 2025a. Synlogic: Synthesizing verifiable reasoning data at scale for learning logical reasoning and beyond.**
    This work is cited as the framework used to programmatically synthesize a large corpus of the logical reasoning data required for the model's reinforcement learning phase.

10. **Qwen, et al. 2025. Qwen2.5 technical report.**
    This report describes the Qwen models that are used both as a primary SOTA competitor for benchmarking and as the base model for the crucial empirical validation comparing CISPO to DAPO and GRPO.
