https://arxiv.org/abs/2506.01300

https://x.com/AiYiyangZ/status/1932188308211474487

**ReAgent-V: A Reward-Driven Multi-Agent Framework for Video Understanding**

### 1. Summary and Rating

**Summary**

This paper introduces ReAgent-V, a novel multi-agent framework designed to enhance the reasoning and understanding capabilities of Large Vision-Language Models (LVLMs) for video tasks. The authors identify that existing LVLMs operate in a static, single-pass manner, which limits their ability to self-correct or adapt to complex scenarios. To address this, ReAgent-V employs a collaborative system of a "target agent" and a "critic agent." The framework's workflow involves three key stages. First, it uses a novel **Entropy-Calibrated Relevance Score (ECRS)** to efficiently select a small subset of video frames that are both semantically relevant to the query and information-rich. Second, the target agent, augmented with external tools, generates an initial answer. Third, the critic agent evaluates this answer, provides a real-time reward signal and structured feedback, and prompts a **multi-perspective reflection** from the target agent (revising the answer from conservative, neutral, and aggressive viewpoints). A key innovation is that these inference-time rewards are also used to automatically curate high-quality, challenging data samples for subsequent model improvement via methods like Direct Preference Optimization (DPO) and Group Relative Policy Optimization (GRPO), creating a self-improving loop. The authors demonstrate the effectiveness of ReAgent-V through extensive experiments on 12 datasets across video understanding, reasoning enhancement, and vision-language-action alignment, showing significant performance gains over strong baselines.

**Rating: 9/10**

This is an excellent and comprehensive paper. It presents a thoughtfully engineered system that cleverly integrates several state-of-the-art concepts—agentic architectures, reflection, tool use, and preference optimization—into a unified framework to address a clear and important limitation in video understanding. The contributions are both practical and impactful. The proposed ECRS for frame selection is an elegant and effective solution to an efficiency bottleneck. The multi-perspective reflection mechanism is a nuanced approach to iterative refinement. Most significantly, the framework's ability to use its own inference-time feedback to generate high-quality preference data for continuous self-improvement is a powerful paradigm. The experimental validation is exceptionally thorough, spanning multiple applications, diverse benchmarks, and detailed ablation studies, which strongly substantiates the authors' claims. The work represents a significant step forward in creating more dynamic, robust, and efficient video understanding systems.

### 2. Main Ideas

1.  **Agentic Reflection with Real-Time Rewards for Iterative Refinement:** The core of the framework is a dynamic, multi-agent reasoning process that moves beyond static, single-pass generation. A critic agent evaluates the initial answer from a target agent, providing immediate, inference-time rewards and structured feedback. This feedback guides a multi-perspective reflection process, where the target agent revises its answer by considering conservative, neutral, and aggressive strategies, ultimately leading to a more robust and accurate final output.

2.  **Efficient, Entropy-Calibrated Frame Selection (ECRS):** To tackle the high computational cost and redundancy of processing long videos, the paper introduces ECRS. This metric combines the semantic similarity between a frame and a query (using CLIP) with the frame's information entropy. This dual consideration allows the system to select a compact set of frames that are not only relevant but also visually rich, leading to improved efficiency and performance.

3.  **Closing the Loop via Reward-Guided Data Curation:** ReAgent-V uniquely leverages the rewards generated during inference to create a data-centric, self-improving cycle. The rewards act as an importance score, enabling the automatic filtering of challenging or informative video examples that required significant model reflection. This high-quality data is then used to fine-tune the model further using preference alignment techniques (like DPO and GRPO), effectively using the agent's own reasoning process to guide its future learning and alignment.

### 3. 10 Most Important Citations

1.  **Wang et al. (2024)**. Videoagent: Long-form video understanding with large language model as agent.
    This paper presents a key competing agentic framework that ReAgent-V compares against and differentiates from, particularly on the grounds of efficiency and real-time reward generation.

2.  **Rafailov et al. (2023)**. Direct preference optimization: Your language model is secretly a reward model.
    This paper introduces Direct Preference Optimization (DPO), a foundational alignment technique that ReAgent-V is designed to supply high-quality preference data for.

3.  **Shao et al. (2024)**. Deepseekmath: Pushing the limits of mathematical reasoning in open language models.
    This work introduces Group Relative Policy Optimization (GRPO), another critical preference alignment method that ReAgent-V uses to fine-tune models after filtering data with its reward signals.
    *   Link: `https://arxiv.org/abs/2402.03300`

4.  **Zhang et al. (2024)**. Video instruction tuning with synthetic data.
    This work introduced LLaVA-Video, which serves as a critical open-source baseline model that ReAgent-V is applied to and demonstrates significant performance enhancements upon.
    *   Link: `https://arxiv.org/abs/2410.02713`

5.  **Shinn et al. (2023)**. Reflexion: Language agents with verbal reinforcement learning.
    This paper’s "Reflexion" paradigm for agent self-correction through verbal feedback is a direct conceptual predecessor to the more structured multi-perspective reflection mechanism developed in ReAgent-V.

6.  **Fu et al. (2024)**. Video-mme: The first-ever comprehensive evaluation benchmark of multi-modal llms in video analysis.
    This is a primary evaluation benchmark used throughout the paper to quantitatively validate the performance improvements provided by the ReAgent-V framework.
    *   Link: `https://arxiv.org/abs/2405.21075`

7.  **Feng et al. (2025)**. Video-r1: Reinforcing video reasoning in mllms.
    The Video-R1-260k dataset from this paper is central to the experiments on video LLM reasoning, where ReAgent-V's ability to select valuable training samples is showcased.
    *   Link: `https://arxiv.org/abs/2503.21776`

8.  **Zhang et al. (2025)**. GRAPE: Generalizing robot policy via preference alignment.
    This work is foundational for the vision-language-action (VLA) alignment application, where ReAgent-V serves as a superior, learned reward model replacement to the template-based one in GRAPE.

9.  **Fan et al. (2024)**. Videoagent: A memory-augmented multimodal agent for video understanding.
    This paper (referred to as VideoMemAgent in tables) represents another significant agent-based video understanding framework that serves as a key point of comparison to demonstrate ReAgent-V's superior performance.

10. **Bai et al. (2025)**. Qwen2. 5-vl technical report.
    The powerful Qwen models serve as a primary base LVLM for experiments, making this technical report an essential reference for the architecture that ReAgent-V successfully enhances.
    *   Link: `https://arxiv.org/abs/2502.13923`
