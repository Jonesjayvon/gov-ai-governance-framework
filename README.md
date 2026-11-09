# Federal AI Compliance & Governance Matrix

[![Framework](https://img.shields.io/badge/Compliance-FedRAMP%20High%20%7C%20DoD%20IL5-blue)](https://www.fedramp.gov)
[![Framework](https://img.shields.io/badge/NIST-AI%20RMF%201.0%20%7C%20SP%20800--53%20Rev.%205-green)](https://www.nist.gov)
[![Classification](https://img.shields.io/badge/Environment-Classified%20Enclaves%20%2F%20CUI-orange)](https://cui.dodsstate.gov)

## 📌 Overview

Deploying frontier Large Language Models (LLMs) and generative AI applications into federal agencies and national security environments requires bridging traditional cloud compliance with AI-specific risk surfaces. Traditional compliance frameworks (FedRAMP High / DoD IL5) address infrastructure confidentiality, integrity, and availability, but fall short of addressing non-deterministic AI behavior like prompt injection, model drift, data poisoning, and unauthorized output generation.

This repository provides:
1. **NIST SP 800-53 Rev. 5 to AI Risk Mapping:** A crosswalk aligning FedRAMP High (410 controls) & DoD IL5 baselines with LLM risk vectors and NIST AI RMF core functions (Govern, Map, Measure, Manage).
2. **ISSM/ISSO LLM Evaluation Checklist:** A operational review guide for Agency Authorizing Officials (AOs), Information System Security Managers (ISSMs), and ISSOs evaluating air-gapped or high-assurance LLM integrations in classified enclaves.

---

## 🛠 Framework Crosswalk Matrix

Below is a subset of key control families mapped to AI-specific deployment risks and technical mitigation strategies:

| NIST SP 800-53 Family | Control ID | FedRAMP High / DoD IL5 Context | AI/LLM Risk Vector | Product Guardrail & Mitigation Strategy | NIST AI RMF Mapping |
| :--- | :--- | :--- | :--- | :--- | :--- |
| **Access Control (AC)** | AC-3 / AC-6 | Least Privilege & Role-Based Access Control | Prompt Injection / Privilege Escalation via System Instructions | Input sanitization layers, deterministic RBAC wrappers around API endpoints, and model instruction separation. | *Manage 1.1* |
| **System & Info Integrity (SI)** | SI-3 / SI-4 | Malicious Code Protection & Monitoring | Hallucination, Data Poisoning, & Training Data Contamination | Retrieval-Augmented Generation (RAG) groundness scoring, confidence thresholding, and continuous output auditing. | *Measure 2.3* |
| **Audit & Accountability (AU)** | AU-2 / AU-6 | Audit Record Events & Monitoring | Non-Deterministic Output & Inadequate Forensic Tracing | Full prompt-completion telemetry logging, deterministic seed parameter tracking, and immutable vector store query logging. | *Govern 1.2* |
| **Configuration Mgmt (CM)** | CM-3 / CM-8 | Baseline Configuration & Inventory | Model Drift, Shadow LLM Usage, & Uncontrolled Model Updates | Strict model weight versioning, pinned inference container hashes, and continuous eval benchmarks prior to deployment. | *Manage 2.2* |
| **Media Protection (MP)** | MP-6 | Media Sanitization | PII/CUI Leakage in Model Memory or Context Windows | Zero-retention vendor policies, client-side PII scrubbing pre-inference, and Context Window flushing post-session. | *Map 1.5* |

---

## 📋 ISSM/ISSO Evaluation Checklist for Classified Enclaves

Designed for security officers evaluating an LLM integration within DoD IL5/IL6 or air-gapped intelligence enclaves:

### 1. Data Ingestion & Privacy Controls
- [ ] **Zero-Data Retention (ZDR):** Is the inference endpoint verified to operate under strict zero-retention (inputs/outputs are not saved for vendor model training)?
- [ ] **Context Window Sanitization:** Does the application purge temporary context memory immediately upon session termination or CAC/PIV logoff?
- [ ] **RAG Data Access Alignment:** Are vector embeddings scoped dynamically to the user's explicit DoD/IC access control level (e.g., verifying document-level security markings)?

### 2. Adversarial & Model Robustness
- [ ] **Indirect Prompt Injection:** Are inputs from retrieved external files or web feeds filtered for embedded malicious instructions before reaching the model context?
- [ ] **Out-of-Bounds Query Blocking:** Is an independent input/output moderation layer running to intercept requests seeking classified system configurations or restricted procedures?
- [ ] **Determinism & Reproducibility:** Are temperature settings locked or logged alongside system seeds to allow audit reproduction of flags?

### 3. Boundary & Infrastructure Isolation
- [ ] **Air-Gap Capability:** Can the inference engine and evaluation harness execute with zero external internet connectivity or phoning home to external telemetry endpoints?
- [ ] **Boundary Encryption:** Is all data in transit between the application layer, vector store, and model inference endpoint encrypted using FIPS 140-3 validated modules?

---

## 💡 About the Author

**Jayvon Marcel Jones**  
*TS/SCI-cleared Technical Product Leader & U.S. Navy Chief Warrant Officer*  
- **Focus:** Federal AI Platform Product Management, High-Assurance Security, DoD/FedRAMP Compliance, Zero-Trust Architecture.
- **Experience:** U.S. Navy IT Operations Lead, AWS/Azure Enterprise Cloud Engineering, Federal Consulting.
