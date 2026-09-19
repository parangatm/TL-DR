# AI Risk Mitigation on Hardware
### An overview of current research areas in AI Safety on hardware

Parangat Mittal

AI Safety, Ethics and Society - Summer 2025

## Abstract

The rapid development of Artificial Intelligence capabilities necessitates a rethinking of hardware security. The long-standing security practices on modern chips and deployment platforms already go a long way towards limiting misuse, but the more urgent need and less explored but more pressing challenge is misalignment. This article analyzes hardware strategies for AI Risk Mitigation, decouples misuse from misalignment, and proposes a hardware-anchored agenda for misalignment focusing on containment and responsible development. It closes with research directions aimed at making hardware a reliable foundation for oversight and long-term safety.

## 1. Introduction

AI systems increasingly exhibit high capability, autonomy and generalized intelligence, which poses a larger risk towards adversarial misuse and endogenous misalignment. Many schools of thought exist for risk modelling and mitigation, each targeting different threats and areas of intervention. For the scope of this article, we find that the central distinction guiding hardware responses is between misuse and misalignment, and makes it the most practical model for hardware.

Misuse aligns with traditional adversarial models covering exploitation of AI systems for harmful purposes. Misalignment refers to harms intended by the AI system when it pursues goals inconsistent with human values, and shows signs of power seeking, manipulation and control-resistance. The former overlaps classical computer and cloud security practices, while the latter requires new mechanisms that constrain capability development, make training and deployment verifiable and governable.

In this article, we argue:

1. Industry-standard hardware security substantially addresses misuse by providing confidentiality, integrity and attestation across compute clusters
2. Misalignment requires a different class of controls: containment and responsible development, that must be embedded at the Silicon and tied to governance.

## 2. AI Misuse on Hardware

At the hardware level, misuse encompasses well-studied cases of software-driven attacks that extract or corrupt secrets by exploiting microarchitectural features. 

The classical transient-execution attacks, such as Spectre, Meltdown, Speculative Store Bypass, abuse misspeculation and cache timing to read privileged memory across boundaries. They generalize to branch predictor, buffer, and store-forwarding types with measurable leakage via timing side channels. Beyond speculation, software side channels (cache sets, TLBs, DRAM banks, port contention) and microarchitectural covert channels can exfiltrate model weights, prompts, or API keys from otherwise secure hardware. Recent surveys of TEEs systematize these vectors and their defenses.

Beyond speculative attacks, memory-based vulnerabilities remain relevant in AI workloads due to their dependence on large shared memory hierarchies. Classic Memory attacks include DRAM, PCIe abuse and cold-boot-style attacks, which target confidentiality or integrity of host/accelerator memory maps. In multi-tenant clouds, these threats couple with virtualization layers to create cross-VM risk. These threats are orthogonal to whether the workload is “AI”.

### 2.1. Why Misuse is largely addressed by mature hardware security

Most misuse attack vectors are mitigated by industry-standard security measures. These have been validated first on non-AI workloads before being applied to AI. For speculative-execution flaws, vendors shipped microcode updates and OS changes. These mitigations were validated across diverse workloads, including operating systems, browsers, TLS libraries, and hypervisors, before being extended to AI applications. Further isolation was ensured by providing remote attestation, encrypted memory, and integrity metadata. These were proven under general-purpose databases (PostgreSQL/MySQL), web and financial services, containerized microservices (Kubernetes), and data analytics long before being routine for AI training or inference. 

Together, these controls, initially tested in mainstream non-AI computing contexts, now substantially shrink the classic misuse surface that AI inherits when it runs on shared hardware. However, these safeguards primarily target external adversaries, not misaligned internal objectives of AI systems, thus necessitating new forms of defense.


## 3. AI Misalignment on Hardware

