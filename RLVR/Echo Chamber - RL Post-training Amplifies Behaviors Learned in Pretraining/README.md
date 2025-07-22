https://arxiv.org/abs/2504.07912

Echo Chamber: RL Post-training Amplifies Behaviors Learned in Pretraining

1. Summary and Rating

This paper conducts a systematic, end-to-end investigation into how reinforcement learning (RL) post-training interacts with pretraining data composition, model scale, and RL algorithms to shape the mathematical reasoning capabilities of language models. The authors address a critical gap in understanding these mechanisms, often hindered by the proprietary nature of pretraining datasets used in many existing models. To overcome this, they pretrain decoder-only language models (150M and 1B parameters) entirely from scratch on various mixtures of fully open-source mathematical text corpora and instruction-following datasets (TinyGSM, OpenMathInstruct1, OpenMathInstruct2). They then fine-tune these models using different RL algorithms (PPO, GRPO, Expert Iteration) with verifiable rewards on mathematical reasoning tasks (GSM8K) and evaluate performance and output characteristics, including transfer to harder datasets like MATH and AIME.

The study reveals several key findings:

Echo Chamber Effect: RL fine-tuning consistently drives models to converge towards generating outputs in the format of a single, dominant distribution learned during pretraining, effectively amplifying those specific patterns while suppressing others. This convergence often coincides with the largest performance gains.
Scale-Dependent Distribution Preference: The choice of the dominant output distribution is scale-dependent. Smaller models (150M) tend to favor simpler, code-like output formats (e.g., TinyGSM style), whereas larger models (1B) shift towards preferring more natural language or complex code formats (e.g., OpenMathInstruct2 style), even if those were not initially the most performant or frequent.
Refinement and Generalization: Beyond just format preference, RL fine-tuning can refine qualitative properties within the chosen distribution. Furthermore, post-training on simpler problems (like GSM8K) can lead to performance improvements on more complex, unseen mathematical reasoning tasks (like MATH), indicating that certain reasoning capabilities can generalize.
Algorithmic Differences: Different RL algorithms (PPO, GRPO, EI) show nuanced differences in training stability and the extent of distribution shift, highlighting the impact of algorithmic choices.
The paper's primary contribution lies in its rigorous, controlled experimental setup, training models "from scratch" to isolate the effects of pretraining data. This methodology provides valuable insights into the "echo chamber" nature of RL fine-tuning and its interplay with model scale, suggesting that pretraining data significantly preconditions the outcomes of RL post-training.

Rating: 9/10 For a PhD-level audience, this paper is a strong contribution. Its methodological rigor in training models from scratch on open datasets to disentangle pretraining effects from RL fine-tuning effects is highly commendable and addresses a significant limitation in prior work. The findings regarding the "echo chamber" phenomenon and scale-dependent biases are insightful and have important implications for understanding and controlling LLM behavior. The systematic exploration across model scales, data mixtures, and RL algorithms provides a solid empirical foundation. The paper is well-structured and clearly articulates its findings, which are relevant to current research on LLM alignment and capabilities. While focused on mathematical reasoning, the principles likely generalize. The work paves the way for more principled approaches to pretraining and fine-tuning strategies.

2. Main Ideas Discussed

RL Fine-Tuning as an "Echo Chamber" Amplifying Pretrained Behaviors: The core finding is that RL fine-tuning does not necessarily teach entirely new behaviors but rather amplifies and converges upon specific output patterns and formats already present in the model due to its pretraining data. The model rapidly hones in on one "preferred" distribution from the pretraining mixture, suppressing others, and this often leads to performance improvements.
Scale-Dependent Biases in Amplified Behaviors: The specific pretraining-induced behavior that gets amplified by RL is dependent on the model's scale. Smaller models tend to converge towards simpler, more structured (e.g., code-like) output formats, potentially because these offer a more direct path to verifiable correctness. Larger models, with greater capacity, may amplify more complex or natural language-based reasoning patterns. This suggests that model scale influences how a model generalizes and what strategies it "chooses" to rely on post-RL fine-tuning.
Generalization of Reasoning from Simpler Tasks and Refinement within a Distribution: RL post-training on relatively simpler question-answering datasets (like GSM8K) can lead to performance improvements on more challenging and structurally different mathematical tasks (like MATH). This indicates a degree of transfer learning where underlying reasoning capabilities, not just output formatting, are enhanced. The paper also shows that fine-tuning refines qualitative aspects of generations within the chosen dominant distribution (e.g., consistent docstring formatting).
3. 10 Most Important Citations

Schulman et al. 2017. Proximal policy optimization algorithms. (arXiv:1707.06347)
This paper introduces Proximal Policy Optimization (PPO), a core RL algorithm used extensively by the authors for fine-tuning their language models.
Lambert et al. 2024. T" ulu 3: Pushing frontiers in open language model post-training. (arXiv:2411.15124)
This work is relevant for its discussion on post-training techniques and is cited by the authors for the concept of "verifiable rewards," a crucial component of their RL fine-tuning reward mechanism.
Groeneveld et al. 2024. Olmo: Accelerating the science of language models. (In Proceedings of the 62nd Annual Meeting of the Association for Computational Linguistics)
This paper introduces OLMo, the codebase used by the authors to pretrain their language models from scratch, enabling their controlled experimental setup.
Liu et al. 2023. Tinygsm: achieving¿ 80% on gsm8k with small language models. (arXiv:2312.09241)
This paper introduces the TinyGSM dataset, one of the key synthetic instruction datasets used in the pretraining mixtures and for fine-tuning/evaluation, allowing the authors to track format-specific model outputs.
Toshniwal et al. 2025b. Openmathinstruct-1: A 1.8 million math instruction tuning dataset. (Advances in Neural Information Processing Systems)
This paper introduces OpenMathInstruct-1, another distinct instruction dataset used in pretraining, characterized by its specific code-based formatting, which the authors track to observe distribution shifts.
Toshniwal et al. 2025a. Openmathinstruct-2: Accelerating ai for math with massive open-source instruction data. (In The Thirteenth International Conference on Learning Representations)
This paper introduces OpenMathInstruct-2, a pretraining instruction dataset featuring natural language solutions, contrasting with code-based datasets and allowing analysis of preferences for different output modalities.
Havrilla et al. 2024. Teaching large language models to reason with reinforcement learning. (arXiv:2403.04642)
The authors identify this as the "closest work to our own," as it also studies PPO performance across scales on base and fine-tuned models for reasoning tasks.
Kirk et al. 2024. Understanding the effects of rlhf on llm generalisation and diversity. (In The Twelfth International Conference on Learning Representations)
This paper's findings on reduced generation diversity following RLHF/RL fine-tuning align with the current paper's observation of pass@64 accuracy declining towards the end of training due to distribution collapse.
Guo et al. 2025. Deepseek-r1: Incentivizing reasoning capability in llms via reinforcement learning. (arXiv:2501.12948)
Cited as an example of state-of-the-art reasoning models that utilize RL-based fine-tuning, contextualizing the importance of understanding the mechanisms studied in the current paper.
Anthony et al. 2017. Thinking fast and slow with deep learning and tree search. (Advances in neural information processing systems)
This paper introduces Expert Iteration (EI), one of the fine-tuning methodologies compared against PPO and GRPO by the authors in their study.
