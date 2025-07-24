https://arxiv.org/abs/2505.07903

**SEM: REINFORCEMENT LEARNING FOR SEARCH-EFFICIENT LARGE LANGUAGE MODELS**

**1. Summary and Rating**

This paper introduces SEM (Search-Efficient large language Models), a novel post-training reinforcement learning (RL) framework designed to teach Large Language Models (LLMs) to judiciously use external search tools. The core problem addressed is the tendency of LLMs, even those trained with RL, to perform redundant or unnecessary searches, leading to inefficiency. SEM tackles this by training LLMs on a balanced dataset constructed from Musique (questions requiring external search) and MMLU (questions typically answerable from internal knowledge). This allows the model to learn to distinguish when a search is genuinely needed. The framework employs a structured reasoning template (involving `<think>`, `<answer>`, `<search>`, `<result>` tags) and utilizes Group Relative Policy Optimization (GRPO) for fine-tuning. The reward function is designed to incentivize accurate answers while penalizing unnecessary search invocations if the model can answer correctly from its internal knowledge, and rewarding effective search use when external information is required. Experimental results on benchmarks like HotpotQA, MuSiQue, MMLU, and GSM8K demonstrate that SEM significantly reduces redundant search operations while maintaining or improving answer accuracy compared to baselines like Naive RAG and ReSearch. The paper showcases SEM's ability to enhance both the efficiency and reasoning capabilities of LLMs in leveraging external knowledge.

**Rating: 8.5/10**

For a PhD-level audience, this paper presents a well-motivated and thoughtfully designed solution to a pertinent problem in LLM tool-use. The novelty lies in the specific combination of a balanced "known/unknown" dataset strategy, the structured reasoning template for RL, and the application of GRPO with a carefully crafted reward function to optimize search decisions. The experimental validation is reasonably comprehensive, covering diverse datasets and metrics that highlight the model's improved search efficiency and accuracy. The clear articulation of the method and results is commendable. The paper contributes to the growing field of making LLMs more efficient and reliable agents. Minor points that prevent a higher score might include the reliance on a relatively small number of training steps (200) for RL (though acknowledged as sufficient for gains) and the noted discrepancy in reproducing ReSearch baseline performance, which, while explained, slightly complicates direct comparison to its original reported strength. Overall, it's a solid contribution with practical implications.

**2. Main Ideas**

The main ideas discussed in this paper are:

1.  **Selective Search Invocation via Reinforcement Learning:** The central idea is to train LLMs to make intelligent decisions about when to use an external search tool versus relying on their parametric knowledge. This is achieved through a post-training RL framework (SEM) that explicitly rewards models for either answering directly (if confident and correct) or searching effectively (if uncertain or initially incorrect), thereby optimizing search utility and reducing redundancy.
2.  **Balanced Dataset for Search Decision Learning:** A key component of SEM is the construction of a balanced training dataset by combining questions that inherently require external search (from Musique) with questions that are generally answerable using the LLM's internal knowledge (from MMLU). This diverse training environment forces the model to learn to differentiate between these scenarios, crucial for developing effective search-awareness.
3.  **Structured Reasoning and Group Relative Policy Optimization (GRPO):** The paper employs a specific structured output format (using `<think>`, `<answer>`, `<search>`, `<result>` tags) to facilitate the RL training and evaluation of the search behavior. The optimization is performed using GRPO, which compares groups of model outputs to encourage the generation of the best possible reasoning chain for a given query, coupled with a tailored reward function that promotes accuracy, adherence to format, and judicious search.

**3. List of 10 Most Important Citations**

1.  **Chen et al. 2025.** Research: Learning to reason with search for llms via reinforcement learning.
    *This paper (ReSearch) is a direct baseline against which SEM is compared; SEM aims to improve upon ReSearch's search behaviors, particularly in reducing unnecessary searches.* (No direct link provided in paper, cited as CoRR, abs/2503.19470)
2.  **Shao et al. 2024.** Deepseekmath: Pushing the limits of mathematical reasoning in open language models.
    *This paper is cited as the source for Group Relative Policy Optimization (GRPO), the RL algorithm adopted by SEM to train the model's search behaviors.* (No direct link provided in paper, cited as CoRR, abs/2402.03300)
3.  **Trivedi et al. 2022.** MuSiQue: Multihop questions via single-hop question composition.
    *MuSiQue is a key dataset used in SEM for training and evaluation, providing questions that typically require external multi-hop search, helping to teach the model when search is necessary.* (No direct link provided in paper)
4.  **Hendrycks et al. 2021.** Measuring massive multitask language understanding.
    *MMLU is the other key dataset used in SEM's balanced training approach, providing questions generally answerable from an LLM's internal knowledge, teaching the model when not to search.* (Link: OpenReview.net, specific URL not in citation text)
5.  **Lewis et al. 2020.** Retrieval-augmented generation for knowledge-intensive NLP tasks.
    *This paper introduced Retrieval-Augmented Generation (RAG), a foundational technique for integrating external knowledge into LLMs, which SEM aims to make more efficient by optimizing the retrieval trigger.* (No direct link provided in paper)
6.  **Qin et al. 2025.** Tool learning with foundation models.
    *This survey provides a broad context for SEM, as it details the landscape of LLMs learning to use tools, a capability that SEM specifically refines for search tools.* (No direct link provided in paper, cited as ACM Comput. Surv.)
7.  **Schulman et al. 2017.** Proximal policy optimization algorithms.
    *PPO is a foundational RL algorithm upon which GRPO (used in SEM) builds, making it relevant to understanding the RL methodology employed.* (No direct link provided in paper, cited as CoRR, abs/1707.06347)
8.  **Yang et al. 2018.** Hotpotqa: A dataset for diverse, explainable multi-hop question answering.
    *HotpotQA is an important benchmark dataset used for evaluating SEM's performance on tasks requiring complex, multi-hop search, demonstrating its effectiveness in challenging scenarios.* (No direct link provided in paper)
9.  **Cobbe et al. 2021.** Training verifiers to solve math word problems.
    *GSM8K is used as an evaluation dataset where questions (math problems) typically do not require external search, testing SEM's ability to refrain from unnecessary searching while maintaining accuracy.* (No direct link provided in paper, cited as CoRR, abs/2110.14168)
10. **Feng et al. 2025.** Retool: Reinforcement learning for strategic tool use in llms.
    *This work is highly relevant as it also focuses on using reinforcement learning for strategic tool use in LLMs, aligning with SEM's objective of optimizing search tool invocation.* (No direct link provided in paper, year cited as 2025)