While defenses against misuse can follow a one-size-fits-all approach, the same is not true for defenses against misalignment. The threat here is the inherent intent of the AI model, which varies across model types and deployments. However, this diverges from the hardware design paradigm, where specialized accelerators and high-performance GPUs are able to run all kinds of artificial intelligence models with minimal to no performance bottleneck. Given this diversity, defining broad defense objectives at the hardware level becomes challenging yet necessary. This claim does not necessarily undermine the model-specific safety mechanisms developed during training, but it argues that such a diverse safety standard would be ineffective on hardware.

The current such state-of-the-art defenses can be categorized into two broad categories:

1. Containment (Intervene under danger)
2. Responsible Development (Constrain before danger)

### 3.1. Containment

**1. Post-deployment training lockout**

_Idea_: fine-tuning models can rapidly defeat safety guardrails, so the model should not have access to hardware which supports training

1. **Inference-only or non-finetunable hardware**: Build chips that can only run pre-approved models and cannot be used for further training or unexpected behavior modification.

2. **Provisioning of “inference-only” mode**: Permanently disable optimizer kernel/gradient accumulation paths in accelerator firmware, unless a verified license token is presented under attestation.

3. **Hardware isolation**: Prevent the deployed model to access hardware-level information about its environment, operators, or containment systems, limiting its ability to learn about and subvert human motives.

**2. Tripwire interruption**

_Idea_: pre-commit the if-then responses to early warning signs of dangerous capabilities in form of a tripwire, which gets triggered if any of the preset conditions are met during model’s execution

1. **On-device monitors**: detect when the model attempts to change its own code or environment through self-modification patterns or code patches, triggering shutdown and alerts.

2. **Compute ceiling at fabric controller**: block any job expansion over a threshold FLOP budget or requested cluster size, unless pre-approved

**3. Communication restriction**

_Idea_: reduce manipulation or covert channels in the system by collapsing outputs to low-bandwidth verifiable formats during incident response

1. **Output-restricted channels**: Restricting outputs to simple, verifiable responses (such as limited yes/no answers, or shuffling outputs) to avoid subtle social engineering or value misgeneralization.

2. **Environment virtualization**: Keep the model entirely within a virtual/constructed world with minimal information leaks about the real world, reducing the risk of learning misaligned strategies or goals.


### 3.2. Responsible Development

**1. Verifiable training and inference**

1. Attest code, platform, and accelerators (TDX/SEV-SNP + H100 CC) and sign tamper-resistant logs of code hashes, device identities, and runtime.

2. Zero-Knowledge based verifiable ML techniques to cryptographically prove aspects of training/inference without revealing data or weights.

**2. Compute thresholds and topology attestation**

1. Monitor and enforce limits on how many chips can be joined in a high-bandwidth network for training massive models

2. Export the data from on-device FLOP/time counters Trusted Execution Environments to enforce per-job resource limits

**3. Location Verification and regional controls**

1. Bind attestations to verified sites (DC anchors, network/satellite challenges) for export-control or sovereignty over AI models.

2. Inspect AI supply chain visually (packaging, die, markings), firmware attestation, and tamper sensors for unauthorized replacement or addition.


**4. Offline licensing**

1. Embed governance logic in firmware/silicon, such as cryptographically signed licenses that meter aggregate training compute, enforce inference-only modes, or require re-attestation after crossing thresholds.

## 4. Open Research Avenues

While there are systems in place to address an immediate need, the field of AI Alignment on hardware is still very new. There are a lot of research areas and questions that have to be addressed soon, given the longer timelines of hardware research and deployment. The key research areas, in our findings, are:


Table 1 - Potential Research Ideas in AI Safety on Hardware

