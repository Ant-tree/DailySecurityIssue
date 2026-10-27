This file covers 8 peer-reviewed conference and journal papers in the Mobile category published in Q2 2026 (April to June). Preprints (arXiv, IACR ePrint) are excluded.

- Malware and Analysis (2)
- Privacy (4)
- Other (2)

---

**Subcategory: Malware and Analysis**

# MalPurifier: Enhancing Android Malware Detection With Adversarial Purification Against Evasion Attacks
> IEEE Transactions on Dependable and Secure Computing (TDSC), journal article
> 2026

ML-based Android malware detectors are vulnerable to evasion attacks built from adversarial examples that modify non-functional instructions. MalPurifier is an adversarial-purification framework targeting this: it injects a diverse range of perturbations to improve robustness and generalization, injects protective noise into benign data, and uses a denoising autoencoder (DAE) with a dual reconstruction-and-prediction loss to purify and classify.

Paper: https://arxiv.org/abs/2312.06423 (journal version: IEEE TDSC, 2026)

### Contribution
- A purification framework tailored to Android's discrete feature space and diverse attack vectors, injecting everything from no perturbation to worst-case perturbations to harden against unforeseen attacks.
- A DAE-based purification model independent of the label space and detection model, acting as a lightweight, model-agnostic plug-in module.

### Evaluation
- Across the Drebin and AndroZoo datasets it withstood 37 perturbation-based evasion attacks, holding robust accuracy above 90.91%.
- On clean data its false-positive rate stayed low (2.55% on Drebin, 2.30% on AndroZoo), with small clean-accuracy loss (1.72% and 0.66%).
- Reproducible with public datasets and code (full text on arXiv), with clear grounds from comparisons against many recent defenses.

#### Comment
- Treating adversarial purification as a plug-in module separate from the detector is directly applicable when adding defenses to a production Android malware-detection engine.
- Verification of a Chinese institution: work from Southeast University (Yuyang Zhou, Guang Cheng) and others, published in IEEE TDSC, a top-tier security journal. The full text on arXiv let the experimental details (dataset construction, compared defenses, figures) be checked directly; it uses public code and datasets and reports trade-offs without exaggeration, so the paper is included.

---

# Understanding Concept Drift With Deprecated Permissions in Android Malware Detection
> IEEE Transactions on Dependable and Secure Computing (TDSC), journal article
> 2026

Android's permission system evolves as permissions are deprecated, restricted, or reserved for system use, which shifts the feature space for malware detection and introduces concept drift. This paper studies how those changes affect machine learning models, using a dataset of over 70,000 apps and 166 permissions.

Paper: IEEE TDSC, 2026

### Contribution
- A systematic, large-scale analysis of the concept drift that deprecated, restricted, and system-only permission changes cause in the detection feature space.
- Quantifies how time-aware permission selection and dataset balancing affect detection performance.

### Evaluation
- (This summary is based on the abstract; only some details were verified as the full text was unavailable.) Removing restricted permissions without considering time reduced accuracy by 1.3 to 2.1 percentage points, while excluding deprecated or not-for-third-party permissions had marginal effect. Training on one year and testing on others, dataset balancing improved F1.

#### Comment
- A practical reference showing that permission-system changes erode detection performance over time for anyone running permission-based Android malware-detection models.
- IEEE TDSC is a top-tier security journal. This entry rests on the abstract because the full text could not be opened, so detailed assessment requires checking the original.

---

**Subcategory: Privacy**

# Exercising the CCPA Opt-out Right on Android: Legally Mandated but Practically Challenging
> PoPETs 2026 Issue 2 (Privacy Enhancing Technologies Symposium), journal-style conference
> 2026

Many mobile apps' business model relies on sharing user data with ad networks, and the California Consumer Privacy Act (CCPA) gives residents the right to opt out of that sharing. This paper evaluates, in two experiments, how far popular Android apps actually honor the right. Exercising it manually through app UIs, only 48 of 100 apps offered the setting; sending Global Privacy Control (GPC) signals automatically across an 1,811-app dataset, GPC was largely ineffective.

Paper: https://petsymposium.org/popets/2026/popets-2026-0065.pdf

### Contribution
- Measures a compliance gap showing the CCPA opt-out right cannot be effectively exercised on Android at either the app or the platform level.
- Proposes concretely that repurposing the Android Advertising ID (AdID) setting as a CCPA opt-out setting could close the gap.

