Source: https://www.nature.com/articles/s44172-026-00632-5 (original fetch attempt was blocked by an idp.nature.com login/cookie wall; bibliographic details were cross-checked via PMC mirror PMC13133102). **This version supersedes the earlier partial extract** — Karl supplied the complete paper text directly, so the content below is treated as full/authoritative rather than an AI-summarized extract.

**Authorship:** Karl was a main contributor to this paper (Tejwani, Payne, Velazquez, Bonato, Asada).

# Adaptive robot guidance through real-time compliance estimation and dual-modal control

- **Journal:** Communications Engineering (Nature portfolio)
- **Volume/Issue:** 5:81 (2026)
- **Received:** 9 June 2025
- **Accepted:** 20 February 2026
- **Published online:** 19 March 2026
- **DOI:** 10.1038/s44172-026-00632-5
- **License:** Open access, CC BY-NC-ND 4.0
- **Corresponding author:** Ravi Tejwani (tejwanir@mit.edu)
- **Data:** https://doi.org/10.17632/bgybkjtpn9.2
- **Code:** https://github.com/robot-guidance-controller/robot-guidance-controller/ (confirmed as the official repo by the paper's own data/code availability statement — see `publications/github-robot-guidance-controller-repo.md` for what was archived from it)

## Author List & Affiliations

1. **Ravi Tejwani** — Electrical Engineering and Computer Science, MIT
2. **John Payne** — Electrical Engineering and Computer Science, MIT
3. **Karl Velazquez** — Electrical Engineering and Computer Science, MIT
4. **Paolo Bonato** — Department of Physical Medicine, Harvard Medical School; Spaulding Rehabilitation Hospital
5. **Harry Asada** — Mechanical Engineering, MIT

## Author Contributions (verbatim from paper)

> "R.T. conceived the project, developed the controller, and wrote the manuscript. J.P. and K.V. contributed to the implementation of the controller, designed the experiments, data collection and analysis, and wrote the manuscript. P.B. provided clinical expertise and access to rehabilitation facilities. H.A. supervised the project and provided guidance on robot control methodology. All authors reviewed and approved the final manuscript."

So: Tejwani conceived the project and developed the core controller; Payne and Velazquez implemented the controller, designed/ran the experiments, did data collection and analysis, and co-wrote the manuscript alongside Tejwani — consistent with Karl's framing of himself as a main contributor.

## Abstract (full)

> "When human instructors guide learners through motor tasks, they seamlessly coordinate physical touch with verbal explanations - a dance teacher positions a student's arms while describing the movement, a therapist supports a patient's limb while offering encouragement. In contrast, a robot applying physical forces without verbal context can feel invasive or unsettling to humans. We present a robot guidance controller that learns to coordinate physical and verbal guidance as human instructors naturally do. Our system adaptively balances these modalities based on real-time estimation of human compliance: when learners struggle, it provides firmer physical corrections with explicit instructions; as they improve, it transitions to lighter touch with encouraging phrases. Our method comprises three components: (1) an estimator that infers physical and verbal compliance from tracking errors, (2) an optimization method that dynamically allocates guidance between force and language, and (3) a force-to-language model that generates contextually appropriate utterances. User studies (N=12) demonstrate that adaptive coordination of guidance significantly outperforms single-modality guidance and fixed-combination baselines: up to 50% reduction in tracking error, 39% improvement in movement smoothness, and 27% faster task completion. While validated in rehabilitation therapy, our approach generalizes to any human-robot collaborative learning scenario."

## System overview

A "Robot Guidance Controller" for a UR5 robot arm that adaptively allocates **physical** (force) vs. **verbal** guidance to a human learner, driven by a real-time Bayesian estimate of the learner's "compliance" (physical and verbal compliance, each modeled as binary low/high states). Three components:

