This file covers 5 peer-reviewed conference and journal papers in the Obfuscation category published in Q1 2026 (January to March). Preprints (arXiv, IACR ePrint) are excluded.

---

# From Obfuscated to Obvious: A Comprehensive JavaScript Deobfuscation Tool for Security Analysis
> NDSS 2026 (Network and Distributed System Security Symposium), presented February 2026
> 2026

Malicious JavaScript evades static analysis with layered obfuscation such as string encoding, function-name scrambling, and anti-analysis tricks. Existing deobfuscators fail on diverse input formats or handle only specific obfuscation types, and their output is hard to read. JSIMPLIFIER is a deobfuscation tool that chains preprocessing, AST-based static analysis, dynamic execution tracing, and LLM-based identifier renaming to address this. The authors also release a public dataset of over 44,000 samples (23,212 real malicious and 21,209 benign).

Paper: https://www.ndss-symposium.org/ndss-paper/from-obfuscated-to-obvious-a-comprehensive-javascript-deobfuscation-tool-for-security-analysis/

### Contribution
- A comprehensive deobfuscation tool that combines two strategies (static AST analysis and controlled execution) with LLM-based semantic enhancement, aiming at readable code recovery.
- Multi-dimensional evaluation metrics combining control and data flow, degree of code simplification, entropy, and LLM-based readability.
- The largest released dataset of real-world obfuscated JavaScript.

### Evaluation
- It reports 100% processing capability across 20 obfuscation techniques, 100% syntactic correctness on the evaluation subset, 88.2% Halstead complexity reduction, and more than fourfold readability improvement validated by several LLMs.
- Semantic consistency was 83%, above GPT (74.29%) and the earlier tool JST (55.32%). LLM experiments cost about $480 to $500 with GPT-4o-mini, and the authors note core claims can be validated in AST-only mode.
- "100% processing capability" means no processing failures, and recovery correctness is on a manually verified subset, so it should not be read as 100% overall recovery quality.

#### Comment
- For anyone building JavaScript obfuscation tools, the released large dataset and multi-dimensional metrics are directly usable as a deobfuscation research benchmark.
- Verification of a Chinese institution: joint work by Beijing University of Posts and Telecommunications and the QI-ANXIN research institute. Code and datasets are on Zenodo and GitHub for reproduction, the metrics and costs are reported transparently, and the numbers are presented without exaggeration, so the paper is included. QI-ANXIN is a major, clearly real Chinese security company.

---

# WBSLT: A Framework for White-Box Encryption Based on Substitution-Linear Transformation Ciphers
> NDSS 2026 (Network and Distributed System Security Symposium), presented February 2026
> 2026

The white-box threat model assumes an attacker with full control of the cryptographic implementation and its execution environment, which fits unattended settings such as IoT devices. Prior white-box designs mostly protected a single key-dependent table, letting white-box and side-channel attacks recover the key. WBSLT is a design framework for tabulated white-box implementations of substitution-linear transformation (SLT) ciphers such as AES and SERPENT. It defers part of each component's computation to the next, blurring table boundaries to defeat single-table attacks, and adds masking, shuffling, and external encoding to resist differential computation analysis and differential fault analysis.

Paper: https://www.ndss-symposium.org/ndss-paper/wbslt-a-framework-for-white-box-encryption-based-on-substitution-linear-transformation-ciphers/

### Contribution
- A white-box implementation framework applicable to arbitrary SLT ciphers that defends algebraic cryptanalysis by blurring component boundaries.
- A comprehensive security analysis under two definitions, unbreakability and one-wayness, with a claim of achieving unbreakability, which the authors say prior schemes do not.
- A new security metric, the distinguishable SA-structure number, to measure the blurring between rounds.

### Evaluation
- Encryption speed, memory, and energy were measured on four high-performance and four resource-limited platforms (including a Raspberry Pi and smartphones). The optimized WB-AES fit 20 of 23 popular IoT gateways (86.96%).
- The IDDHO-DCA attack success rate dropped from 100% without the defense to 0.40% with it, effectively random guessing. The authors compare it as matching Chow et al.'s WB-AES in performance while being more secure.
- There is storage overhead versus plain AES, and much of the security claim rests on theoretical analysis, so independent cryptanalysis is still needed.

#### Comment
- For work on binary hardening and white-box cryptography, the limits of single-table protection and the boundary-blurring design idea are directly relevant.
- Verification of a Chinese institution: from Tongji University, with code on GitHub and Zenodo. White-box ciphers are often broken after publication, so the unbreakability claim deserves caution, but the paper reports measured attack-success reductions and releases the implementation for reproduction and refutation, so it is included.

