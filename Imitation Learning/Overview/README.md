### Where *behavior cloning / imitation learning* fits in **π0** and **GR00T N1**

| Model        | BC/IL objective                                                                                                                     | What data do they mimic?                                                                                                                           | Key twists beyond “vanilla” BC                                                                                                                                                                                                                                                                                      |
| ------------ | ----------------------------------------------------------------------------------------------------------------------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **π0**       | **Flow‑matching diffusion loss** on action tokens—still a *purely supervised* loss matching each demonstration action chunk         | • ≈10 000 h of robot demos from 7 in‑house dexterous platforms <br>• Open X‑Embodiment (22 more robots)                                            | 1. *Vision‑Language–Action (VLA)* backbone so demos are <br>  annotated with language goals. <br>2. Cross‑embodiment action space (pad small robots to 18‑D). <br>3. Two‑stage recipe: large, noisy **pre‑train** → small, curated **post‑train**, mirroring LLM RLHF pipelines.                                    |
| **GR00T N1** | Same **flow‑matching diffusion BC**—DiT predicts the denoising vector that brings a “noised” action chunk back to the expert action | • Real humanoid & arm demos • Simulation rollouts (DexMimicGen) • Neural videos generated with a fine‑tuned vid‑diffuser • Egocentric human videos | 1. Two‑system VLA stack: VLM (reasoning) + DiT (motor). <br>2. **Latent‑action coding**: a VQ‑VAE or inverse‑dynamics model invents “pseudo‑actions” so action‑less videos can be cloned too. <br>3. “Data pyramid” co‑training mixes web, synthetic and real data, then embodiment‑specific **post‑training**.     |

---

#### What “behavior cloning” looks like inside these flow‑based VLAs

1. **Tokenize an action *chunk*** (e.g., 50 × 18‑D joint actions for π0, 16‑step chunk for GR00T).
2. **Add Gaussian noise** to get a corrupted chunk $A^{\tau}$.
3. **Predict the vector field** $v_\theta(o,\;A^{\tau})$ that should bring $A^{\tau}$ back to the clean expert actions $A$.
4. **Mean‑square error** between prediction and ground‑truth denoising vector is minimized—identical in spirit to MSE or cross‑entropy BC, just expressed through flow‑matching maths.

Because the loss is still *per demo time‑step*, no rewards or rollouts are needed: both papers remain squarely in the offline imitation‑learning camp, only scaling the data and the model.

---

#### Why they adopt this style of BC

* **High‑frequency dexterity.** Diffusion / flow matching lets the policy model multi‑modal, fine‑grained action distributions that classic Gaussian BC struggles with. π0 runs at 50 Hz; GR00T N1 at 120 Hz.
* **Language‑conditioned generality.** By appending language tokens to every demonstration, a single BC model can be prompted with new goals at test time.
* **Data leverage.** GR00T’s latent‑action trick turns billions of human‑video frames into BC training pairs; π0’s cross‑embodiment padding folds 29 robot arms into one action space.
* **Simple deployment.** Once trained, the policy just autoregressively denoises—no DAgger or on‑policy interaction required.

---

#### Big picture takeaway

Both π0 and GR00T N1 stay true to the spirit of behavior cloning—**learn to imitate demonstrations via supervised loss**—but super‑charge it with:

* diffusion/flow objectives for smoother action synthesis,
* massive, heterogeneous datasets (robot demos + videos + simulation), and
* a Vision‑Language front‑end so a single BC policy can be *prompted* to do many tasks.

In other words, they show that modern foundation‑model tricks can turn the “old” idea of BC into a practical route toward generalist robot skills.
