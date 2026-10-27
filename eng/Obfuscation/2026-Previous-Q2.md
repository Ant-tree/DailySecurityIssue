This file covers 4 peer-reviewed conference and journal papers in the Obfuscation category published in Q2 2026 (April to June). Preprints (arXiv, IACR ePrint) are excluded.

---

# DNN Obfuscation With Contrastive Learning for Efficient Defense Against Side-Channel Attacks
> IEEE Transactions on Dependable and Secure Computing (TDSC), journal article
> 2026

Deep neural networks risk model theft through side-channel attacks. Existing DNN-obfuscation defenses require impractical hardware modifications or scale poorly because of time-consuming deployment on target platforms. This paper's CLOb-DNN is a contrastive-learning framework that uses triplet networks to reduce the need for repeated physical deployment while improving the efficiency and robustness of obfuscation.

Paper: IEEE TDSC, 2026

### Contribution
- A framework that improves both the efficiency and robustness of DNN obfuscation through contrastive learning.
- Triplet networks reduce the burden of repeated physical deployment, easing the scalability problem.

### Evaluation
- (This summary is based on the abstract; evaluation data and figures were not verified as the full text was unavailable.)

#### Comment
- Obfuscating the model itself to prevent side-channel-based model theft is worth noting as a cross-topic between on-device model protection and binary hardening.
- Verification of Chinese institutions: a collaboration among Nanjing University, Ocean University of China, Imperial College London, and Nanyang Technological University. IEEE TDSC is a top-tier journal. This entry is abstract-based, so detailed assessment and the credibility of figures require the original.

---

# SOOM: A Schedule-Search-Based Operator Obfuscation Method Against Model Extraction Attacks
> IEEE Transactions on Information Forensics and Security (TIFS), journal article
> 2026

Model executables compiled efficiently by deep learning compilers can be reverse-engineered into trainable models, leading to further threats such as adversarial attacks. Prior defenses relied mainly on TEEs. SOOM is a method that obfuscates by searching over operator schedules at compile time to defend against model-extraction attacks.

Paper: IEEE TIFS, 2026

### Contribution
- A defense that searches and obfuscates operator schedules in deep-learning-compiler executables to make model extraction harder.
- Presents compile-level obfuscation as an alternative to TEE-dependent defenses.

### Evaluation
- (This summary is based on the abstract; experimental details and figures were not verified as the full text was unavailable.)

#### Comment
- Obfuscating the operator structure of compiled model binaries is interesting as it touches both model-extraction defense for on-device deployment and binary hardening.
- Verification of a Chinese institution: work from Nanjing University of Aeronautics and Astronautics. IEEE TIFS is a top-tier journal. This entry is abstract-based, so detailed assessment and the credibility of figures require the original.

---

# SemAder: Evading LLM-Based Binary Code Analysis via Structure-Semantics Joint Induction
> ACM Transactions on Privacy and Security (TOPS), journal article
> 2026

As LLMs are widely used for code comprehension and analysis, their strong semantic parsing introduces new software-security threats: attackers can use LLMs to reverse-engineer deeper code logic, steal core algorithms, or find vulnerabilities. SemAder is a structure-semantics joint-induction framework that generates adversarial yet function-preserving binaries to mislead LLMs' functional judgments, aiming to reduce the reliability of LLM-based binary analysis.

Paper: ACM TOPS, 2026

### Contribution
- A structure-semantics joint-induction framework that generates function-preserving adversarial binaries to mislead LLM binary analysis.
- Starts from a defensive motivation of protecting software intellectual property against LLM-based reverse engineering.

### Evaluation
- (This summary is based on the abstract; experimental details and figures were not verified as the full text was unavailable.)

#### Comment
- Obfuscating binaries against the trend of LLMs being used as reverse-engineering tools is a very direct reference for anyone building binary-hardening and obfuscation tooling; the focus on defending against LLM-based analysis is especially interesting.
- Verification of a Chinese institution: work from a Ministry of Education cyberspace-security lab, published in ACM TOPS, a well-regarded security journal. The full text could not be opened, so this entry rests on the abstract and the credibility of figures requires the original.

---

# Privacy-Preserving Data Completion With Location and Value Obfuscation in Spatial Crowdsourcing
> IEEE Transactions on Dependable and Secure Computing (TDSC), journal article
> 2026

Spatial crowdsourcing gathers broad data via mobile devices but faces data sparsity. Existing completion techniques that infer missing data from observed data require detailed spatial-temporal information, raising privacy concerns, and protecting via location obfuscation disrupts spatial-temporal correlations and increases errors. This paper proposes a differential-privacy-based obfuscation strategy intended to preserve privacy while maintaining data accuracy.

Paper: IEEE TDSC, 2026

### Contribution
- A differential-privacy strategy that obfuscates both location and value while preserving spatial-temporal correlations to maintain data-completion accuracy.

### Evaluation
- (This summary is based on the abstract; datasets and figures were not verified as the full text was unavailable.)

#### Comment
- It is filed under obfuscation because it balances location and value obfuscation with data completion, but note it concerns data obfuscation (differential privacy), not code obfuscation.
- Verification of Chinese institutions: a collaboration among Jilin University, China Telecom, and Northwestern Polytechnical University. IEEE TDSC is a top-tier journal. This entry is abstract-based, so detailed assessment requires the original.
