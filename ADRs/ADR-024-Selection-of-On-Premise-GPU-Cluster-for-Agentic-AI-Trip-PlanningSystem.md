# Selection of On-Premise GPU Cluster for Agentic AI Trip Planning System

**Author**: Bahram Jahanshahi<br />
**Status**: PROPOSED<br />
**Type**: INFRASTRUCTURE<br />
**Created**: 2025-10-21<br />
**Post-history**:  

Decision to deploy and operate the **Llama 3 (70B)** model for the Agentic AI Trip Planning System using a dedicated **on-premise GPU cluster** to ensure cost efficiency, data control, and sustained high-performance inference for agentic reasoning and MCP-based tool-calling.

# CONTEXT

The Agentic Trip Planning AI system relies on large-scale reasoning, multi-step planning, and dynamic tool execution through MCP clients.  
While cloud-based GPUs offer flexibility, the ongoing cost of large model inference (e.g., $40–$50/hr per node for H100 instances) quickly becomes unsustainable for continuous workloads.  
Moreover, sensitive travel data and user preferences are subject to **data protection (GDPR)**, requiring controlled and auditable infrastructure.

**Drivers:**
- Need for **high-performance inference** for Llama 3 (70B) and other future models
- **Predictable and lower long-term cost** vs. cloud GPU rentals
- Full **data locality and privacy compliance** for travel-related personal data
- Ability to **customize infrastructure** for RAG, MCP, and multi-agent workflows
- **Persistent availability** for offline, internal, or private deployments

Evaluated options:
1. **Cloud GPUs (AWS p5 / Azure NDv5)**
    - Pros: On-demand scaling, managed infrastructure
    - Cons: High recurring cost and limited data control
2. **On-Premise GPU Cluster (NVIDIA A100 / RTX 6000 Ada / A40)**
    - Pros: Long-term cost savings, total control, high performance
    - Cons: High upfront investment, requires maintenance staff
3. **Hybrid Model**
    - Pros: Flexibility for dev/test vs. production workloads
    - Cons: Added complexity and network synchronization costs

#### Hardware and Cost Breakdown (Estimated, 2025)
| Component | Quantity | Description | Est. Unit Cost (USD) | Total Cost (USD) |
|------------|-----------|--------------|----------------------|------------------|
| **NVIDIA A100 (80GB)** | 4 | Core inference GPUs for Llama 3 (70B) | $20,000 | $80,000 |
| **RTX 6000 Ada (48GB)** | 2 | Development and testing GPUs | $12,500 | $25,000 |
| **Compute Nodes (Dual Xeon, 512GB RAM)** | 2 | High-performance servers | $10,000 | $20,000 |
| **NVMe Storage (20TB RAID)** | 1 | Model weights, embeddings, and cache | $8,000 | $8,000 |
| **Networking, Cooling, and Power Systems** | – | Cluster infrastructure and redundancy | – | $12,000 |
| **Total Estimated Cost (One-time Investment)** | – |  |  | **~$145,000 ** |


# DECISION
**Chosen Infrastructure:** **On-Premise GPU Cluster** using **NVIDIA A100 (80GB)** and **RTX 6000 Ada** GPUs.

**Rationale:**
The on-premise GPU cluster provides the best balance between **long-term cost control, data sovereignty, and high-performance inference**.  
By owning the hardware, the team eliminates ongoing cloud billing and retains full control over sensitive data processing.  
NVIDIA A100 (80GB) GPUs are optimal for Llama 3 (70B) inference due to their large memory capacity, while RTX 6000 Ada cards can support development, quantized inference, and smaller models like Mistral 7B for testing.

The cluster will run **vLLM** or **TensorRT-LLM** for optimized model serving, supporting quantization and batching to reduce inference latency.  
This setup ensures stable throughput for multi-user agentic operations and sustained reasoning-heavy workloads.

**Estimated Hardware Configuration and Cost (2025 rates):**

#### Hardware and Cost Breakdown (Estimated, 2025)
| Component | Quantity | Description | Est. Unit Cost (USD) | Total Cost (USD) |
|------------|-----------|--------------|----------------------|------------------|
| **NVIDIA A100 (80GB)** | 4 | Core inference GPUs for Llama 3 (70B) | $20,000 | $80,000 |
| **RTX 6000 Ada (48GB)** | 2 | Development and testing GPUs | $12,500 | $25,000 |
| **Compute Nodes (Dual Xeon, 512GB RAM)** | 2 | High-performance servers | $10,000 | $20,000 |
| **NVMe Storage (20TB RAID)** | 1 | Model weights, embeddings, and cache | $8,000 | $8,000 |
| **Networking, Cooling, and Power Systems** | – | Cluster infrastructure and redundancy | – | $12,000 |
| **Total Estimated Cost (One-time Investment)** | – |  |  | **~$145,000 ** |


**Pros:**
- Predictable and lower total cost of ownership (TCO) over 2–3 years
- Full control over model deployment, security, and data access
- High throughput for sustained reasoning workloads
- Supports fine-tuning, quantization, and offline inference
- Enables experimentation with multiple open-source models

**Cons:**
- High initial investment and setup cost
- Requires in-house DevOps expertise for GPU maintenance and scaling
- Hardware lifecycle management (driver, firmware, cooling, redundancy)

# CONSEQUENCES
**Positive Impacts:**
- Enables **stable and low-latency inference** for Llama 3 (70B) and agentic reasoning tasks
- Reduces dependency on external cloud providers and their cost volatility
- Enhances **data privacy and compliance** under GDPR for travel data processing
- Facilitates research, fine-tuning, and local RAG experiments
- Long-term savings compared to continuous cloud GPU rental

**Trade-offs:**
- Higher upfront capital expenditure
- Limited short-term scalability (compared to cloud burst capacity)
- Requires dedicated infrastructure management and monitoring

# COMPLIANCE
To ensure compliance:
- Host the GPU cluster in a **secure EU-based data center** with access control and audit logging.
- Implement **full disk encryption**, **TLS-secured endpoints**, and **role-based access (RBAC)** for all model services.
- Maintain **GPU utilization and energy monitoring** for cost and sustainability reporting.
- Follow GDPR and ISO/IEC 27001 standards for all stored and processed data.
- Back up all model weights, logs, and RAG embeddings regularly to secure storage.

# COMMENTS
**References:**
- NVIDIA A100 and RTX 6000 Ada Technical Specifications
- vLLM and TensorRT-LLM Performance Benchmarks
- Meta Llama 3 70B Deployment Guide
- EU GDPR Compliance Guidelines for AI Infrastructure

**Notes:**
- The initial cluster (4× A100, 2× RTX 6000 Ada) supports ~20 concurrent sessions at sub-second latency.
- Expansion to 8 GPUs planned in Year 2 as usage scales.
- Future-proofing includes modular rack design for next-gen GPUs (H200/B100).
- Estimated breakeven point compared to cloud deployment: **≈14–16 months**.
