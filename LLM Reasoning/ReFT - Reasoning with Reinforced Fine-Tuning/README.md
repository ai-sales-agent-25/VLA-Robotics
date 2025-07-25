https://arxiv.org/abs/2401.08967

REFT: Reasoning with Reinforced Fine-Tuning

1.  **Brief Summary and Rating:**

    The paper "REFT: Reasoning with Reinforced Fine-Tuning" introduces a novel two-stage fine-tuning method, ReFT, designed to enhance the reasoning capabilities and generalization of Large Language Models (LLMs), particularly for mathematical problem-solving. The authors identify a key limitation in standard Supervised Fine-Tuning (SFT) which typically relies on a single Chain-of-Thought (CoT) annotation per problem, potentially restricting the model's ability to generalize. ReFT addresses this by first "warming up" the model using SFT with the available CoT data. Subsequently, it employs on-line reinforcement learning (RL), specifically Proximal Policy Optimization (PPO), to encourage the model to sample and learn from a diverse set of plausible reasoning paths for the same questions. Crucially, the reward signal for the RL stage is derived directly from the correctness of the final answer based on ground-truth, eliminating the need for a separately trained reward model or additional human annotations.

    Experiments conducted on standard mathematical reasoning datasets (GSM8K, MathQA, SVAMP) using both natural language CoTs (N-CoT) and program-based CoTs (P-CoT) demonstrate that ReFT significantly outperforms SFT. This improvement in generalization is achieved using the same training questions as SFT, without relying on extra or augmented training data. The paper also shows that ReFT's performance can be further enhanced by integrating inference-time strategies such as majority voting and re-ranking.

    **Rating: 8.5/10**

    For a PhD-level audience, this paper presents a solid and well-executed piece of research. The core idea of using RL to explore multiple reasoning paths beyond the single provided annotation is intuitive and addresses a genuine limitation of SFT for reasoning tasks. The two-stage approach (SFT warm-up + PPO) is methodologically sound, and the ability to leverage ground-truth answers for rewards is a practical advantage. The empirical validation is comprehensive, covering multiple datasets, model architectures (Galactica, CodeLLAMA), and CoT types, along with insightful ablation studies (e.g., impact of KL penalty, partial rewards) and analysis (e.g., reward hacking on MCQ datasets, generalization over training epochs). The reported performance gains are significant and practically relevant. While PPO is a standard RL algorithm, its specific application here to "enrich" the learning signals from existing data for better generalization is a valuable contribution. The paper is clearly written and the results are compelling. It might not introduce a completely new theoretical paradigm in RL or LLMs, but it offers a refined and effective technique for improving a critical LLM capability.

2.  **Main Ideas Discussed:**

    1.  **Limitation of Single-Path SFT for Reasoning:** A primary idea is that conventional Supervised Fine-Tuning (SFT) of LLMs using Chain-of-Thought (CoT) annotations is suboptimal for generalization because it typically trains the model on only one correct reasoning path per question, even when multiple valid paths might exist. This limits the diversity of reasoning strategies the model learns.
    2.  **Reinforced Fine-Tuning (ReFT) for Diverse Path Exploration:** The core proposal is ReFT, a two-stage fine-tuning approach. It first warms up the LLM with SFT and then uses online reinforcement learning (PPO) to allow the model to actively sample multiple, potentially novel, reasoning paths for each training question. The model is rewarded based on the correctness of the final answer derived from these sampled paths, encouraging exploration and learning from a richer set of successful (and implicitly, unsuccessful) reasoning strategies.
    3.  **Improved Generalization without Additional Labeled Data:** ReFT demonstrates enhanced generalization and performance on mathematical reasoning tasks compared to SFT, notably by learning from the *same set of training questions* without requiring extra manually annotated CoTs or augmented data. This suggests a more efficient utilization of available data by encouraging the model to discover and internalize a broader range of valid problem-solving approaches.

3.  **List of 10 Most Important Citations:**

    1.  **Wei et al. 2022. Chain-of-thought prompting elicits reasoning in large language models.**
        This foundational work introduced Chain-of-Thought (CoT) prompting, which forms the basis of the reasoning annotations that ReFT aims to learn from more effectively by exploring multiple such paths.
    2.  **Schulman et al. 2017. Proximal policy optimization algorithms. [https://arxiv.org/abs/1707.06347](https://arxiv.org/abs/1707.06347)**
        This paper introduced Proximal Policy Optimization (PPO), the specific reinforcement learning algorithm adopted by ReFT in its second stage to fine-tune the model by sampling and learning from diverse reasoning paths.
    3.  **Cobbe et al. 2021a. Training verifiers to solve math word problems. [https://arxiv.org/abs/2110.14168](https://arxiv.org/abs/2110.14168)**
        This work introduced the GSM8K dataset, a key benchmark for mathematical reasoning extensively used in ReFT's experiments, and also explored training verifiers, which relates to evaluating the correctness of reasoning.
    4.  **Ouyang et al. 2022. Training language models to follow instructions with human feedback.**
        This influential paper details Reinforcement Learning from Human Feedback (RLHF), a major paradigm for aligning LLMs; ReFT applies RL in a related spirit but uses automated rewards from ground-truth answers, contrasting with the human-labeled rewards or learned reward models typical in RLHF.
    5.  **Gao et al. 2023. PAL: Program-aided language models.**
        This paper proposed program-based CoTs (referred to as P-CoT in ReFT), which ReFT demonstrates its effectiveness on, highlighting the versatility of the ReFT method across different reasoning formalisms.
    6.  **Sutton et al. 2018. Reinforcement learning: An introduction.**
        This is a fundamental textbook in reinforcement learning, providing the theoretical underpinnings for the RL techniques, including PPO, that are central to ReFT's methodology.
    7.  **Ziegler et al. 2019. Fine-tuning language models from human preferences. [https://arxiv.org/abs/1909.08593](https://arxiv.org/abs/1909.08593)**
        This research is an important early example of using PPO to fine-tune language models based on preferences, providing a precedent for ReFT's approach of using RL for LLM refinement, albeit with a different reward source.
    8.  **Uesato et al. 2022. Solving math word problems with process-and outcome-based feedback. [https://arxiv.org/abs/2211.14275](https://arxiv.org/abs/2211.14275)**
        This paper explores outcome-based reward models and reranking for math problems, and ReFT demonstrates that its performance can be further boosted by integrating such inference-time techniques.
    9.  **Wang et al. 2023a. Mathcoder: Seamless code integration in llms for enhanced mathematical reasoning. [https://arxiv.org/abs/2310.03731](https://arxiv.org/abs/2310.03731)**
        Cited as a state-of-the-art approach for math problem solving using SFT with high-quality program-based CoTs, providing a relevant point of comparison for ReFT's achievements.
    10. **Luo et al. 2023. Wizardmath: Empowering mathematical reasoning for large language models via reinforced evol-instruct. [https://arxiv.org/abs/2308.09583](https://arxiv.org/abs/2308.09583)**
        This work presents another strong contemporary method for improving mathematical reasoning in LLMs through SFT on augmented data, highlighting the context in which ReFT achieves its gains without such external data augmentation.
