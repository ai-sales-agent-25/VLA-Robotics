https://arxiv.org/abs/2505.08402

**TUMS: Enhancing Tool-use Abilities of LLMs with Multi-structure Handlers**

1.  **Brief Summary and Rating:**
    This paper introduces TUMS (Tool-use Abilities of LLMs with Multi-structure Handlers), a framework designed to improve the proficiency of Large Language Models (LLMs) in utilizing external tools. The authors identify a key limitation in existing tool-augmented LLMs: the parameter generation process for tools is often coarse-grained and confined to the tool level, failing to account for the varying complexities and parameter requirements of different tools. TUMS addresses this by shifting to a finer-grained, parameter-level processing approach. The framework comprises four main components: (1) an Intent Recognizer to discern user intent and narrow down relevant tools/datasets; (2) a Task Decomposer to break complex queries into simpler subtasks, each mapped to a tool call; (3) a Subtask Processor equipped with multi-structure handlers (Direct, Parallel, and Serial Generation) that adaptively generate parameters based on tool complexity; and (4) an Executor to run the tools. Empirical results on the ToolQA benchmark demonstrate that TUMS significantly outperforms existing baselines (like ReAct and Chameleon) on both easy and hard question sets, with ablation studies confirming the contributions of its components, particularly the multi-structure handlers and the intent recognizer for efficiency.

    **Rating: 8.5/10**
    This paper presents a well-motivated and thoughtfully designed framework that addresses a pertinent and non-trivial problem in the practical application of LLMs for tool use. The core novelty lies in the introduction of multi-structure handlers within the subtask processor, allowing for adaptive and more precise parameter generation tailored to tool complexity. This parameter-level processing is a logical and impactful refinement over more monolithic tool-level approaches. The experimental validation on ToolQA is solid, with appropriate baselines and insightful ablation studies that clearly demonstrate the efficacy of the proposed components. The improvements, particularly the average of 19.6% on easy and 50.6% on hard ToolQA benchmarks, are substantial. The paper is clearly written and contributes valuable insights into improving the reliability of tool-augmented LLMs. While the framework itself is somewhat sophisticated with multiple components, this complexity appears justified by the problem's nature. The discussion on preference-based hints in the appendix to tackle extremely challenging tasks also shows a practical understanding of current limitations. The work could be further strengthened by exploring the framework's scalability to a larger, more diverse set of tools and its robustness to noisier or more ambiguous user intents, but it stands as a strong contribution to the field.

2.  **Main Ideas Discussed:**

    *   **Parameter-Level Processing with Multi-Structure Handlers:** The central idea is to move beyond coarse-grained, tool-level parameter generation. TUMS introduces a subtask processor with three distinct parameter generation structures (Direct for simple tools, Parallel for tools with multiple independent parameters, and Serial for complex tools like SQL query generation). This allows the LLM to adapt its parameter generation strategy based on the specific demands and complexity of the tool being invoked, leading to more accurate parameters and fewer execution errors.
    *   **Modular Decomposition for Enhanced Tool Invocation:** The TUMS framework employs a modular, multi-stage pipeline. This includes an initial Intent Recognizer to help the LLM understand the task context and constrain the tool search space, followed by a Task Decomposer that breaks down the main query into manageable subtasks each requiring a tool. This structured approach, inspired by human problem-solving, allows the LLM to tackle complex multi-tool tasks more effectively and efficiently, with the decomposer capable of reflective adjustments.
    *   **(Implicitly) Addressing Limitations of Uniform Tool Handling:** The paper critiques the "one-size-fits-all" strategy common in LLM tool use, where parameter generation doesn't adequately differentiate between simple and complex tools or between tools requiring single versus multiple parameters. By explicitly designing for this variance, TUMS aims to mitigate issues like missing, irrelevant, or incorrect parameters that plague less nuanced systems.

3.  **10 Most Important Citations:**

    1.  **Zhuang et al. (2024)** Toolqa: A dataset for llm question answering with external tools.
        *   This citation is crucial as ToolQA is the benchmark dataset used for evaluating the TUMS framework and comparing it against baselines.
        *   Link: Not explicitly provided, but typically found on conference proceedings sites like NeurIPS databasets and benchmarks track or arXiv. (The paper cites it as "Advances in Neural Information Processing Systems 36 (2024)")

    2.  **Yao et al. (2022)** React: Synergizing reasoning and acting in language models.
        *   ReAct is a highly influential framework for enabling LLMs to combine reasoning and tool use (acting), serving as a key baseline against which TUMS is compared.
        *   Link: arXiv:2210.03629

    3.  **Lu et al. (2024)** Chameleon: Plug-and-play compositional reasoning with large language models.
        *   Chameleon is another significant baseline method that employs LLMs as controllers for multi-tool tasks, providing a point of comparison for TUMS's performance.
        *   Link: Not explicitly provided, but cited as "Advances in Neural Information Processing Systems 36 (2024)".

    4.  **Wei et al. (2022)** Chain-of-thought prompting elicits reasoning in large language models.
        *   Chain-of-Thought (CoT) prompting is a fundamental technique for improving LLM reasoning, and a CoT-enhanced Qwen model is used as a baseline in the experiments.
        *   Link: Not explicitly provided, but cited as "Advances in neural information processing systems 35, 24824-24837 (2022)".

    5.  **Qin et al. (2023)** Tool learning with foundation models.
        *   This paper discusses the broader concept of LLMs learning to use tools, providing foundational context for the problem TUMS aims to solve and likely inspiring aspects of tool integration.
        *   Link: arXiv:2304.08354

    6.  **Team Q. (2024)** Introducing qwen1.5.
        *   The Qwen1.5-72B model is the specific LLM utilized as the backbone for all methods in the TUMS experiments, making this citation essential for reproducibility and context.
        *   Link: https://qwenlm.github.io/blog/qwen1.5/

    7.  **Achiam et al. (2023)** Gpt-4 technical report.
        *   Represents the state-of-the-art in general LLM capabilities, setting a benchmark for the kind of advanced reasoning and understanding TUMS aims to leverage and enhance for tool use.
        *   Link: arXiv:2303.08774

    8.  **Khot et al. (2022)** Decomposed prompting: A modular approach for solving complex tasks.
        *   This work on task decomposition is relevant as TUMS incorporates a "task decomposer" module to break down complex questions, aligning with the principles discussed in this citation.
        *   Link: arXiv:2210.02406

    9.  **Dong et al. (2022)** A survey on in-context learning.
        *   TUMS utilizes few-shot prompting for its modules, making this survey on in-context learning relevant for understanding the underlying mechanism enabling the LLM to perform tasks like intent recognition and task decomposition based on examples.
        *   Link: arXiv:2301.00234

    10. **Shen et al. (2024)** Hugginggpt: Solving ai tasks with chatgpt and its friends in hugging face.
        *   HuggingGPT is an example of earlier work on enabling LLMs to use multiple tools by planning and selecting from a toolset, providing context for the evolution of tool-augmented LLMs which TUMS builds upon.
        *   Link: Not explicitly provided, but cited as "Advances in Neural Information Processing Systems 36 (2024)".
