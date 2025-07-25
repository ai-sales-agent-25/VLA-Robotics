https://arxiv.org/abs/2507.12507

https://x.com/shizhediao/status/1948127047177601141

### Scaling Up RL: Unlocking Diverse Reasoning in LLMs via Prolonged Training

**1. Summary and Rating**

This technical report investigates methods for improving the reasoning capabilities of a relatively small (1.5B parameter) language model through prolonged reinforcement learning (RL). The authors identify key challenges in long-duration RL training, including entropy collapse, training instability, and performance stagnation. To address these, they propose and validate a framework that combines several critical components: training on a diverse set of tasks with verifiable rewards (math, coding, STEM, logic puzzles), enhancing the Group Relative Policy Optimization (GRPO) algorithm with techniques from DAPO like decoupled clipping and dynamic sampling, and maintaining stability via controlled KL regularization. A core practical contribution is the introduction of periodic "hard resets" of the reference policy and optimizer states, which is shown to effectively counteract performance plateaus and enable continued learning.

The resulting model, Nemotron-Research-Reasoning-Qwen-1.5B, demonstrates significant performance improvements over its baseline across all reasoning domains. Notably, despite being trained on a diverse task mix, the model achieves competitive performance against domain-specialized models in both mathematics and coding, highlighting the framework's ability to foster strong, generalizable reasoning skills. The paper's value lies in its systematic, empirical approach to providing a stable and effective "recipe" for large-scale RL, demonstrating that algorithmic rigor and prolonged training can unlock impressive capabilities even in smaller models.

**Rating: 8.5/10**

The paper is a strong piece of empirical research that provides a valuable, practical guide for training reasoning-focused LLMs with RL. It meticulously documents the challenges of long-horizon training and presents a clear, well-validated set of solutions. The ablation studies are thorough and convincingly support the authors' claims about the importance of each component, particularly the periodic reset strategy and the enhancements adapted from DAPO. While it doesn't introduce a fundamentally new algorithm, its contribution lies in the successful synthesis, scaling, and systematic analysis of existing techniques to create a robust training framework. For a research audience, this work serves as an excellent case study and a replicable recipe for achieving strong reasoning performance in resource-efficient models, making it a significant engineering and empirical contribution.

**2. Main Ideas**

1.  **Prolonged Training via Stability and Periodic Resets:** The central argument is that significant reasoning gains can be achieved through prolonged RL training, but this requires overcoming inherent instabilities like entropy collapse and performance stagnation. The paper's key strategy is to combine stability-enhancing techniques (e.g., DAPO's decoupled clipping, a small KL penalty) with a novel "hard reset" of the reference policy and optimizer. This periodic reset allows the model to break free from local optima and learning plateaus, effectively restoring the training dynamics and enabling continued improvement over hundreds of thousands of steps.

2.  **Diverse, Verifiable Tasks Foster Generalization:** The authors demonstrate that training on a wide variety of reasoning tasks with programmatically verifiable rewards—spanning mathematics, coding, logic puzzles, STEM, and instruction following—is crucial. This diverse curriculum not only provides a robust training signal but also pushes the model to develop generalized reasoning skills. The success of their single, multi-task model against domain-specialized baselines proves that this approach can bridge the gap between general-purpose and specialized reasoning systems without being narrowly overfitted to a specific task format.

3.  **Algorithmic Refinements are Essential for RL Success:** The paper shows that off-the-shelf RL algorithms are not sufficient. They build on the GRPO algorithm but integrate crucial enhancements from DAPO, such as decoupled clipping (to encourage exploration by up-weighting less likely tokens) and dynamic sampling (to focus training on problems of intermediate difficulty). Their ablation studies validate that these specific modifications lead to more stable entropy, more efficient learning, and ultimately, better final performance compared to a standard GRPO implementation.

**3. 10 Most Important Citations**

1.  **Guo et al. 2025. Deepseek-r1: Incentivizing reasoning capability in llms via reinforcement learning.** This paper introduces a state-of-the-art reasoning model that, along with OpenAI's O1, represents the paradigm of using RL to unlock advanced reasoning, motivating the current work.

2.  **Luo et al. 2025. Deepscaler: Surpassing o1-preview with a 1.5b model by scaling rl.** This work is a primary baseline for comparison, as it also demonstrates success in training a small model for mathematical reasoning using scaled-up RL. [https://pretty-radio-b75.notion.site/DeepScaleR-Surpassing-01-Preview-with-a-1-5B-Model-by-Scaling-RL-19681902c14d68005bed8ca303013a4e2](https://pretty-radio-b75.notion.site/DeepScaleR-Surpassing-01-Preview-with-a-1-5B-Model-by-Scaling-RL-19681902c14d68005bed8ca303013a4e2)

3.  **Yu et al. 2025. Dapo: An open-source llm reinforcement learning system at scale.** This paper provides the key algorithmic improvements—decoupled clipping and dynamic sampling—that the authors adopt to enhance training stability and performance.

4.  **Shao et al. 2024. Deepseekmath: Pushing the limits of mathematical reasoning in open language models.** This paper introduces Group Relative Policy Optimization (GRPO), which is the core RL algorithm implemented and extended in this study.

5.  **Schulman et al. 2017. Proximal policy optimization algorithms.** This is the foundational paper on PPO, the ubiquitous RL algorithm upon which GRPO and many other modern large-scale RL methods are based.

6.  **Luo et al. 2025. Deepcoder: A fully open-source 14b coder at 03-mini level.** This work provides the DeepCoder model, which serves as a critical domain-specialized baseline for evaluating the coding performance of the authors' generalized reasoning model. [https://pretty-radio-b75.notion.site/DeepCoder-A-Fully-Open-Source-14B-Coder-at-03-mini-Level-1cf81902c14680b3bee5eb349a512a51](https://pretty-radio-b75.notion.site/DeepCoder-A-Fully-Open-Source-14B-Coder-at-03-mini-Level-1cf81902c14680b3bee5eb349a512a51)

7.  **Stojanovski et al. 2025. Reasoning gym: Reasoning environments for reinforcement learning with verifiable rewards.** This citation is important as it provides the "Reasoning Gym" dataset and environment, a key source of diverse logical puzzle tasks with verifiable rewards used for training and evaluation.

8.  **Jaech et al. 2024. Openai o1 system card.** This system card for OpenAI's O1 model is cited as a prime example of the recent paradigm shift toward using scaled test-time computation and RL to achieve major breakthroughs in complex reasoning.

9.  **Zhou et al. 2023. Instruction-following evaluation for large language models.** This paper introduces the IFEval benchmark, which the authors use to rigorously evaluate their model's ability to adhere to specific instructions, a key axis of their diverse training.

10. **He et al. 2025. Skywork open reasoner series.** This is cited as relevant parallel work that also investigates strategies for mitigating entropy collapse, providing context and a point of comparison for the authors' ablation studies on training dynamics. [https://capricious-hydrogen-41c.notion.site/Skywork-Open-Reaonser-Series-1d0bc9ae823a80459b46c149e4f51680](https://capricious-hydrogen-41c.notion.site/Skywork-Open-Reaonser-Series-1d0bc9ae823a80459b46c149e4f51680)
