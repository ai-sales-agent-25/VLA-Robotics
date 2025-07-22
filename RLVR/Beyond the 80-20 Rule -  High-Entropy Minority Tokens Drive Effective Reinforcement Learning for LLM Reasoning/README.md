https://huggingface.co/papers/2506.01939

Beyond the 80/20 Rule: High-Entropy Minority Tokens Drive Effective Reinforcement Learning for LLM Reasoning

1.  **Brief Summary and Rating:**
    This paper investigates the mechanisms of Reinforcement Learning with Verifiable Rewards (RLVR) for enhancing LLM reasoning, focusing on token entropy patterns. The authors observe that in Chain-of-Thought (CoT) reasoning, a small fraction of tokens ("forking tokens") exhibit high entropy and are critical for guiding reasoning paths, while the majority are low-entropy. Their analysis reveals that RLVR training largely preserves the base model's entropy patterns but primarily modifies the entropy of these high-entropy tokens. Building on this, they demonstrate that restricting policy gradient updates in RLVR (specifically using DAPO) to only the top 20% highest-entropy tokens achieves performance comparable to, or even significantly surpassing, full-gradient updates, especially on larger models (e.g., Qwen3-32B). Conversely, training on low-entropy tokens degrades performance. This "beyond 80/20" finding suggests that the efficacy of RLVR stems mainly from optimizing these critical high-entropy minority tokens, offering a more efficient training strategy and deeper insights into LLM reasoning and generalization.

    **Rating: 9/10**
    This paper presents a novel and insightful analysis of RLVR through the lens of token entropy, leading to a practical and effective modification of the training process. The core finding—that high-entropy minority tokens are the primary drivers of RLVR efficacy—is well-supported by comprehensive experiments across different model sizes, including SOTA results on reasoning benchmarks and out-of-distribution generalization. The work provides a compelling explanation for its observations and connects them to broader discussions on RL generalization versus SFT memorization, and the nature of exploration in LLMs. The "beyond 80/20" claim is impactful and the methodology is sound. While the experiments are predominantly on the Qwen family and math reasoning, the clarity of the findings and their potential implications for understanding and optimizing RL for LLMs make this a strong contribution.

2.  **Main Ideas Discussed:**

    1.  **Identification and Role of High-Entropy "Forking Tokens":** The paper identifies that in LLM Chain-of-Thought reasoning, token generation entropy is highly skewed. A small minority of tokens exhibit high entropy; these "forking tokens" act as critical decision points that steer the model toward diverse reasoning pathways. The majority of tokens have low entropy and typically complete established linguistic or logical structures. Maintaining or even increasing the entropy of these forking tokens is shown to be beneficial for reasoning performance.
    2.  **Selective RLVR Training on High-Entropy Tokens:** The core experimental finding is that RLVR's effectiveness is primarily driven by updates to these high-entropy minority tokens. By restricting policy gradient updates (using the DAPO algorithm) to only the top ~20% of highest-entropy tokens, the models achieve comparable or significantly better reasoning performance than training on all tokens, particularly for larger models. This suggests that much of the gradient computation on low-entropy tokens is inefficient or potentially even detrimental. This selective training also shows positive scaling trends with model size and improved generalization.
    3.  **RLVR Mechanisms and Implications:** The paper posits that RLVR preserves the base model's overall entropy patterns but specifically adjusts the entropy of high-entropy tokens. This targeted adjustment, focusing on "forking tokens," may explain why RL can generalize better than supervised fine-tuning (SFT) by maintaining reasoning path flexibility. It also suggests why techniques like "clip-higher" in DAPO are effective, as they implicitly prioritize updates on tokens with higher importance (which the paper links to higher entropy), contrasting with uniform entropy bonuses that might negatively affect low-entropy, high-certainty tokens.

