This file covers 1 peer-reviewed conference and journal papers in the Other Notable Papers category published in Q1 2026 (January to March). Preprints (arXiv, IACR ePrint) are excluded.

---

# Unveiling BYOVD Threats: Malware's Use and Abuse of Kernel Drivers
> NDSS 2026 (Network and Distributed System Security Symposium), presented February 2026
> 2026

BYOVD (Bring Your Own Vulnerable Driver) attacks abuse legitimate, signed but flawed Windows drivers to enter kernel space and disable security controls. Because most public sandboxes inspect only user-mode activity, this kernel-level abuse evades detection. This paper presents the first dynamic taxonomy of BYOVD behavior, synthesized from real-incident analysis and kernel tracing, and proposes a virtualization-based sandbox that follows the execution path from the user-mode request down to the lowest kernel instructions without re-signing drivers or modifying the host.

Paper: https://www.ndss-symposium.org/ndss-paper/unveiling-byovd-threats-malwares-use-and-abuse-of-kernel-drivers/

### Contribution
- A "kill chain" taxonomy that breaks BYOVD attacks into five stages: driver dropping, loading, communication, execution complexity, and observable suspicious behavior.
- A DRAKVUF-based virtualization sandbox that deeply inspects kernel-mode activity triggered from user space and automatically generates a report against the taxonomy; released as open source.
- Designed to capture sequences not in the taxonomy, so it also handles unfamiliar BYOVD techniques.

### Evaluation
- Analyzing 8,779 malware samples that load 773 distinct signed drivers, it flagged suspicious behavior in 48 drivers.
- Manual verification led to responsible disclosure of seven previously unknown vulnerable drivers to Microsoft, vendors, and public threat-intelligence platforms.
- It shows that transparent tracing of kernel control flow can expose BYOVD abuse that traditional pipelines miss. As an offline analyzer, it differs from real-time detection.

#### Comment
- Though the focus here is mobile security, kernel-driver signing and low-level abuse analysis are worth reading from a binary-hardening and runtime-protection perspective. It is filed under "Other" as it fits none of the three main categories.
- Joint work by the University of Milan and EURECOM (Davide Balzarotti), with the sandbox released, published at NDSS.
