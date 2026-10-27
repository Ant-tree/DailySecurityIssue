This file covers 4 peer-reviewed conference and journal papers in the AI Security category published in Q3 2026 (July to September). Preprints (arXiv, IACR ePrint) are excluded.

---

# Measuring Real-World Prompt Injection Attacks in LLM-based Resume Screening
> USENIX Security 2026 (35th USENIX Security Symposium), presented August 2026
> 2026

As LLMs are used for resume screening, prompt injection where applicants embed instructions in their resumes to steer the screening model actually happens. This paper measures these real-world prompt-injection attacks in LLM-based resume screening, analyzing how widespread they are, what forms they take, and how they affect actual screening outcomes.

Paper: https://www.usenix.org/conference/usenixsecurity26/presentation/zhang-mohan

### Contribution
- Measures the real occurrence and effect of prompt injection in the concrete application of resume screening.
- Quantifies how far attacks shift screening outcomes in the attacker's favor, giving concrete evidence of the practical threat.

### Evaluation
- Evaluated by measuring the occurrence and impact of prompt injection in an LLM-based resume-screening setting; the method is verifiable from the open PDF.
- As a measurement focused on one application (hiring), generalization depends on how the screening pipeline is built.

#### Comment
- A canonical indirect-injection case where external input (a resume) steers an LLM's judgment, useful for input-trust design in any mobile or server application that feeds user data to an LLM.
- Joint work by UNC Chapel Hill, Duke University, Arizona State University, and UC Berkeley, published at USENIX Security.

---

# Overcoming the Retrieval Barrier: Indirect Prompt Injection in the Wild for LLM Systems
> USENIX Security 2026 (35th USENIX Security Symposium), presented August 2026
> 2026

As LLM systems retrieve information from external corpora, indirect prompt injection (IPI) becomes a new attack surface. Prior work flagged the risk but avoided the hardest step: ensuring the malicious content is actually retrieved. In practice, unoptimized IPI is rarely retrieved under natural queries, leaving its real-world impact unclear. This paper decomposes malicious content into a trigger fragment that guarantees retrieval and an attack fragment encoding the objective, designing an efficient black-box attack that overcomes the retrieval barrier.

Paper: https://www.usenix.org/conference/usenixsecurity26/presentation/chang-hongyan

### Contribution
- Tackles head-on the "getting retrieved" step of indirect prompt injection that prior work avoided.
- Separates a trigger fragment from an attack fragment to achieve both guaranteed retrieval and delivery of the attack objective in a black-box attack algorithm.

### Evaluation
- Evaluated by measuring both the real retrieval rate of injected content and attack success in retrieval-based LLM systems; the method is verifiable from the open PDF.
- Addressing a realistic threat model that includes the retrieval step distinguishes it from prior work and highlights, for defense, the importance of the retrieval stage.

#### Comment
- The point that injection must actually be retrieved for the threat to hold in RAG architectures shows that defenses for on-device and server LLMs pulling in external knowledge must consider the retrieval stage.
- From the Mohamed bin Zayed University of Artificial Intelligence (MBZUAI), published at USENIX Security.

---

# SoK: Attack and Defense Landscape of Agentic AI Systems
> USENIX Security 2026 (35th USENIX Security Symposium), presented August 2026
> 2026

This systematization-of-knowledge paper comprehensively maps the attack and defense landscape of agentic AI systems from a system perspective. It characterizes agents through seven design dimensions (input trust, access sensitivity, workflow, action, memory, tool, and user interface) and analyzes how flexibility along each affects security risk. Defenses are organized into three categories: runtime protection, secure-by-design, and component hardening.

Paper: https://www.usenix.org/conference/usenixsecurity26/presentation/

### Contribution
- A systematic framework characterizing agentic AI systems through seven design dimensions, analyzing the relationship between flexibility in each and security risk.
- Classifies defenses into runtime protection, secure-by-design, and component hardening, identifying specific design dimensions and open challenges.
- Presented as the first systematic analysis of agent security from a comprehensive system perspective.

### Evaluation
- A systematization that classifies and contrasts attacks and defenses along design dimensions, focused on structuring the overall landscape rather than measuring individual techniques.
- Provides a foundational framework for understanding agent security risks and defense strategies.

#### Comment
- As a landscape covering agent-security architectures such as Q1's ACE and SAGA, it is a good starting point for organizing threat models and defense design for on-device agents.
- Published at USENIX Security.

---

# Patcher: Post-Hoc Patching of Backdoored Large Language Models
> USENIX Security 2026 (35th USENIX Security Symposium), presented August 2026
> 2026

Large language models can be manipulated by backdoors planted during training so that specific triggers produce attacker-intended output. Patcher is a defense that patches an already-backdoored LLM after the fact to neutralize the backdoor, aiming to remove it at the post-deployment stage without retraining the model from scratch.

Paper: https://www.usenix.org/conference/usenixsecurity26/presentation/gao-anjun

### Contribution
- A defense that patches a backdoored LLM post-hoc to remove the backdoor without retraining.
- Aims at practical applicability as a defense that can be applied after deployment.

### Evaluation
- (The full text was retrieved, but the summary digest did not surface enough detailed figures. The evaluation consists of measuring backdoor-removal effectiveness across several attacks and the preservation of normal performance.)
- Post-hoc patching is realistic for large models where retraining is costly; specific figures are best confirmed against the original.

#### Comment
- Mitigating backdoor risk after deployment in settings that consume open-weight models has direct implications for anyone using external LLMs on-device or in-house.
- Joint work by the University of Louisville and the University of North Texas, published at USENIX Security.
