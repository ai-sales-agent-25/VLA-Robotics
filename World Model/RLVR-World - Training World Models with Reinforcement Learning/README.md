https://arxiv.org/abs/2505.13934v1

**RLVR-World: Training World Models with Reinforcement Learning**

### 1. Summary and Rating

This paper presents RLVR-World, a unified framework for improving pre-trained world models by post-training them with Reinforcement Learning with Verifiable Rewards (RLVR). The central thesis is that standard training objectives for generative models, such as Maximum Likelihood Estimation (MLE), are often misaligned with the ultimate task-specific goals of a world model, like achieving high state-prediction accuracy or good perceptual quality. This misalignment can lead to issues like blurry predictions in video models or hallucinations in language models.

The RLVR-World framework addresses this by reformulating the world modeling task—predicting the next state given a current state and an action—as a reinforcement learning problem. After an initial pre-training phase with MLE, the world model is fine-tuned by generating next-state predictions, which are then evaluated against the ground truth using a verifiable, task-aligned metric (e.g., F1-score for state changes in web navigation, or LPIPS for perceptual similarity in video). This metric's output serves as a direct reward signal to update the model's policy using an RL algorithm. The authors demonstrate the framework's effectiveness by unifying both language and video world models under an autoregressive, token-based paradigm and show significant performance improvements on tasks including text-based games, web navigation, and robotic manipulation trajectory prediction. The method is shown to be highly efficient, achieving large gains with minimal post-training, and effective at mitigating issues like repetition artifacts in video generation.

**Rating: 9/10**

This is a high-quality paper that addresses a well-defined and important problem in the training of generative world models. The proposed solution is elegant, generalizable, and builds logically upon recent successes in aligning large language models (like RLHF), while cleverly sidestepping the need for human data or learned reward models by focusing on tasks with machine-verifiable reward functions. The experimental validation is strong and comprehensive, with convincing results across multiple modalities (language and video) and challenging domains. The paper clearly demonstrates the value of direct optimization and its ability to not only boost performance but also mitigate known failure modes of MLE training. For a PhD-level audience, the work is novel, methodologically sound, and its findings are impactful, suggesting a promising and broadly applicable post-training paradigm for a wide range of generative models.

### 2. Main Ideas

1.  **Direct Optimization of World Models with RLVR:** The core idea is to fine-tune world models using reinforcement learning to directly optimize for the desired, often non-differentiable, evaluation metrics. Instead of relying on surrogate objectives like next-token prediction (MLE), this approach uses the actual performance metric (e.g., prediction accuracy, F1-score, or perceptual similarity) as a "verifiable reward" to guide the model's learning process. This directly bridges the gap between the training objective and the ultimate task goal.

2.  **Unification of Multi-Modal World Modeling:** The paper treats world models across diverse modalities—specifically language and video—within a single, unified autoregressive framework. By tokenizing states and actions, it models the prediction of the next state as a sequence generation task. This unified view allows the RLVR-World post-training paradigm to be applied broadly, demonstrating its versatility as a general principle for improving generative models, not just a domain-specific trick.

3.  **Efficient Fine-Tuning to Mitigate Pre-training Flaws:** The paper demonstrates that RLVR is a highly efficient post-training method that can achieve substantial performance gains with orders of magnitude fewer gradient steps than MLE pre-training. Furthermore, it shows that by optimizing for holistic prediction quality (e.g., video-level metrics) rather than token-level likelihood, RLVR can effectively correct for artifacts introduced during pre-training, such as the tendency for video models to generate repetitive, static frames.

### 3. 10 Most Important Citations

1.  **Ha et al. 2018** - Recurrent world models facilitate policy evolution.
    *   This is a foundational paper that introduced and popularized the concept of "world models" which learn a compressed model of an environment to facilitate policy learning through simulated experience.

2.  **Ouyang et al. 2022** - Training language models to follow instructions with human feedback.
    *   This paper introduced Reinforcement Learning from Human Feedback (RLHF) via InstructGPT, establishing the paradigm of using RL to align generative models with human preferences, which is a direct precursor to the RLVR approach used in RLVR-World.

3.  **Shao et al. 2024** - Deepseekmath: Pushing the limits of mathematical reasoning in open language models.
    *   This citation is important as it introduces the Group Relative Policy Optimization (GRPO) algorithm, the specific reinforcement learning algorithm leveraged by the authors to implement their RLVR framework.

4.  **Sutton et al. 1998** - Reinforcement learning: An introduction.
    *   This is the definitive textbook on reinforcement learning, providing the fundamental theories of Markov decision processes, rewards, and policies that are the bedrock of the entire method proposed in the paper.

5.  **Chae et al. 2025** - Web agents with world models: Learning and leveraging environment dynamics in web navigation.
    *   This paper provides the WMA benchmark, dataset, and model predictive control setup for web navigation that RLVR-World uses as a key evaluation testbed for its language world models.

6.  **Wang et al. 2024** - Can language models serve as text-based world simulators?
    *   This work introduced the ByteSized32-State-Prediction dataset, which is the benchmark used in the paper to evaluate the performance of language models as world simulators for text-based games.

7.  **Brohan et al. 2023** - RT-1: Robotics transformer for real-world control at scale.
    *   This paper presented the RT-1 dataset of real-world robotic manipulation trajectories, which serves as the training and evaluation data for the video world model experiments in RLVR-World.

8.  **Wu et al. 2024** - ivideogpt: Interactive videogpts are scalable world models.
    *   The authors of RLVR-World build upon their own prior work, iVideoGPT, which is the autoregressive video world model architecture used as the base model for their video-based experiments.

9.  **Zhang et al. 2018** - The unreasonable effectiveness of deep features as a perceptual metric.
    *   This paper introduced the LPIPS metric, which measures perceptual similarity between images and is used in RLVR-World as the verifiable reward function for fine-tuning video world models.

10. **Bommasani et al. 2021** - On the opportunities and risks of foundation models.
    *   This influential paper provides the broad context for the entire work, outlining the landscape of large-scale foundation models and motivating the need for novel training and alignment techniques like RLVR-World.
