https://ozyyshr.github.io/RAST/

RAST: Reasoning Activation in LLMs via Small-model Transfer

**1. Summary and Rating**

This paper introduces RAST (Reasoning Activation via Small-model Transfer), a novel and computationally efficient decoding-time method to enhance the reasoning capabilities of large language models (LLMs). The central hypothesis is that reinforcement learning (RL) primarily improves LLM reasoning not by imparting new knowledge, but by selectively modulating the output probabilities of a small subset of key tokens crucial for reasoning behaviors (e.g., branching out, backtracking, self-verification). The authors propose that these RL-induced probability shifts are largely invariant to model size.

RAST operationalizes this by first training a relatively small LLM with RL. Then, it computes the logit differences (ΔR) between this small RL-tuned model (SRL) and its corresponding base model (Sbase) for each token. During inference with a much larger base LLM (Mbase), these ΔR values (derived from the SRL/Sbase pair) are added to Mbase's logits before the softmax layer. This "injects" the learned reasoning patterns from the small RL model into the large base model without requiring expensive direct RL fine-tuning on the large model.

Comprehensive experiments across various mathematical reasoning (MATH500, GSM8K, AIME, etc.) and code generation benchmarks demonstrate that RAST substantially improves the performance of large base models. In many cases, RAST-enhanced models approach or even surpass the performance of their counterparts fully fine-tuned with RL, while using significantly less GPU memory and computational resources. The paper further validates its hypothesis through analyses like Path Coverage Rate (PCR), showing high alignment between base and RL-tuned model outputs, and explores RAST's impact on reasoning diversity (pass@k) and token-level behavioral shifts.

**Rating: 8.5/10**
This paper presents a clever and pragmatic solution to a significant problem in LLM development: the high cost of RL-based reasoning enhancement for large models. The core hypothesis regarding the nature of RL's impact—activating latent skills via localized, transferable probability shifts—is insightful and well-motivated by recent literature. The RAST method is elegant in its simplicity and demonstrates strong empirical results across diverse benchmarks and model scales. The efficiency gains are substantial. For a PhD-level audience, the work is commendable for its novel transfer mechanism, rigorous experimental validation, and thoughtful analyses. While a deeper theoretical underpinning of "model-size invariance" and the nature of "reasoning tokens" could be further explored, the practical impact and the clarity with which the research is presented make it a strong contribution.

**2. Main Ideas Discussed**

1.  **RL Activates Latent Reasoning via Localized Probability Shifts:** The primary thesis is that RL fine-tuning enhances LLM reasoning not by fundamentally adding new knowledge, but by "activating" latent capabilities already present in the base model. This activation occurs through selective adjustments to the output probabilities of a small subset of tokens critical for reasoning processes (like self-verification, branching, or backtracking). The paper hypothesizes these RL-induced probabilistic shifts are largely model-size invariant.
2.  **RAST: Small-model Transfer of Reasoning Patterns:** Building on the first idea, the paper proposes RAST, a decoding-time method to transfer these learned reasoning adjustments. It involves training a small model with RL, calculating the difference in logits (ΔR) between this RL-tuned small model and its base version, and then injecting these ΔR values into the logits of a larger base model during inference. This allows the larger model to benefit from RL-induced reasoning behaviors without undergoing costly RL training itself.
3.  **Efficient and Effective Reasoning Enhancement:** RAST is shown to substantially and consistently improve the reasoning capabilities of base LLMs across various mathematical and coding benchmarks. Notably, this enhancement often allows the base models to approach or even exceed the performance of larger, fully RL-trained models, but with significantly lower GPU memory requirements and computational overhead, highlighting RAST as a practical and scalable approach.

**3. 10 Most Important Citations**

1.  **Guo et al. 2025.** Deepseek-r1: Incentivizing reasoning capability in llms via reinforcement learning. arXiv preprint arXiv:2501.12948.
    *   This citation is important as Deepseek-R1 represents a state-of-the-art model demonstrating the power of RL for reasoning and introduces the "zero-RL" paradigm (applying RL directly to base LLMs), which RAST aims to make more efficient for very large models. (Link: `https://arxiv.org/abs/2501.12948`)
2.  **Yue et al. 2025.** Does reinforcement learning really incentivize reasoning capacity in llms beyond the base model? arXiv preprint arXiv:2504.13837.
    *   This work directly investigates the paper's core hypothesis by questioning whether RL adds new knowledge or primarily activates latent capabilities, providing context for RAST's premise. (Link: `https://arxiv.org/abs/2504.13837`)
3.  **Lin et al. 2024.** The unlocking spell on base llms: Rethinking alignment via in-context learning. In The Twelfth International Conference on Learning Representations, ICLR 2024, Vienna, Austria, May 7-11, 2024. OpenReview.net.
    *   This paper is cited as a key inspiration for RAST's hypothesis that RL activates latent reasoning capabilities already present in base models. (Link: `https://openreview.net/forum?id=xM6fS7cHWB` - actual link for ICLR 2024)
4.  **Li et al. 2023.** Contrastive decoding: Open-ended text generation as optimization. In Proceedings of the 61st Annual Meeting of the Association for Computational Linguistics (Volume 1: Long Papers).
    *   This citation is relevant as contrastive decoding involves manipulating logits from multiple models (e.g., expert and amateur) for improved generation, a concept related to RAST's use of logit differences from a small expert.
5.  **Zeng et al. 2025.** Simplerl-zoo: Investigating and taming zero reinforcement learning for open base models in the wild. arXiv preprint arXiv:2503.18892.
    *   This is crucial as SimpleRL-Zoo provides the specific RL-trained small models and the "RL from scratch" methodology that RAST leverages as the source of the transferable reasoning signals (ΔR). (Link: `https://arxiv.org/abs/2503.18892`)
6.  **Hendrycks et al. 2021.** Measuring mathematical problem solving with the MATH dataset. In Thirty-fifth Conference on Neural Information Processing Systems Datasets and Benchmarks Track (Round 2).
    *   The MATH dataset is a primary benchmark used extensively in the paper to evaluate and demonstrate the effectiveness of RAST in enhancing mathematical reasoning.
7.  **Schulman et al. 2017.** Proximal policy optimization algorithms. arXiv preprint arXiv:1707.06347.
    *   PPO is a foundational RL algorithm commonly used for fine-tuning LLMs, including the small expert models from which RAST derives its reasoning signals. (Link: `https://arxiv.org/abs/1707.06347`)
8.  **Jaech et al. 2024.** Openai o1 system card. arXiv preprint arXiv:2412.16720.
    *   Represents a prominent example of a highly capable reasoning model improved by RL, underscoring the motivation for developing more efficient methods like RAST to achieve similar gains. (Link: `https://arxiv.org/abs/2412.16720`)
9.  **Liu et al. 2021.** DExperts: Decoding-time controlled text generation with experts and anti-experts. In Proceedings of the 59th Annual Meeting of the Association for Computational Linguistics and the 11th International Joint Conference on Natural Language Processing (Volume 1: Long Papers).
    *   This work on DExperts, which uses logit differences between expert and anti-expert models for controlled generation, is conceptually similar to RAST's approach of using differential signals from a smaller expert.
10. **Zhao et al. 2025.** Echo chamber: Rl post-training amplifies behaviors learned in pretraining. arXiv preprint arXiv:2504.07912.
    *   This study supports RAST's underlying premise by suggesting that RL post-training primarily amplifies behaviors already learned during pretraining, rather than teaching entirely new skills. (Link: `https://arxiv.org/abs/2504.07912`)