### Evaluation
- With 95% confidence, 62% to 81% of dataset apps are estimated to be required to honor the opt-out right, yet many did not. Even sending GPC signals and disabling AdID access, 338 apps still had the Vungle ad network set to opted_in and only 26 to opted_out.
- Both experiments rest on real apps and traffic measurement, giving clear grounds. Results depend on the app versions and ad-network behavior at measurement time.

#### Comment
- From a mobile-security view concerned with advertising IDs and tracking identifiers, it is a useful empirical account of the gap between platform settings and legal rights.
- Joint work by Wesleyan University and Maastricht University, with open PDF and GitHub code, published in PoPETs.

---

# FreeLens: Revealing Mobile App Feature Differences and Their Security and Privacy Implications Across Geographical Regions
> IEEE Transactions on Dependable and Secure Computing (TDSC), journal article
> 2026

Mobile apps ship different versions by region to fit local regulations and market preferences. Where prior work examined metadata differences such as permissions and privacy policies, this paper is the first systematic study of code-implementation-level geographic differences (GFDs) that may affect security. FreeLens is a framework that overcomes challenges such as code obfuscation and analysis scalability to identify these differences.

Paper: IEEE TDSC, 2026

### Contribution
- The first systematic study of code-level geographic differences in Android apps.
- FreeLens, a framework that identifies regional feature differences despite code obfuscation and large-scale analysis difficulty.

### Evaluation
- (This summary is based on the abstract; dataset size and detailed figures were not verified as the full text was unavailable.) The abstract goes as far as identifying code-level regional differences and analyzing their security and privacy implications.

#### Comment
- The point that region-specific app versions can create security and privacy gaps is worth noting for teams shipping multi-country SDKs, and treating code obfuscation as an analysis challenge is interesting.
- IEEE TDSC is a top-tier journal. This entry is abstract-based, so detailed assessment requires the original.

---

# PriLabel: Toward Comprehensively Uncovering Omitted Disclosures in Privacy Labels of Android Apps on a Large Scale
> IEEE Transactions on Information Forensics and Security (TIFS), journal article
> 2026

Privacy labels (such as the Data Safety section on Google Play) aim to replace long privacy policies with concise, standardized summaries. Studies have repeatedly found omissions and misrepresentations in these self-reported labels. This paper proposes Iterative Context Reconstruction (ICR), an evidence-driven workflow that reconstructs context to find such discrepancies at scale, addressing the semantic ambiguity inherent in label auditing.

Paper: IEEE TIFS, 2026

### Contribution
- An ICR workflow targeting the coverage and scalability earlier methods lacked, along with the semantic ambiguity of label auditing.
- Systematically uncovers omitted disclosures in privacy labels at scale.

### Evaluation
- (This summary is based on the abstract; dataset and accuracy figures were not verified as the full text was unavailable.)

#### Comment
- Auditing the gap between apps' real data collection and their declared labels at scale is a useful reference for anyone dealing with mobile privacy compliance and SDK data flows.
- IEEE TIFS is a top-tier journal. This entry is abstract-based, so detailed assessment requires the original.

---

# SentinelTouch: A Lightweight Privacy-Preserving Biometric-Fingerprinting Authentication and Identification System Based on Neural Networks and Homomorphic Encryption
> PoPETs 2026 Issue 2 (Privacy Enhancing Technologies Symposium), journal-style conference
> 2026

A leaked fingerprint cannot be changed, so secure storage and computation matter. Homomorphic encryption (HE) gives strong privacy by computing on encrypted data, but the high dimensionality of fingerprint images and the complexity of accurate neural networks had blocked practical use. SentinelTouch is an open framework that combines a preprocessing pipeline reducing fingerprint images to as small as 28x28 while preserving discriminative detail with a lightweight, HE-friendly neural network that generalizes on the compact data.

Paper: https://petsymposium.org/popets/2026/popets-2026-0041.pdf

### Contribution
- Two optimizations, fingerprint dimensionality reduction and an HE-friendly lightweight network, bring encrypted fingerprint authentication and identification to a practical level.
- Presents and releases both a full-privacy pipeline and a hybrid pipeline that encrypts only embeddings.

