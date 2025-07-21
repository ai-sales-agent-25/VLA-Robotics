https://arxiv.org/abs/2505.24156

Towards a Generalizable Bimanual Foundation Policy via Flow-based Video Prediction

**1. Summary and Rating**

This paper introduces CogRobot, a novel framework for learning generalizable bimanual manipulation policies by leveraging pre-trained text-to-video (T2V) models. The core challenge addressed is the difficulty of training policies for bimanual tasks due to large action spaces, coordination requirements, and scarcity of high-quality bimanual data. CogRobot proposes a two-stage approach to fine-tune a T2V model (CogVideoX) for predicting future robot trajectories. First, a "text-to-flow" model predicts optical flow sequences from language instructions, serving as a concise intermediate representation of motion that concretizes textual intent. Second, a "flow-to-video" model uses this predicted optical flow to guide the generation of fine-grained bimanual video trajectories. This two-stage process is designed to mitigate the ambiguity in language instructions and significantly reduce the robot-specific data needed for fine-tuning, compared to direct video prediction or methods requiring extensive low-level action labels. Finally, a lightweight diffusion policy is trained to translate these predicted video trajectories into executable low-level actions for the dual-arm robot. The authors demonstrate the effectiveness of CogRobot through experiments in simulated (RoboTwin) and real-world environments, showing improved performance and generalization compared to baselines, particularly in data-limited scenarios. They also provide ablation studies highlighting the benefits of the flow-based intermediate representation for video quality.

**Rating: 8.5/10**

For a PhD-level audience, this paper presents a compelling and timely approach to a significant robotics challenge. The novelty lies in the intelligent use of optical flow as an intermediate representation to bridge large-scale T2V foundation models with the specific demands of bimanual robotics. This addresses a critical bottleneck—data efficiency—by making T2V models more amenable to fine-tuning with limited domain-specific data. The two-stage (text-to-flow, then flow-to-video) decomposition is a clever way to inject stronger motion priors and reduce the learning burden on the T2V model. The experimental validation, including both simulation and real-world deployment on a custom bimanual setup, is solid and supports the claims. The paper is well-written and clearly articulates its contributions and the limitations of prior work. While the ultimate goal of a true "foundation policy" is ambitious and the current work still requires task-specific action policy training (a noted limitation), CogRobot offers a significant step by improving high-level planning. The method's ability to reduce reliance on low-level action data for the video prediction stage is a valuable contribution to the field of robot learning.

**2. Main Ideas Discussed**

1.  **Leveraging Text-to-Video (T2V) Models for Bimanual Trajectory Prediction:** The paper proposes using powerful pre-trained T2V models (specifically CogVideoX) as high-level planners for bimanual robots. Instead of directly predicting actions, the T2V model is fine-tuned to predict future video frames, representing the desired robot trajectory based on language instructions and an initial observation.
2.  **Two-Stage Video Prediction with Optical Flow as an Intermediate Representation:** To overcome the challenges of directly fine-tuning T2V models with scarce bimanual data and ambiguous language, the paper introduces a two-stage paradigm.
    *   **Text-to-Flow:** The model first predicts optical flow from the text instruction. Optical flow serves as a concise, intermediate variable capturing fine-grained motion details and concretizing the language intent.
    *   **Flow-to-Video:** The predicted optical flow then guides a second model to generate a detailed video of the robot's actions. This approach reduces data requirements and improves the precision of predicted movements by explicitly modeling motion.
3.  **Hierarchical Policy Learning:** The overall system operates hierarchically. The fine-tuned T2V model (via the text-to-flow and flow-to-video stages) acts as a high-level planner generating target visual states. A separate, lightweight diffusion policy then serves as a low-level controller, taking the predicted video frames as goals to generate executable joint actions for the bimanual robot.

**3. 10 Most Important Citations**

1.  Yang et al. 2025. Cogvideox: Text-to-video diffusion models with an expert transformer.
    *   This paper introduces CogVideoX, the foundational text-to-video model that CogRobot fine-tunes for bimanual trajectory prediction.
2.  Chi et al. 2023. Diffusion policy: Visuomotor policy learning via action diffusion.
    *   This work presents Diffusion Policy, the architecture adopted by CogRobot for the low-level controller that translates predicted videos into executable robot actions.
3.  Liu et al. 2024. Rdt-1b: a diffusion foundation model for bimanual manipulation. arXiv preprint arXiv:2410.07864. Link: [https://arxiv.org/abs/2410.07864](https://arxiv.org/abs/2410.07864)
    *   RDT-1B is a significant bimanual manipulation dataset and model used for pre-training/fine-tuning CogRobot and serves as a key baseline in experiments.
4.  Wu et al. 2024. Robomind: Benchmark on multi-embodiment intelligence normative data for robot manipulation. arXiv preprint arXiv:2412.13877. Link: [https://arxiv.org/abs/2412.13877](https://arxiv.org/abs/2412.13877)
    *   RoboMIND is another important bimanual dataset used for fine-tuning CogRobot, contributing to its ability to handle diverse manipulation tasks.
5.  Shi et al. 2023. Flowformer++: Masked cost volume autoencoding for pretraining optical flow estimation.
    *   This paper introduces FlowFormer++, the method used in CogRobot to extract ground-truth optical flow from video clips, which is crucial for training the text-to-flow model.
6.  Du et al. 2023. Learning universal policies via text-guided video generation.
    *   This reference is relevant as it explores the idea of using text-guided video generation for learning robot policies, aligning with CogRobot's high-level approach.
7.  Mu et al. 2024. Robotwin: Dual-arm robot benchmark with generative digital twins (early version). arXiv preprint arXiv:2409.02920. Link: [https://arxiv.org/abs/2409.02920](https://arxiv.org/abs/2409.02920)
    *   RoboTwin is the simulation framework used for evaluating CogRobot, providing diverse and realistic bimanual manipulation scenarios.
8.  Zhao et al. 2023. Learning Fine-Grained Bimanual Manipulation with Low-Cost Hardware.
    *   This is an influential work in bimanual manipulation, highlighting challenges and approaches relevant to the problems CogRobot aims to solve.
9.  Zheng et al. 2024. Open-sora: Democratizing efficient video production for all. arXiv preprint arXiv:2412.20404. Link: [https://arxiv.org/abs/2412.20404](https://arxiv.org/abs/2412.20404)
    *   Cited as Sora, this represents state-of-the-art in T2V generation, providing context for the capabilities of models CogRobot builds upon and aims to adapt.
10. Shi et al. 2024. Motion-i2v: Consistent and controllable image-to-video generation with explicit motion modeling.
    *   This work is cited by the paper to highlight the challenges of directly predicting raw optical flow (modality gap), motivating CogRobot's approach of converting optical flow into a "flow video" format.
