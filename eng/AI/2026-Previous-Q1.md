This file covers 5 peer-reviewed conference and journal papers in the AI Security category published in Q1 2026 (January to March). Preprints (arXiv, IACR ePrint) are excluded.

---

# ACE: A Security Architecture for LLM-Integrated App Systems
> NDSS 2026 (Network and Distributed System Security Symposium), presented February 2026
> 2026

LLM-integrated app systems answer user queries by alternating planning and execution while calling third-party apps, which lets a malicious app break the integrity of planning or execution or compromise availability and privacy. ACE splits planning into two phases: it first builds an abstract execution plan from trusted information only, then maps it to a concrete plan using installed apps. Static analysis on the structured plan output verifies that user-specified information-flow constraints hold, and during execution ACE enforces data and capability barriers between apps.

Paper: https://www.ndss-symposium.org/ndss-paper/ace-a-security-architecture-for-llm-integrated-app-systems/

### Contribution
- Three new attacks that break the planning integrity and the execution integrity and availability of the prior defense IsolateGPT.
- ACE, a secure-by-design architecture built on the insight that planning from trusted components only allows strong security policies to be enforced statically.
- App outputs are treated strictly as schema-defined data rather than LLM control flow, so indirect prompt injection cannot hijack control.

### Evaluation
- Using GPT-4o, o3-mini, GPT-4.1, Claude 3.7 Sonnet, and Qwen-2.5-72B as the underlying models, ACE blocked all indirect-prompt-injection attacks from INJECAGENT and Agent Security Bench as well as the newly introduced attacks.
- Real-world utility was measured on the LangChain Tool Usage benchmark, staying above 80%.
- Evaluation is limited to two benchmarks plus the authors' own attacks, so claiming the defense stops all injection variants needs further validation.

#### Comment
- The design principles of building the abstract plan from trusted information only and treating app outputs as data are worth noting when designing on-device agents or app-integrated security products.
- From Northeastern University (Alina Oprea, Cristina Nita-Rotaru), with code on GitHub, published at NDSS.

---

# Attention is All You Need to Defend Against Indirect Prompt Injection Attacks in LLMs
> NDSS 2026 (Network and Distributed System Security Symposium), presented February 2026
> 2026

LLM applications that pull in external data, such as web agents and email assistants, are vulnerable to indirect prompt injection, where instructions embedded in external data steer the model into doing what the attacker wants. RENNERVATE is a defense framework that uses attention features to detect covert injections at the token level and sanitize only those parts, neutralizing the attack while preserving functionality. A two-step attentive pooling over attention heads and response tokens forms the token-level detector.

Paper: https://www.ndss-symposium.org/ndss-paper/attention-is-all-you-need-to-defend-against-indirect-prompt-injection-attacks-in-llms/

### Contribution
- Token-level injection detection and sanitization using attention features, achieving high precision, strong transferability, and a compact parameter size at once.
- An identification algorithm that treats long runs of consecutive injected tokens as an attack signal.
- FIPI, a 100k-instance dataset with fine-grained labels covering five injection methods and 300 NLP tasks, to be open-sourced.

### Evaluation
- Across five architecturally diverse models (ChatGLM, Dolly, Falcon, LLaMA2, LLaMA3) and six datasets, it reports precision exceeding 15 commercial and academic defenses.
- It also shows transferability to unseen attacks and robustness against adaptive adversaries.
- The evaluated models are mostly open-weight LLMs, so effectiveness on proprietary closed models needs separate confirmation.

#### Comment
- Using attention signals for defense is a useful reference for designing injection defenses when on-device LLMs handle external data.
- Verification of a Chinese institution: from Yanjiao Chen's and Wenyuan Xu's group at Zhejiang University, which has a steady record at top security venues. The comparison against 15 prior defenses is concrete, the dataset is to be released for reproducibility, and the numbers are not skewed toward a particular model, so the paper is included.

---

# NeuroStrike: Neuron-Level Attacks on Aligned LLMs
> NDSS 2026 (Network and Distributed System Security Symposium), presented February 2026
> 2026

Safety alignment steers LLMs away from harmful output, but alignment based on supervised fine-tuning or RLHF is fragile and can be bypassed by crafted adversarial prompts. This paper identifies a root weakness: alignment relies on a sparse set of specialized "safety neurons" responsible for detecting and suppressing harmful inputs. NeuroStrike, a defensive vulnerability analysis, finds these neurons through feedforward activation analysis and prunes them at inference in the white-box setting, and in the black-box setting exploits their transferability via prompt generators trained on open-weight surrogate models.

Paper: https://www.ndss-symposium.org/ndss-paper/neurostrike-neuron-level-attacks-on-aligned-llms/