| Area | Ideas |
|------|-------|
Hardware-Enabled Mechanisms (HEMs) | Tamper-resistant enclaves controlling AI chips with flexible, updatable policy engines; provable policy enforcement and privacy-preserving attestation |
| Standardized compute metering | Define FLOP-counting semantics (precision, sparsity, optimizer overhead) and proof formats that satisfy both the regulators and the engineers |
| Composite attestation | Extend CPU–GPU co-attestation to multi-vendor accelerators and interconnects outside of NVIDIA H100 ecosystem |
| Inference-only SKUs | Design fuse layouts, microcode gates, and IOMMU policies guaranteeing non-bypassability under realistic threat models |
| Tripwire benchmarks | Operationalize capability-tripwire detection for autonomous replication or cyber-offense and enable automatic de-escalation actions |
| Policy-Tech Integration | Policy-as-code in hardware: geo-fencing, compute caps, export policy bindings; auditable-by-design logs |
| Tooling, Benchmarks, and Workforce | Open testbeds for containment red team exercises; standardized benchmarks for replication, exfiltration, and sandbox escape |


## 5. Conclusion

As AI systems scale in capability, hardware must evolve from securing data to securing behavior. The same primitives that protect against tampering must now serve as substrates for verifiable alignment and containment. Progress in this direction demands interdisciplinary collaboration between hardware engineers, AI researchers, and policymakers to define testable, measurable outcomes of responsible computation. By embedding safety enforcement at the level of circuits and interconnects, hardware can become the first line of defense against misaligned intelligence.

## References

- “2025 AI Safety Index,” Future of Life Institute. [Online]. Available: https://futureoflife.org/ai-safety-index-summer-2025/

- Ziemann, “AI alignment through programmable cryptography.”  [Online]. Available: https://ziemann.me/ai-crypto/

- C. S. de Witt, “Open Challenges in Multi-Agent Security: Towards Secure Systems of Interacting AI Agents,” May 04, 2025, arXiv: arXiv:2505.02077. doi: 10.48550/arXiv.2505.02077.

- C. L. Wang, T. Singhal, A. Kelkar, and J. Tuo, “MI9 -- Agent Intelligence Protocol: Runtime Governance for Agentic AI Systems,” Aug. 08, 2025, arXiv: arXiv:2508.03858. doi: 10.48550/arXiv.2508.03858.

- K. Uppal, “Secure Boot and Runtime Security in Embedded Systems,” Fidus Systems.  [Online]. Available: https://fidus.com/blog/secure-boot-and-runtime-security-in-fpga-based-embedded-systems/

- P. Slattery et al., “The AI Risk Repository: A Comprehensive Meta-Review, Database, and Taxonomy of Risks From Artificial Intelligence,” Apr. 10, 2025, arXiv: arXiv:2408.12622. doi: 10.48550/arXiv.2408.12622.

- C. Schnabl, D. Hugenroth, B. Marino, and A. R. Beresford, “Attestable Audits: Verifiable AI Safety Benchmarks Using Trusted Execution Environments,” Jun. 30, 2025, arXiv: arXiv:2506.23706. doi: 10.48550/arXiv.2506.23706.

- F. Rosas, A. Boyd, and M. Baltieri, “AI in a vat: Fundamental limits of efficient world modelling for agent sandboxing and interpretability,” Apr. 06, 2025, arXiv: arXiv:2504.04608. doi: 10.48550/arXiv.2504.04608.

- A. Ribeiro, “AI-powered threats, cyber workforce gaps, policy crisis undermine global security,” Industrial Cyber.  [Online]. Available: https://industrialcyber.co/critical-infrastructure/ai-powered-threats-cyber-workforce-gaps-policy-crisis-undermine-global-security/

- H. Rahaman, A. Chatterjee, and S. Bhunia, “Runtime Detection of Adversarial Attacks in AI Accelerators Using Performance Counters,” Mar. 10, 2025, arXiv: arXiv:2503.07568. doi: 10.48550/arXiv.2503.07568.

- A. O’Gara et al., “Hardware-Enabled Mechanisms for Verifying Responsible AI Development,” Apr. 02, 2025, arXiv: arXiv:2505.03742. doi: 10.48550/arXiv.2505.03742.

- J. O’Brien et al., “Expert Survey: AI Reliability & Security Research Priorities,” May 27, 2025, arXiv: arXiv:2505.21664. doi: 10.48550/arXiv.2505.21664.

