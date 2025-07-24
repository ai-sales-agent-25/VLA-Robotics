https://arxiv.org/abs/2505.22094

**ReinFlow: Fine-tuning Flow Matching Policy with Online Reinforcement Learning**

### 1. Summary and Rating

This paper introduces ReinFlow, a novel and effective framework for fine-tuning pre-trained flow matching policies for robotic control using online reinforcement learning (RL). The core problem addressed is that policies trained via imitation learning on imperfect data are often suboptimal and lack a mechanism for exploration and self-improvement. ReinFlow tackles this by injecting learnable, state-conditioned noise into the deterministic generation process of a flow policy. This key step transforms the policy into a discrete-time Markov process, which allows for the exact and tractable computation of action log-probabilities. This, in turn, enables the direct application of standard policy gradient algorithms, like PPO, for stable online fine-tuning.

The authors demonstrate ReinFlow's effectiveness across a variety of robotic locomotion and manipulation tasks, including those with sparse rewards and visual inputs. The framework is shown to be versatile, successfully fine-tuning different flow model variants like Rectified Flow and Shortcut Models. Empirically, ReinFlow achieves substantial performance gains, with an average reward increase of 135.36% in locomotion tasks and a success rate increase of 40.34% in manipulation tasks. A significant practical advantage is its computational efficiency; by enabling fine-tuning with very few (even a single) denoising steps, it reduces wall-clock time by an average of 62.82% compared to the state-of-the-art diffusion policy fine-tuning method, DPPO. The paper supports its algorithmic design with a policy gradient theorem tailored for the proposed noise-injected process.

**Rating: 9/10**

This is a high-quality paper that makes a novel and significant contribution to the intersection of generative models and reinforcement learning for robotics. The central idea of converting a deterministic flow into a stochastic Markov process via learnable noise injection is both elegant and effective, cleanly solving the problem of applying policy gradient RL to this model class. The theoretical justification, coupled with extensive and strong empirical results on challenging, relevant benchmarks, is compelling. The demonstrated computational efficiency is a major practical advantage that the robotics community will value highly. The work is well-positioned against prior art and clearly articulates its advantages over existing methods for both diffusion and flow models.

### 2. Main Ideas

1.  **Stochasticizing Flow Policies for Online RL:** The primary idea is a novel method to make deterministic flow matching policies compatible with online policy gradient RL. By injecting learnable Gaussian noise at each discrete step of the generation process, the authors convert the policy's deterministic ODE trajectory into a stochastic, discrete-time Markov process. This allows for an exact, closed-form computation of the policy's log-likelihood, which is essential for policy gradient methods but notoriously difficult to compute for continuous-time flow models. This circumvents the need for unstable numerical divergence estimators and enables stable fine-tuning.

2.  **An Efficient and General Fine-Tuning Framework:** ReinFlow is presented as a general framework that stably fine-tunes a family of flow matching policies (e.g., Rectified Flow, Shortcut Models) using online RL. A key aspect of this framework is its efficiency. It can dramatically improve policy performance even when using very few (or a single) denoising steps for inference. This significantly reduces the wall-clock time for both training rollouts and final execution compared to methods that fine-tune diffusion models (like DPPO), which typically require more steps. This makes the approach highly practical for real-world robotics where inference speed is critical.

3.  **Principled Exploration with a Discardable Noise Network:** The framework introduces a dedicated noise injection network that is trained jointly with the original flow model's velocity network using the same RL objective. This allows the agent to learn an adaptive exploration strategy, automatically adjusting the magnitude of the injected noise to balance exploration and exploitation. After fine-tuning is complete, this auxiliary noise network is discarded, and the policy reverts to its original fast, deterministic form for deployment, incurring no additional architectural overhead at inference time.

### 3. 10 Most Important Citations

1.  Lipman et al. (2023). Flow matching for generative modeling.
    This paper introduces the foundational concept of flow matching, which is the core generative modeling technique that ReinFlow is built to fine-tune.

2.  Liu et al. (2022). Flow straight and fast: Learning to generate and transfer data with rectified flow.
    This citation is crucial as it introduces Rectified Flow (ReFlow), a simplified and powerful flow model variant that the authors use as a primary example (ReinFlow-R) to demonstrate their method's effectiveness.
    Link: https://arxiv.org/abs/2209.03003

3.  Ren et al. (2024). Diffusion policy policy optimization.
    This paper presents DPPO, the state-of-the-art online RL algorithm for fine-tuning *diffusion* policies, which serves as the main high-performance baseline that ReinFlow is benchmarked against.

4.  Park et al. (2025). Flow q-learning.
    This work (FQL) represents the state-of-the-art for *offline* RL with flow models, and the paper uses it as a key point of comparison to highlight ReinFlow's novelty and superior performance as an *online* RL method.

5.  Schulman et al. (2017). Proximal policy optimization algorithms.
    This citation is fundamental to the paper's implementation, as PPO is the specific on-policy RL algorithm used as the optimization subroutine within the ReinFlow framework.

6.  Agarwal et al. (2021). On the theory of policy gradient methods: Optimality, approximation, and distribution shift.
    This work provides the modern theoretical foundation for policy gradient methods, upon which the paper's own theoretical derivations for noise-injected flows (Theorem 4.1) are built.

7.  Chen et al. (2018). Neural ordinary differential equations.
    This paper is foundational for continuous-time generative models, establishing the connection between neural networks and ordinary differential equation solvers that underpins flow matching models.

8.  Frans et al. (2024). One step diffusion via shortcut models.
    This paper introduces Shortcut Models, another advanced flow matching variant that the authors use (as ReinFlow-S) to demonstrate the generality and flexibility of their ReinFlow framework.
    Link: https://arxiv.org/abs/2410.12557

9.  Fu et al. (2021). D4{r1}: Datasets for deep data-driven reinforcement learning.
    This paper describes the D4RL benchmark dataset, which was used to pre-train the policies for the OpenAI Gym locomotion tasks, making it essential for reproducing and understanding the experimental setup.

10. Mandlekar et al. (2022). What matters in learning from offline human demonstrations for robot manipulation.
    This work introduces the Robomimic suite, including the environments and datasets used for the challenging visual manipulation experiments in the paper.
