# Controls and Governance Frameworks

Governance structures, risk management frameworks, and control mechanisms for sovereign AI deployments.

---

## Governance Framework Landscape

### Primary Frameworks

| Framework | Type | Issuer | Scope | Key Feature |
|-----------|------|--------|-------|-------------|
| **EU AI Act** | Binding regulation | European Commission | Any AI system in EU market | Risk-based classification with mandatory obligations |
| **NIST AI RMF** | Voluntary framework | US NIST | Organizations building/deploying AI | 4 functions: Govern, Map, Measure, Manage |
| **ISO/IEC 42001** | Certifiable standard | ISO/IEC | AI management systems | Structured, auditable, certifiable |
| **Singapore MGFGAI** | Voluntary guidance | IMDA/PDPC | GenAI systems | Practical governance for generative AI |
| **Singapore Agentic AI** | Voluntary guidance | IMDA | Agentic AI systems | First framework addressing autonomous AI agents (Jan 2026) |
| **ASEAN AI Guide** | Regional guidance | ASEAN | Cross-jurisdictional | Ethics and governance alignment across SE Asia |

### How They Work Together

**NIST AI RMF** provides the *"what"* and *"why"* — identifying and measuring risks across the AI lifecycle.

**ISO/IEC 42001** provides the *"how"* — a formal management system structure with policies, procedures, roles, and audit trails.

**EU AI Act** provides the *"must"* — mandatory obligations with enforcement teeth.

**Recommended approach:** Use NIST AI RMF as the risk identification layer, ISO 42001 as the management system, and map both to EU AI Act obligations (or local equivalents) for compliance.

