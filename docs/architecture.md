# Architecture and Technology Pillars

Reference architectures, technology patterns, and infrastructure options for sovereign AI deployments.

---

## The Four Pillars

Sovereign AI requires control across four technology pillars:

### 1. Sovereign Compute

National GPU clusters and HPC infrastructure under domestic control.

| Country/Region | Initiative | Scale |
|----------------|-----------|-------|
| **EU** | EuroHPC AI Factories (7+ sites) | EUR 1.5B total; federated 50,000-GPU virtual supercomputer (France-Germany) |
| **France** | Jean Zay (IDRIS), Adastra (CINES), Alice Recoque (2026 exascale) | EUR 750M+ |
| **Japan** | METI AI supercomputers, SoftBank Hokkaido facility | $135B combined (gov + corp) through 2030 |
| **South Korea** | National AI Computing Center, Samsung/SK AI Factories | 260,000+ GPUs, 50,000+ per factory |
| **India** | Yotta Shakti Cloud (NVIDIA H100) | Gigawatt-scale AI Factory planned (L&T-NVIDIA) |
| **Saudi Arabia** | HUMAIN AI Zone with AWS | 150,000 AI accelerators (incl. NVIDIA GB300) |
| **UAE** | 5GW UAE-US AI Campus | Largest AI infrastructure outside US |
| **Germany** | Deutsche Telekom AI data center | EUR 1B |

### 2. Sovereign Models

Foundation models developed domestically, trained on local data, reflecting local languages and legal frameworks.

| Model | Country | Parameters | License | Notes |
|-------|---------|-----------|---------|-------|
| **Mistral** (family) | France | Up to 675B | Apache 2.0 | European sovereignty standard |
| **Aleph Alpha Pharia** | Germany | 7B | Proprietary | Tokenizer-free architecture, EU AI Act compliant |
| **Falcon Arabic / Falcon-H1** | UAE | Various | Open | Leading Arabic benchmarks; H1 hybrid architecture |
| **DeepSeek V4** | China | Trillion+ | Open weights | Multimodal; Huawei CANN native support |
| **Qwen** (Alibaba) | China | Various | Open | Growing global adoption |
| **BHASHINI** | India | Various | Government | 35+ languages, 1,600+ models |
| **OpenEuroLLM** | EU (20 orgs) | TBD | Open | EUR 37.4M; all European languages by 2028 |

### 3. Sovereign Data

Governance frameworks ensuring data is collected, stored, and processed under national laws.

Key components:
- **Data classification:** Sovereign (must stay local), hybrid (conditional sharing), global (unrestricted)
- **Metadata tagging:** Automated identification of PII, financial data, training data provenance
- **Federated architectures:** Distributed control with centralized visibility and lineage tracking
- **Data trusts:** Proposed mechanisms for anonymized data sharing across borders
- **Training data vetting:** Copyright compliance, harmful content filtering, provenance tracking

### 4. Sovereign Infrastructure

The physical and cloud infrastructure under domestic control.

Options span a spectrum from full self-hosting to managed sovereign zones:

```
Full Self-Host          Sovereign Cloud Zone         Public Cloud
←─────────────────────────────────────────────────────────────→
Maximum control                                    Maximum capability
Maximum cost                                       Minimum cost
Maximum complexity                                 Maximum dependency
```

---

## Reference Architecture

A sovereign AI deployment requires control across these layers:

```
┌──────────────────────────────────────────────────────────────────┐
│                        APPLICATIONS                              │
│   Sector solutions, chatbots, analytics, automation              │
├──────────────────────────────────────────────────────────────────┤
│                     ORCHESTRATION LAYER                           │
│   Workflow engines, tool calling, agent frameworks, RAG          │
├──────────────────────────────────────────────────────────────────┤
│                      MODEL SERVING                               │
│   Inference engines (vLLM, TGI, Ollama), model registry,        │
│   fine-tuning pipelines, evaluation frameworks                   │
├──────────────────────────────────────────────────────────────────┤
│                    GOVERNANCE & SAFETY                            │
│   PII detection, policy enforcement, audit logging,              │
│   model cards, bias monitoring, explainability                   │
├──────────────────────────────────────────────────────────────────┤
│                     DATA PLATFORM                                │
│   Vector databases, object storage, data lakes,                  │
│   classification engine, encryption (customer-managed keys)      │
├──────────────────────────────────────────────────────────────────┤
│                    COMPUTE & NETWORK                              │
│   GPU clusters, confidential computing (TEEs),                   │
│   sovereign cloud zones, edge devices, networking                │
├──────────────────────────────────────────────────────────────────┤
│                   PHYSICAL INFRASTRUCTURE                         │
│   Data centers (domestic), power supply, cooling,                │
│   physical security, jurisdiction                                │
└──────────────────────────────────────────────────────────────────┘
```

### Non-Negotiable Control Points

