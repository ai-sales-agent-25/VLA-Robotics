https://arxiv.org/abs/2505.01399

**Dynamic Robot Tool Use with Vision Language Models**

### 1. Summary and Rating

This paper introduces the Inverse Tool-Use Planning (iTUP) framework, a novel system designed to enable robots to perform a variety of tool-use tasks, with a particular focus on dynamic interactions. The authors identify two primary challenges in existing research: the lack of fine-grained, open-vocabulary understanding and the failure to account for the physical dynamics (e.g., torques) involved in high-force tasks. iTUP addresses these gaps by integrating a Vision-Language Model (VLM) for semantic understanding with physics-informed planning.

The framework operates through a hierarchical grounding process. First, in "Coarse Grounding," a VLM identifies the appropriate tool and target object from a scene based on a natural language command. Then, in "Fine Grounding," the VLM specifies the exact contact points on both the tool and the object, along with the interaction direction. Crucially, the system plans backward from this desired tool-object interaction to determine a suitable motion trajectory. This trajectory information is then used by the "Stable Dynamic Grasp Network" (SDG-Net), a custom physics-informed network, to select a grasp pose that minimizes predicted torque and instability during the dynamic task. The authors evaluate iTUP in both simulation and the real world on quasi-static, dynamic (hammering), and cluster (sweeping) tasks, demonstrating superior performance (76.67% success rate) compared to a baseline (CoPa) and ablation versions of their own model.

**Rating: 8.5/10**

For a PhD-level audience, this paper is a strong contribution. Its primary strength lies in its novel synthesis of large-scale semantic reasoning (from VLMs) with low-level, physics-aware motion and grasp planning specifically for *dynamic* tool use. The concept of "inverse planning" from the point of interaction is an intelligent way to constrain the problem, ensuring that the physical requirements of the task's climax inform all prior steps, including grasping. The introduction of SDG-Net to explicitly optimize grasps against interaction forces and torques is a significant and necessary step beyond existing methods that often treat grasping as a static precursor to the task. The empirical results, including real-world experiments and targeted ablation studies, are thorough and effectively validate the contributions of the framework's key components. The paper is well-structured and clearly articulates its novelties. It loses minor points for its reliance on a modular pipeline, which can be prone to compounding errors, and for limitations in its trajectory planner, which does not account for collisions—both of which the authors acknowledge.

### 2. Main Ideas

1.  **Inverse Tool-Use Planning (iTUP):** The core methodological idea is to structure the planning process in reverse. Instead of selecting a tool, grasping it, and then planning a motion, iTUP starts by using a VLM to determine the desired goal state—the precise contact points and interaction forces between the tool and the target. The robot's trajectory and grasp are then derived backward from these physical constraints. This "inverse" approach ensures that the entire plan is grounded in the physical requirements of the most critical part of the task.

2.  **Physics-Informed Grasping for Dynamic Tasks:** The paper argues that most prior work fails by using grasp planners designed for static picking, which are inadequate for dynamic tasks involving significant forces and torques (e.g., hammering). To solve this, the authors introduce the Stable Dynamic Grasp Network (SDG-Net). This network scores potential grasps not just on static stability but on their ability to resist the specific torques predicted to occur during the planned dynamic interaction, leading to more robust tool manipulation.

3.  **Hierarchical VLM-driven Grounding:** The framework uses a VLM in a two-stage process to bridge high-level language instructions with low-level physical parameters. The "Coarse Grounding" stage identifies the relevant objects (e.g., "hammer," "nail"). The "Fine Grounding" stage then reasons about *how* to use the tool, specifying the exact contact points (e.g., "head of the hammer," "top of the nail") and interaction vectors, which are essential inputs for the downstream inverse planning modules.

### 3. 10 Most Important Citations

1.  **Toussaint et al. (2018)** Differentiable physics and stable modes for tool-use and manipulation planning.
    This paper is foundational for planning complex, dynamic interactions by incorporating physics into the optimization process, which aligns with iTUP's goal of handling dynamic constraints.

2.  **Qin et al. (2023)** Robot tool use: A survey.
    This citation provides a comprehensive overview of the field, establishing the context and challenges (like generalization and dynamic interactions) that the iTUP framework aims to address.

3.  **Huang et al. (2024)** Copa: General robotic manipulation through spatial constraints of parts with foundation models.
    This paper is used as the primary experimental baseline (CoPa), making it critical for evaluating the performance and novelty of iTUP.
    *   **Link:** https://openreview.net/forum?id=H0tu0qfBL1

4.  **Wei et al. (2023)** Chain-of-thought prompting elicits reasoning in large language models.
    This work is cited as a key technique for enhancing the VLM's reasoning capabilities, which is fundamental to iTUP's hierarchical grounding module.

5.  **Yang et al. (2023)** Set-of-mark prompting unleashes extraordinary visual grounding in gpt-4v.
    The "Set-of-Mark" prompting technique is explicitly used in the paper's coarse grounding stage to segment the scene and identify objects, making this a direct methodological building block.
    *   **Link:** https://arxiv.org/abs/2310.11441

6.  **Gao et al. (2024)** Physically grounded vision-language models for robotic manipulation.
    This represents highly relevant concurrent work on physically grounding VLMs, highlighting the area of research to which this paper contributes and distinguishes itself from.

7.  **Mahler et al. (2017)** Dex-net 2.0: Deep learning to plan robust grasps with synthetic point clouds and analytic grasp metrics.
    This is a landmark paper in data-driven grasp planning, and its associated GQ-CNN is used as a baseline in Table 1 to show the superiority of the proposed SDG-Net for dynamic tasks.

8.  **Fang et al. (2023)** Anygrasp: Robust and efficient grasp perception in spatial and temporal domains.
    Cited as a state-of-the-art grasp generation method, it helps frame the high standard of performance in modern grasp planning and serves as a point of contrast for iTUP's task- and physics-aware approach.

9.  **Sundermeyer et al. (2021)** Contact-graspnet: Efficient 6-dof grasp generation in cluttered scenes.
    This is another significant and frequently-cited method for grasp pose generation, mentioned in the related work to situate the paper's contributions within the broader field of grasp planning.

10. **Duan et al. (2025)** AHA: A vision-language-model for detecting and reasoning over failures in robotic manipulation.
    This citation points to the frontier of using VLMs to understand and reason about robot interactions, a capability that is central to the high-level cognitive component of the iTUP framework.
    *   **Link:** https://openreview.net/forum?id=JVkdSi7Ekg
