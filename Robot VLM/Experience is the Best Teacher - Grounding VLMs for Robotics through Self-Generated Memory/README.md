https://arxiv.org/abs/2507.16713

Experience is the Best Teacher: Grounding VLMs for Robotics through Self-Generated Memory

### 1. Summary and Rating

This paper presents EXPTEACH, a novel framework for grounding Vision-Language Models (VLMs) in the physical world, enabling a robot to learn from its own real-world experiences. The core problem addressed is that VLMs, despite their powerful reasoning capabilities, lack an intrinsic understanding of a specific robot's physical abilities and limitations. EXPTEACH tackles this by creating a closed-loop system where the robot autonomously plans actions, executes them, uses its VLM to detect success or failure, and reflects on the outcome.

This process leverages a dual-memory system. A **short-term memory (STM)** records the action-feedback history within a single task, allowing the robot to adapt and recover from failures in real-time (e.g., deciding to use a sponge as a tool after failing to push a small object). Upon task completion, the experience is summarized by the VLM and stored in a **long-term memory (LTM)**. This LTM is then used to guide future tasks through retrieval-augmented generation (RAG), allowing the robot to recall relevant past experiences to solve new, similar problems more efficiently. The framework also incorporates an on-demand image annotation module to enhance the VLM's spatial understanding for precise manipulation. The authors demonstrate through extensive real-world experiments that this self-generated memory significantly improves task success rates, boosting single-trial performance from 22% to 80% on a set of 12 scenarios.

**Rating: 9/10**

This is an excellent systems paper that makes a significant empirical contribution to the field of robot learning. It addresses the critical challenge of grounding large pre-trained models in a principled and effective way. The novelty lies in the elegant integration of a VLM as a planner, success detector, and summarizer within a dual-memory architecture that facilitates both immediate adaptation (STM) and long-term generalization (LTM with RAG). The experimental validation is thorough, conducted on a complex real-world robotic platform, and demonstrates impressive performance gains with clear ablation studies. While it builds upon existing concepts like reflection and RAG, its autonomous, closed-loop implementation for physical robot grounding is a substantial step forward. The work provides a strong blueprint for developing more adaptive and competent general-purpose robots.

### 2. Main Ideas

1.  **Autonomous Grounding via a Dual-Memory Architecture:** The central idea is that a robot can teach itself about its own physical capabilities and the environment through experience. This is realized with a two-part memory system. The **Short-Term Memory (STM)** enables in-task learning, where the robot reflects on immediate failures and adapts its strategy, leading to emergent behaviors like creative tool use. The **Long-Term Memory (LTM)** stores summaries of these experiences, which are retrieved using Retrieval-Augmented Generation (RAG) to inform planning in new, but similar, situations. This allows learned knowledge to persist and generalize across tasks.

2.  **A Unified VLM for Closed-Loop Control and Learning:** The framework uniquely employs a single, powerful VLM (GPT-4V) to perform multiple critical functions in a closed loop. The VLM acts as the high-level **task planner**, a **success detector** that provides feedback by observing outcomes, and an **experience summarizer** that condenses the STM into concise knowledge for the LTM. This integration creates a self-sufficient system that can plan, act, evaluate, and learn without needing external supervision or manually engineered feedback signals.

3.  **On-Demand Spatial Grounding for Precise Manipulation:** To overcome the limitations of VLMs in precise spatial reasoning, EXPTEACH incorporates an on-demand image annotation module. When a task requires fine-grained interaction (e.g., grasping the stick of a skewer, not the meat), the system uses segmentation models (Grounded SAM) to overlay numbered candidate interaction points on the image. The VLM can then select the most appropriate point, translating its high-level semantic understanding into a precise, spatially-grounded action.

### 3. 10 Most Important Citations

1.  **Ahn et al. (2022)** *Do as i can, not as i say: Grounding language in robotic affordances.*
    This is a foundational paper that grounds language models in a robot's skills, enabling the model to generate feasible action plans, a core concept that EXPTEACH builds upon.
    (Link: https://arxiv.org/abs/2204.01691)

2.  **Liang et al. (2023)** *Code as policies: Language model programs for embodied control.*
    This work introduced the idea of having LLMs generate robot policy code directly, influencing the paradigm of using large language models for high-level robot task planning.
    (Link: https://arxiv.org/abs/2209.07753)

3.  **Lewis et al. (2020)** *Retrieval-augmented generation for knowledge-intensive nlp tasks.*
    This paper introduced Retrieval-Augmented Generation (RAG), the fundamental mechanism EXPTEACH uses for its long-term memory to retrieve relevant past experiences and guide future planning.
    (Link: https://arxiv.org/abs/2005.11401)

4.  **Shinn et al. (2023)** *Reflexion: Language agents with verbal reinforcement learning.*
    This paper introduced a method for agents to reflect on failures and generate verbal feedback to improve subsequent attempts, which is a core inspiration for the self-reflection mechanism in EXPTEACH's short-term memory.
    (Link: https://arxiv.org/abs/2303.11366)

5.  **Achiam et al. (2023)** *Gpt-4 technical report.*
    This report details the capabilities of GPT-4, the powerful VLM that serves as the backbone for planning, detection, and summarization in the EXPTEACH framework.
    (Link: https://arxiv.org/abs/2303.08774)

6.  **Brohan et al. (2023)** *Rt-2: Vision-language-action models transfer web knowledge to robotic control.*
    This work demonstrated that a VLM can be directly trained as a robotic policy, translating visual and language commands into actions, highlighting the potential of such models that EXPTEACH aims to ground.
    (Link: https://arxiv.org/abs/2307.15818)

7.  **Zhi et al. (2024)** *Closed-loop open-vocabulary mobile manipulation with gpt-4v.*
    This paper (ComeRobot) is used as a direct experimental baseline in EXPTEACH to demonstrate the significant performance improvement gained from using long-term memory.
    (Link: https://arxiv.org/abs/2404.10220)

8.  **Liu et al. (2023)** *Reflect: Summarizing robot experiences for failure explanation and correction.*
    This work focuses specifically on summarizing robot experiences to explain and correct failures, a concept highly relevant to the reflection and memory summarization modules in EXPTEACH.
    (Link: https://openreview.net/forum?id=vSMEzP5vlS)

9.  **Sarch et al. (2024)** *Vlm agents generate their own memories: Distilling experience into embodied programs of thought.*
    This citation is directly related as it also explores how VLM-based agents can autonomously generate their own memories by distilling experiences, which aligns with the core thesis of EXPTEACH.
    (Link: https://arxiv.org/abs/2309.06149)

10. **Ren et al. (2024)** *Grounded sam: Assembling open-world models for diverse visual tasks.*
    This paper describes the Grounded SAM model, which is a critical technical component of EXPTEACH's on-demand image annotation tool for enabling precise object segmentation and interaction.
    (Link: https://arxiv.org/abs/2401.14159)