### Contribution
- Identifies the shared weakness that safety alignment depends on sparse, specialized safety neurons, and formalizes it into a generalizable attack framework.
- Presents both white-box neuron pruning and a black-box profiling attack using a prompt generator trained on surrogate models.
- Shows that safety neurons transfer across model variants, so the attack carries over to fine-tuned and distilled models.

### Evaluation
- Across more than 20 open-weight LLMs from Meta, Google, Alibaba, DeepSeek, and Microsoft, removing under 0.6% of neurons in targeted layers raised the average attack success rate from 12.1% to 76.9%.
- It reports 100% success on harmful image inputs for four multimodal models and an average 63.7% across five black-box models, including the Gemini family.
- Success is judged by classifying harmful output, so the metric depends on the classification criteria, and results against defended models are covered in a separate section.

#### Comment
- The finding that alignment concentrates in a few neurons has important implications for defense design and shows the robustness limits of alignment for anyone handling on-device open-weight models. This entry stays at the level of the vulnerability's existence and principle, not a reproducible attack procedure.
- Joint work by TU Darmstadt (Ahmad-Reza Sadeghi), the University of Zagreb, and Radboud University, published at NDSS.

---

# Shadow in the Cache: Unveiling and Mitigating Privacy Risks of KV-cache in LLM Inference
> NDSS 2026 (Network and Distributed System Security Symposium), presented February 2026
> 2026

The KV cache stores attention key-value pairs to speed up LLM inference. Even when user-server communication is encrypted, the KV cache is often transmitted and stored in plaintext, and this paper gives the first comprehensive analysis showing an adversary can reconstruct user input from the cache alone. It designs three attacks: an inversion attack that uses known model weights, a collision attack that compares caches of candidate inputs, and an injection attack that abuses the model's instruction-following. It then proposes KV-Cloak, a lightweight defense that protects the cache with reversible matrix-based obfuscation and operator fusion.

Paper: https://www.ndss-symposium.org/ndss-paper/shadow-in-the-cache-unveiling-and-mitigating-privacy-risks-of-kv-cache-in-llm-inference/

### Contribution
- Systematically exposes KV-cache privacy risks through three attacks (inversion, collision, injection); the collision attack is broadly applicable because it needs no reverse computation.
- Proposes KV-Cloak, a reversible matrix-obfuscation defense that protects the cache with little overhead and no accuracy loss.

### Evaluation
- It measures reconstruction quality under each attack and after defense, reporting that KV-Cloak reduces reconstruction to essentially random noise.
- The defense is reported to incur virtually no model-accuracy degradation and minimal performance overhead.
- Attacks and defense are evaluated by the same authors, so the defense's robustness should be further tested against independent adaptive attacks.

#### Comment
- The finding that input privacy can break in serving architectures that transmit or share the KV cache has direct implications for anyone working on on-device or edge-cloud split LLMs.
- Verification of a Chinese institution: joint work by Zhejiang University's State Key Laboratory of Blockchain and Data Security and Huawei. The lab has a steady record at top privacy-attack venues, both attacks and defense are backed by measurements, and the numbers are not skewed to particular conditions, so the paper is included. A code-release link was not confirmed, however.

---

# SAGA: A Security Architecture for Governing AI Agentic Systems
> NDSS 2026 (Network and Distributed System Security Symposium), presented February 2026
> 2026

LLM-based agents increasingly interact, collaborate, and delegate tasks to one another autonomously. Prior designs for agent identity, authorization, and delegation have mostly stayed theoretical and offered no way for users to control their own agents. SAGA is a security architecture that gives users oversight of their agents' lifecycle: users register agents with a central Provider that holds contact information and user-defined access-control policies and helps agents enforce them on inter-agent communication. A cryptographic mechanism derives access-control tokens for fine-grained control over agent interactions.

Paper: https://www.ndss-symposium.org/ndss-paper/saga-a-security-architecture-for-governing-ai-agentic-systems/

### Contribution
- A security architecture giving users control and oversight of their LLM agents, with access-control tokens encrypted under shared agent keys for fine-grained control of inter-agent communication.
- Token secrecy, agent-to-Provider authentication, and authentication between any two agents are formalized in ProVerif and automatically proven against an attacker who can observe, intercept, modify, and replay messages.

### Evaluation
- Several agentic tasks (scheduling meetings, submitting expense reports, collaborative writing) were evaluated with agents in different geolocations and multiple on-device and cloud LLMs.
- It reports minimal overhead with no loss of task utility across conditions, and the code is on GitHub.
- The design concentrates trust in a central Provider, so a compromised Provider falls outside its assumptions.

#### Comment
- Cryptographically enforcing user-controlled access policies on inter-agent communication is a useful reference model for securing on-device agents that interact with external agents.
- From Northeastern University (Cristina Nita-Rotaru, Alina Oprea), with formal proofs and public code, published at NDSS.