Source: [CSA](https://cloudsecurityalliance.org/blog/2025/01/29/how-can-iso-iec-42001-nist-ai-rmf-help-comply-with-the-eu-ai-act), [Hicomply](https://www.hicomply.com/blog/iso-42001-vs-nist-ai-rmf)

---

## NIST AI Risk Management Framework

Four core functions:

### 1. GOVERN

Establish organizational policies, roles, and accountability for AI risk:
- AI governance board or committee
- Clear ownership of AI risk decisions
- Integration with enterprise risk management
- Stakeholder engagement processes

### 2. MAP

Contextualize risks within the specific AI system and use case:
- Identify intended and unintended uses
- Map data flows and dependencies
- Assess impact on affected communities
- Document assumptions and limitations

### 3. MEASURE

Quantify and evaluate risks using metrics and testing:
- Bias and fairness testing across demographic groups
- Performance benchmarks and degradation monitoring
- Security and adversarial robustness testing
- Explainability and interpretability assessment

### 4. MANAGE

Mitigate identified risks and monitor continuously:
- Implement technical safeguards
- Establish human oversight mechanisms
- Create incident response procedures
- Conduct ongoing monitoring and re-evaluation

Source: [NIST AI RMF](https://www.nist.gov/itl/ai-risk-management-framework)

---

## Sovereign AI Control Categories

### 1. Data Controls

| Control | Description | Implementation |
|---------|------------|----------------|
| **Data classification** | Categorize data by sovereignty requirements | Automated tagging (PII, financial, defense, public) |
| **Data residency** | Ensure data stays within jurisdictional boundaries | Sovereign cloud zones, on-premise storage |
| **Encryption at rest** | Protect stored data | AES-256 with customer-managed keys (CMK) |
| **Encryption in transit** | Protect data in motion | TLS 1.3, mTLS for service-to-service |
| **Encryption in use** | Protect data during processing | Confidential computing (TEEs) |
| **Access control** | Restrict who can access what data | RBAC, ABAC, zero-trust architectures |
| **Data lineage** | Track data from source through processing | Metadata management, provenance tracking |
| **Retention and disposal** | Manage data lifecycle | Automated retention policies, secure deletion |

### 2. Model Controls

| Control | Description | Implementation |
|---------|------------|----------------|
| **Training data provenance** | Know where model training data came from | Data cards, supply chain documentation |
| **Copyright compliance** | Ensure training data doesn't violate IP rights | Licensing audits, opt-out mechanisms |
| **Bias evaluation** | Test for discriminatory outputs | Fairness metrics across demographic groups |
| **Safety evaluation** | Test for harmful outputs | Red-teaming, safety benchmarks, guardrails |
| **Model cards** | Document model capabilities and limitations | Standardized documentation per model |
| **Version control** | Track model versions and changes | Model registry with rollback capability |
| **Drift monitoring** | Detect behavioral changes over time | Statistical monitoring, output sampling |
| **Explainability** | Understand why models produce specific outputs | Attention visualization, feature attribution |

### 3. Infrastructure Controls

| Control | Description | Implementation |
|---------|------------|----------------|
| **Physical security** | Protect data center facilities | Access controls, surveillance, geographic restrictions |
| **Network isolation** | Separate sovereign workloads | Air-gapped networks, VPCs, microsegmentation |
| **Hardware attestation** | Verify hardware integrity | TPM, secure boot, TEE attestation |
| **Patch management** | Keep systems updated | Automated patching with sovereignty-compliant sources |
| **Disaster recovery** | Ensure continuity | Replication within sovereign boundaries only |
| **Supply chain verification** | Validate hardware/software origins | BOM tracking, vendor assessment |

### 4. Operational Controls

| Control | Description | Implementation |
|---------|------------|----------------|
| **Audit logging** | Record all AI system activities | Immutable logs, centralized SIEM |
| **Incident response** | Handle AI-related security events | Playbooks for data breach, model compromise, adversarial attack |
| **Change management** | Control modifications to AI systems | Approval workflows, impact assessment |
| **Personnel security** | Vet individuals with access | Background checks, citizenship requirements for classified workloads |
| **Third-party assessment** | Evaluate vendor sovereignty claims | Due diligence framework, contractual requirements |

---

## Data Classification for Sovereign AI

A practical three-tier model:

### Tier 1 — Sovereign (Maximum Protection)

**Data types:** Classified defense data, citizen biometrics, national security intelligence, critical infrastructure control data, health records under strict regulation

**Requirements:**
- On-premise or air-gapped sovereign infrastructure
- Non-US-headquartered provider (avoids CLOUD Act exposure)
- Customer-managed encryption keys
- Personnel with security clearance
- No cross-border data movement under any circumstance

### Tier 2 — Controlled (Regulated Protection)

**Data types:** Business-sensitive PII, financial data under GDPR/PDPA, enterprise IP, regulated industry data

**Requirements:**
- Sovereign cloud zone with data residency guarantees
- Customer-managed encryption keys
- Audit logging and access controls
- Cross-border movement only with explicit legal basis
- Regular compliance audits

### Tier 3 — Open (Standard Protection)

**Data types:** Public data, anonymized datasets, non-sensitive analytics, open-source model weights

**Requirements:**
- Standard cloud security practices
- Encryption in transit and at rest
- Access controls and monitoring
- No special residency requirements

---

## Model Governance for Sovereign AI

### Training Data Governance

| Concern | Control | Why It Matters |
|---------|---------|---------------|
| **Provenance** | Document all data sources with licenses | Avoid copyright claims (NYT v. OpenAI precedent) |
| **Consent** | Verify consent for personal data in training sets | GDPR/PDPA compliance |
| **Bias** | Audit training data for demographic representation | Models reflect their training data — biased data = biased outputs |
| **Quality** | Filter noise, duplicates, harmful content | Training data quality directly affects model quality |
| **Versioning** | Track which data was used for which model version | Reproducibility and audit trail |

### Model Lifecycle Governance

```
Training Data → Pre-Training → Fine-Tuning → Evaluation → Deployment → Monitoring → Retirement
     ↑              ↑              ↑              ↑             ↑             ↑            ↑
  Provenance    Compute       Domain data    Safety tests   Guardrails   Drift alerts   Archival
  audit         logging       compliance     bias tests     PII filters  performance    policy
                                             red-teaming    audit logs   re-eval
```

---

## Supply Chain Security

AI has two supply chains, both vulnerable:

### Hardware Supply Chain

| Choke Point | Risk | Example |
|-------------|------|---------|
| **Rare earth minerals** | Geographic concentration (China: 60%+ of processing) | Export restrictions could constrain chip manufacturing |
| **EUV lithography** | Single supplier (ASML) | Any disruption halts leading-edge chip production |
| **Advanced fabrication** | TSMC dominance (~90% of leading-edge nodes) | Taiwan Strait tensions = existential risk |
| **AI accelerators** | NVIDIA 80–90% market share | Export controls = immediate scarcity |
| **Power supply** | Data centers consume growing share of grid | Energy constraints limit sovereign compute buildout |

### Model Supply Chain

| Risk | Description | Mitigation |
|------|------------|------------|
| **Training data poisoning** | Malicious data injected into training sets | Data provenance tracking, adversarial testing |
| **Model backdoors** | Hidden behaviors triggered by specific inputs | Red-teaming, safety evaluations, formal verification |
| **Dependency on foreign model updates** | Using a model whose weights could change | Pin model versions, maintain local copies |
| **Open-source supply chain attacks** | Compromised model files on Hugging Face, etc. | Checksum verification, provenance attestation |
| **Fine-tuning data leakage** | Sensitive data extractable from fine-tuned models | Differential privacy, membership inference testing |

---

## International AI Safety Cooperation

### International Network of AI Safety Institutes (INASI)

10 member countries/entities collaborating on AI evaluation:
- US, UK, EU, France, Japan, Kenya, Korea, Singapore, Australia, Canada
- Shared evaluation tools and methodologies
- Bilateral agreements (e.g., UK-US MoU on AI evaluation tools)

### Key Events

| Event | Date | Outcome |
|-------|------|---------|
| Paris AI Action Summit | Feb 2025 | Called for harmonized global standards |
| China's Global AI Governance Framework | Jul 2025 | China positions as alternative standard-setter |
| UN Global Dialogue on AI | Ongoing | New multilateral cooperation mechanisms |
| Agentic AI Foundation (AAIF) | Dec 2025 | Anthropic + OpenAI + Block under Linux Foundation — open agentic AI standards |

Source: [CSIS](https://www.csis.org/analysis/ai-safety-institute-international-network-next-steps-and-recommendations)

---

## Compliance Mapping

How sovereign AI controls map to major regulatory requirements:

| Control Area | EU AI Act | GDPR | NIST AI RMF | ISO 42001 |
|-------------|-----------|------|-------------|-----------|
| Risk classification | Required (risk tiers) | — | GOVERN/MAP | Clause 6 (Planning) |
| Data governance | Required (high-risk) | Required | MAP | Annex A |
| Transparency | Required (all tiers) | Required (Art. 13-14) | GOVERN | Clause 7 (Support) |
| Human oversight | Required (high-risk) | — | MANAGE | Annex A |
| Bias testing | Required (high-risk) | — | MEASURE | Clause 9 (Evaluation) |
| Documentation | Required (all tiers) | Required (Art. 30) | All functions | Clause 7 (Documentation) |
| Incident response | Required | Required (Art. 33-34) | MANAGE | Clause 10 (Improvement) |
| Audit trail | Required (high-risk) | Required | GOVERN | Clause 9 (Internal audit) |

---

*Next: [Ecosystem — key players, investments, and market map](ecosystem.md).*
