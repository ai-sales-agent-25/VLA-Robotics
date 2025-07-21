https://arxiv.org/abs/2412.06685

**Policy Agnostic RL: Offline RL and Online RL Fine-Tuning of Any Class and Backbone**

---

### 1. Brief summary & rating

The paper introduces **Policy-Agnostic Reinforcement Learning (PA-RL)**, a two-stage actor-critic procedure that *decouples* policy improvement from policy parameter updates.

1. **Action optimisation stage.** Multiple candidate actions are sampled from the current policy, globally re-ranked by the critic and then locally nudged with gradient ascent to maximise Q-value.
2. **Supervised distillation stage.** The policy is trained to imitate the “optimised” actions with a standard likelihood-based loss (cross-entropy for autoregressive transformers, DDPM noise-prediction loss for diffusion models).

Because gradients never flow through the policy, the same algorithm works for Gaussian, diffusion and autoregressive transformer policies, and it plugs into existing critics such as IQL and Cal-QL without modification .

Extensive experiments on D4RL AntMaze, FrankaKitchen and CALVIN as well as three real-robot manipulation tasks show state-of-the-art offline performance and up to **2 ×** higher sample-efficiency during online fine-tuning relative to IDQL, DQL, DPPO and Cal-QL baselines . Notably, PA-RL is the first method to fine-tune a 7 B-parameter OpenVLA foundation model on a real robot, lifting zero-shot success from 40 % to 70 % in 40 minutes .

**Rating (PhD-oriented): 9 / 10.**
*Strengths:* elegant algorithmic decoupling; broad policy-class coverage; thorough ablations; compelling real-world validation.
*Weaknesses:* action sampling and gradient steps impose non-trivial inference cost; theoretical analysis of convergence is limited.

---

### 2. Key ideas

| Idea                                                                    | Explanation                                                                                                                                                                                                  | Evidence |
| ----------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | -------- |
| **Action-space optimisation instead of parameter-space gradients**      | PA-RL treats the critic as a search objective, performing global re-ranking followed by local gradient steps *on actions* to sidestep policy-gradient pathologies for diffusion and discrete token policies. |          |
| **Universal supervised distillation loss**                              | After optimisation, the best (or a Q-weighted set of) actions are cloned with a standard supervised loss, letting practitioners reuse mature training stacks for diffusion or transformer models.            |          |
| **Plug-and-play with existing critics across offline → online regimes** | By swapping only the policy-update rule, PA-RL seamlessly pairs with IQL or Cal-QL critics, achieving consistent gains in offline, hybrid and online fine-tuning scenarios.                                  |          |

---

### 3. Ten influential citations

| #  | Reference                                                                                                                                                                            | Relevance to PA-RL                                                                                                                              |
| -- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | ----------------------------------------------------------------------------------------------------------------------------------------------- |
| 1  | Haarnoja et al., 2018. *Soft Actor-Critic: Off-Policy Maximum Entropy Deep RL with a Stochastic Actor.* [https://arxiv.org/pdf/1801.01290.pdf](https://arxiv.org/pdf/1801.01290.pdf) | Baseline Gaussian actor-critic whose reparameterised gradient becomes unstable for diffusion/AR policies, motivating PA-RL’s decoupled update . |
| 2  | Kumar et al., 2020. *Conservative Q-Learning for Offline RL.*                                                                                                                        | Provides the pessimistic value-learning principle that PA-RL inherits via Cal-QL critic .                                                       |
| 3  | Kostrikov et al., 2022. *Offline RL with Implicit Q-Learning.*                                                                                                                       | IQL forms the policy-agnostic critic alternative evaluated alongside Cal-QL .                                                                   |
| 4  | Nakamoto et al., 2024. *Cal-QL: Calibrated Offline RL Pre-training for Efficient Online Fine-Tuning.*                                                                                | The main critic algorithm paired with PA-RL in simulation and real-robot studies .                                                              |
| 5  | Hansen-Estruch et al., 2023. *IDQL: Implicit Q-Learning as an Actor-Critic Method with Diffusion Policies.*                                                                          | Strong diffusion-policy baseline that PA-RL substantially outperforms .                                                                         |
| 6  | Chi et al., 2023. *Diffusion Policy: Visuomotor Policy Learning via Action Diffusion.*                                                                                               | Supplies the diffusion-policy architecture fine-tuned by PA-RL .                                                                                |
| 7  | Ren et al., 2024. *Diffusion Policy Policy Optimisation.*                                                                                                                            | Alternative diffusion-based RL algorithm contrasted with PA-RL in ablations .                                                                   |
| 8  | Chebotar et al., 2023. *Q-Transformer: Scalable Offline RL via Autoregressive Q-Functions.*                                                                                          | Highlights challenges of token-level autoregressive policies that PA-RL addresses .                                                             |
| 9  | Fu et al., 2020. *D4RL: Datasets for Deep Data-Driven RL.*                                                                                                                           | Standardised offline benchmarks used for PA-RL evaluation .                                                                                     |
| 10 | Levine et al., 2020. *Offline Reinforcement Learning: Tutorial, Review, and Perspectives.*                                                                                           | Surveys the offline RL landscape, framing the need for safe policy optimisation that PA-RL advances .                                           |

---
