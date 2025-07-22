https://huggingface.co/papers/2505.24864

https://x.com/_akhaliq/status/1929540706374201756

https://x.com/shizhediao/status/1929556870186098911

https://x.com/GXiming/status/1929613286372421830

https://x.com/YangYue_THU/status/1929892574522904586


ProRL: Prolonged Reinforcement Learning Expands Reasoning Boundaries in Large Language Models

**1. Summary and Rating**

**Summary:**
This paper challenges the prevailing skepticism about whether reinforcement learning (RL) can genuinely expand the reasoning capabilities of Large Language Models (LLMs) beyond merely amplifying high-reward outputs already latent in the base model. The authors introduce ProRL, a novel training methodology designed for prolonged RL. ProRL incorporates techniques such as KL divergence control, periodic reference policy resetting, and training on a diverse suite of tasks (math, code, STEM, logic puzzles, instruction following) to ensure stable and effective long-horizon training.

Using ProRL, the authors developed Nemotron-Research-Reasoning-Qwen-1.5B, which they claim is the "world's best 1.5B reasoning model." Their empirical analysis demonstrates that this RL-trained model consistently outperforms its base model (DeepSeek-R1-1.5B) across a wide range of pass@k evaluations. Crucially, the paper provides evidence that ProRL can uncover novel reasoning strategies and solution pathways that are inaccessible to the base model, even under extensive sampling. This is particularly evident in scenarios where the base model fails entirely or on out-of-distribution tasks. The authors show that improvements in reasoning boundaries correlate strongly with the base model's initial competence on a task (greater gains where the base model struggles) and the duration of RL training. The findings suggest that RL, when applied with appropriate techniques over extended periods, can indeed explore and populate new regions of the solution space, pushing the reasoning frontiers of LLMs. The authors also release model weights to support further research.

**Rating for a PhD-level Audience: 9/10**

**Justification for Rating:**
This paper makes a significant contribution by directly addressing a contentious and important question in the field of LLM reasoning: the true impact of RL on expanding inherent capabilities.
*   **Novelty and Significance (Strengths):** The core thesis – that prolonged and carefully managed RL (ProRL) can lead to qualitatively new reasoning abilities – challenges some recent pessimistic findings and offers a more optimistic outlook on RL's role. The ProRL methodology, with its emphasis on stability over long training horizons through KL control and reference policy resets, is a valuable practical contribution. The demonstration of ProRL's effectiveness in enabling models to solve problems previously unsolvable by the base model, and its generalization to OOD tasks, is compelling. The release of the model and the breadth of evaluation are commendable.
*   **Methodological Rigor (Strengths):** The experimental setup is comprehensive, involving diverse datasets and rigorous evaluation metrics (pass@k, creativity index, OOD generalization). The analysis in Section 4, particularly the correlation between base model performance and RL gains (Figure 3) and the categorization of reasoning boundary evolution (Figure 4), provides insightful evidence supporting their claims.
*   **Clarity (Strength):** The paper is well-written and structured, clearly articulating the problem, proposed solution, and findings. Figures effectively illustrate key results.
*   **Potential for Discussion/Minor Weaknesses:** While the evidence is strong, a direct ablation study detailing the individual contributions of each component of ProRL (KL control, reset frequency, diversity of tasks, DAPO elements) within the main paper would have further solidified the understanding of *why* ProRL is effective. The "world's best 1.5B model" claim, while supported by their benchmarks, is always subject to the evolving landscape of model releases. However, these are minor points in the context of the paper's overall impact.

The paper is not unnecessarily complicated; its complexity is warranted by the nuanced problem it tackles and the sophisticated methods employed. It robustly argues its main points and provides substantial empirical backing, making it a high-quality piece of research that should stimulate further investigation into long-horizon RL for cognitive tasks in LLMs.

**2. Main Ideas Discussed**

The main ideas discussed in this paper are:

1.  **Prolonged RL (ProRL) Genuinely Expands Reasoning Capabilities:** The central argument is that extended and well-managed reinforcement learning, termed ProRL, can do more than just refine existing abilities or improve sampling efficiency. It can enable LLMs to discover and internalize novel reasoning strategies and solution pathways that were previously inaccessible to the base model, effectively expanding its reasoning boundaries.
2.  **ProRL Methodology for Stable and Effective Long-Horizon Training:** The paper introduces specific techniques within the ProRL framework crucial for achieving this expansion. These include KL divergence control to maintain entropy and prevent policy collapse, periodic hard resets of the reference policy and optimizer to ensure continued learning and stability, and training on a diverse set of tasks to foster generalizable reasoning skills. These elements collectively allow for the prolonged training necessary for the model to explore new solution spaces.
3.  **Conditions for and Evidence of Reasoning Boundary Expansion:** The paper demonstrates that ProRL is particularly effective at expanding reasoning boundaries in domains where the base model initially struggles. It also shows that improvements correlate with training duration. Evidence for this expansion includes superior performance on pass@k evaluations (especially at high k), generation of more novel trajectories (higher Creativity Index), and successful generalization to out-of-distribution (OOD) tasks and tasks of increasing difficulty, sometimes achieving 100% pass rates where the base model completely failed.

**3. 10 Most Important Citations**

Here is a list of 10 important citations from the paper, formatted as requested:

1.  Jaech et al. 2024. Openai o1 system card. This citation refers to OpenAI's O1 model, setting the context for advanced reasoning models which ProRL aims to improve upon. Link: `arXiv preprint arXiv:2412.16720`
2.  Guo et al. 2025. Deepseek-r1: Incentivizing reasoning capability in llms via reinforcement learning. This paper introduces DeepSeek-R1, a key state-of-the-art reasoning model and RL approach that serves as a primary baseline and point of comparison for ProRL. Link: `arXiv preprint arXiv:2501.12948`
3.  Luo et al. 2025. Deepscaler: Surpassing o1-preview with a 1.5b model by scaling rl. This work on DeepScaleR, a math-specialized reasoning model, is an important piece of related research that ProRL (a generalist model) is compared against, particularly in the context of scaling RL for reasoning. Link: `https://pretty-radio-b75.notion.site/DeepScaleR-Surpassing-O1-Preview-with-a-1-5B-Model-by-Scaling-RL-19681902c1468005bed8ca303013a4e2`
4.  Yu et al. 2025. Dapo: An open-source llm reinforcement learning system at scale. Components from the DAPO algorithm are explicitly adopted in ProRL to address entropy collapse and maintain exploration during prolonged RL training.
5.  Yue et al. 2025. Does reinforcement learning really incentivize reasoning capacity in llms beyond the base model?. This citation represents the opposing viewpoint that RL does not genuinely extend reasoning capabilities, a central claim that the current paper directly challenges with its ProRL findings.
6.  Dang et al. 2025. Assessing Diversity Collapse in Reasoning. This work highlights issues like mode collapse in RL for reasoning, which ProRL's techniques (e.g., KL control, policy resets) are designed to mitigate to enable discovery of diverse solutions.
7.  Zhao et al. 2025. Echo chamber: Rl post-training amplifies behaviors learned in pretraining. This paper argues that RL primarily reinforces existing pretrained patterns, contrasting with ProRL's demonstration of learning novel reasoning strategies not apparent in the base model.
8.  Shao et al. 2024. Deepseekmath: Pushing the limits of mathematical reasoning in open language models. This paper is cited as the reference for Group Relative Policy Optimization (GRPO), which forms the core RL algorithm utilized within the ProRL methodology. Link: `arXiv preprint arXiv:2402.03300`
9.  Schulman et al. 2017. Proximal policy optimization algorithms. PPO is a foundational RL algorithm in the field; GRPO (used in ProRL) is presented as an alternative that modifies PPO's approach, for instance, by removing the value model.
10. Lu et al. 2024. Ai as humanity's salieri: Quantifying linguistic creativity of language models via systematic attribution of machine text against web text. This paper introduces the Creativity Index, a metric adopted by the authors of ProRL to quantify the novelty of the reasoning trajectories generated by their RL-trained model compared to pretraining data. (Utilizing details from reference [40] in the paper for completeness.) Link: `ArXiv, abs/2410.04265`
