https://arxiv.org/abs/2506.15799?utm_source=chatgpt.com

Steering Your Diffusion Policy with Latent Space Reinforcement Learning

### 1. Summary and Rating

This paper introduces Diffusion Steering via Reinforcement Learning (DSRL), a novel method for efficiently improving pre-trained robotic policies that are based on diffusion models. The core problem is that while policies learned from demonstrations via behavioral cloning (BC) provide a strong starting point, they often require further refinement to succeed in real-world, open-ended scenarios. Traditional reinforcement learning (RL) fine-tuning of large diffusion models is often sample-inefficient, computationally expensive, and numerically unstable.

DSRL elegantly sidesteps these issues by freezing the weights of the pre-trained diffusion policy and instead learning a separate, lightweight "steering" policy. This steering policy operates in the latent noise space of the diffusion model. Its goal is to select an initial noise vector that, when processed by the frozen diffusion model, results in an action that maximizes the task reward. This reframes the policy improvement problem as a simpler RL task in a latent space, treating the complex diffusion model as a fixed, black-box component of the environment. The authors also propose a specialized actor-critic variant, Noise-Aliased DSRL (DSRL-NA), which leverages offline data to further improve sample efficiency.

The method is validated through extensive experiments on simulated benchmarks, real-world robotic manipulation tasks, and even large-scale generalist robot policies. The results demonstrate that DSRL is highly sample-efficient—achieving significant performance gains with very few online interactions—and effective in online, offline, and offline-to-online settings.

**Rating: 9/10**

This paper presents a simple, clever, and highly effective solution to the critical and challenging problem of adapting large, pre-trained robotic policies. The approach of operating in the latent space is not entirely novel in itself, but its application to modern diffusion policies in robotics, which are notoriously difficult to fine-tune, is a significant and timely contribution. The extensive and compelling empirical evidence, including successful real-world deployment and the steering of a state-of-the-art generalist policy, strongly supports the authors' claims of sample efficiency and practical utility. The work is well-executed and clearly presented, making a valuable contribution to the field.

### 2. Main Ideas

1.  **Latent-Space RL for Diffusion Policy Improvement**: The central idea is to adapt a pre-trained diffusion policy not by changing its weights, but by changing its input. The method freezes the diffusion policy and uses reinforcement learning to train a much smaller, secondary policy that selects the optimal initial noise vector `w` from the latent space. This "steers" the output of the frozen, high-capacity diffusion model towards high-reward actions, avoiding the instability and computational cost of backpropagating through the entire denoising chain.

2.  **Noise-Aliased DSRL (DSRL-NA) for Sample Efficiency**: To further boost sample efficiency, particularly when offline data is available, the paper proposes a specific actor-critic algorithm called DSRL-NA. It leverages the fact that different noise vectors in the latent space can be denoised into the same action. DSRL-NA learns two critics: one in the original action space (which can be trained on standard offline data) and one in the latent-noise space. The latent-space critic distills information from the action-space critic, allowing the agent to infer the value of many latent actions without having to explore them directly, thereby accelerating learning.

3.  **Black-Box, Efficient Adaptation of Generalist Policies**: A key demonstrated strength of DSRL is its ability to serve as a practical, black-box fine-tuning method. Since it only requires forward passes of the base policy, it can adapt proprietary models or models available only through an API. The paper showcases this by successfully steering `πο`, a large state-of-the-art generalist robot policy, improving its performance on downstream tasks dramatically with a small number of real-world interactions—a result that is very difficult to achieve with conventional fine-tuning methods.

### 3. 10 Most Important Citations

1.  **Ho et al. (2020)** Denoising diffusion probabilistic models.
    This paper is foundational for denoising diffusion models, the class of generative models that the base policies in this work are built upon.

2.  **Chi et al. (2023)** Diffusion policy: Visuomotor policy learning via action diffusion.
    This work established diffusion models as a powerful and widely used methodology for imitation learning in robotics, creating the pre-trained policies that DSRL is designed to improve.

3.  **Black et al. (2024)** πρ: A vision-language-action flow model for general robot control.
    This is the state-of-the-art, large-scale generalist robot policy that the authors use to demonstrate the power and scalability of DSRL in a challenging, real-world setting.

4.  **Ren et al. (2024)** Diffusion policy policy optimization.
    This paper represents a key contemporary approach to fine-tuning diffusion policies with RL and serves as a direct, state-of-the-art baseline against which DSRL's superior sample efficiency is demonstrated.

5.  **Singh et al. (2020)** Parrot: Data-driven behavioral priors for reinforcement learning.
    This is the most similar prior work, which also performed RL in the latent space of a generative model, but for normalizing flows; this paper distinguishes itself by tackling the more challenging but more prevalent diffusion models.

6.  **Haarnoja et al. (2018)** Soft actor-critic: Off-policy maximum entropy deep reinforcement learning with a stochastic actor.
    This introduces the SAC algorithm, a standard and highly effective off-policy RL method that is used as a core component for instantiating DSRL.

7.  **Ouyang et al. (2022)** Training language models to follow instructions with human feedback.
    This paper is cited to draw a parallel between DSRL and Reinforcement Learning from Human Feedback (RLHF) in LLMs, motivating the need for efficient RL-based fine-tuning of large pre-trained models.

8.  **Hansen-Estruch et al. (2023)** Idql: Implicit q-learning as an actor-critic method with diffusion policies.
    This introduces IDQL, an important algorithm for offline reinforcement learning with diffusion policies, which serves as a key baseline for evaluating DSRL's performance in the offline setting.

9.  **Ball et al. (2023)** Efficient online reinforcement learning with offline data.
    This work introduces RLPD, a strong method for offline-to-online RL that is used as a baseline in the real-world experiments, where DSRL demonstrates superior adaptation capabilities.

10. **Lipman et al. (2022)** Flow matching for generative modeling.
    This citation is important because the paper shows DSRL's applicability extends beyond diffusion models to flow-based models, and `πο` (a key model they steer) uses a flow-based action head.
