https://huggingface.co/papers/2505.20561

**Paper:** Beyond Markovian: Reflective Exploration via Bayes-Adaptive RL for LLM Reasoning

**1. Summary and Rating:**

This paper addresses the limitations of conventional Markovian Reinforcement Learning (RL) in explaining or guaranteeing the emergence of reflective reasoning (e.g., backtracking, error correction) in Large Language Models (LLMs), particularly at test time. The authors argue that Markovian RL confines exploration to the training phase to learn a deterministic policy and relies only on the current state, offering no incentives for adaptive, history-dependent exploration during inference. To overcome this, they propose recasting reflective exploration within the Bayes-Adaptive RL framework. This framework explicitly optimizes for test-time generalization by maximizing expected return under a posterior distribution over Markov Decision Processes (MDPs), thereby incentivizing both reward-maximizing exploitation and information-gathering exploration (i.e., reflection to reduce MDP uncertainty).

The authors introduce a novel algorithm, Bayes-Adaptive RL for LLM Reasoning (BARL), which guides the LLM to stitch and switch between reasoning strategies based on observed outcomes by maintaining and updating beliefs over MDP hypotheses. BARL performs online rollouts, computes state-action values weighted by current beliefs, and penalizes mismatches between predicted and observed rewards to signal strategy switches. Empirical results on synthetic tasks and mathematical reasoning benchmarks (GSM8K, MATH, CollegeMath, OlympiadBench) using various LLMs demonstrate that BARL outperforms standard Markovian RL approaches in test-time performance and token efficiency. The paper also provides a theoretical argument (Theorem 4.2) showing that a Bayes-Adaptive policy can achieve exponentially higher expected return than an optimal Markovian policy in scenarios requiring adaptation.

**Rating: 9/10**

This paper offers a sophisticated and principled approach to a significant problem in LLM reasoning. Grounding reflective exploration in Bayes-Adaptive RL provides a strong theoretical foundation for why and how LLMs might benefit from such behaviors, moving beyond mere empirical observation. The BARL algorithm is a novel contribution that operationalizes this framework. The comprehensive experiments, including a didactic synthetic example and evaluations on challenging math reasoning tasks, effectively demonstrate the advantages of BARL. The paper clearly articulates the limitations of existing methods and the contribution of its proposed approach. The connection made between belief updates over MDPs and the "Aha moment" or reflective reasoning is insightful. The work is theoretically sound and empirically well-supported, making a strong case for moving "Beyond Markovian" approaches for complex LLM reasoning.

**2. Main Ideas Discussed:**

1.  **Limitations of Markovian RL for Reflective LLM Reasoning:** The paper argues that conventional Markovian RL is insufficient for fostering or explaining emergent reflective behaviors in LLMs at test time. This is because: (a) exploration is typically limited to the training phase to learn an optimal deterministic policy, which is then purely exploited at test time, and (b) the Markov assumption restricts policies to depend only on the current state, not the broader history of interactions (including rewards and belief updates about the task's nature) that would incentivize adaptive exploration or reflection. Thus, Markovian RL doesn't guarantee that reflective strategies will emerge or be beneficial during inference.
2.  **Bayes-Adaptive RL as a Framework for Reflective Exploration:** The core proposal is to use Bayes-Adaptive RL (BAMDPs) to model reflective reasoning. This framework explicitly optimizes for test-time generalization by maintaining a posterior distribution over possible MDPs. This naturally incentivizes "epistemic exploration"—actions taken to gather information and reduce uncertainty about the true underlying MDP—alongside reward-seeking exploitation. Reflective steps (like backtracking or trying alternative paths) are framed as such epistemic actions that update the LLM's belief about the best reasoning strategy.
3.  **The BARL Algorithm for Principled Reflective Reasoning:** The paper introduces BARL (Bayes-Adaptive RL for LLM Reasoning), an algorithm that operationalizes the Bayes-Adaptive framework. BARL allows the LLM to generate multiple candidate reasoning traces (hypotheses about the MDP), weights their values based on current beliefs, and updates these beliefs based on observed rewards. Discrepancies between predicted and observed rewards signal the need for strategy switching (reflection) by downweighting hypotheses that are inconsistent with evidence. This provides a principled mechanism for deciding when and how to reflect, rather than relying on ad-hoc heuristics.

**3. 10 Most Important Citations:**

1.  **Wei et al. 2022.** Chain-of-thought prompting elicits reasoning in large language models.
    *   This paper introduced Chain-of-Thought (CoT) reasoning, a foundational concept for the intermediate deliberation steps in LLMs that the current paper aims to enhance and make more reflective. (Cited as [50])
2.  **Guo et al. 2025.** Deepseek-rl: Incentivizing reasoning capability in llms via reinforcement learning.
    *   This work demonstrates emergent deliberative reasoning abilities like self-reflection ("Aha moment") in RL-trained LLMs and is a key example of the phenomena the current paper seeks to explain and improve upon; DeepSeek-R1 is also one of the models used in experiments. (Cited as [17])
3.  **Bellman et al. 1959.** On adaptive control processes. IRE Transactions on Automatic Control.
    *   This is a foundational, early citation for Bayes-Adaptive MDPs (BAMDPs), the core theoretical framework adopted by the paper to model reflective exploration. (Cited as [4])
4.  **Duff, M. O. 2002.** Optimal Learning: Computational procedures for Bayes-adaptive Markov decision processes.
    *   This PhD thesis provides a comprehensive treatment of BAMDPs, which are central to the paper's proposed approach for enabling adaptive, reflective reasoning. (Cited as [11])
5.  **Ghavamzadeh et al. 2015.** Bayesian reinforcement learning: A survey. Foundations and Trends® in Machine Learning.
    *   This survey provides a broad overview of Bayesian RL, the field within which the paper's Bayes-Adaptive RL approach is situated, contextualizing the use of belief distributions over MDPs. (Cited as [13])
6.  **Qu et al. 2025.** Optimizing test-time compute via meta reinforcement fine-tuning.
    *   This related work also studies LLM generalization and uses progress rewards; the current paper compares its BARL approach, particularly in how it additionally encourages exploring plausible strategies under a Bayesian framework. (Cited as [37])
7.  **Lidayan et al. 2024.** Bamdp shaping: a unified framework for intrinsic motivation and reward shaping. In The Thirteenth International Conference on Learning Representations.
    *   This recent work on BAMDPs is cited in the paper's problem formulation when defining Bayes-Adaptive RL, indicating its relevance to the theoretical underpinnings of the proposed method. (Cited as [28])
8.  **Cobbe et al. 2021.** Training verifiers to solve math word problems. arXiv preprint arXiv:2110.14168.
    *   This paper introduced the GSM8K dataset, one of the key benchmarks used to evaluate BARL's performance on mathematical reasoning tasks. (Cited as [7]) (Link: https://arxiv.org/abs/2110.14168)
9.  **Hendrycks et al. 2021.** Measuring mathematical problem solving with the math dataset. arXiv preprint arXiv:2103.03874.
    *   This paper introduced the MATH dataset, another important benchmark used for evaluating BARL's mathematical reasoning capabilities. (Cited as [21]) (Link: https://arxiv.org/abs/2103.03874)
10. **Xiang et al. 2025.** Towards system 2 reasoning in llms: Learning how to think with meta chain-of-though.
    *   This paper is discussed as related work that studies LLM generalization from a meta-RL perspective, justifying deliberative reasoning, and provides a contrasting approach to the BARL framework. (Cited as [52])
