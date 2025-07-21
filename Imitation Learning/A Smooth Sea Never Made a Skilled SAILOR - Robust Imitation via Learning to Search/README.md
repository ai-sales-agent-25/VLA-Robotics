https://arxiv.org/abs/2506.05294

A Smooth Sea Never Made a Skilled SAILOR: Robust Imitation via Learning to Search

### 1. Summary and Rating

This paper addresses the fundamental problem of compounding errors in imitation learning, where agents trained via behavioral cloning (BC) fail to recover after making a mistake that takes them outside the state distribution of the expert demonstrations. The authors propose a new framework, SAILOR (Searching Across Imagined Latents Online for Recovery), which shifts the paradigm from simple imitation to "learning to search" (L2S). Instead of only learning a policy, SAILOR uses expert demonstrations to also learn a latent world model (WM) and a reward model (RM). At test time, SAILOR uses its base policy (a Diffusion Policy) to generate a nominal plan, but then refines this plan via local online search using the WM to imagine outcomes and the RM to evaluate them. This allows the agent to proactively correct for potential failures and recover from unseen states.

The training process is structured into three phases for stability and sample efficiency: a "warm-start" phase to initialize the models, an "online fine-tuning" phase where the full SAILOR system collects data to improve its components, and an "expert iteration" phase that distills the successful search-based corrections back into the base policy. Through extensive experiments across 12 visual manipulation tasks, the authors demonstrate that SAILOR significantly outperforms standard Diffusion Policies trained on the same data. Critically, they show that even scaling the demonstration data for BC by 5-10x is insufficient to close the performance gap, providing strong evidence that a more sophisticated reasoning mechanism is required for robust performance.

**Rating: 9/10**

The paper makes a significant contribution by providing a well-motivated and robust solution to the critical issue of compounding errors in imitation learning. The core idea of combining modern world models, reward learning, and online planning into a cohesive "learning to search" framework is both elegant and effective. The experimental results are comprehensive and compelling, particularly the comparison against scaled-up BC, which directly challenges the "more data is all you need" perspective for this problem. The ablations on the training phases are insightful and justify their specific algorithmic design. For a PhD-level audience, this paper presents a high-quality, technically sound, and impactful piece of research that pushes the state-of-the-art in robust robot learning from demonstrations.

### 2. Main Ideas

1.  **Learning to Search (L2S) for Recovery:** The central idea is to move beyond direct policy learning (like BC) and instead use expert data to learn the necessary components for online planning—a world model to predict the future and a reward model to evaluate which futures are good. At test time, this enables the agent to perform a local search in its imagined latent space to find a corrective action sequence that recovers from errors and better matches the expert's intent, a capability BC inherently lacks.
2.  **A Three-Phase Training Pipeline for Stable and Efficient Learning:** The paper proposes a carefully designed training schedule to make the complex system work. It starts with **(1) Warm-Start:** using the base policy to collect initial data for the world and reward models. This is followed by **(2) Online Fine-Tuning:** using the full planning-based agent to collect better, on-policy data to iteratively refine all components. Finally, **(3) Expert Iteration** distills the successful plans discovered via search back into the base policy, making it more competent over time and reducing the reliance on expensive online search.
3.  **The Limits of Scaling Behavioral Cloning:** A key empirical finding is that simply increasing the number of expert demonstrations for a standard BC policy (Diffusion Policy) yields diminishing returns and fails to match the performance of SAILOR. This result serves as strong evidence that for robust robotic control, architectural improvements that enable reasoning and recovery (like L2S) are more critical than simply scaling data with a naive learning algorithm.

### 3. 10 Most Important Citations

1.  **Chi et al. (2023)** *Diffusion policy: Visuomotor policy learning via action diffusion.*
    This paper introduces Diffusion Policies, which SAILOR uses as its base policy and primary baseline, making it a central point of reference and comparison.

2.  **Ratliff et al. (2009)** *Learning to search: Functional gradient techniques for imitation learning.*
    This work is the conceptual origin of the "Learning to Search" (L2S) paradigm that SAILOR modernizes and adapts for high-dimensional visual imitation learning.

3.  **Hafner et al. (2020)** *Dream to control: Learning behaviors by latent imagination.*
    This paper (part of the Dreamer series) introduced a powerful agent that learns a world model and uses it for planning in latent space, providing the architectural foundation for SAILOR's world model.
    *   Link: https://openreview.net/forum?id=S1l0TC4tDS

4.  **Ross et al. (2011)** *A reduction of imitation learning and structured prediction to no-regret online learning.*
    This paper introduced DAgger, a foundational algorithm for mitigating covariate shift via expert queries, which provides the conceptual basis for SAILOR's "Expert Iteration" phase where SAILOR acts as its own expert.

5.  **Swamy et al. (2021)** *Of moments and matching: A game-theoretic framework for closing the imitation gap.*
    This work provides the moment-matching loss function used to train SAILOR's reward model as a discriminator between expert and learner states.

6.  **Williams et al. (2017)** *Model predictive path integral control: From theory to parallel computation.*
    This paper details the Model-Predictive Path Integral (MPPI) control algorithm, which SAILOR employs as its online planner to search for corrective actions within the learned world model.

7.  **Pomerleau (1988)** *Alvinn: An autonomous land vehicle in a neural network.*
    This is the seminal paper on behavioral cloning (BC), the standard imitation learning method whose fundamental limitations (compounding errors) SAILOR is designed to overcome.

8.  **Silver et al. (2018)** *Residual policy learning.*
    This paper's concept of learning a residual policy to correct a primary policy is conceptually linked to SAILOR's approach of learning residual plans to correct a base policy's outputs.

9.  **Ren et al. (2024b)** *Hybrid inverse reinforcement learning.*
    This citation supports SAILOR's methodology of training its world and reward models on a "hybrid" dataset composed of both expert demonstrations and on-policy learner rollouts.
    *   Link: https://arxiv.org/abs/2402.08848

10. **Ziebart et al. (2008)** *Maximum entropy inverse reinforcement learning.*
    This is a foundational paper in inverse reinforcement learning (IRL) that established a principled method for learning reward functions from demonstrations, providing the broader context for SAILOR's reward learning component.
