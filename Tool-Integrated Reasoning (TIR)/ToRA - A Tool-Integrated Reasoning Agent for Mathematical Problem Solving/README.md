https://arxiv.org/abs/2309.17452

TORA: A TOOL-INTEGRATED REASONING AGENT FOR MATHEMATICAL PROBLEM SOLVING

### 1. Summary and Rating

**Summary:**

This paper introduces TORA (Tool-integrated Reasoning Agent), a series of open-source language models designed to solve complex mathematical problems. The core innovation is a hybrid reasoning format that synergistically interleaves natural language rationales (for planning and semantic understanding) with program-based tool use (for precise computation and symbolic manipulation). The training process involves two key stages. First, the authors curate a new dataset, TORA-CORPUS, by using GPT-4 to generate high-quality, interactive tool-use trajectories, and then use this dataset for imitation learning on LLaMA-2 and CodeLLaMA base models. Second, they propose a novel "output space shaping" technique, which further refines the models by training them on a larger, more diverse set of trajectories generated via self-sampling and correction by a teacher model. The results are state-of-the-art for open-source models, with TORA demonstrating 13%-19% absolute improvements over previous models on 10 math datasets. Notably, TORA-70B surpasses GPT-4's Chain-of-Thought performance on the challenging MATH benchmark, and TORA-CODE-34B is competitive with GPT-4's program-based approach.

**Rating:** **9/10**

This is an excellent and high-impact paper. The primary contribution is not just the idea of tool integration, but the specific, well-engineered methodology for making it effective for complex mathematical reasoning on open-source models. The two-stage training process, particularly the "output space shaping" refinement, is a strong and well-motivated contribution that demonstrably yields significant performance gains. The experimental setup is comprehensive, with thorough ablations and comparisons against a wide range of strong baselines, including proprietary models. The results are impressive, significantly advancing the state-of-the-art for open-source mathematical reasoning and substantially closing the gap with top-tier closed-source models like GPT-4. The paper is clearly written and the analysis of failure modes provides valuable direction for future research. It represents a solid step forward in making powerful reasoning agents more accessible.

### 2. Main Ideas

1.  **Synergistic Tool-Integrated Reasoning Format:** The central idea is to combine the strengths of natural language reasoning and program execution. Instead of relying solely on step-by-step rationales (like Chain-of-Thought) which can fail at precise computation, or solely on program synthesis (like Program-aided Language Models) which can lack planning and flexibility, TORA interleaves them. The model generates natural language to analyze a problem, writes code to call external tools (e.g., a symbolic math library) for computation, receives the tool's output, and then uses natural language again to interpret the results and decide the next step, creating a more robust and capable problem-solving loop.
2.  **Two-Stage Training with Output Space Shaping:** The paper introduces a highly effective two-stage training pipeline.
    *   **Stage 1 (Imitation Learning):** An initial dataset of high-quality, interleaved reasoning trajectories (TORA-CORPUS) is curated using GPT-4. An open-source model is then fine-tuned on this data.
    *   **Stage 2 (Output Space Shaping):** To overcome the limitations of learning from a fixed set of trajectories, the model's reasoning capabilities are diversified. This is done by using the stage-1 model to sample a large number of potential solution paths. Valid paths are retained, while invalid paths are corrected by a stronger "teacher" model. The model is then retrained on this augmented dataset of valid and corrected trajectories, which significantly improves its flexibility and error-handling.
3.  **Bridging the Performance Gap with Open-Source Models:** A key outcome of this work is demonstrating that this methodology can create open-source models that achieve state-of-the-art performance on difficult mathematical benchmarks like MATH and GSM8k. TORA models significantly outperform prior leading open-source models (like WizardMath) and achieve performance competitive with, or in some cases superior to, proprietary models like ChatGPT and even GPT-4's standard CoT prompting.

### 3. Top 10 Citations

1.  **Wei et al. (2022)** Chain of thought prompting elicits reasoning in large language models.
    This paper introduced Chain-of-Thought (CoT) prompting, the foundational "rationale-only" method that TORA builds upon and integrates with program-based tool use.
    *   Link: [https://openreview.net/forum?id=_VjQlMeSB_J](https://openreview.net/forum?id=_VjQlMeSB_J)

2.  **Gao et al. (2022)** Pal: Program-aided language models.
    This paper introduced Program-aided Language Models (PAL), which offload reasoning to a code interpreter; TORA's method is a synthesis of the approaches in PAL and CoT.

3.  **Cobbe et al. (2021)** Training verifiers to solve math word problems.
    This introduced the GSM8k dataset, a crucial benchmark for elementary mathematical reasoning that is used for both training and evaluation in the TORA paper.
    *   Link: [https://arxiv.org/abs/2110.14168](https://arxiv.org/abs/2110.14168)

4.  **Hendrycks et al. (2021)** Measuring mathematical problem solving with the math dataset.
    This introduced the MATH dataset, a challenging competition-level benchmark that is central to the paper's claims of achieving state-of-the-art performance.

5.  **Touvron et al. (2023b)** Llama 2: Open foundation and fine-tuned chat models.
    This paper introduced the LLaMA-2 family of models, which serve as the open-source foundation models that TORA is built upon.
    *   Link: [https://doi.org/10.48550/arXiv.2307.09288](https://doi.org/10.48550/arXiv.2307.09288)

6.  **Luo et al. (2023)** Wizardmath: Empowering mathematical reasoning for large language models via reinforced evol-instruct.
    This paper presented WizardMath, which was the previous state-of-the-art open-source model for mathematical reasoning that TORA uses as a key performance baseline to demonstrate its significant improvements.

7.  **OpenAI (2023)** Gpt-4 technical report.
    This report describes GPT-4, which was used both to generate the initial TORA-CORPUS training data and as the primary high-performance proprietary model for benchmarking comparisons.

8.  **Yao et al. (2023)** React: Synergizing reasoning and acting in language models.
    This paper proposed the ReAct framework, a seminal work on interleaving reasoning traces and actions (tool use), which is a core conceptual parallel to TORA's methodology.
    *   Link: [https://openreview.net/forum?id=WE_vluYUL-X](https://openreview.net/forum?id=WE_vluYUL-X)

9.  **Schick et al. (2023)** Toolformer: Language models can teach themselves to use tools.
    This is another foundational paper on tool-augmented LLMs that TORA is conceptually related to and compares against, demonstrating how LLMs can learn to use external tools.

10. **Li et al. (2023)** Making language models better reasoners with step-aware verifier.
    This paper is cited for the observation that reasoning errors often occur midway through a trajectory, which provides motivation for TORA's output space shaping strategy of correcting partially-correct reasoning paths.
