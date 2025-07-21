https://imle-policy.github.io/

https://x.com/krshnrana/status/1930858454161182735

https://arxiv.org/abs/2502.12371

**IMLE Policy: Fast and Sample Efficient Visuomotor Policy Learning via Implicit Maximum Likelihood Estimation**

### 1. Summary and Rating

This paper introduces IMLE Policy, a novel behaviour cloning approach for visuomotor control that leverages Implicit Maximum Likelihood Estimation (IMLE). The method's primary goal is to address two critical challenges in robotics: sample efficiency and inference speed. Unlike popular generative methods like diffusion policies, which require large datasets and iterative refinement for inference, IMLE Policy is designed to learn multi-modal action distributions effectively from a small number of demonstrations. Its core mechanism is an extension of Rejection-Sampling IMLE (RS-IMLE) to the conditional setting of policy learning. The training objective ensures that for every demonstration in the dataset, at least one generated action sequence is a close match, thereby preventing the model from ignoring less frequent behaviours (mode collapse). This results in a policy that generates diverse and valid actions in a single, fast forward pass. To handle potential mode-switching in multi-modal tasks, the authors also propose a simple and effective inference-time temporal consistency mechanism based on batched trajectory selection. The method is validated across a suite of simulated and real-world manipulation tasks, demonstrating superior sample efficiency and a ~97% inference speedup compared to diffusion policies, while successfully capturing complex, multi-modal behaviours where other single-step methods fail.

**Rating: 9/10**

This is an excellent paper that makes a strong, practical contribution to the field of imitation learning for robotics. The application of IMLE to address the well-known limitations of diffusion models (sample inefficiency and slow inference) is both novel and highly relevant. The experimental validation is rigorous, with direct comparisons to state-of-the-art baselines across multiple benchmarks and real-world tasks, clearly supporting the claims of superior sample and computational efficiency. The qualitative analyses and ablation studies, particularly regarding mode coverage and temporal consistency, add significant depth. For a PhD-level audience, this work is compelling as it presents an elegant, alternative generative modeling framework that directly tackles pressing issues in deploying learned policies on physical hardware. While the training-time nearest-neighbor search could be a scalability concern for massive datasets, the paper focuses on the low-data regime where this is less of an issue and the benefits are most pronounced.

### 2. Main Ideas

1.  **Conditional Rejection-Sampling IMLE for Behaviour Cloning:** The core contribution is the formulation of a behaviour cloning policy using a conditional variant of Rejection-Sampling Implicit Maximum Likelihood Estimation (RS-IMLE). The training objective minimizes the distance between each ground-truth trajectory and its single nearest-neighbor among a set of generated candidate trajectories. This "per-example" loss ensures that the policy learns to cover all modes present in the demonstration data, even those that are rare, leading to exceptional sample efficiency and preventing the mode collapse common in other generative models.

2.  **Fast, Single-Step Multi-Modal Inference:** Unlike diffusion models that require many iterative denoising steps, IMLE Policy is a single-step generative model. It maps a latent vector and an observation directly to a full action sequence in one forward pass. This architectural simplicity results in extremely fast inference speeds, making it suitable for real-time control loops on computationally constrained robotic platforms, without sacrificing the ability to represent multi-modal action distributions.

3.  **Temporal Consistency through Batched Trajectory Selection:** To stabilize policy execution in tasks with multiple valid modes, the paper introduces an inference-time consistency mechanism. At each planning step, the policy generates a batch of candidate action sequences. The chosen sequence is the one that has the minimal deviation from the unexecuted portion of the previously selected plan. This simple heuristic effectively prevents oscillatory behaviour and encourages smooth, coherent trajectories without requiring changes to the model architecture or training process.

### 3. 10 Most Important Citations

1.  **Li et al. (2018). Implicit maximum likelihood estimation.**
    This paper introduces the original IMLE framework, which is the foundational generative modeling objective that IMLE Policy is built upon.

2.  **Vashist et al. (2025). Rejection sampling imle: Designing priors for better few-shot image synthesis.**
    This work introduces the Rejection Sampling (RS-IMLE) variant that the authors adapt, which improves sample quality and training stability, forming the direct technical basis for their method.

3.  **Chi et al. (2023). Diffusion policy: Visuomotor policy learning via action diffusion.**
    This is the primary state-of-the-art baseline method that IMLE Policy is compared against, representing the dominant iterative generative approach for imitation learning that this paper aims to improve upon.
    *   Link: http://www.roboticsproceedings.org/rss19/p026.pdf

4.  **Lipman et al. (N/A). Flow matching for generative modeling.**
    This paper introduces Flow Matching, a powerful alternative to diffusion models, which the authors implement as a key single-step baseline to show that IMLE Policy better preserves multi-modality during fast inference.

5.  **Song et al. (2023). Consistency models.**
    This work on distilling multi-step diffusion models into single-step policies is cited to contextualize the pursuit of fast inference, highlighting that IMLE Policy achieves this natively without a separate distillation stage.
    *   Link: https://arxiv.org/abs/2303.01469

6.  **Mandlekar et al. (2021). What matters in learning from offline human demonstrations for robot manipulation.**
    This paper introduces the Robomimic benchmark and the Proficient-Human (PH) dataset, which is a major simulation environment used for evaluating IMLE Policy's performance.

7.  **Florence et al. (2021). Implicit behavioral cloning.**
    This is an important related work on implicit policies for behaviour cloning that uses Energy-Based Models (EBMs), providing context for alternative approaches to modeling multi-modal action distributions.

8.  **Argall et al. (2009). A survey of robot learning from demonstration.**
    This is a foundational survey that establishes the context and importance of the broader field of imitation learning, the subfield to which this paper contributes.

9.  **Liu et al. (2024). Bidirectional decoding: Improving action chunking via closed-loop resampling.**
    Cited as concurrent work, this paper addresses the same challenge of temporal consistency in multi-modal policies, showing the authors are aware of cutting-edge research on the limitations they discuss.
    *   Link: https://arxiv.org/abs/2408.17355

10. **Zhao et al. (2024). ALOHA unleashed: A simple recipe for robot dexterity.**
    This paper is cited as evidence that state-of-the-art methods like diffusion policies often require very large datasets, which motivates the core goal of IMLE Policy to achieve high performance in low-data regimes.
    *   Link: https://openreview.net/forum?id=gvdXE7ikHI
