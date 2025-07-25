https://arxiv.org/abs/2505.11140

Scaling Reasoning can Improve Factuality in Large Language Models

**1. Summary and Rating:**

**Summary:**
This paper investigates whether extended reasoning processes in Large Language Models (LLMs) enhance factual accuracy in complex open-domain question-answering (QA), moving beyond typical mathematical reasoning tasks. The authors distill reasoning traces from advanced models (QwQ-32B and DeepSeek-R1) and fine-tune a range of Qwen2.5 models (0.5B to 32B parameters) on these traces. A key contribution is "fs1," a dataset of approximately 6,000 reasoning traces enhanced with factual information from Wikidata knowledge graph paths. Through 168 experimental runs across six QA benchmarks (encompassing over 22.6K questions), the study finds that smaller fine-tuned models (0.5B-1.5B) show significant improvements in factual accuracy (up to 10 percentage points) when using these structured, KG-enhanced reasoning traces compared to their original instruction-tuned counterparts. For larger models (beyond 3B parameters), this benefit from fine-tuning on longer/enhanced traces is less pronounced. However, the paper demonstrates that test-time scaling—either through increased computational budget (token length for reasoning) or parallel sampling (generating multiple answers)—consistently improves factual accuracy by 2-8% even for the largest models. The authors conclude that longer, structured reasoning is beneficial, particularly for smaller models when enhanced with KG information, and that test-time compute is a reliable method for boosting factuality across model sizes. They release their datasets (fs1, 1.7M reasoning traces), models, and code to facilitate further research.

**Rating: 9/10**

**Justification for Rating (for a PhD-level audience):**
This paper earns a high rating due to its comprehensive and rigorous investigation into an important and nuanced area of LLM capabilities.
*   **Methodological Rigor and Scale:** The extensive experimental setup, involving multiple model sizes, diverse datasets, a large number of experimental runs (168), and analysis of 1.7 million reasoning traces, provides a strong empirical foundation for its conclusions.
*   **Significant Contributions:** The introduction and public release of the `fs1` dataset (KG-enhanced reasoning traces) and the broader set of reasoning traces are valuable resources for the research community. The paper’s insights into the interplay between model scale, reasoning strategies (KG-enhanced fine-tuning vs. test-time scaling), and factual accuracy are significant.
*   **Clarity and Novelty:** The research addresses a pertinent question about generalizing "long reasoning" benefits beyond mathematical tasks to factual QA. The findings regarding the differential impact on smaller versus larger models and the consistent benefits of test-time scaling offer clear and actionable insights. The approach of incorporating KG paths directly into reasoning traces for fine-tuning is a practical method for improving factuality.
*   **Reproducibility:** The commitment to open-sourcing all experimental artifacts (code, datasets, models) is commendable and crucial for scientific progress.

The paper is well-structured and clearly written. A point is reserved primarily because, while the empirical results are strong, further qualitative analysis or deeper dives into *why* larger models benefit less from the KG-enhanced fine-tuning (beyond just "already learned it") could strengthen the interpretative aspect, though this is an inherently challenging problem in LLMs. The reliance on "LLM-as-a-judge" for evaluation, while practical and increasingly common, carries its own known limitations (which the authors acknowledge and attempt to mitigate with other metrics). Overall, it represents a solid piece of research.

**2. Main Ideas Discussed:**

