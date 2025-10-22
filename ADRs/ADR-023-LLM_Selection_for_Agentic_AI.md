# Selection of Open-Source Agentic LLM for Trip Planning AI

**Author**: Bahram Jahanshahi<br />
**Status**: PROPOSED<br />
**Type**: TECHNOLOGY<br />
**Created**: 2025-10-21<br />
**Post-history**:

Selection of an open-source large language model (LLM) to power an agentic AI trip planning system capable of advanced reasoning, multi-step strategy formulation, and direct tool-calling via MCP clients for travel APIs.

# CONTEXT

We are developing an **Agentic Trip Planning AI** that must autonomously reason, plan, and execute multi-step workflows. The system will integrate with external tools (e.g., travel APIs, maps, booking engines) through **Model Context Protocol (MCP)** and **tool-calling capabilities**.  

**Drivers:**
- Need for **strategic multi-step reasoning** for itinerary generation and personalization.
- **Tool-calling support** (JSON/structured outputs) for API integrations.
- **Compatibility with MCP client architecture** for dynamic agent control.
- High **context length** for managing multi-API state and user preferences.
- **Open or commercially safe license**.
- **Scalable model size (70B+)** acceptable for reasoning-heavy workflows.

Evaluated models:
- **Llama 3 (70B, Meta)**
- **Mistral / Mixtral (8x22B, Mistral AI)**
- **Gemma 2 (27B, Google DeepMind)**
- **DeepSeek-V2 (67B, DeepSeek AI)**
- (Considered but deprioritized: Falcon 180B – excessive compute requirement)

# DECISION
**Chosen Model:** **Llama 3 (70B, Meta AI)**

**Rationale:**
Llama 3 (70B) provides the best trade-off between **agentic reasoning capacity, ecosystem maturity, and licensing flexibility**.  
It supports **structured tool outputs**, **multi-turn strategy reasoning**, and **RAG (Retrieval-Augmented Generation)** integration.  
The model’s maturity and broad community adoption make it ideal for **MCP-based multi-tool orchestration** and **autonomous planning agents**.

**Secondary Option:** **Mixtral 8x22B (Mistral AI)**
- Chosen for its **Mixture-of-Experts architecture**, which yields near-GPT-4-level reasoning performance at lower inference cost.
- Useful for production scaling where parallelism and cost-efficiency are important.
- Slightly weaker multilingual coverage and smaller context window than Llama 3.

**Pros:**
- Exceptional reasoning and strategy formulation
- Native support for structured tool-calling and JSON-based outputs
- Compatible with MCP client frameworks and agentic orchestration layers
- Commercially safe open license (Meta Llama 3 community license)
- Supported by rich inference tooling (Hugging Face, Ollama, vLLM, Llama.cpp)

**Cons:**
- High compute and memory requirements for 70B inference
- Requires fine-tuning or RAG augmentation for domain-specific travel data
- May need latency optimization (quantization or distributed inference)

# CONSEQUENCES
**Positive Impacts:**
- Enables agentic, reasoning-capable travel assistants with direct tool invocation
- Facilitates multi-step trip planning (e.g., recommend → refine → book → summarize)
- Fully open and self-hostable — no dependency on closed APIs
- Scalable for enterprise and multi-agent collaboration use cases

**Trade-offs:**
- Increased operational cost and hardware demand (GPU inference at 70B scale)
- Fine-tuning or domain adaptation required for optimal travel domain performance
- More complex observability and orchestration for MCP-based tool interactions

# COMPLIANCE
To ensure compliance:
- Host and serve **Llama 3 (70B)** under Meta’s community license, ensuring full license alignment.
- Implement **MCP client and tool validation layer** to verify JSON outputs and safe tool execution.
- Enforce **logging and traceability** for all tool-calling actions and reasoning steps.
- Maintain reproducible, containerized inference environments (e.g., via vLLM or Ollama).
- Perform regular **evaluation and audits** on tool-calling accuracy and reasoning reliability.

# COMMENTS
**References:**
- Meta AI — *Llama 3 Model Card & License*
- Mistral AI — *Mixtral 8x22B Technical Overview*
- Google DeepMind — *Gemma 2 Model Documentation*
- DeepSeek AI — *DeepSeek-V2 Technical Report*
- Model Context Protocol (MCP) — *OpenAI MCP Specification (2025)*

**Notes:**
- Prototype phase will use **Llama 3 70B** hosted via **vLLM** for full reasoning capacity.
- Integration testing with **LangGraph + MCP client** for multi-tool reasoning orchestration.
- Evaluate latency, cost, and reasoning performance before production scaling.
