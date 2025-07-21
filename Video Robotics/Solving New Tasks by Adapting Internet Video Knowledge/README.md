https://arxiv.org/abs/2504.15369

SOLVING NEW TASKS BY ADAPTING INTERNET VIDEO KNOWLEDGE

### 1. Summary and Rating

This paper investigates how large-scale, pretrained text-to-video models, which possess general world knowledge from internet data, can be effectively adapted for specific, in-domain robotics tasks using only a small amount of demonstration data. The authors bridge the gap between the strong generalization of internet-scale models and the environmental specificity of models trained purely on in-domain data. The work systematically compares three adaptation techniques—Direct Finetuning, Subject Customization (via DreamBooth), and Probabilistic Adaptation—and introduces a novel variant, **Inverse Probabilistic Adaptation**. This new method, where the large pretrained model leads generation while being guided by a small in-domain model, is shown to be particularly effective. The adapted models are rigorously evaluated on their ability to perform novel, text-conditioned tasks in downstream robotic applications, specifically through **visual planning** (generating future frames as a goal) and **policy supervision** (providing a reward signal). Experiments across MetaWorld and DeepMind Control Suite benchmarks demonstrate that Inverse Probabilistic Adaptation achieves superior generalization, and remarkably, maintains strong performance even when adapted using suboptimal, non-expert data.

**Rating: 9/10**

This is a high-quality, well-executed paper that provides significant practical insight for the robotics and foundation model communities. Its primary strength lies in the thorough and systematic comparison of well-motivated adaptation strategies, evaluated not on abstract visual metrics but on concrete downstream task success. The introduction and successful validation of "Inverse Probabilistic Adaptation," especially its robustness to low-quality data, is a strong and impactful contribution, addressing a key bottleneck in robot learning. The experimental design is comprehensive, and the findings provide clear, actionable guidance for practitioners seeking to leverage large video models for robotics.

### 2. Main Ideas

1.  **A Systematic Framework for Adapting Video Models (Adapt2Act):** The paper’s core idea is to move beyond the dichotomy of using either a general internet-scale model or a specialized in-domain model. It instead proposes and empirically evaluates a spectrum of adaptation techniques that combine the strengths of both. This provides a structured understanding of the trade-offs between data cost (from a few static images to full video trajectories), computational effort, and generalization capability when applying foundation models to new robotic environments.

2.  **Inverse Probabilistic Adaptation for Robust Generalization:** The paper introduces a novel adaptation technique where a large, frozen pretrained model's generative process is guided by a small, lightweight model trained on in-domain data. This inverts the typical score composition relationship and is shown to be the most effective method overall. Its key advantage is strong generalization to novel tasks and, critically, robustness to the quality of the adaptation data, enabling successful task learning even from suboptimal demonstrations.

3.  **Evaluating Adaptation via Downstream Robotic Task Performance:** The authors argue that standard visual metrics like Fréchet Video Distance (FVD) are insufficient for assessing a model's utility in robotics. They instead propose a more meaningful evaluation paradigm centered on downstream task success. By testing each adapted model in two distinct robotics frameworks—as a **visual planner** and as a **policy supervisor**—the paper provides a more holistic and practical measure of how well each adaptation technique captures task-relevant dynamics and semantics.

### 3. 10 Most Important Citations

1.  **Guo et al. 2023. Animate your personalized text-to-image diffusion models without specific tuning.**
    This paper introduces AnimateDiff, the core pretrained text-to-video model that serves as the foundation for adaptation and experimentation throughout this work.
    *   Link: [https://arxiv.org/abs/2307.04725](https://arxiv.org/abs/2307.04725)

2.  **Luo et al. 2024. Text-aware diffusion for policy learning.**
    This paper (Video-TADPoLe) provides the essential framework for using a video diffusion model as a policy supervisor, which is one of the two primary evaluation methods used to measure the performance of the adapted models.

3.  **Du et al. 2024a. Learning universal policies via text-guided video generation.**
    This work (UniPi) establishes the methodology for using a generative video model as a visual planner to solve robotic tasks, forming the basis for the paper's second main evaluation approach.

4.  **Yang et al. 2023a. Probabilistic adaptation of text-to-video models.**
    This paper introduces the original concept of probabilistic adaptation via score composition, which the authors directly build upon and invert to create their novel and highly effective "Inverse Probabilistic Adaptation" method.
    *   Link: [https://arxiv.org/abs/2306.01872](https://arxiv.org/abs/2306.01872)

5.  **Ruiz et al. 2023. Dreambooth: Fine tuning text-to-image diffusion models for subject-driven generation.**
    This paper introduces DreamBooth, the specific technique used for the "Subject Customization" adaptation strategy, which adapts the model using only a few static images of the robotic environment.

6.  **Rombach et al. 2022. High-resolution image synthesis with latent diffusion models.**
    This is the seminal paper on Stable Diffusion, the latent diffusion model that provides the underlying image synthesis architecture for AnimateDiff, making it a foundational component of the entire technical stack.
    *   Link: [https://arxiv.org/abs/2112.10752](https://arxiv.org/abs/2112.10752) (Note: Link is to the arXiv preprint; paper was published at CVPR 2022)

7.  **Ho et al. 2020. Denoising diffusion probabilistic models.**
    This paper introduced the denoising diffusion probabilistic model (DDPM), the core generative modeling paradigm that underpins all the diffusion-based video and image models used in this work.

8.  **Escontrela et al. 2024. Video prediction models as rewards for reinforcement learning.**
    This work (VIPER) is a key piece of prior art that demonstrates the viability of using in-domain video prediction models to provide rewards for policy learning, setting the stage for the paper's policy supervision experiments.

9.  **Yu et al. 2020. Meta-world: A benchmark and evaluation for multi-task and meta reinforcement learning.**
    This paper introduces the MetaWorld benchmark, the suite of robotic manipulation tasks used for the majority of the empirical evaluations.
    *   Link: [https://arxiv.org/abs/1910.10897](https://arxiv.org/abs/1910.10897) (Note: Link is to the arXiv preprint; paper was published at CoRL 2020)

10. **Tassa et al. 2018. Deepmind control suite.**
    This paper introduces the DeepMind Control Suite, the continuous control benchmark (including "Humanoid" and "Dog" agents) used to evaluate the adaptation methods on locomotion tasks.
    *   Link: [https://arxiv.org/abs/1801.00690](https://arxiv.org/abs/1801.00690)
