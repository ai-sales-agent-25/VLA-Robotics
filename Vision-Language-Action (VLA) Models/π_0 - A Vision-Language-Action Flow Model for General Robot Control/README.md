https://arxiv.org/abs/2410.24164

### Big‑picture common ground

| Aspect              | RT‑2                                                                                                                                                                   | π0 (pi‑zero)                                                                                                                | What’s shared?                                                                                                                   |
| ------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------- | --------------------------------------------------------------------------------------------------------------------------- | -------------------------------------------------------------------------------------------------------------------------------- |
| **Core idea**       | Treats a *pre‑trained* vision‑language model (PaLI‑X or PaLM‑E) as the backbone and adds robot actions so the model becomes a **Vision‑Language‑Action (VLA)** policy. | Builds on the open‑source PaliGemma VLM, adds an “action‑expert” head, yielding another **VLA** policy.                     | Both start from Internet‑scale VLMs and fine‑tune them with robot data, so language, vision *and* control live in one network.   |
| **Training recipe** | *Co‑fine‑tunes* VLM web data + robot demonstrations to avoid catastrophic forgetting.                                                                                  | Distinct **pre‑training (broad, noisy, multi‑robot)** then **post‑training (task‑specific, high‑quality)** phases.          | Both rely on *very large*, heterogeneous robot datasets to teach manipulation skills.                                            |
| **Goal**            | Generalise to unseen objects, scenes and instructions; show emergent symbol reasoning.                                                                                 | General‑purpose, *cross‑embodiment* control (single, dual‑arm & mobile) and long‑horizon dexterity (e.g. laundry folding).  | Push toward “foundation models” for robotics that reuse web knowledge for physical tasks.                                        |

---

### Key differences at a glance

| Dimension                        | RT‑2                                                                                                                                                                 | π0                                                                                                                                                                        |
| -------------------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **Action representation**        | **Discrete tokens**: every 6‑DoF pose & gripper value is quantised into 256 bins → 8 integer tokens per step; model is trained with standard next‑token prediction.  | **Continuous chunks via flow‑matching diffusion**: predicts a length‑50 action chunk in one go with a conditional vector‑field loss, giving high‑precision trajectories.  |
| **Control‑rate & deployment**    | Runs from a cloud‑TPU service; 55 B model reaches **1‑3 Hz**, 5 B ≈ 5 Hz.                                                                                            | Designed for **up to 50 Hz** on‑robot by integrating only 10 diffusion steps per chunk.                                                                                   |
| **Model size & architecture**    | Multiple scales: PaLI‑X **5 B / 55 B** and PaLM‑E **12 B**; single shared transformer (no extra expert) so language and action weights are identical.                | Backbone **3 B** PaliGemma + **0.3 B** action‑expert (≈ 3.3 B total); uses a *mixture‑of‑experts* so robotics tokens are routed to a smaller, faster head.                |
| **Data scale**                   | \~13 robots, 17 months of kitchen demos (+ web VQA) — 6 k eval trials.                                                                                               | **≈ 10 000 h** of demonstrations from **7 robot families, 68 tasks**, plus the 22‑robot OXE dataset.                                                                      |
| **Targets & strengths**          | Strong at semantic reasoning, symbol grounding and language‑conditioned pick‑and‑place; struggles with fine dexterity.                                               | Excels at long, dexterous, multi‑stage tasks (folding, bussing, assembly) thanks to high‑rate continuous control.                                                         |
| **Limitations noted by authors** | Cloud latency and coarse, discretised actions cap precision.                                                                                                         | Training & inference still costly; diffusion adds several forward passes per control step.                                                                                |

---

### Take‑away

*RT‑2* and *π0* share the same ambition—**meld internet‑scale perception‑and‑language knowledge with robot control**—but they make **orthogonal engineering choices**:

* RT‑2 keeps the language‑modeling machinery intact, simply **casting actions as text**, which is elegant and scales to giant models, but incurs token‑by‑token latency and quantisation.
* π0 **switches to diffusion‑style continuous action prediction**, trading parameter count for fine control and high servo rates, and introduces an action‑specific expert to keep inference light.

Which approach you’d prefer depends on your robot’s needs: if you want jet‑powered generalisation and can tolerate \~5 Hz cloud control, RT‑2 is compelling; if you need on‑board, real‑time dexterity across many robot bodies, π0’s flow‑matching path is the better fit.
