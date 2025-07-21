https://arxiv.org/abs/2410.11758

LATENT ACTION PRETRAINING FROM VIDEOS

### 1. Summary and Rating

**Summary**

This paper introduces Latent Action Pretraining for General Action Models (LAPA), a novel unsupervised method for pretraining Vision-Language-Action (VLA) models for robotics without requiring ground-truth action labels. The core problem addressed is the data bottleneck in robot learning, as large-scale robot datasets with teleoperated actions are expensive and difficult to scale, while unlabeled internet videos are abundant. LAPA's methodology consists of three stages: 1) **Latent Action Quantization**, where a VQ-VAE-based model is trained to learn a discrete vocabulary of "latent actions" by encoding the change between consecutive video frames; 2) **Latent Pretraining**, where a VLA model is pretrained to predict these latent action tokens based on visual observations and language instructions; and 3) **Action Finetuning**, where the pretrained model is fine-tuned on a small, action-labeled robot dataset to map the learned latent representations to the robot's specific, executable action space.

Experiments across simulation (Language Table, SIMPLER) and real-world robot manipulation tasks demonstrate that LAPA significantly outperforms existing methods for learning from actionless video. Remarkably, it also outperforms state-of-the-art VLA models (OpenVLA) that were pretrained on large-scale datasets *with* ground-truth actions, especially in challenging cross-embodiment and cross-environment scenarios. The paper also shows that LAPA can achieve positive transfer when pretrained purely on human manipulation videos, highlighting its potential to leverage web-scale data. Finally, the LAPA framework is shown to be over 30 times more computationally efficient for pretraining than comparable state-of-the-art approaches.

**Rating: 9/10**

For a PhD-level audience, this paper is excellent. Its primary strength lies in its elegant and effective solution to a critical bottleneck in robotics: the scarcity of action-labeled data. The conceptual framework of "tokenizing" actions from raw video pixels and then using a pretrain-finetune paradigm is both novel and highly practical. The experimental validation is comprehensive and convincing, with comparisons against strong baselines (including the state-of-the-art) across a variety of well-chosen benchmarks that test for different types of generalization. The results, particularly LAPA's superior performance in cross-embodiment transfer and its ability to learn from human-only videos, are highly impactful and strongly support the authors' claims. The demonstrated pretraining efficiency further solidifies its value as a scalable method. The work is well-contextualized within recent literature and clearly articulates its contributions. A point is withheld only because the full extent of the method's limitations (e.g., in very fine-grained tasks like grasping, which the authors acknowledge) and its scalability to truly web-scale, unstructured video remains to be explored in future work.

### 2. Main Ideas

1.  **Unsupervised Latent Action Tokenization:** The core technical idea is to learn a discrete vocabulary of actions directly from video frames without any action labels. By using a VQ-VAE-based objective to model the "delta" or change between consecutive frames, the model learns to quantize dynamic visual information into a set of discrete "action tokens." This transforms the complex problem of predicting continuous, high-dimensional, embodiment-specific actions into a more manageable problem of predicting discrete, universal latent action tokens during the pretraining phase.

2.  **A Scalable Pretrain-Finetune Paradigm for Actionless Video:** LAPA establishes a powerful three-stage learning pipeline. First, it learns general world dynamics and behaviors from vast, unlabeled video sources (e.g., internet videos, diverse robot videos). Second, it pretrains a policy to act within this learned latent space. Finally, it uses a very small amount of labeled data to finetune the policy, effectively learning a simple mapping from the abstract latent actions to a specific robot's control space. This approach drastically improves data efficiency and unlocks the potential of leveraging diverse video data that was previously unusable for action-conditioned models.

3.  **Learning an Embodiment-Invariant Action Prior:** A key finding is that by learning actions in an abstract latent space rather than a concrete, robot-specific one, the model develops a shared action representation that is more robust to shifts in robot morphology, environments, and even the human-robot embodiment gap. This is demonstrated by LAPA's strong performance in cross-embodiment transfer tasks, where it outperforms models that were pretrained directly on ground-truth actions and likely overfitted to a specific robot's kinematics and dynamics. This makes LAPA a promising method for building a single, generalist foundation model for robotics.

### 3. Top 10 Most Important Citations

*Note: The paper does not provide hyperlinks in its bibliography.*

1.  **Kim et al. 2024. Openvla: An open-source vision-language-action model.** This is the primary state-of-the-art VLA model used as a key performance benchmark throughout the paper, which LAPA is shown to outperform in several real-world settings.

2.  **Collaboration et al. 2023. Open x-embodiment: Robotic learning datasets and rt-x models.** This paper introduced the large-scale, multi-embodiment robot dataset (Open X-Embodiment) that LAPA uses for pretraining, providing the diverse data that is crucial for testing multi-embodiment generalization.

3.  **Brohan et al. 2023. Rt-2: Vision-language-action models transfer web knowledge to robotic control.** This is a foundational VLA paper that established the paradigm of finetuning large vision-language models for robotic control, setting the intellectual stage for follow-up work like LAPA.

4.  **van den Oord et al. 2017. Neural discrete representation learning.** This work introduced the Vector Quantised-Variational AutoEncoder (VQ-VAE), the fundamental deep learning technique that LAPA leverages to create its discrete codebook of latent actions from raw video frames.

5.  **Bruce et al. 2024. Genie: Generative interactive environments.** This is a highly related contemporary work on learning latent actions for creating generative environments, and LAPA's latent action quantization model is directly inspired by and adapted from this paper's approach.

6.  **Baker et al. 2022. Video pretraining (vpt): Learning to act by watching unlabeled online videos.** This paper introduced VPT, a critical baseline method that also learns from unlabeled video by training an inverse dynamics model (IDM) to create pseudo-action-labels, against which LAPA demonstrates superior performance.

7.  **Du et al. 2023. Learning universal policies via text-guided video generation.** This work introduced UNIPI, another key baseline that uses video diffusion models for planning and an IDM for control, allowing for a comparison that highlights the strengths of LAPA's latent action approach over generative video models for this task.

8.  **Goyal et al. 2017. The" something something" video database for learning and evaluating visual common sense.** This is the large-scale human action video dataset (Something-Something V2) used to successfully demonstrate LAPA's ability to transfer knowledge from non-robot, human-centric videos to downstream robot manipulation tasks.

9.  **Lynch et al. 2023. Interactive language: Talking to robots in real time.** This paper introduced the Language Table benchmark, one of the main simulation environments used for rigorous evaluation of LAPA's performance on tasks requiring language understanding and generalization.

10. **Liu et al. 2024. World model on million-length video and language with ringattention.** This work introduced the Large World Model (LWM) which serves as the backbone VLM for LAPA, and its unique pretraining objective (which includes next-state prediction) is hypothesized as a key factor behind LAPA's remarkable pretraining efficiency.
