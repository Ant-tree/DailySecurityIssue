This file covers 2 peer-reviewed conference and journal papers in the AI Security category published in Q2 2026 (April to June). Preprints (arXiv, IACR ePrint) are excluded.

---

# CURE: Privacy-Preserving Split Learning Done Right
> PoPETs 2026 Issue 2 (Privacy Enhancing Technologies Symposium), journal-style conference
> 2026

Split Learning divides model layers between client and server for distributed training and reduces privacy risk by limiting the server's access to the full parameter set. Yet the intermediate outputs exchanged between server and client can compromise client data privacy, and homomorphic-encryption (HE) solutions often impose heavy computation. CURE is an HE-based system for the single-client setting that encrypts only the server side of the model (and optionally the data), substantially improving communication and parallelization.

Paper: https://petsymposium.org/popets/2026/popets-2026-0047.pdf

### Contribution
- CURE, a split-learning system that ensures confidentiality of labels and optionally data with HE in a single-server, single-client setting.
- Two packing schemes for efficient computation, generalized to multi-layer server operations, enabling evaluation of ResNet blocks under encryption.
- The first estimator that recommends the optimal network split given server and client resources.

### Evaluation
- It maintains accuracy similar to plaintext split learning while being up to 210x faster in runtime than state-of-the-art privacy-preserving alternatives.
- Public code and an open HE API for deep learning support reproduction and extension.
- Focused on the single-client setting, so extension to multi-party settings is separate future work.

#### Comment
- Blocking intermediate-output leakage with HE in edge-cloud split inference and training while keeping latency practical is a direct reference for on-device LLM and split-inference security.
- Joint work by Koç University and Bilkent University (Türkiye), with open PDF and GitHub code, published in PoPETs.

---

# Privacy Bias in Language Models: A Contextual Integrity-based Auditing Metric
> PoPETs 2026 Issue 2 (Privacy Enhancing Technologies Symposium), journal-style conference
> 2026

As LLMs are integrated into sociotechnical systems, examining the privacy biases they exhibit matters. This paper draws on Contextual Integrity (CI) theory to define "privacy bias" as the appropriateness value of information flows in LLM responses. The deviation between privacy biases and expected values (the privacy bias delta) can indicate privacy violations, and the metric can help model trainers, service providers, and policymakers audit LLM chatbots and agents.

Paper: https://petsymposium.org/popets/2026/popets-2026-0062.pdf

### Contribution
- Argues that prior LLM privacy evaluations conflate CI with data minimization or category protection, and defines an auditing metric faithful to CI principles.
- Presents a method to evaluate multiple LLMs' responses while accounting for response sensitivity across prompt variations.

### Evaluation
- Evaluates several LLMs' responses with a CI-based methodology and accounts for sensitivity across prompt variations; the methodology is verifiable from the open PDF.
- Because the metric rests on a normative judgment of "appropriateness," interpretation can shift with the chosen expected values, which the authors treat as a premise.

#### Comment
- A framework for normatively auditing whether LLM chatbots and agents leak information inappropriately is a useful reference for designing privacy evaluation of on-device assistants.
- Joint work by York University and the University of Waterloo, published in PoPETs.
