https://arxiv.org/abs/2411.04983

DINO-WM: World Models on Pre-trained Visual Features enable Zero-shot Planning

### 1. Summary and Rating

This paper introduces DINO-WM, a novel world model designed for task-agnostic, zero-shot visual planning in robotics. The core innovation is to leverage fixed, pre-trained patch features from a DINOv2 vision transformer as the state representation, rather than learning a representation from scratch or predicting raw pixels. The system consists of a frozen DINOv2 encoder that converts images to patch embeddings and a separate transformer-based transition model that is trained on offline trajectory data to predict future patch embeddings given past embeddings and actions.

Because the model operates in this compact and semantically rich feature space, it can be trained efficiently on offline, reward-free data. At test time, it can plan for arbitrary, visually-specified goals without any fine-tuning. A planning algorithm, such as Model Predictive Control (MPC), is used to optimize a sequence of actions that minimizes the difference between the predicted future features and the goal features. The authors demonstrate that this approach significantly outperforms state-of-the-art world models like DreamerV3 and IRIS, particularly on complex manipulation tasks involving contact dynamics and deformable objects. The method's effectiveness stems from using spatially-aware patch features, which retain crucial information lost by global feature representations, and from decoupling the dynamics learning from the difficult task of image reconstruction.

**Rating: 9/10**

This is an excellent paper. The central idea of building a world model on top of pre-trained patch-level features is both elegant and highly effective. It cleverly sidesteps the notoriously difficult problem of learning a good visual representation from scratch, which is a major hurdle for many contemporary world models. The experimental results are comprehensive and compelling, with strong performance on a diverse set of challenging environments and thorough ablations that validate the key design choices. The work represents a significant step towards creating more general, capable, and data-efficient world models for robotic control, making a valuable contribution to the field.

### 2. Main Ideas

1.  **Leveraging Pre-trained Spatial Features for World Modeling:** The central thesis is that modern, pre-trained vision models like DINOv2 provide representations that are powerful enough to serve as the state space for a dynamics model. By using fixed, patch-level features, the model inherits a rich understanding of objects, geometry, and spatial relationships without needing to learn them from scratch. This allows the system to focus its training exclusively on learning the environment's dynamics, leading to superior sample efficiency and performance, especially in tasks requiring precise spatial reasoning.

2.  **Task-Agnostic Training for Zero-Shot Generalization:** The world model is trained on a collection of offline, reward-free trajectories, making it entirely task-agnostic. At test time, a task is simply specified by providing a goal image. Planning is then framed as an optimization problem in the latent feature space: finding an action sequence that steers the predicted state feature to the goal state feature. This enables the model to solve novel tasks and generalize to unseen environment configurations (e.g., new maze layouts, different object shapes) in a zero-shot manner, without any task-specific training or fine-tuning.

3.  **Decoupling Representation, Dynamics, and Reconstruction:** The architecture intentionally separates its main components. The observation encoder (DINOv2) is frozen. The transition model is trained independently to predict latent features. A visual decoder is also trained separately and is entirely optional, used only for visualization. This decoupling is critical, as it prevents the primary objective of learning accurate dynamics from being compromised by a complex and potentially distracting image reconstruction loss, a choice the authors validate through ablation studies.

### 3. Top 10 Most Important Citations

1.  **Oquab et al. 2024. Dinov2: Learning robust visual features without supervision.** This paper provides the pre-trained DINOv2 model whose patch features are used as the core visual representation for the world state in DINO-WM. [https://arxiv.org/abs/2304.07193](https://arxiv.org/abs/2304.07193)

2.  **Hafner et al. 2024. Mastering diverse domains through world models.** This paper introduces DreamerV3, a leading state-of-the-art world model that learns its own representations from scratch and is used as a primary baseline for comparison in the experiments. [https://arxiv.org/abs/2301.04104](https://arxiv.org/abs/2301.04104)

3.  **Micheli et al. 2023. Transformers are sample-efficient world models.** This paper presents IRIS, another strong transformer-based world model baseline that DINO-WM is directly compared against. [https://arxiv.org/abs/2209.00588](https://arxiv.org/abs/2209.00588)

4.  **Hansen et al. 2024. Td-mpc2: Scalable, robust world models for continuous control.** This work introduces TD-MPC2, a decoder-free world model used as a key baseline, particularly relevant due to DINO-WM's optional decoder design. [https://arxiv.org/abs/2310.16828](https://arxiv.org/abs/2310.16828)

5.  **Ha et al. 2018. World models.** This influential paper helped popularize the concept of learning compressed, predictive models of the world to train agents, establishing the general framework that DINO-WM operates within. [https://zenodo.org/record/1207631](https://zenodo.org/record/1207631)

6.  **Dosovitskiy et al. 2021. An image is worth 16x16 words: Transformers for image recognition at scale.** This paper introduced the Vision Transformer (ViT), the architecture which DINO-WM adapts for its transition model to predict future latent patch features. [https://arxiv.org/abs/2010.11929](https://arxiv.org/abs/2010.11929)

7.  **Ebert et al. 2018. Visual foresight: Model-based deep reinforcement learning for vision-based robotic control.** This is a key prior work that established a framework for visual model predictive control where tasks are defined by goal images, similar to the planning setup in DINO-WM. [https://arxiv.org/abs/1812.00568](https://arxiv.org/abs/1812.00568)

8.  **Sutton et al. 1991. Dyna, an integrated architecture for learning, planning, and reacting.** This is a foundational paper in reinforcement learning cited for the historical context of integrating a learned world model with planning to guide actions.

9.  **Caron et al. 2021. Emerging properties in self-supervised vision transformers.** This paper introduced the original DINO model, establishing the self-distillation learning paradigm and the effectiveness of patch-based features that DINOv2 builds upon. [https://arxiv.org/abs/2104.14294](https://arxiv.org/abs/2104.14294)

10. **Ko et al. 2023. Learning to act from actionless videos through dense correspondences.** This paper presents AVDC, a diffusion-based generative model used for comparison to show that DINO-WM's predictive approach is more suitable for precise planning than current generative video models. [https://arxiv.org/abs/2310.08576](https://arxiv.org/abs/2310.08576)