1. **Bayesian compliance estimator.** Infers physical compliance (P) and verbal compliance (V) from position/velocity tracking errors in real time.
2. **Allocation optimizer.** A quadratic-program optimizer distributes weights A_p / A_v (summing to 1) between the physical and verbal guidance channels based on the estimated compliance state. Cost structure is deliberately asymmetric and matches real therapist behavior: the cost of physical guidance *rises* as physical compliance rises (don't keep pushing once it's working), while the cost of verbal guidance *rises* as verbal compliance *falls* (stop talking if the person is tuning it out).
3. **Force-to-language model.** Converts the verbal guidance "wrench" (see control theory below) into an actual spoken phrase, drawn from a therapist-style phrase library, delivered via Festival/GNUspeech text-to-speech. This model is built directly on Karl's own RSS 2025 paper — reference 25 in this Nature paper is literally: *"Tejwani, R., Velazquez, K., Payne, J., Bonato, P. & Asada, H. Cross-modality embedding of force and language for natural human-robot communication. In Proceedings of Robotics: Science and Systems (Los Angeles, California, 2025)."* This confirms the Nature paper is a direct extension/application of the RSS 2025 work, by the same core team.

## Control theory

Built on an admittance-control formulation: M𝑥̈ + B𝑥̇ = U_p + F_h, where the total guidance wrench U is decomposed into a physical component U_p and a verbal component U_v (U = U_p + U_v), constructed so that U_v cancels out of the physical dynamics entirely — meaning pure language doesn't physically perturb the robot. U_v is a "virtual" wrench representing the intended force-content of speech (e.g., "push harder" carries directional/magnitude force semantics without any actual force). The paper proves the controller is **passive** (Theorem 1), via a storage function combining kinetic and potential tracking-error energy — i.e., the system provably cannot inject net energy into the human-robot system, which is the standard safety requirement for physical human-robot interaction (pHRI).

## Observational study (motivating the design)

Conducted at Spaulding Rehabilitation Hospital: the team observed the hospital's Chief Physical Therapist guiding patients through shoulder-flexion exercises under four conditions (reference-only, verbal-only, physical-only, combined), 10 trials each, to derive the adaptive patterns that motivated the controller design. Key observed patterns:
- Median physical force dropped from **2.33 N** at low compliance to **1.12 N** at high compliance.
- Speaking frequency dropped from **1.77 to 0.36 words/sec** as verbal compliance rose.
- Instructional-to-encouraging phrase ratio shifted from **3.67 to 1.60** as compliance rose.

## User study

- **N=12** MIT students (8 male / 4 female, mean age 23).
- IRB-approved: MIT COUHES Protocol #2212000845R001.
- Within-subjects design on a UR5 robot arm with a 6-DOF force/torque sensor at the end-effector.
- Compared four conditions: verbal-only, physical-only, a fixed-weight combined baseline, and the adaptive Robot Guidance Controller (their method).

**Results:**
- Adding the missing modality when one was being ignored produced the largest single gains — up to a **73% drop in position error**.
- The full adaptive controller beat the fixed-weight combined baseline by **13–50%** on position/velocity accuracy and **8–50%** on smoothness, and completed tasks **27% faster**.
- Post-experiment interviews/Likert ratings: the adaptive dual-modal approach was rated significantly more "natural" (M=5.8/7) than the fixed combined baseline (M=4.1/7, p<0.01, Cohen's d=1.58).
- **11 of 12** participants preferred the adaptive approach over any single-modality condition.

## Real-time implementation & safety

- UR5 via Universal Robots' RTDE interface.
- Admittance control loop running at **200 Hz** (sub-5ms force feedback latency).
- Bayesian compliance filter + allocation optimization running at **1 Hz**.
- Festival TTS for speech output.
- Safety: ISO/TS 15066 + ISO 10218 compliant; end-effector velocity capped at 250 mm/s during contact; 50 N force threshold with automatic intervention; e-stop accessible to all participants.

## Data & code availability

- Dataset: https://doi.org/10.17632/bgybkjtpn9.2
- Code: https://github.com/robot-guidance-controller/robot-guidance-controller/ — confirmed by the paper itself as the official repository (not Karl's own GitHub account — see `publications/github-robot-guidance-controller-repo.md`).