- K. Madhavan, A. Yazdinejad, F. Zarrinkalam, and A. Dehghantanha, “Quantifying Security Vulnerabilities: A Metric-Driven Security Analysis of Gaps in Current AI Standards,” Jul. 26, 2025, arXiv: arXiv:2502.08610. doi: 10.48550/arXiv.2502.08610.

- S. Longpre et al., “In-House Evaluation Is Not Enough: Towards Robust Third-Party Flaw Disclosure for General-Purpose AI,” Mar. 25, 2025, arXiv: arXiv:2503.16861. doi: 10.48550/arXiv.2503.16861.

- Z. Lin, H. Sun, and N. Shroff, “AI Safety vs. AI Security: Demystifying the Distinction and Boundaries,” Jun. 21, 2025, arXiv: arXiv:2506.18932. doi: 10.48550/arXiv.2506.18932.

- O. Kuperman, “Why isn’t AI containment the primary AI safety strategy?,” Feb. 2025,  [Online]. Available: https://www.lesswrong.com/posts/RTs5hpFPYQaY9SoRd/why-isn-t-ai-containment-the-primary-ai-safety-strategy

- S. G. Engineering, “Sandboxed AI: Deploying LLMs in Air-Gapped Environments.”  [Online]. Available: https://thesoogroup.com/blog/sandboxed-ai-deploying-llms-airgapped

- P. Barnett, A. Scher, and D. Abecassis, “Technical Requirements for Halting Dangerous AI Activities,” Jul. 13, 2025, arXiv: arXiv:2507.09801. doi: 10.48550/arXiv.2507.09801.

- “The Rogue Replication Threat Model,” METR Blog, Nov. 2024,  [Online]. Available: https://metr.org/blog/2024-11-12-rogue-replication-threat-model/

- H. Karnofsky, “A Sketch of Potential Tripwire Capabilities for AI,” Dec. 2024. [Online]. Available: https://carnegieendowment.org/research/2024/12/a-sketch-of-potential-tripwire-capabilities-for-ai 

- P. Henderson et al., “Safety Risks from Customizing Foundation Models via Fine-tuning,” Jan. 2024. [Online]. Available: https://hai.stanford.edu/policy/policy-brief-safety-risks-customizing-foundation-models-fine-tuning 

- R. Chapman et al., “Formal verification of cryptographic software at AWS - Current practices and future trends,” Amazon Science.  [Online]. Available: https://www.amazon.science/publications/formal-verification-of-cryptographic-software-at-aws-current-practices-and-future-trends

- Armstrong, S., Sandberg, A. & Bostrom, N. Thinking Inside the Box: Controlling and Using an Oracle AI. Minds & Machines 22, 299–324 (2012). https://doi.org/10.1007/s11023-012-9282-2 

- Andrew Trask at al., “Secure Enclaves for AI Evaluation,” OpenMined.  [Online]. Available: https://openmined.org/blog/secure-enclaves-for-ai-evaluation/

- A. Mutschler, “Partitioning Processors For AI Workloads,” Semiconductor Engineering.  [Online]. Available: https://semiengineering.com/partitioning-processors-for-ai-workloads/

- F. Li, X. Li, and M. Gao, “Secure MLaaS with Temper: Trusted and Efficient Model Partitioning and Enclave Reuse,” in Annual Computer Security Applications Conference, Austin TX USA: ACM, Dec. 2023, pp. 621–635. doi: 10.1145/3627106.3627145.

- J. Babcock, J. Kramar, and R. V. Yampolskiy, “Guidelines for Artificial Intelligence Containment,” Jul. 24, 2017, arXiv: arXiv:1707.08476. doi: 10.48550/arXiv.1707.08476.

- E. Yudkowsky, “That Alien Message,” May 2008,  [Online]. Available: https://www.lesswrong.com/posts/5wMcKNAwB6X4mp9og/that-alien-message

