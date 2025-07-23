https://arxiv.org/abs/2505.16517

**Paper:** ManipLVM-R1: Reinforcement Learning for Reasoning in Embodied Manipulation with Large Vision-Language Models

### 1. Summary and Rating

This paper introduces ManipLVM-R1, a novel reinforcement learning framework designed to train Large Vision-Language Models (LVLMs) for robotic manipulation tasks. The authors identify a key limitation in current methodologies: an over-reliance on large, costly, human-annotated datasets for supervised fine-tuning (SFT), which restricts model generalization to new, out-of-domain (OOD) scenarios. To overcome this, ManipLVM-R1 replaces SFT with Reinforcement Learning using Verifiable Rewards (RLVR). This approach trains the model by directly optimizing for task success using rule-based rewards that require no human annotation. The framework decomposes manipulation into two subtasks: affordance perception and trajectory prediction. It introduces specific, structured rewards for each—an "Affordance Perception Reward" based on Intersection-over-Union (IoU) and a "Trajectory Match Reward" using a composite of geometric distance metrics. Experimental results demonstrate that ManipLVM-R1 achieves substantially better performance and generalization than SFT-based counterparts, notably improving affordance detection by 144% (in terms of IoU) while using only 50% of the training data.

**Rating: 8/10**

For a PhD-level audience, this paper is a strong contribution. Its novelty lies in the intelligent application of the RLVR paradigm to the domain of robotic manipulation, directly addressing the well-known bottlenecks of data cost and poor generalization associated with supervised learning. The design of the verifiable, multi-metric reward functions is a thoughtful piece of engineering that effectively tackles the sparse reward problem common in robotics, guiding the model toward learning physically plausible and spatially precise actions. The experimental validation is thorough, with both in-domain and out-of-domain evaluations against relevant and strong baselines. The paper is well-written and the results are compelling. The rating is not a perfect 10 primarily because the work, as acknowledged by the authors, is limited to 2D trajectory prediction and does not yet address the full complexity of 3D robot control or long-horizon tasks, which are critical for real-world deployment. Nonetheless, it establishes a very promising direction for creating more scalable and adaptable robot learning systems.

### 2. Main Ideas

1.  **Applying RLVR to Robotic Manipulation to Bypass Supervised Fine-Tuning:** The central idea is to use Reinforcement Learning with Verifiable Rewards (RLVR) as an alternative to the standard Supervised Fine-Tuning (SFT) approach for training LVLMs in robotics. Instead of learning to imitate a fixed dataset of expert demonstrations, the model learns by optimizing a policy against objective, rule-based reward signals. This approach is designed to reduce dependence on expensive human-annotated data and improve the model's ability to generalize to unseen environments and tasks.

2.  **Structured, Multi-Metric Reward Design for Dense Feedback:** The paper proposes a novel reward design that provides dense and informative feedback, which is crucial for effective reinforcement learning in complex tasks. The authors decompose the problem into affordance perception and trajectory prediction and create tailored rewards for each. The **Affordance Perception Reward** uses Intersection-over-Union (IoU) for spatial accuracy, while the **Trajectory Match Reward** combines multiple geometric metrics (Discrete Fréchet Distance, Hausdorff Distance, and RMSE) to evaluate the entire path, not just the endpoint. This encourages the model to learn a deeper, more systematic understanding of physical interactions rather than just shallow pattern matching.

3.  **Achieving Sample-Efficient Learning and Superior Generalization:** A key finding and contribution is that the RLVR framework is not only effective but also highly sample-efficient. The experiments show that ManipLVM-R1 significantly outperforms models trained with full supervision, even when using only half of the training data. This demonstrates that learning from direct task-based rewards enables the model to develop more robust and generalizable reasoning capabilities, leading to strong performance in both in-domain and, most notably, out-of-domain scenarios.

### 3. 10 Most Important Citations

1.  **Lambert et al. 2024.** T\" ULU 3: Pushing Frontiers in Open Language Model Post-Training
    *   This paper is cited as a key reference for the Reinforcement Learning with Verifiable Rewards (RLVR) training paradigm, which is the foundational methodology adapted by ManipLVM-R1.

2.  **Ji et al. 2025.** Robobrain: A unified brain model for robotic manipulation from abstract to concrete
    *   This work is the primary supervised fine-tuning (SFT) baseline for comparison and is also the source of the "ShareRobot" dataset used for in-domain training and evaluation.

3.  **O'Neill et al. 2024.** Open x-embodiment: Robotic learning datasets and rt-x models: Open x-embodiment collaboration 0
    *   This paper introduced the large-scale Open X-Embodiment dataset, from which the authors' "ShareRobot" training data was curated, making it a critical upstream data source.

4.  **Brohan et al. 2022.** Rt-1: Robotics Transformer for Real-World Control at Scale
    *   Cited as a foundational work in using Transformer-based models for real-world robotic control, establishing a paradigm that subsequent vision-language-action models build upon.

5.  **Huang et al. 2023a.** VoxPoser: Composable 3D Value Maps for Robotic Manipulation with Language Models
    *   This is referenced as a significant related work that also leverages large language models for manipulation tasks, specifically by generating 3D value maps for zero-shot trajectory synthesis.

6.  **Guo et al. 2025.** Deepseek-r1: Incentivizing reasoning capability in llms via reinforcement learning
    *   This work is cited as the inspiration for the Group Relative Policy Optimization (GRPO) update rule used in ManipLVM-R1 and for its findings on emergent reasoning in LLMs.

7.  **Eiter et al. 1994.** Computing Discrete Fréchet Distance.
    *   This paper provides the theoretical basis for the Discrete Fréchet Distance (DFD), a key metric used within the paper's novel Trajectory Match Reward function to measure path similarity.

8.  **Huttenlocher et al. 1993.** Comparing images using the Hausdorff distance
    *   This work introduced the Hausdorff Distance, another core metric integrated into the Trajectory Match Reward to evaluate the maximum deviation between the predicted and ground-truth trajectories.

9.  **Nguyen et al. 2017.** Object-based affordances detection with convolutional neural networks and dense conditional random fields
    *   This paper is the source of the UMD Part Affordance dataset, which was used as the out-of-domain benchmark to evaluate the generalization capability of ManipLVM-R1's affordance perception.

10. **Niu et al. 2024.** LLARVA: Vision-Action Instruction Tuning Enhances Robot Learning
    *   The pre-training dataset from this work, VAIT, was used as the out-of-domain test set for evaluating the generalization of the trajectory prediction task.
