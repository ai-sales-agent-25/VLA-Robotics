https://arxiv.org/abs/2504.05812

**Right Question is Already Half the Answer: Fully Unsupervised LLM Reasoning Incentivization**

**1. Summary and Rating**

This paper introduces Entropy Minimized Policy Optimization (EMPO), a novel reinforcement learning (RL) method designed to enhance the reasoning capabilities of Large Language Models (LLMs) in a fully unsupervised manner. Unlike existing approaches that predominantly rely on supervised fine-tuning (SFT) or RL with external supervisory signals (e.g., labeled reasoning traces, verified answers, pre-trained reward models), EMPO operates without any such supervision. The core idea is to minimize the predictive semantic entropy of an LLM's outputs for unlabeled questions. EMPO samples multiple responses from the policy model, clusters them based on semantic equivalence (meaning), and then assigns higher rewards to responses belonging to more probable (i.e., more consistent) semantic clusters. This incentivizes the model to produce more consistent and, by extension, more reliable reasoning traces. To mitigate potential reward hacking and stabilize training, EMPO incorporates an entropy thresholding mechanism. The authors demonstrate EMPO's effectiveness on both mathematical and free-form natural reasoning tasks, showing significant improvements over base models (e.g., Qwen2.5-Math-7B accuracy boosted from 30.7% to 48.1% on math benchmarks, and Qwen2.5-7B Base accuracy improved from 32.1% to 50.1% on MMLU-Pro). The paper argues that EMPO, like other RL-based post-training methods, primarily serves to elicit and refine reasoning pathways already learned during pre-training rather than instilling fundamentally new reasoning skills.

**Rating: 8.5/10**

**Justification:** This paper addresses a critical challenge in LLM development: the heavy reliance on supervised data for improving reasoning. The proposed EMPO method offers a principled and fully unsupervised approach, which is a significant contribution. The concept of using semantic entropy minimization as an intrinsic reward signal is innovative and well-motivated. The empirical results are compelling, demonstrating competitive performance with supervised methods on strong base models. The discussion on eliciting pre-trained capabilities, supported by pass@k analysis, provides valuable insight into the mechanisms of RL in LLMs. The methodology is clearly explained. The potential for scalability and cost reduction makes this work highly relevant. Minor points for deeper investigation could include the robustness and generalizability of the semantic clustering mechanism (especially the reliance on a small verifier model for natural reasoning) across diverse tasks and model architectures, and further exploration of the interplay between pre-training quality and the effectiveness of unsupervised elicitation. Overall, it's a strong paper with novel ideas and solid execution.

**2. Main Ideas**

1.  **Fully Unsupervised Reasoning Incentivization via Semantic Entropy Minimization:** The central idea is EMPO, a reinforcement learning algorithm that enhances LLM reasoning without any external labels. It achieves this by rewarding the LLM for generating semantically consistent answers to unlabeled questions, effectively minimizing the semantic entropy of its output distributions.
2.  **Eliciting and Refining Pre-Trained Capabilities:** The paper posits that methods like EMPO do not primarily teach LLMs new reasoning skills from scratch. Instead, they improve the model's ability to efficiently access, prioritize, and consistently select strong, pre-existing reasoning pathways learned during its initial large-scale pre-training. This is supported by pass@k analysis showing that while pass@1 (accuracy) improves significantly, the performance gap between base and RL-trained models narrows or closes at higher k values.
3.  **Practical Unsupervised RL with Reward Hacking Mitigation:** EMPO operationalizes unsupervised RL by sampling multiple outputs, performing semantic clustering to define "meanings," and then using the probability of these meaning clusters as reward signals. To prevent the model from exploiting this unsupervised objective (e.g., by overconfidently producing frequent but incorrect answers), it employs an entropy thresholding strategy, filtering out prompts that lead to overly high or overly low entropy responses during training.

**3. 10 Most Important Citations**

1.  **Schulman et al. 2017.** Proximal policy optimization algorithms. (arXiv:1707.06347)
    *   This paper introduces PPO, a foundational reinforcement learning algorithm that is widely used for training LLMs, and EMPO's optimization objective structure is related to such policy gradient methods.
2.  **Shao et al. 2024.** Deepseekmath: Pushing the limits of mathematical reasoning in open language models. (arXiv:2402.03300)
    *   This work presents DeepSeekMath which utilizes Group Relative Policy Optimization (GRPO), a supervised RL method that EMPO is compared against, highlighting the performance of EMPO in a fully unsupervised setting.
3.  **Guo et al. 2025.** Deepseek-r1: Incentivizing reasoning capability in llms via reinforcement learning. (arXiv:2501.12948)
    *   DeepSeek-R1-Zero, discussed in this paper, demonstrates robust reasoning by initiating RL directly from a base model (though still using rule-based/verified rewards), inspiring EMPO's exploration of fully unsupervised approaches.
4.  **Kuhn et al. 2023.** Semantic uncertainty: Linguistic invariances for uncertainty estimation in natural language generation. (arXiv:2302.09664)
    *   This paper introduces the concept of "semantic entropy" which EMPO directly leverages as its core unsupervised optimization objective and reward signal.
5.  **Grandvalet et al. 2004.** Semi-supervised learning by entropy minimization. (Advances in neural information processing systems, 17)
    *   This is a foundational work demonstrating the principle of entropy minimization for improving model confidence and classification accuracy on unlabeled data, which underpins EMPO's objective.
6.  **Huang et al. 2022.** Large language models can self-improve. (arXiv:2210.11610)
    *   This paper explores self-improvement frameworks where LLMs generate pseudo-labels for fine-tuning, representing a form of self-supervision that EMPO contrasts with its fully unsupervised RL approach.
7.  **Jiao et al. 2024.** Preference optimization for reasoning with pseudo feedback. (arXiv:2411.16345)
    *   This paper (PFPO) presents another approach to reasoning optimization using pseudo-feedback but still relies on some form of supervision or frontier LLM signals for initialization, which EMPO aims to remove entirely.
8.  **Wang et al. 2020.** Tent: Fully test-time adaptation by entropy minimization. (arXiv:2006.10726)
    *   TENT uses entropy minimization for test-time adaptation, showing the utility of this principle in adapting models without labels, a concept related to EMPO's unsupervised training objective.
9.  **Wu et al. 2024.** Reft: Representation finetuning for language models. (Advances in Neural Information Processing Systems, 37:63908–63962)
    *   This paper is cited to support the argument that pre-training endows LLMs with their core abilities, and fine-tuning (including RL-based methods like EMPO) primarily refines or "positions" the model to better utilize these existing capabilities.
10. **Yue et al. 2025.** Does reinforcement learning really incentivize reasoning capacity in llms beyond the base model? (arXiv:2504.13837)
    *   This recent work is cited to support EMPO's finding that RL's main benefit might be in enhancing sampling efficiency (pass@k for small k) rather than fundamentally expanding the LLM's inherent reasoning capacity beyond what's learned in pre-training.
