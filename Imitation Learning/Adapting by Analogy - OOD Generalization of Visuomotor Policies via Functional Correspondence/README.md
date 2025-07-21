https://arxiv.org/abs/2506.12678

Adapting by Analogy: OOD Generalization of Visuomotor Policies via Functional Correspondence

### 1. Summary and Rating

This paper introduces "Adapting by Analogy" (ABA), a method for improving the out-of-distribution (OOD) generalization of visuomotor policies at test time. The core problem is that policies trained with imitation learning on a limited set of "in-distribution" (ID) data often fail when presented with novel objects or visual conditions, and collecting new demonstrations for every OOD scenario is inefficient. The key insight is that many OOD tasks do not require entirely new behaviors, but can be solved by reusing existing learned behaviors if a "functional correspondence" to an ID scenario is established (e.g., a robot that knows how to pick up a pen can apply the same skill to a pencil).

ABA works by first detecting if a current observation is OOD. If it is, the system queries a human expert for a high-level textual instruction that describes the functional correspondence (e.g., "treat a pencil like a pen"). This instruction is used to find functionally analogous observations in the original training dataset. The system can interactively ask for refinements if the retrieved behaviors are ambiguous. Finally, instead of executing an action based on the confusing OOD observation, the policy is given the latent embedding of the corresponding ID observation, effectively "tricking" it into executing a known, successful behavior. The method is validated on a real-world Franka robot for two manipulation tasks, demonstrating significant improvement in success rates on OOD objects and backgrounds with minimal human intervention compared to baselines that rely on learned embeddings or pre-trained vision models alone.

**Rating: 9/10**

This is a high-quality paper that addresses a critical and practical problem in robot learning. The core contribution—using expert-guided functional correspondence for test-time observation-space intervention—is both novel and elegant. It provides a data-efficient alternative to constant re-demonstration. The methodology is sound, the real-world experiments are well-designed and convincing, and the analysis effectively supports the central claims. The paper is well-written and clearly articulates the problem, solution, and results. It represents a strong contribution to the field of test-time adaptation and human-in-the-loop robotics.

### 2. Main Ideas

1.  **Generalization through Functional Correspondence:** The central idea is that policies can generalize to novel OOD objects not by learning new motor skills, but by understanding the *functional analogy* between the new object and a familiar one. Instead of retraining or collecting new demonstrations, the system reuses its existing repertoire of behaviors by mapping the OOD situation to a functionally equivalent ID one. For example, a pencil affords the same "grasp-and-place" action as a pen, even if it looks different.

2.  **Expert-Guided Test-Time Intervention:** The paper proposes a human-in-the-loop framework to establish this functional correspondence efficiently at deployment time. The system detects when it is in an unfamiliar OOD state and proactively solicits high-level, language-based feedback from an expert. This feedback is not a low-level corrective action but a semantic link ("match pencils with pens") that allows the system to identify the correct ID behavior to reuse. This process is interactive, allowing the system to request clarification until it is confident in the retrieved behavior.

3.  **Observation-Space Adaptation:** The mechanism for adaptation is an intervention in the policy's *observation space* rather than its action space or weights. After identifying the most functionally relevant ID observation(s) based on expert guidance, the system computes their latent embedding(s) and feeds this synthetic embedding to the policy's decoder. This effectively makes the policy "believe" it is seeing a familiar scene, thereby eliciting the correct, previously learned behavior without modifying the policy itself.

### 3. 10 Most Important Citations

1.  **Chi et al. (2024). Diffusion policy: Visuomotor policy learning via action diffusion.**
    This paper provides the diffusion-based visuomotor policy architecture that serves as the foundational "base policy" which the authors' method (ABA) adapts at test-time.

2.  **Oquab et al. (2023). Dinov2: Learning robust visual features without supervision.**
    This work provides the DINOv2 model, which is used to create a key baseline (`DINOEmbed`) for comparing whether powerful, pre-trained visual features can implicitly handle functional correspondence without explicit expert guidance.

3.  **Lai et al. (2021). The functional correspondence problem.**
    This citation is foundational as it formally defines the "functional correspondence problem" that the paper directly aims to solve, providing the theoretical context for the work.

4.  **Brohan et al. (2023). Rt-2: Vision-language-action models transfer web knowledge to robotic control.**
    This paper is cited to frame the current work within the broader context of large-scale vision-language-action models, highlighting the community-wide push for generalization that this paper contributes to.

5.  **Hancock et al. (2024). Run-time observation interventions make vision-language-action models more visually robust.**
    This is a crucial piece of related work that also proposes intervening on a policy's observations at runtime to improve robustness, helping to situate the paper's specific contribution.

6.  **Ren et al. (2024). Grounded sam: Assembling open-world models for diverse visual tasks.**
    This work provides the Grounded Segment Anything model, a critical tool used in the paper's method to perform the semantic segmentation necessary to link the expert's language description to specific regions in the OOD and ID images.

7.  **Tang et al. (2025). Functo: Function-centric one-shot imitation learning for tool manipulation.**
    This is cited as highly relevant work that also leverages the concept of functional correspondence for robot learning, showing that this is an active and important area of research.

8.  **Khazatsky et al. (2024). Droid: A large-scale in-the-wild robot manipulation dataset.**
    This citation helps frame the paper's motivation by pointing to the existence of large-scale datasets while arguing that collection is expensive and OOD failures still occur, justifying their more efficient adaptation approach.

9.  **Nakamoto et al. (2024). Steering your generalists: Improving robotic foundation models via value guidance.**
    This is an important related work on test-time intervention, which steers policies using offline-trained Q-functions, providing a contrasting approach to the paper's method of using expert-guided observation replacement.

10. **Chi et al. (2024). Universal manipulation interface: In-the-wild robot teaching without in-the-wild robots.**
    This paper provides the UMI gripper used in the hardware experiments, which is an important detail for the reproducibility and grounding of the real-world validation.
