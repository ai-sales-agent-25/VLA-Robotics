https://arxiv.org/abs/2206.11795

**Video PreTraining (VPT): Learning to Act by Watching Unlabeled Online Videos**

### 1. Summary and Rating

**Summary:**
This paper introduces Video PreTraining (VPT), a semi-supervised method for training agents in sequential decision-making domains by leveraging massive amounts of unlabeled online video data. The core problem is that while internet-scale data has fueled progress in NLP and computer vision, similar data for domains like robotics and gaming often lacks action labels, making imitation learning difficult. The authors demonstrate their method in Minecraft, a complex, open-ended environment.

The VPT method consists of two main stages. First, they collect a small dataset of labeled gameplay (~2,000 hours) from contractors and use it to train an Inverse Dynamics Model (IDM). The IDM is a non-causal model that predicts the action taken at a specific timestep given both past and future video frames. The authors show this task is far more data-efficient than learning a policy directly. Second, this accurate IDM is used to generate pseudo-labels for a huge dataset of unlabeled Minecraft videos scraped from the internet (~70,000 hours). A large, causal transformer-based model is then trained via behavioral cloning on this massive, pseudo-labeled dataset to create a "VPT foundation model."

This pre-trained model exhibits impressive zero-shot capabilities, such as chopping trees and crafting basic items. The paper's most significant contribution is showing that this model can be fine-tuned to solve extremely difficult, long-horizon tasks that are impossible to solve with reinforcement learning (RL) from scratch. Through fine-tuning with a combination of behavioral cloning and RL, their agent becomes the first to successfully craft a diamond pickaxe—a task requiring a sequence of over 24,000 actions that takes a proficient human over 20 minutes to complete. The work provides a generalizable and highly effective recipe for bootstrapping capable agents in complex domains where unlabeled video is abundant but labeled actions are scarce.

**Rating: 9.5/10**

This paper represents a landmark achievement in reinforcement learning and imitation learning. For a PhD-level audience, its strengths are numerous:
*   **Conceptual Elegance:** It successfully extends the "pre-train on the internet" paradigm to sequential decision-making. The two-stage IDM-then-BC approach is a simple but powerful solution to the problem of sparse action labels.
*   **Methodological Rigor and Scale:** The experiments are conducted at a massive scale (70k hours of video, 500M parameter models, extensive RL fine-tuning). The authors perform insightful ablations, validating key hypotheses such as the data efficiency of the IDM over behavioral cloning and the critical importance of the pre-trained prior (via a KL-divergence loss) for preventing catastrophic forgetting during RL fine-tuning.
*   **Significance of Results:** Crafting a diamond pickaxe in Minecraft using the native human interface (20Hz mouse/keyboard) is a state-of-the-art result that solves a long-standing, hard-exploration grand challenge for the field. It convincingly demonstrates a viable path toward solving long-horizon, sparse-reward tasks.
*   **Impact and Generalizability:** The VPT framework provides a clear, general recipe that could be applied to other important domains like robotics or general computer usage, paving the way for a new class of capable, data-driven agents.

The paper is an exceptional piece of research that combines a clever idea with massive-scale engineering and experimentation to push the boundaries of what is possible in AI.

### 2. Main Ideas

1.  **Semi-Supervised Imitation Learning via an Inverse Dynamics Model (IDM):** The central idea is to unlock the potential of vast unlabeled video datasets for imitation learning. The key is to first train an IDM on a much smaller, manageable set of labeled data (action-video pairs). This IDM learns the relatively simple task of inferring an action from surrounding video frames. This model is then used as a cheap, automatic tool to generate "pseudo-action-labels" for the massive unlabeled video corpus, effectively converting an intractable labeling problem into a large-scale, supervised learning problem.

2.  **Pre-training Foundational Behavioral Priors for Hard-Exploration RL:** The paper demonstrates that training a large model on this internet-scale (pseudo-labeled) data produces a powerful "behavioral prior." This pre-trained model learns a wide range of basic skills and latent behaviors present in the data. This prior is an exceptionally effective starting point for fine-tuning. For hard-exploration RL tasks with sparse rewards, this prior guides the agent toward useful parts of the state space, making it possible to learn tasks (like obtaining a diamond pickaxe) that are statistically impossible to solve with RL from a random initialization.

3.  **Data Efficiency of IDM vs. Behavioral Cloning (BC):** A crucial hypothesis and finding is that learning an inverse dynamics model is fundamentally easier and more data-efficient than learning a behavioral cloning policy. The IDM is non-causal (it can see the future) and only needs to learn the deterministic mechanics of the environment (e.g., what mouse movement corresponds to a crosshair change). In contrast, a BC policy is causal and must learn the much more complex distribution of human intent. The paper empirically shows the IDM achieves high performance with orders of magnitude less data, which is the key insight that makes the entire VPT pipeline practical and cost-effective.

### 3. Top 10 Citations

1.  **Brown et al. 2020. Language models are few-shot learners.**
    This paper on GPT-3 is the canonical example of a "foundation model" trained on internet-scale data, a paradigm that this paper explicitly aims to extend to sequential decision-making domains.

2.  **Torabi et al. 2018. Behavioral cloning from observation.**
    This is cited as one of the most similar prior works, as it also trains an IDM to enable behavioral cloning from observation, but the VPT paper scales this concept to a vastly larger and more complex setting and decouples the IDM and BC training stages.

3.  **Vinyals et al. 2019. Grandmaster level in starcraft ii using multi-agent reinforcement learning.**
    This work (AlphaStar) is a key example of using imitation learning on a large dataset of human gameplay as a crucial bootstrapping mechanism for a state-of-the-art reinforcement learning agent.

4.  **Aytar et al. 2018. Playing hard exploration games by watching youtube.**
    This paper shares the high-level goal of learning from online videos but uses them to learn a reward function to guide an RL agent, whereas VPT directly learns a behavioral policy prior.

5.  **Ecoffet et al. 2021. First return, then explore.**
    This highlights the extreme difficulty of hard-exploration problems for pure RL agents, providing context for the necessity of the powerful priors that VPT learns.

6.  **Guss et al. 2019. Minerl: A large-scale dataset of minecraft demonstrations.**
    This introduced a major competition and dataset for Minecraft, catalyzing research in the domain and establishing a benchmark for imitation learning that VPT's approach ultimately surpasses.

7.  **Kirkpatrick et al. 2017. Overcoming catastrophic forgetting in neural networks.**
    This provides the foundational concept for understanding catastrophic forgetting, a problem that VPT addresses during RL fine-tuning by using a KL-divergence loss to the original, frozen pre-trained policy.

8.  **Ho et al. 2016. Generative adversarial imitation learning.**
    This paper introduced GAIL, a seminal method for imitation learning from observations, which represents a popular alternative approach that the authors contrast with their simpler and more scalable method.

9.  **Cobbe et al. 2021. Phasic policy gradient.**
    This is the specific, modern reinforcement learning algorithm used for the fine-tuning experiments, making it a critical methodological citation for the paper's RL results.
    *Link: https://proceedings.mlr.press/v139/cobbe21a.html*

10. **Silver et al. 2016. Mastering the game of go with deep neural networks and tree search.**
    This landmark AlphaGo paper demonstrated the power of combining supervised learning on human expert data with self-play reinforcement learning, a hybrid approach philosophically similar to VPT's use of data priors to bootstrap RL.
