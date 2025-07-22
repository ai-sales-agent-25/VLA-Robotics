https://arxiv.org/abs/2411.19309

GRAPE: Generalizing Robot Policy via Preference Alignment

### 1. Summary and Rating

This paper introduces GRAPE (Generalizing Robot Policy via Preference Alignment), a novel framework designed to improve the generalization capabilities of Vision-Language-Action (VLA) models in robotics. The authors identify a key weakness in existing VLA models: their reliance on supervised fine-tuning (SFT) using only successful expert demonstrations. This approach leads to poor performance on unseen tasks and a failure to adapt to diverse objectives like safety or efficiency.

To address this, GRAPE employs Trajectory-wise Preference Optimization (TPO), a technique inspired by recent advances in aligning large language models. This allows the policy to learn from both successful and failed trajectories, creating an implicit reward model that leads to a more robust and global understanding of tasks. The most significant contribution is the **Guided-Cost Preference Generation (GCPG)** pipeline, which automates the creation of preference data. GCPG uses a Vision-Language Model (VLM) to decompose complex tasks into temporal stages and identify keypoints. Subsequently, a large language model (like GPT-4) generates customized, stage-specific cost functions based on high-level goals (e.g., task completion, safety). The final policy is trained iteratively by sampling trajectories, ranking them using a composite reward score, and using the resulting preference pairs to fine-tune the model.

Experiments conducted in both simulated and real-world environments show that GRAPE significantly outperforms state-of-the-art baselines like OpenVLA and Octo, increasing success rates on unseen tasks by up to 58.20%. Furthermore, the framework demonstrates the flexibility to align with specific objectives, successfully reducing collision rates by 37.44% for a safety-focused policy and rollout step-length by 11.15% for an efficiency-focused one.

**Rating: 9/10**

For a PhD-level audience, this paper is excellent. It presents a methodologically sound and novel solution to the critical and well-known problem of generalization in robot learning. The primary contribution—automating the generation of scalable, objective-driven preference feedback using large models—is both clever and highly practical, directly addressing the bottlenecks of reward engineering and human annotation. The technical approach is a well-motivated synthesis of ideas from LLM alignment (DPO/TPO) and robotics (task decomposition). The experimental validation is comprehensive, with strong baselines, extensive ablations, and convincing results in both simulation and the real world that directly support the paper's claims of improved generalization and flexible objective alignment. The work represents a significant step forward in making learned robot policies more robust and adaptable.

### 2. Main Ideas

1.  **Trajectory-wise Preference Optimization for Robot Policies**: The central idea is to shift from standard behavior cloning on successful trajectories to a preference-based reinforcement learning approach. By optimizing the policy based on preferences between entire trajectories (e.g., a successful vs. a failed one), the model learns a more holistic understanding of the task objectives. This use of both positive and negative examples allows it to generalize better than models that only ever see perfect demonstrations.

2.  **Automated and Guided Preference Generation**: The paper's most novel contribution is the Guided-Cost Preference Generation (GCPG) pipeline, which makes preference-based learning scalable. Instead of requiring laborious human feedback, GRAPE uses a VLM to automatically segment tasks into stages and an LLM to generate corresponding cost functions based on customizable, high-level goals like "safety" or "efficiency." This allows for the automatic creation of a rich training signal that guides the policy toward desired behaviors without manual reward engineering.

3.  **Flexible Alignment with Diverse Objectives**: A direct result of the GCPG pipeline is the ability to easily customize the robot's behavior. By simply changing the textual prompts used to generate the cost functions, the same GRAPE framework can be used to train policies that prioritize different objectives. The paper demonstrates this effectively by creating separate models for task completion, safety (collision avoidance), and efficiency (path length), each outperforming the baseline in its respective domain.

### 3. 10 Most Important Citations

1.  **Rafailov et al. (2024)** Direct preference optimization: Your language model is secretly a reward model.
    *   This paper introduced Direct Preference Optimization (DPO), the foundational algorithm that GRAPE's Trajectory-wise Preference Optimization (TPO) loss is derived from and directly builds upon.

2.  **Kim et al. (2024)** Openvla: An open-source vision-language-action model.
    *   OpenVLA is used as the primary backbone model for GRAPE and serves as the main state-of-the-art baseline for experimental comparison, making this a critical foundational work.

3.  **Schulman et al. (2017)** Proximal policy optimization algorithms.
    *   This paper introduced PPO, a benchmark reinforcement learning algorithm that the authors mention as a powerful but often impractical alternative for VLA training, setting the context for why a more sample-efficient, preference-based RL method like GRAPE is needed.

4.  **Huang et al. (2024)** Rekep: Spatio-temporal reasoning of relational keypoint constraints for robotic manipulation.
    *   GRAPE's method for decomposing complex tasks into temporal stages with keypoint constraints is directly built upon insights from this work, forming a core component of the automated cost generation pipeline.

5.  **Team et al. (2024)** Octo: An open-source generalist robot policy.
    *   Octo is another major state-of-the-art generalist robot policy that is used as a key baseline in the paper's experimental evaluations.

6.  **Christiano et al. (2017)** Deep reinforcement learning from human preferences.
    *   This is a seminal paper that established the viability of using human preferences to guide reinforcement learning, providing the fundamental motivation for preference-based alignment methods like GRAPE.

7.  **Achiam et al. (2023)** Gpt-4 technical report.
    *   The paper explicitly uses a "powerful LLM" based on this work (GPT-4) to automatically generate customized cost functions, which is a critical step in the Guided-Cost Preference Generation (GCPG) pipeline.

8.  **Brohan et al. (2023)** Rt-2: Vision-language-action models transfer web knowledge to robotic control.
    *   This paper on RT-2 represents the class of large-scale, state-of-the-art VLA models whose limitations (poor generalization from SFT) GRAPE aims to address, providing essential context for the problem statement.

9.  **Bai et al. (2022)** Training a helpful and harmless assistant with reinforcement learning from human feedback.
    *   This paper on RLHF is cited to frame GRAPE's approach within the broader, successful paradigm of aligning foundation models using preference data, connecting robotics to recent breakthroughs in LLMs.

10. **Hu et al. (2022)** LoRA: Low-rank adaptation of large language models. [https://openreview.net/forum?id=nZeVKeeFYf9](https://openreview.net/forum?id=nZeVKeeFYf9)
    *   The authors explicitly state they use LoRA for parameter-efficient fine-tuning of the OpenVLA model during both the supervised and preference alignment stages, making it a key implementation detail for their method.
