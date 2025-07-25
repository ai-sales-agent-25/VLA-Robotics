https://arxiv.org/abs/2502.04644

**Paper:** Agentic Reasoning: A Streamlined Framework for Enhancing LLM Reasoning with Agentic Tools

### 1. Summary and Rating

This paper introduces "Agentic Reasoning," a framework designed to enhance the reasoning capabilities of Large Language Models (LLMs) by integrating them with a suite of external, specialized agentic tools. The framework dynamically employs a Web-Search agent for information retrieval, a Code agent for quantitative analysis and execution, and a novel Mind-Map agent. The Mind-Map agent is a key innovation that constructs a knowledge graph from the reasoning context to serve as a structured memory. This graph helps maintain logical coherence over long reasoning chains, clarifies complex relationships, and provides rich, structured context to the other agents.

The authors demonstrate that when applied to the open-source DeepSeek-R1 model, Agentic Reasoning achieves state-of-the-art results among public models on several challenging benchmarks, including Humanity's Last Exam, the PhD-level GPQA science benchmark, and the GAIA general assistant benchmark. The framework significantly closes the performance gap to top-tier proprietary models like OpenAI's Deep Research. Through extensive ablation studies, the paper validates the effectiveness of its three-agent combination and the specific design choices for the Web-Search agent, proving their synergistic contribution to the model's reasoning power.

**Rating: 9/10**

For a PhD-level audience, this paper earns a high rating due to its rigorous empirical methodology, significant and well-documented performance improvements, and a novel contribution in the form of the Mind-Map agent. While the concept of tool-use is not new, the paper's strength lies in the systematic construction and evaluation of a synergistic, multi-agent framework. The introduction of a knowledge graph as a dynamic reasoning memory (Mind-Map) is a clever and effective method for tackling the common LLM challenges of maintaining long-range coherence and understanding complex logical structures. The extensive ablation studies and comparisons against a strong field of both open and proprietary models provide compelling evidence for the framework's efficacy. The paper is a well-executed piece of research that pushes the state-of-the-art for open models and provides a clear, replicable framework for others to build upon.

### 2. Main Ideas

1.  **A Synergistic Multi-Agent Framework:** The core idea is that complex reasoning is best achieved not by a monolithic model or a single tool, but by a streamlined framework where an LLM orchestrates a set of specialized agents. The paper identifies a highly effective trio: a **Web-Search agent** to ground the model in external facts, a **Code agent** to handle precise quantitative reasoning, and a **Mind-Map agent** to manage the reasoning process itself.
2.  **Mind-Map as Structured Reasoning Memory:** This is the paper's most novel contribution. Instead of relying solely on the transient context of an LLM, the Mind-Map agent creates a persistent knowledge graph to structure the entire reasoning chain. This externalized "mind" helps the model track complex logical relationships, maintain coherence during long and multi-step tasks, and provide structured context to other tools, significantly reducing errors and improving performance on logic-heavy problems and strategic games.
3.  **Systematic Design and Optimization of Tools:** The paper demonstrates that the *quality* and *combination* of tools are more important than the sheer quantity. Through detailed ablation studies, it shows that its specific, carefully designed three-agent toolbox is superior to larger, more generic toolkits. Furthermore, it details an effective multi-step process for its Web-Search agent—involving query breakdown, reranking, and iterative refinement—which proves superior to simpler RAG approaches.

### 3. 10 Most Important Citations

1.  **Shao et al. 2024.** Assisting in writing wikipedia-like articles from scratch with large language models. This paper introduces STORM, a complex agent-based system for deep research, which serves as a key benchmark and point of comparison for a state-of-the-art agentic workflow.
    *   Link: `https://arxiv.org/abs/2402.14207`
2.  **Li et al. 2025.** Search-O1: Agentic search-enhanced large reasoning models. This paper presents a direct competitor and a recent state-of-the-art approach for integrating search into reasoning, against which Agentic Reasoning demonstrates superior performance.
    *   Link: `https://arxiv.org/abs/2501.05366`
3.  **Edge et al. 2024.** From local to global: A graph rag approach to query-focused summarization. This paper introduces GraphRAG, the core methodology of which is explicitly cited as the inspiration for constructing and querying the knowledge graph in the Mind-Map agent.
    *   Link: `https://arxiv.org/abs/2404.16130`
4.  **Mialon et al. 2023.** Gaia: a benchmark for general ai assistants. This paper provides the GAIA benchmark, which is used extensively to evaluate the model's proficiency in web browsing, tool use, and complex reasoning, making it a crucial tool for validating the framework's capabilities.
    *   Link: `https://arxiv.org/abs/2311.12983`
5.  **Rein et al. 2023.** Gpqa: A graduate-level google-proof q&a benchmark. This work supplies the GPQA dataset, a PhD-level science benchmark that the authors use to prove their framework's ability to solve expert-level problems.
    *   Link: `https://arxiv.org/abs/2311.12022`
6.  **Lewis et al. 2020.** Retrieval-augmented generation for knowledge-intensive nlp tasks. This is the foundational paper for RAG, a core concept that the paper builds upon and enhances with its more sophisticated, multi-step Web-Search agent.
7.  **Phan et al. 2025.** Humanity's last exam. This paper introduces a broad, expert-level benchmark used in the abstract to provide the first piece of evidence for Agentic Reasoning's high performance and its ability to narrow the gap with proprietary models.
    *   Link: `https://arxiv.org/abs/2501.14249`
8.  **Wei et al. 2022.** Chain-of-thought prompting elicits reasoning in large language models. This is a foundational paper establishing a key technique for improving LLM reasoning, providing the context for more advanced frameworks like Agentic Reasoning that aim to structure and augment this process.
9.  **DeepSeek Team. 2024.** Deepseek-r1-lite-preview is now live: unleashing supercharged reasoning power. This citation refers to the base model (DeepSeek-R1) used in the experiments, which is critical as the paper's central claim is that it significantly enhances the capabilities of already powerful reasoning models.
10. **Jaech et al. 2024.** Openai o1 system card. This system card describes OpenAI's o1, a state-of-the-art proprietary reasoning model that serves as a key high-level benchmark and contextualizes the authors' claims of approaching top-tier performance.
    *   Link: `https://arxiv.org/abs/2412.16720`
