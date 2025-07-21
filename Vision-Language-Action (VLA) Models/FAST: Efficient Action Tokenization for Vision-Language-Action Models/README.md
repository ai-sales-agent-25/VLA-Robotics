https://arxiv.org/abs/2501.09747

**FAST: Efficient Action Tokenization for Vision-Language-Action Models**

### 1. Summary and Rating

This paper addresses a critical bottleneck in training autoregressive Vision-Language-Action (VLA) models for robotics: action tokenization. The authors identify that standard tokenization methods, which independently discretize each action dimension at each timestep, perform poorly for high-frequency and dexterous tasks. This is because high-frequency control signals lead to highly correlated consecutive actions, resulting in a weak and redundant learning signal for the next-token prediction objective.

To solve this, the paper proposes **Frequency-space Action Sequence Tokenization (FAST)**, a novel approach inspired by time-series compression. FAST treats a chunk of future actions as a continuous signal, transforms it into the frequency domain using the Discrete Cosine Transform (DCT), and then compresses the resulting coefficients using quantization and byte-pair encoding (BPE). This method effectively distills the crucial information of an action sequence into a much shorter, more information-dense sequence of tokens.

The authors demonstrate that FAST enables autoregressive VLAs to successfully learn complex, high-frequency manipulation tasks where prior methods failed entirely. Furthermore, they train and release **FAST+**, a universal, off-the-shelf action tokenizer trained on 1 million diverse robot trajectories, which generalizes across different robots and tasks. When integrated with a state-of-the-art VLA (π₀), the resulting model, π₀-FAST, matches the performance of powerful diffusion-based VLAs on challenging benchmarks while reducing training time by up to 5x.

**Rating: 9.5/10**

This paper receives a high rating for its clear diagnosis of a significant and practical problem in robot learning and for providing an elegant, effective, and computationally efficient solution. The core insight—that action sequences should be treated as compressible signals—is powerful. The experimental validation is exceptionally thorough, testing across multiple VLA backbones, comparing against strong baselines (including naïve binning, learned quantization, and diffusion models), and evaluating on a diverse suite of challenging, dexterous tasks. The creation and release of FAST+, a universal action tokenizer, is a substantial practical contribution that could accelerate future research by simplifying the VLA training pipeline. The work successfully repositions autoregressive models as a highly competitive and efficient alternative to diffusion models for creating generalist robot policies.

### 2. Main Ideas

1.  **Action Tokenization via Frequency-Domain Compression:** The central idea is to abandon the standard per-timestep, per-dimension binning of robot actions. Instead, the paper proposes treating a sequence of actions as a signal to be compressed. By applying a Discrete Cosine Transform (DCT), the action sequence is moved to the frequency domain, where most of the signal's energy is concentrated in a few low-frequency coefficients. These coefficients are then quantized and further compressed with byte-pair encoding (BPE), creating a short and information-rich token sequence that is far more suitable for an autoregressive transformer's next-token prediction objective.

2.  **A Universal Robot Action Tokenizer (FAST+):** The paper demonstrates that the FAST tokenization scheme is general enough to create a single, "universal" tokenizer. By training the BPE vocabulary on a large-scale, cross-embodiment dataset (1M action sequences), they create FAST+, a pre-trained tokenizer that can be used off-the-shelf for a wide variety of new robots, action spaces, and control frequencies without needing to be retrained. This is a significant practical contribution that lowers the barrier to training new, high-performance VLAs.

3.  **Making Autoregressive VLAs Competitive and Efficient:** This work shows that with a proper tokenization scheme, autoregressive VLAs can achieve performance comparable to state-of-the-art diffusion-based policies, even on highly dexterous tasks. Their primary model, π₀-FAST, matches the performance of the powerful π₀ diffusion model but requires significantly less computation, achieving up to a 5x speedup in training time. This result revitalizes the autoregressive approach, demonstrating it is a highly viable and efficient path toward building generalist robot policies.

### 3. 10 Most Important Citations

1.  **Black et al. (2024)** - *π₀: A vision-language-action flow model for general robot control.*
    This citation introduces the π₀ VLA, which serves as the primary backbone model and state-of-the-art diffusion-based competitor that the authors compare their FAST-based autoregressive model against.

2.  **Brohan et al. (2023)** - *RT-2: Vision-language-action models transfer web knowledge to robotic control.*
    This paper introduces RT-2, a seminal VLA that uses the "naïve" per-dimension binning tokenization that FAST is designed to replace, making it a critical point of reference for the problem being solved.

3.  **Khazatsky et al. (2024)** - *Droid: A large-scale in-the-wild robot manipulation dataset.*
    This paper presents the DROID dataset, a key large-scale benchmark used to demonstrate the effectiveness and generalization of FAST, on which the authors achieve the first successful zero-shot evaluation.

4.  **Ahmed et al. (1974)** - *Discrete cosine transform.*
    This is the foundational paper that introduced the Discrete Cosine Transform (DCT), the core mathematical operation used in the FAST tokenization pipeline to convert action signals to the frequency domain for compression.

5.  **Sennrich et al. (2015)** - *Neural machine translation of rare words with subword units.*
    This paper popularized the use of byte-pair encoding (BPE) for tokenizing text in neural models, which is the second key compression step in the FAST pipeline, used to compress the quantized DCT coefficients.

6.  **Kim et al. (2024)** - *Openvla: An open-source vision-language-action model.* [https://arxiv.org/abs/2406.09246](https://arxiv.org/abs/2406.09246)
    This citation introduces OpenVLA, another popular VLA backbone that the authors use to demonstrate that the benefits of FAST are independent of a specific model architecture.

7.  **Open X-Embodiment Collaboration (2023)** - *Open X-Embodiment: Robotic learning datasets and RT-X models.* [https://arxiv.org/abs/2310.08864](https://arxiv.org/abs/2310.08864)
    This work introduced the large-scale, multi-embodiment dataset that was used to train the universal FAST+ tokenizer, enabling its broad generalization capabilities.

8.  **van den Oord et al. (2018)** - *Neural discrete representation learning.* [https://arxiv.org/abs/1711.00937](https://arxiv.org/abs/1711.00937)
    This paper introduced VQ-VAE, a foundational method for learned vector quantization, representing an alternative, learning-based approach to compression that the authors compare against and show FAST to be simpler and more effective for high-fidelity control.

9.  **Chi et al. (2023)** - *Diffusion policy: Visuomotor policy learning via action diffusion.*
    This citation is representative of the diffusion model approach for robotics, which has become a dominant paradigm and serves as the main architectural alternative that FAST-enabled autoregressive models are shown to compete with.

10. **Brohan et al. (2022)** - *RT-1: Robotics transformer for real-world control at scale.*
    This is another foundational paper in scaling up transformer-based policies for robotics, establishing the line of autoregressive models that the FAST paper directly builds upon and significantly improves.