### Evaluation
- The full-privacy pipeline performs one-to-many identification in 16 seconds and the hybrid pipeline in 284 milliseconds, reported as 10x and 2.5x speedups over state-of-the-art results.
- On the SOKOTO and PolyU datasets, Rank-1 accuracy was within ±0.1% of leading encrypted systems.
- Evaluated on public fingerprint datasets for reproducibility; note it uses dataset images rather than fingerprints captured from real mobile sensors.

#### Comment
- As a case of bringing HE into a practical latency range for cloud or server authentication that must take biometrics off the device, it is a useful reference for on-device or server-linked biometric authentication design.
- From the STAM Center at Arizona State University, with code on GitHub, published in PoPETs.

---

**Subcategory: Other**

# Can Vibration Patterns Identify Users? Authentication for Smartphone-Watch Collaboration
> IEEE Transactions on Dependable and Secure Computing (TDSC), journal article
> 2026

Traditional authentication such as passwords and fingerprints is vulnerable to forgery and replay. This paper studies how active vibration signals propagate through the hand and wrist during natural touch and shows that individual differences in wrist structure and micro-dynamics produce stable, distinguishable vibration responses. Based on this, it proposes VIP, a dual-device authentication system using both a smartphone and a smartwatch: both devices generate vibration and collect responses with accelerometers, gyroscopes, and magnetometers, which a TouchFormer model uses to identify the user.

Paper: IEEE TDSC, 2026 (full text verified)

### Contribution
- VIP, an authentication system using active vibration from both phone and watch, designed to deploy on commercial devices with no extra hardware.
- TouchFormer, a model that extracts direction-sensitive features under multi-axis, cross-modal, asynchronous conditions to fuse multiple signals.
- A measured dataset spanning users of different gender, age, and body structure across varied interaction scenarios (wearing tightness, palm humidity, and so on).

### Evaluation
- Data were collected over four months (IRB approved) from 30 legitimate users and 7 impersonation attackers on four commercial phones and a Redmi Watch 5; TouchFormer averaged 98.65% accuracy, ahead of prior methods.
- False-acceptance rates under simulated and replay attacks were 1.55% and 2.71%, on average 0.61 and 0.28 percentage points lower than prior work; at 60% vibration intensity, FAR was 0.34% and FRR 1.35%.
- With 30 users it is a modest-scale study needing further generalization, mitigated by 5-fold cross-validation.

#### Comment
- Behavioral biometric authentication pairing a wearable and a phone is a useful reference for mobile runtime protection and user-authentication design, and the sensor-response basis is interesting from a device-hardening view. It is filed under "Other" as it does not fit the three mobile subcategories exactly.
- Verification of a Chinese institution: a collaboration among Chang'an University, Xi'an Jiaotong University, and Jinan University with the University of Essex (UK) and Edith Cowan University (Australia). IEEE TDSC is a top-tier journal, and the verified full text shows concrete methodology (IRB approval, cross-validation, per-attack figures) with results reported without exaggeration, so the paper is included.

---

# Security risk assessment of android automotive OS software supply chain using firmware reverse engineering
> Computers & Security (Elsevier), journal article
> 2026

Android Automotive OS (AAOS) is becoming the in-vehicle platform for infotainment and domain-controller functions in modern cars, spanning both infotainment and vehicle-control domains while supporting media streaming, over-the-air updates, navigation, and sensor fusion. Its open-source foundations and reliance on third-party libraries introduce risks, from outdated components to malicious modules, that can undermine vehicle functionality and passenger safety. This paper assesses the security risks of the AAOS software supply chain through firmware reverse engineering.

Paper: Computers & Security, 2026

### Contribution
- Treats the AAOS software supply chain as a security-risk-assessment target through firmware reverse engineering.
- Highlights outdated-component and third-party-library risks on a platform spanning infotainment and vehicle control.

### Evaluation
- (This summary is based on the abstract; the number of firmware images analyzed and detailed results were not verified as the full text was unavailable.)

#### Comment
- Covering the supply chain and firmware reverse engineering of an automotive Android platform makes it an interesting extension from a mobile/embedded hardening and binary-analysis perspective. It is filed under "Other" as it does not fit the mobile subcategories exactly.
- Computers & Security is a reputable security journal. This entry is abstract-based, so detailed assessment requires the original.
