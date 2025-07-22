https://arxiv.org/abs/2503.14476

https://x.com/TheTuringPost/status/1921524793956008169

https://x.com/_philschmid/status/1902258522059866504

# DAPO: an Open-Source LLM Reinforcement Learning System at Scale

## 1. Summary and Rating

This paper introduces DAPO (Decoupled Clip and Dynamic sampling Policy Optimization), a novel reinforcement learning algorithm for large language models (LLMs) designed to address the challenges of scaling RL for complex reasoning tasks.  The authors highlight the lack of transparency and reproducibility in state-of-the-art reasoning LLMs, particularly concerning RL training details.  DAPO is presented as a fully open-sourced RL system, including algorithm, training code (based on the `verl` framework), and dataset.  The paper details four key techniques within DAPO: Clip-Higher (decoupling clip ranges for importance sampling), Dynamic Sampling (over-sampling and filtering prompts based on accuracy), Token-Level Policy Gradient Loss (addressing imbalances in sample-level loss calculation for long sequences), and Overlong Reward Shaping (mitigating reward noise from truncated samples).  Empirical results demonstrate that DAPO achieves state-of-the-art performance on the AIME 2024 benchmark using a Qwen2.5-32B base model, outperforming previous methods like DeepSeek-R1-Zero-Qwen-32B with fewer training steps.  The paper also provides insightful analysis of training dynamics, such as response length, reward, and entropy, offering practical guidance for RLHF in LLMs.  The open-source nature of DAPO and the detailed exposition of its components are significant contributions to the field, promoting reproducibility and further research.

**Rating: 9/10**

The paper is well-written, clearly explains the motivation and methodology, and provides strong empirical validation.  The emphasis on open-source and reproducibility is highly valuable. The proposed techniques are well-justified and address specific challenges in scaling RL for LLMs.  The analysis of training dynamics is also a strong point.  The paper is technically sound and relevant to a PhD-level audience working on LLMs and RLHF.  Minor improvements might include more in-depth comparisons to other contemporary RLHF algorithms beyond GRPO and PPO, and potentially a more detailed ablation study of each individual component's contribution in combination with others.  However, these are minor points and do not significantly detract from the paper's overall high quality and impact.


## 2. Main Ideas

1.  **Open-Source and Reproducible LLM RL System:** The paper's central idea is to provide the research community with a fully transparent and reproducible RL system for training high-performing reasoning LLMs.  By open-sourcing the algorithm (DAPO), code, and dataset, the authors aim to democratize access to state-of-the-art RLHF techniques and facilitate further research and development in this area.  This directly addresses the opacity of existing industry models and the challenges in replicating their results.

2.  **Decoupled Clip and Dynamic Sampling Policy Optimization (DAPO) Algorithm:** DAPO introduces several key algorithmic innovations designed to improve the stability, efficiency, and performance of RLHF for long-context reasoning tasks.  Specifically, the *Clip-Higher* strategy tackles entropy collapse by allowing more aggressive updates for low-probability tokens, *Dynamic Sampling* enhances sample efficiency by focusing on prompts that yield informative gradients, *Token-Level Policy Gradient Loss* addresses imbalances in loss calculation for variable length responses, and *Overlong Reward Shaping* mitigates reward noise from truncated samples. These techniques collectively contribute to a more robust and effective RL training process.

3.  **Practical Insights into LLM RL Training Dynamics:** Beyond the algorithmic contributions, the paper offers valuable practical insights into the dynamics of LLM RL training.  By analyzing metrics like response length, reward, and entropy throughout training, the authors provide guidance on monitoring and interpreting the RL training process, identifying potential issues like entropy collapse or overfitting, and ultimately refining the system for better performance. This focus on practical considerations is essential for researchers and practitioners working to scale RLHF for LLMs.

## 3. 10 Most Important Citations