---

# Empirical assessment of the code comprehension effort needed to attack programs protected with obfuscation
> Computers & Security (Elsevier), journal article
> 2026

Obfuscation is widely used, but how much it actually slows an attacker's comprehension of code has rarely been evaluated rigorously. This paper designs a controlled experiment in which Master's students perform code-comprehension tasks on obfuscation-protected programs. It has two goals: to measure whether obfuscation really delays an attacker's comprehension, and to determine whether complexity metrics can predict the protective effect on the success rate and duration of comprehension tasks.

Paper: https://arxiv.org/abs/2511.21301 (journal version in Computers & Security)

### Contribution
- Described as the first study to evaluate obfuscation effectiveness through a human-subject controlled experiment, measuring its effect as a delay in comprehension.
- It examines whether complexity metrics can serve as predictors of protection, in terms of both success rate and task duration.

### Evaluation
- Master's students carried out code-comprehension tasks on obfuscated applications, and success rate and duration were measured.
- As a human-subject study, the participants are Master's students, who may differ from skilled real-world attackers. The sample and task scope limit how far the results generalize.

#### Comment
- For obfuscation-tool builders, the argument that protection should be judged by actual comprehension delay rather than by complexity metrics is practically useful and supports the view that metrics alone cannot justify a protection-strength claim.
- Joint work by Politecnico di Torino, CNR, and the University of Cagliari in Italy, published in Computers & Security. The full text is available on arXiv in addition to the journal version, which is how the content was verified.

---

# Securing Symmetric Encryption Based on Substitution-Permutation Network Against White-Box Attacks
> IEEE Transactions on Information Forensics and Security (TIFS), journal article
> 2026

The security of symmetric ciphers has mostly been studied in the black-box setting, where the execution platform is assumed secure. This paper proposes a new method to protect substitution-permutation network (SPN) ciphers in the white-box setting, where the attacker has full visibility into the implementation and full control of the platform. The key idea is to add secret components into lookup tables to greatly expand and alter the cipher's internal state, targeting the fact that most prior approaches have been broken.

Paper: https://doi.org/ (IEEE TIFS, 2026)

### Contribution
- Protects SPN-based symmetric ciphers in the white-box setting by adding secret components to lookup tables to expand the internal state.
- Frames the problem around the many broken prior white-box schemes and presents a design intended to raise resistance to key recovery.

### Evaluation
- (This summary is based on the abstract. The full text could not be obtained, so experimental details and figures were not verified.) The abstract goes as far as noting the weakness of prior approaches and claiming resistance for the new design.

#### Comment
- Read alongside NDSS 2026's WBSLT on the same topic, it offers a comparison point for recent white-box symmetric-cipher protection designs.
- Verification of a Chinese institution: joint work by Tongji University and Hong Kong Polytechnic University (Xiapu Luo, a well-known software-security researcher). The venue, IEEE TIFS, is a top-tier security journal with clear indexing and reputation. This entry is based only on the abstract because the full text could not be opened, so detailed assessment requires checking the original.

---

# GAEDM: Genetic Algorithm-Enhanced Static Analysis for Detection of API Hashing Obfuscation in Malware
> ACM Transactions on Privacy and Security (TOPS), journal article
> 2026

Malware authors hide system calls with API hashing, replacing function names with hashes computed at runtime to evade detection. This creates three difficulties: locating the hash function inside obfuscated code, linking a computed hash back to its API call, and detecting the growing variety of hash-algorithm variants. GAEDM is a deobfuscation-oriented framework that combines static taint analysis with a genetic-algorithm-enhanced assembly language model, generating diverse training variants to detect previously unseen hash variants.

Paper: ACM TOPS, 2026

### Contribution
- Approaches API-hashing detection by combining deep learning with program analysis and diversifying training variants via a genetic algorithm to improve robustness against unknown hash variants.
- Also tackles linking computed hashes back to their API calls through static taint analysis.

### Evaluation
- (This summary is based on the abstract. The full text could not be obtained, so dataset, baselines, and accuracy details were not verified.)

#### Comment
- API hashing is a classic Windows-malware evasion technique, which is why this is filed under deobfuscation; the approach itself is worth noting for binary-analysis tooling.
- Verification of a Chinese institution: work from Chinese institutions including a Ministry of Education cyberspace-security lab, published in ACM TOPS, a well-regarded security journal. However, the full text could not be opened, so this entry rests on the abstract and the credibility of the reported figures was not verified; the original should be checked. Given this limitation, future collections should confirm full-text availability first.
