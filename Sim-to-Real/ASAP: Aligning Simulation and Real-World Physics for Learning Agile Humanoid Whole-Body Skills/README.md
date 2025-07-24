https://arxiv.org/abs/2502.01143

**Paper:** ASAP: Aligning Simulation and Real-World Physics for Learning Agile Humanoid Whole-Body Skills

### 1. Summary and Rating

This paper introduces ASAP (Aligning Simulation and Real Physics), a two-stage framework for transferring agile, whole-body humanoid skills from simulation to the real world. The core challenge addressed is the "sim-to-real" gap, where mismatches between simulated and real-world physics degrade the performance of learned control policies.

The ASAP framework operates in two stages. First, a base motion-tracking policy is pre-trained in a simulator using reinforcement learning (RL), with the goal of imitating reference motions derived from human video data. In the second stage, this pre-trained policy is deployed on the real humanoid robot to collect trajectory data. This data is then used to train a "delta action" model via RL, which learns to output a corrective action that accounts for the physics mismatch between the simulator and the real world. Finally, the initial policy is fine-tuned in the simulator, which has been augmented with this delta action model, thereby aligning the learning environment with real-world dynamics.

The authors demonstrate the framework's effectiveness by successfully deploying a variety of highly dynamic and complex skills (e.g., jumps, balancing, and sports celebrations inspired by famous athletes) on a Unitree G1 humanoid robot. Extensive experiments, both in sim-to-sim and sim-to-real settings, show that ASAP significantly outperforms baseline methods like System Identification (SysID) and Domain Randomization (DR), reducing tracking errors and enabling motions that were previously difficult to achieve.

**Rating: 9/10**

This paper is a high-quality contribution to the field of humanoid robotics and reinforcement learning. The methodology is well-conceived, addressing the critical sim-to-real challenge with a novel and practical framework. The use of a learned delta action model is an elegant way to capture complex, unmodeled dynamics without requiring laborious manual system identification. The experimental validation is thorough and compelling, with the successful real-world deployment of diverse, agile skills on a physical humanoid being a standout achievement. The work represents a significant step forward in enabling robots to perform complex, human-like motions, and the results are both visually impressive and quantitatively strong.

### 2. Main Ideas Discussed

1.  **Two-Stage Sim-to-Real Transfer via a Delta Action Model:** The central idea is a structured, two-stage process to bridge the sim-to-real gap. Instead of relying on traditional methods like Domain Randomization (which can be too conservative) or System Identification (which may not capture all physical discrepancies), the paper proposes learning the *residual* of the dynamics. This is accomplished by training a "delta action" model that learns a corrective term for the actions commanded by the policy, effectively teaching the simulator to behave like the real world.

2.  **Data-Driven Simulation Alignment:** The framework uses data collected from the real world to directly inform and correct the simulation environment. After a base policy is trained in an idealized simulator, it is run on the physical robot. The resulting state-action trajectories are then "replayed" in the simulator. The discrepancy between the simulated outcome and the recorded real-world outcome provides a powerful learning signal for the delta action model, effectively aligning the simulator's physics with the real robot's dynamics.

3.  **Learning Agile and Expressive Skills from Video:** The entire pipeline is initiated using motion data from videos of humans performing dynamic actions. This data is first reconstructed into a 3D format (SMPL), cleaned, and then retargeted to the robot's morphology. This allows the system to learn a wide repertoire of complex, expressive, and agile skills that go beyond simple locomotion, pushing the frontier of what humanoid robots can physically accomplish.

### 3. 10 Most Important Citations

1.  **Schulman et al. 2017.** Proximal policy optimization algorithms.
    This paper introduces Proximal Policy Optimization (PPO), the reinforcement learning algorithm used extensively in ASAP to train both the initial motion tracking policy and the delta action model.

2.  **Peng et al. 2018.** Deepmimic: Example-guided deep reinforcement learning of physics-based character skills.
    This is a foundational paper for learning physics-based character skills, and ASAP is inspired by its phase-based motion tracking formulation and its Reference State Initialization (RSI) technique to improve training stability.

3.  **Hwangbo et al. 2019.** Learning agile and dynamic motor skills for legged robots.
    This landmark paper demonstrated successful sim-to-real transfer for a quadruped robot and serves as a key point of comparison for work in learning-based control on real hardware.

4.  **Makoviychuk et al. 2021.** Isaac gym: High performance gpu based physics simulation for robot learning.
    This is the high-performance GPU-based simulator used for policy pre-training in ASAP, enabling the massive parallelization required for efficient reinforcement learning.

5.  **Tobin et al. 2017.** Domain randomization for transferring deep neural networks from simulation to the real world.
    This paper popularised Domain Randomization (DR), a key baseline method for sim-to-real transfer that ASAP compares against and aims to improve upon.

6.  **Peng et al. 2018.** Sim-to-real transfer of robotic control with dynamics randomization.
    This work provides another critical perspective on using dynamics randomization for sim-to-real transfer, a standard approach that ASAP contrasts with its targeted, data-driven alignment method.

7.  **Wang et al. 2025.** Tram: Global trajectory and motion of 3d humans from in-the-wild videos.
    This citation refers to TRAM, the specific computer vision model used in the first stage of the ASAP pipeline to reconstruct 3D human motions from video clips.

8.  **He et al. 2024.** Learning human-to-humanoid real-time whole-body teleoperation.
    This is prior work from the same authors from which ASAP adopts its two-stage shape-and-motion retargeting process to transfer human motions to the robot's kinematic structure.

9.  **Karnan et al. 2020.** Reinforced grounded action transformation for sim-to-real transfer.
    This paper is cited as related work on residual learning, as it also learns an action transformation to bridge the sim-to-real gap, providing a conceptual precedent for ASAP's delta action model.

10. **Loper et al. 2023.** Smpl: A skinned multi-person linear model.
    This paper introduces the SMPL model, a standard parameterized 3D model of the human body that is fundamental to ASAP's data pipeline for representing human motion captured from video.