1. **Schulman et al. 2017. Proximal policy optimization algorithms.** [https://arxiv.org/abs/1707.06347](https://arxiv.org/abs/1707.06347) This paper introduces Proximal Policy Optimization (PPO), a foundational on-policy RL algorithm that DAPO builds upon and compares to, particularly in the context of clipped surrogate objectives.

2. **Ouyang et al. 2022. Training language models to follow instructions with human feedback.** In *Advances in Neural Information Processing Systems*. [https://proceedings.neurips.cc/paper_files/paper/2022/hash/1db29d19b9a1d7f79e0376131f5d14b7-Abstract-Conference.html](https://proceedings.neurips.cc/paper_files/paper/2022/hash/1db29d19b9a1d7f79e0376131f5d14b7-Abstract-Conference.html) This seminal work demonstrates the effectiveness of Reinforcement Learning from Human Feedback (RLHF) in aligning language models with human instructions, which is the broader context for the DAPO paper's focus on reasoning capabilities through RL.

3. **Guo et al. 2025. Deepseek-r1: Incentivizing reasoning capability in llms via reinforcement learning.** arXiv preprint arXiv:2501.12948. This paper, from DeepSeek, represents the previous state-of-the-art in reasoning LLMs using RL, and is the primary benchmark against which DAPO's performance is evaluated.  DAPO aims to improve upon and provide more transparency compared to the techniques described in DeepSeek-R1.

4. **Sheng et al. 2024. Hybridflow: A flexible and efficient rlhf framework.** arXiv preprint arXiv:2409.19256. [https://arxiv.org/abs/2409.19256](https://arxiv.org/abs/2409.19256)  This paper introduces the `verl` framework, which DAPO is built upon, highlighting the importance of efficient and flexible RLHF infrastructure.

5. **Brown et al. 2020. Language models are few-shot learners.** In *Advances in neural information processing systems*. [https://proceedings.neurips.cc/paper/2020/hash/1457c0d6bfcb4e6733c75396f9f40b69-Abstract-Conference.html](https://proceedings.neurips.cc/paper/2020/hash/1457c0d6bfcb4e6733c75396f9f40b69-Abstract-Conference.html) This foundational paper demonstrates the emergent few-shot learning capabilities of large language models, setting the stage for subsequent research into enhancing reasoning through techniques like RLHF.

6. **Chowdhery et al. 2023. Palm: Scaling language modeling with pathways.** *Journal of Machine Learning Research*, 24(240):1-113. [http://jmlr.org/papers/v24/22-01147.html](http://jmlr.org/papers/v24/22-01147.html)  This paper describes the PaLM model and highlights the importance of scaling language models for improved performance, which motivates the DAPO paper's focus on large-scale RL.

7. **Loshchilov and Hutter. 2019. Decoupled weight decay regularization.** In *International Conference on Learning Representations*. [https://arxiv.org/abs/1812.03268](https://arxiv.org/abs/1812.03268) This paper introduces decoupled weight decay regularization, an optimization technique used in AdamW, the optimizer employed in DAPO, demonstrating attention to modern optimization practices.

8. **Shinn et al. 2023. Reflexion: Language agents with verbal reinforcement learning.** [https://arxiv.org/abs/2303.11366](https://arxiv.org/abs/2303.11366)  This paper explores "Reflexion," a technique for improving reasoning in language agents through self-reflection and iterative refinement, which is related to the DAPO paper's goal of enhancing complex reasoning through RL.

9. **Amodei et al. 2016. Concrete problems in ai safety.** [https://arxiv.org/abs/1606.06565](https://arxiv.org/abs/1606.06565) This paper discusses safety concerns in AI, including reward hacking, which is relevant to DAPO's use of rule-based reward modeling as an alternative to potentially problematic learned reward models.

10. **Shao et al. 2024. Deepseekmath: Pushing the limits of mathematical reasoning in open language models.** arXiv preprint arXiv:2402.03300. [https://arxiv.org/abs/2402.03300](https://arxiv.org/abs/2402.03300) This paper from DeepSeek focuses on mathematical reasoning in LLMs, a domain similar to AIME and relevant to DAPO's evaluation, and further contextualizes the state-of-the-art in this area.