3.  **10 Most Important Citations:**

    1.  **Yu et al. 2025** Dapo: An open-source llm reinforcement learning system at scale. arXiv preprint arXiv:2503.14476.
        *   This is the paper introducing DAPO, the primary RLVR algorithm used as a baseline and modified in the current work to demonstrate the effectiveness of training on forking tokens.
        *   Link: Not explicitly given in the text, but the paper refers to `Yu et al., 2025`. (Assuming the arXiv link from page 19)

    2.  **Yang et al. 2025** Qwen3 technical report. arXiv preprint arXiv:2505.09388.
        *   This paper details the Qwen3 models, which are the primary base models used for experiments in the current work to demonstrate the impact of forking tokens.
        *   Link: Not explicitly given in the text, but the paper refers to `Yang et al., 2025`. (Assuming the arXiv link from page 19)

    3.  **Schulman et al. 2017** Proximal policy optimization algorithms. arXiv preprint arXiv:1707.06347.
        *   Introduces PPO, a foundational policy gradient algorithm widely adopted in RLVR and mentioned as a precursor/component in the development of more advanced RLVR algorithms.
        *   Link: Not explicitly given in the text, but the paper refers to `Schulman et al., 2017`. (Assuming the arXiv link from page 18)

    4.  **Lambert et al. 2025** Tulu 3: Pushing frontiers in open language model post-training. arXiv preprint arXiv:2411.15124. (Note: The paper text often cites Lambert et al. 2025 in relation to RLVR generally, the Tulu 3 paper discusses their open model. The first mention of "RLVR (Lambert et al., 2025)" in the introduction may refer to a more general concept or an earlier work not explicitly listed in the refs, but Tulu 3 is a recent relevant work by Lambert on models involving RL.)
        *   Cited as a key work in RLVR, highlighting its emergence as a powerful technique for enhancing LLM reasoning, setting the context for this paper's investigation.
        *   Link: Not explicitly given in the text, but the paper refers to `Lambert et al., 2025`. (Assuming the arXiv link from page 18)

    5.  **DeepSeek-AI et al. 2025** Deepseek-r1: Incentivizing reasoning capability in llms via reinforcement learning. arXiv preprint arXiv:2501.12948.
        *   Cited as a pivotal work demonstrating that RLVR can significantly improve reasoning in LLMs, including the introduction of "zero RL."
        *   Link: Not explicitly given in the text, but the paper refers to `DeepSeek-AI et al., 2025`. (Assuming the arXiv link from page 16)

    6.  **Shao et al. 2024** Deepseekmath: Pushing the limits of mathematical reasoning in open language models. arXiv preprint arXiv:2402.03300. (Note: Shao et al. 2024 is also cited for GRPO within the DAPO discussion. DeepSeekMath is about reasoning models, GRPO is an RL algorithm. The paper cites GRPO (Shao et al., 2024) in Sec 2.2 & 7. The citation given in references under Shao et al. 2024 is DeepSeekMath. There might be another Shao et al. paper for GRPO or GRPO's first author is Shao, and it's part of the DeepSeek work.)
        *   GRPO (Group Relative Policy Optimization) is an important value-network-free RL algorithm that forms a basis for DAPO, making its foundational concepts relevant to the methods used.
        *   Link: Not explicitly given in the text, but the paper refers to `Shao et al., 2024`. (Assuming the arXiv link from page 18)

    7.  **Chu et al. 2025** Sft memorizes, rl generalizes: A comparative study of foundation model post-training. arXiv preprint arXiv:2501.17161.
        *   This paper is cited in Discussion 1 for its empirical demonstration that RL exhibits stronger generalization than SFT, a key point the current paper's findings on forking token entropy aim to help explain.
        *   Link: Not explicitly given in the text, but the paper refers to `Chu et al., 2025`. (Assuming the arXiv link from page 16)

    8.  **Ouyang et al. 2022** Training language models to follow instructions with human feedback. Advances in neural information processing systems, 35:27730–27744.
        *   This is a foundational paper on RLHF, which established the general methodology of using RL to align LLMs, providing essential background for the subsequent development of RLVR.
        *   Link: Not explicitly given in the text, but the paper refers to `Ouyang et al., 2022`. (Assuming the NIPS link from page 18)

    9.  **Williams 1992** Simple statistical gradient-following algorithms for connectionist reinforcement learning. Machine learning.
        *   Introduces REINFORCE, a fundamental policy gradient algorithm. It's relevant context for understanding online RL methods and the discussion of entropy bonuses in RL.
        *   Link: Not explicitly given in the text, but the paper refers to `Williams, 1992`. (Assuming the Machine Learning journal link from page 19)

    10. **OpenAI 2024** Learning to Reason with LLMs. https://openai.com/index/learning-to-reason-with-1lms/.
        *   Cited as the first to demonstrate that RL can effectively incentivize reasoning capabilities in LLMs at scale, setting the stage for subsequent RLVR research.
        *   Link: `https://openai.com/index/learning-to-reason-with-1lms/` (Given in paper on page 18)