1. **Data classification and permitted uses** — what data can be processed where
2. **Encryption and key ownership** — customer-managed keys, not provider-managed
3. **Identity, access, logging, and monitoring** — who accessed what, when, auditable
4. **Model risk management and evaluation** — bias testing, safety evaluation, drift monitoring
5. **Incident response and legal access pathways** — what happens when a government requests data

### Three Dimensions of Sovereignty

| Dimension | Question |
|-----------|----------|
| **Architectural control** | Who owns the stack? |
| **Operational independence** | Who operates it day-to-day? |
| **Escape velocity** | Can you migrate away if needed? |

True sovereignty requires positive answers on all three. Many "sovereign" cloud offerings score well on architectural control but poorly on escape velocity.

Source: [Introl](https://introl.com/blog/sovereign-cloud-ai-infrastructure-data-residency-requirements-2025)

---

## Cloud Sovereignty Offerings

Major hyperscalers now offer sovereign zones — but with caveats:

| Provider | Offering | Investment | Key Feature | Jurisdiction Concern |
|----------|---------|-----------|-------------|---------------------|
| **AWS** | European Sovereign Cloud | EUR 7.8B | Fully isolated from US regions; Brandenburg, Germany | US-headquartered — CLOUD Act applies |
| **AWS** | AI Factories | Varies | On-prem GPU deployment with managed Bedrock/SageMaker | Hardware ownership model unclear |
| **AWS** | HUMAIN AI Zone (Saudi) | — | 150,000 accelerators including NVIDIA GB300 | US-Saudi partnership tensions |
| **Microsoft** | Sovereign Public + Private Cloud | — | Air-gapped Azure Local + M365 Local | Bleu (France) and Delos (Germany) are JVs with local operators |
| **Microsoft** | In-country AI processing | — | M365 Copilot processed locally for 15 nations by end 2026 | Still US software stack |
| **Google** | Distributed Cloud (Air-gapped) | — | Fully disconnected sovereign environments | NATO contract validates security |
| **Nutanix** | Distributed Sovereign Cloud | — | Cross-17 Google Cloud regions; multi-vendor support | Infrastructure layer only |

### The CLOUD Act Problem

Despite "sovereign" branding, US-headquartered providers may still be subject to US jurisdiction:

> *"The CLOUD Act empowers US authorities to compel US companies to produce data stored anywhere in the world. No amount of sovereign branding changes this legal reality."*
> — Eliatra analysis

**Mitigation strategies:**
- Use non-US-headquartered providers for highest-sovereignty workloads
- Negotiate data processing agreements with explicit jurisdictional exclusions
- Encrypt data with customer-managed keys that the provider cannot access
- Use confidential computing (TEEs) to process data without provider visibility

Source: [Eliatra](https://eliatra.com/blog/the-sovereignty-illusion-why-awss-european-cloud-cannot-escape-us/)

---

## On-Premise Inference Stack

For maximum sovereignty, organizations can self-host the entire AI inference stack.

### Components

| Layer | Purpose | Options |
|-------|---------|---------|
| **Model** | Foundation model weights | Open-weight models (Llama, Mistral, Qwen, DeepSeek) |
| **Serving** | Inference engine with APIs | vLLM, TGI, Ollama, llama.cpp, SGLang, TensorRT-LLM |
| **Orchestration** | Workflows, tool calling, RAG | LangChain, LlamaIndex, custom frameworks |
| **Knowledge** | Vector search, document retrieval | pgvector, Milvus, Chroma, Weaviate |
| **Storage** | Persistent data | PostgreSQL, MinIO, local filesystem |
| **Safety** | PII handling, policy enforcement | Guardrails AI, NeMo Guardrails, custom filters |
| **Monitoring** | Observability, audit logging | Langfuse, OpenTelemetry, custom dashboards |

### Inference Framework Comparison (2025 benchmarks)

| Framework | Best For | Throughput | Notes |
|-----------|---------|-----------|-------|
| **vLLM** | Production GPU inference | 793 tok/s | 1.5–1.8x higher throughput vs TGI; P99 latency 80ms |
| **TGI** (Hugging Face) | Production GPU inference | Strong | Good batching; enterprise support from Hugging Face |
| **Ollama** | Local/developer use | 41 tok/s | Simple setup; Apple Silicon optimized |
| **llama.cpp** | CPU/Apple Silicon | Varies | Lightweight; excellent quantization support |
| **SGLang** | Structured generation | Good | Best for constrained JSON/schema output |
| **TensorRT-LLM** | Max NVIDIA performance | Highest | NVIDIA-optimized; proprietary |

Source: [ITECS](https://itecsonline.com/post/vllm-vs-ollama-vs-llama.cpp-vs-tgi-vs-tensort), [WaterCrawl](https://watercrawl.dev/blog/on-premises-llm-serving-frameworks-compared-genai)

---

## Federated Learning Architecture

When data cannot leave its sovereign zone but models need to learn from distributed data:

```
┌─────────────┐    ┌─────────────┐    ┌─────────────┐
│ Sovereign    │    │ Sovereign    │    │ Sovereign    │
│ Zone A       │    │ Zone B       │    │ Zone C       │
│              │    │              │    │              │
│ Local Data   │    │ Local Data   │    │ Local Data   │
│     ↓        │    │     ↓        │    │     ↓        │
│ Local Train  │    │ Local Train  │    │ Local Train  │
│     ↓        │    │     ↓        │    │     ↓        │
│ Model Update │    │ Model Update │    │ Model Update │
└──────┬───────┘    └──────┬───────┘    └──────┬───────┘
       │                   │                   │
       └───────────┬───────┘                   │
                   ↓                           │
           ┌──────────────┐                    │
           │ Aggregation  │◄───────────────────┘
           │ Server       │
           │ (model only, │
           │  no raw data)│
           └──────┬───────┘
                  ↓
           Updated Global Model
           (distributed back to zones)
```

**Key principle:** Models travel to the data, not data to the model. Only model weight updates (gradients) leave each sovereign zone — raw data never moves.

### Confidential Federated Learning (CFL)

Combines federated learning with **confidential computing** (TEEs) to ensure data remains within its trust domain while enabling transparency and accountability. Particularly relevant for:
- Healthcare (patient data across hospitals)
- Banking (transaction data across institutions)
- Defense (intelligence sharing across allied nations)

Source: [ACM](https://cacm.acm.org/practice/trustworthy-ai-using-confidential-federated-learning/)

---

## Confidential Computing and TEEs

**Trusted Execution Environments (TEEs)** protect the confidentiality and integrity of code and data during processing — even from the infrastructure operator.

### Hardware Implementations

| Vendor | Technology | Capability |
|--------|-----------|-----------|
| **Intel** | SGX (per-process), TDX (per-VM) | Most mature ecosystem |
| **AMD** | SEV-SNP | Full VM encryption with attestation |
| **ARM** | CCA (Confidential Compute Architecture) | Emerging; mobile/edge focus |

### Sovereign AI Applications

- **Process sensitive data on shared infrastructure** without exposing it to the cloud provider
- **Verifiable computation:** Cryptographic proof that code ran unmodified on specific data
- **Multi-party computation:** Multiple organizations can jointly train models without sharing data
- **Regulatory compliance:** Demonstrate to auditors that data processing occurred within TEE boundaries

**2025 trend:** Regulatory push for data sovereignty is driving confidential computing adoption. Expected to become central for federated AI, regulated analytics, and hybrid cloud deployments.

Source: [Duality Tech](https://dualitytech.com/blog/confidential-computing-tees-what-enterprises-must-know-in-2025/)

---

## Workload Segmentation

Not all AI workloads need full sovereignty. A pragmatic approach segments by sensitivity:

| Tier | Workloads | Infrastructure | Examples |
|------|-----------|---------------|----------|
| **Sovereign** | Defense, citizen PII, critical infrastructure, regulated data | On-premise or sovereign cloud (non-US provider) | Military AI, national health records, financial supervision |
| **Hybrid** | Business-sensitive but not classified; regulated with cross-border allowances | Sovereign cloud zone with customer-managed keys | Enterprise analytics, internal chatbots, HR/finance AI |
| **Global** | Non-sensitive, public data, research | Public cloud | Marketing analytics, public-facing chatbots, open research |

This segmentation avoids the cost and complexity of full sovereignty for workloads that don't require it, while ensuring maximum protection for those that do.

---

## Edge AI as Sovereignty Enabler

On-device inference eliminates data residency concerns entirely — data never leaves the device.

### Key Developments (2025)

- **Apple:** 30 tokens/sec on-device inference
- **Qualcomm:** 45 TOPS NPUs in mobile chipsets
- **Small Language Models (SLMs):** 1–7B parameter models achieving 80–90% of frontier model performance for specific tasks
- **SLM market:** $0.93B (2025) → $5.45B by 2032 (CAGR 28.7%)

### Sovereign Edge Architecture

```
┌─────────────────────────────────────────────────┐
│                  EDGE DEVICES                    │
│   Phones, laptops, IoT, industrial controllers   │
│   Running SLMs locally — no data leaves device   │
├─────────────────────────────────────────────────┤
│              SOVEREIGN EDGE GATEWAY              │
│   Aggregation, orchestration, model updates      │
│   On-premise or domestic data center             │
├─────────────────────────────────────────────────┤
│           SOVEREIGN CLOUD (optional)             │
│   Training, fine-tuning, complex queries         │
│   Only anonymized/aggregated data flows up       │
└─────────────────────────────────────────────────┘
```

Edge AI is particularly valuable for sovereign deployments in healthcare, manufacturing, defense, and telecommunications where data sensitivity and latency requirements align.

Source: [CB Insights](https://www.cbinsights.com/research/report/small-language-model-gain-momentum/)

---

*Next: [Controls and governance frameworks](controls-governance.md) for sovereign AI.*
