https://arxiv.org/abs/2506.01185

HOMER: Learning In-the-Wild Mobile Manipulation via Hybrid Imitation and Whole-Body Control

### 1. Summary and Rating

**Summary**

This paper introduces HOMER, a novel imitation learning framework designed for mobile manipulation in complex, real-world environments like homes. The core problem it addresses is the high-dimensional control and long-horizon nature of tasks that require both mobility (navigating the base) and dexterity (manipulating with the arm). HOMER's solution has two main components. First, it uses a fast, kinematics-based Whole-Body Controller (WBC) that abstracts away low-level control; the learning policy simply commands a 6-DoF end-effector pose, and the WBC computes the necessary coordinated joint movements for both the mobile base and the arm. Second, the policy itself is a hybrid model that learns to switch between two action modes: a *keypose* policy for long-range movements (e.g., reaching for a cabinet), which predicts absolute end-effector poses from 3D point cloud data, and a *dense* policy for fine-grained manipulation (e.g., grasping a handle), which predicts relative end-effector motions from RGB images.

The authors demonstrate HOMER's effectiveness on a holonomic mobile manipulator, showing that it can learn complex household tasks like opening cabinets and sweeping trash from only 20 teleoperated demonstrations. It significantly outperforms baselines that lack either the hybrid action space or the whole-body control abstraction. Furthermore, the paper shows that the framework is modular and can be conditioned on salient keypoints from Vision-Language Models (VLMs), enabling it to generalize better to novel objects and cluttered scenes.

**Rating: 9/10**

This paper is a strong contribution to the field of mobile manipulation. It presents a well-designed and pragmatic system that effectively combines several powerful ideas—hybrid action spaces, whole-body control, and VLM conditioning—to tackle a highly relevant and difficult problem. The experimental validation is rigorous, with clear ablations on a challenging set of real-world tasks that convincingly demonstrate the benefits of each of the paper's core contributions. The sample efficiency (20 demos) is particularly impressive and points toward a scalable method for deploying robots in unstructured environments. The work is not a radical paradigm shift but rather an excellent piece of systems research and engineering that cleverly integrates and extends existing concepts, resulting in a state-of-the-art framework that is both effective and serves as a strong foundation for future research.

### 2. Main Ideas

1.  **Decoupling High-Level Learning from Low-Level Control:** The central idea is to simplify the learning problem by using a Whole-Body Controller (WBC). Instead of the policy learning in the high-dimensional, redundant joint space of the arm and base, it learns in the intuitive 6-DoF task space of the end-effector. The WBC handles the complex inverse kinematics of coordinating the base and arm to achieve the desired end-effector pose, while respecting joint limits and avoiding self-collisions. This abstraction makes policy learning more tractable and simplifies data collection via teleoperation.

2.  **Hybrid Action Spaces for Long-Horizon Tasks:** The paper argues that mobile manipulation tasks are naturally multi-phase. To address this, HOMER learns a hybrid policy that switches between two modes. A "keypose" policy predicts absolute goal poses for long-range movements, providing stability and overcoming the compounding error issues of purely relative-action policies. A "dense" policy predicts small, continuous delta poses for reactive, fine-grained manipulation where precision is key. By learning to transition between these modes, the robot can efficiently execute complex, long-horizon tasks that require both broad repositioning and precise interaction.

3.  **Modular VLM Integration for Generalization:** The framework is designed to be modular, allowing it to leverage the capabilities of large, pre-trained models. The paper demonstrates this with HOMER-COND, a variant where the keypose policy is conditioned on salient points identified by a Vision-Language Model (VLM). This allows the system to use semantic, language-based instructions (e.g., "point to the cabinet handle") to ground its actions, enabling robust generalization to novel objects, appearances, and visual clutter without requiring specific training data for those scenarios.

### 3. Top 10 Most Important Citations

1.  **Sundaresan et al. (2024)**. What's the Move? Hybrid Imitation Learning via Salient Points.
    *   This paper (SPHINX) is the direct predecessor for HOMER's hybrid policy architecture, which HOMER extends from tabletop manipulation to the mobile manipulation domain.

2.  **Wu et al. (2024)**. Tidybot++: An open-source holonomic mobile manipulator for robot learning.
    *   This is the specific open-source hardware platform on which HOMER is implemented and evaluated, providing essential context for the real-world experiments.
    *   Link: `arXiv:2412.10447` (Note: The provided OCR'd paper is a preprint, so the link is to the same archive but for the Tidybot++ paper).

3.  **Chi et al. (2023)**. Diffusion Policy: Visuomotor Policy Learning via Action Diffusion.
    *   This work provides the underlying model architecture for HOMER's "dense" sub-policy, which is responsible for fine-grained manipulation.

4.  **Fu et al. (2024)**. Mobile ALOHA: Learning Bimanual Mobile Manipulation with Low-Cost Whole-Body Teleoperation.
    *   This is a highly relevant contemporary work on learning mobile manipulation, and the paper's "decoupled base-arm" baseline is comparable to this approach, making it a key point of comparison.

5.  **Belkhale et al. (2023)**. Hydra: Hybrid Robot Actions for Imitation Learning.
    *   This is cited as another important recent work on hybrid policies for imitation learning, establishing the context and state-of-the-art that HOMER contributes to.

6.  **Deitke et al. (2024)**. Molmo and pixmo: Open weights and open data for state-of-the-art multimodal models.
    *   This citation refers to the specific Vision-Language Model (MolMo) used in the generalization experiments (HOMER-COND) to detect salient keypoints from language prompts.

7.  **Zakka (2024)**. Mink: Python inverse kinematics based on MuJoCo.
    *   This is the specific inverse kinematics library used to implement the paper's Whole-Body Controller, making it a critical component of the underlying system.
    *   Link: `https://github.com/kevinzakka/mink`

8.  **Shridhar et al. (2023)**. Perceiver-Actor: A Multi-task Transformer for Robotic Manipulation.
    *   Cited as a foundational keypose-based policy, this work provides context for the "keypose" half of HOMER's hybrid action space.

9.  **Murray et al. (1994)**. A Mathematical Introduction to Robotic Manipulation.
    *   This is a classic textbook cited for the fundamental kinematic formulation (body-frame twist) used to define pose error within the Whole-Body Controller.

10. **Open X-Embodiment Collaboration et al. (2023)**. Open X-Embodiment: Robotic Learning Datasets and RT-X Models.
    *   This represents the large-scale, generalist policy paradigm (e.g., RT-X) that HOMER's sample-efficient, 20-demonstration approach provides a compelling alternative to.
    *   Link: `https://arxiv.org/abs/2310.08864`