1.  **Knowledge Graph (KG) Enhanced Fine-Tuning Boosts Factuality in Smaller LLMs:** A central idea is that fine-tuning LLMs, especially smaller ones (0.5B-1.5B parameters), on reasoning traces that are explicitly augmented with factual paths from knowledge graphs (like Wikidata) leads to noticeable improvements in their factual accuracy on complex open-domain QA tasks. This is demonstrated by the `fs1` dataset and associated experiments.
2.  **Test-Time Scaling Consistently Improves Factuality Across Model Sizes:** The paper shows that allocating additional computational resources at inference time, either by increasing the token budget for reasoning (sequential scaling/budget forcing) or by generating multiple candidate answers (parallel scaling), reliably enhances factual accuracy (by 2-8%) for all models tested, including larger ones where the KG-enhanced fine-tuning showed diminishing returns. This underscores the general effectiveness of test-time compute for factuality.
3.  **Differential Impact of Reasoning Strategies Based on Model Scale:** The research highlights that the benefits of fine-tuning on longer or KG-enhanced reasoning traces are more pronounced for smaller LLMs. Larger models (>3B parameters) derive less comparative advantage from this specific intervention, possibly because their larger capacity has already enabled them to learn such factual connections or reasoning patterns. However, they still benefit from general test-time scaling techniques. The paper also identifies an optimal reasoning length (around 2K tokens) for budget-forcing experiments, suggesting that "more thinking" isn't always better beyond a certain point.

**3. 10 Most Important Citations:**

1.  **Muennighoff et al. 2025. s1: Simple test-time scaling.** This paper is frequently referenced for the fine-tuning hyperparameters and as a basis for investigating sequential test-time scaling (budget forcing), making it crucial to the experimental design.
    *   *Link: `ArXiv preprint, abs/2501.19393` (implied from reference list)*
2.  **Talmor and Berant. 2018. The web as a knowledge-base for answering complex questions.** This work introduced the ComplexWebQuestions (CWQ) dataset, which is the primary source for generating and evaluating the reasoning traces in this study.
    *   *No explicit link provided in the paper's references.*
3.  **DeepSeek-AI et al. 2025. Deepseek-r1: Incentivizing reasoning capability in Ilms via reinforcement learning.** DeepSeek-R1 is one of the two advanced, large-scale reasoning models from which the authors distill their initial "teacher" reasoning traces.
    *   *Link: `ArXiv preprint, abs/2501.12948` (implied from reference list)*
4.  **Qwen Team. 2025. Qwq-32b: Embracing the power of reinforcement learning.** QwQ-32B is the other advanced reasoning model used to distill the initial reasoning traces, forming a core part of the data generation pipeline.
    *   *No explicit link provided in the paper's references for this specific paper.*
5.  **Wei et al. 2022. Chain-of-thought prompting elicits reasoning in large language models.** This foundational paper on chain-of-thought prompting underpins the concept of "lengthy thinking process" that the current work extends to factual QA.
    *   *No explicit link provided in the paper's references (NIPS proceedings).*
6.  **Vrandečić and Krötzsch. 2014. Wikidata: a free collaborative knowledgebase.** Wikidata is the knowledge graph used to extract factual paths for enhancing the reasoning traces in the paper's `fs1` dataset, a key methodological component.
    *   *No explicit link provided in the paper's references (Communications of the ACM).*
7.  **Bollacker et al. 2008. Freebase: a collaboratively created graph database for structuring human knowledge.** The CWQ dataset, used extensively, is based on Freebase entities and relations, making this reference important for understanding the data's origin.
    *   *No explicit link provided in the paper's references (SIGMOD proceedings).*
8.  **Zhang et al. 2025. What, how, where, and how well? a survey on test-time scaling in large language models.** This survey is cited in the abstract and introduction, providing the broader context and motivation for the paper's investigation into test-time scaling techniques.
    *   *Link: `Preprint, arXiv:2503.24235` (implied from reference list)*
9.  **Chen et al. 2021. Evaluating large language models trained on code.** This paper is cited for defining the pass@k metric, a key evaluation method used in this study to assess performance when multiple completions are generated.
    *   *Link: `arXiv preprint arXiv:2107.03374` (implied from reference list)*
10. **Luo et al. 2023. Reasoning on graphs: Faithful and interpretable large language model reasoning.** Cited in the related work section on graph-enhanced learning, this paper (RoG model) represents a relevant approach to integrating KGs with LLMs for faithful reasoning, contextualizing the current paper's method.
    *   *Link: `arXiv preprint arXiv:2310.01061` (implied from reference list)*
