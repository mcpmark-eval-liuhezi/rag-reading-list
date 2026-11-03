# RAG Reading Group — Literature Scan Digest

**Date:** 2026-11-03
**Scope:** Recent arXiv preprints on Retrieval-Augmented Generation, scanned from four angles: core RAG methods, agentic / multi-step retrieval, long-context vs. retrieval, and RAG evaluation / benchmarks.

## Selected Papers (6)

Each paper is assigned to exactly one theme: **efficiency**, **reasoning**, **multimodality**, or **safety**.

### 1. Q-RAG: Long Context Multi-step Retrieval via Value-based Embedder Training
- **arXiv:** 2511.07328 (v2: 2026-05-04) | **Posted:** 2025-11-10
- **Theme:** efficiency
- **Flag:** must-read
- **Detail:** Q-RAG fine-tunes the embedder itself with reinforcement learning for multi-step retrieval, avoiding the resource-intensive small-LLM fine-tuning used by prior multi-step methods. It reaches state-of-the-art on BabiLong and RULER with contexts up to 10M tokens, and the authors note it is a competitive, resource-efficient alternative for open-domain QA. (ICLR 2026.)

### 2. A Reproducibility Study of Metacognitive Retrieval-Augmented Generation
- **arXiv:** 2604.19899 | **Posted:** 2026-04-21
- **Theme:** reasoning
- **Flag:** must-read
- **Detail:** Reproduces MetaRAG and extends it with PointWise/ListWise rerankers and a comparison against SIM-RAG's lightweight critic for stop-retrieval. Confirms MetaRAG's relative gains over RAG and reasoning baselines but reveals lower absolute scores than reported, attributing this to closed-source LLM updates, missing implementation details, and unreleased prompts. More robust than SIM-RAG with extra retrieval features. (SIGIR 2026.)

### 3. Pix2Evidence: A Multimodal RAG System for Text and Visual Evidence
- **arXiv:** 2610.41335 | **Posted:** 2026-10-30
- **Theme:** multimodality
- **Flag:** must-read
- **Detail:** Encodes each screenshot tile together with its transcription into a single fused image-text representation so layout and readable text are jointly considered in retrieval; a vision-language teacher whitepariaoches evidence descriptions to adapt the retriever, followed by reranking. On five Wikipedia QA benchmarks the non-reranked system leads the main comparison on four, and on MMSearch reaches 26.0%, 4.4 pp above PixelRAG.

### 4. VisR-RAG-Fin: Benchmarking Multimodal RAG over Visually Rich Financial Documents
- **arXiv:** 2610.24822 | **Posted:** 2026-10-17
- **Theme:** multimodality
- **Flag:** skim
- **Detail:** Introduces an open-source benchmark (VisR-RAG-Fin) for page-level QA over visually rich financial documents, systematically comparing text-only, multimodal, and hybrid retrieval/generation configurations. Accepted at SIGIR-AP 2026.

### 5. Securing the Agent: Vendor-Neutral, Multitenant Enterprise Retrieval and Tool Use
- **arXiv:** 2605.05287 | **Posted:** 2026-05-06
- **Theme:** safety
- **Flag:** must-read
- **Detail:** addresses the gap that enterprise RAG/agentic systems rank by relevance, not authorization, so cross-tenant leakage occurs; proposes a layered isolation architecture (policy-aware ingestion, retrieval-time gating, shared inference) with ABAC gating that eliminates cross-tenant leakage with negligible overhead, validated in the open-source OGX framework. (ACM CAIS '26.)

### 6. Analyzing Quality-Latency-Resource Trade-offs in a Technical Documentation RAG Assistant Using LoRA Adaptation
- **arXiv:** 2605.28222 | **Posted:** 2026-05-27
- **Theme:** efficiency
- **Flag:** skim
- **Detail:** Ablates 20 LoRA configurations on Llama-3.2-3B and Llama-3.1-8B over a 5,144-question Kubernetes docs benchmark with a fixed hybrid-retrieval pipeline, reporting token-level F1, groundedness, pass@4, latency, memory and training cost. q/v attention adapters dominate the Pareto front; the 3B/8B choice sets the operating regime.

## Theme Assignment Rationale

- **efficiency:** Q-RAG (RL-trained embedder, SOTA at 10M tokens, resource-efficient vs. small-LLM multi-step) and the LoRA trade-off study (quality-latency-resource Pareto on a real docs benchmark) both target cost/performance engineering of RAG.
- **reasoning:** MetaRAG reproducibility directly concerns when to stop searching and how retrieval critiques reasoning — core reasoning-about-retrieval.
- **multimodality:** Pix2Evidence (fused image-text tile retrieval) and VisR-RAG-Fin (visual financial-document QA benchmark) are the two multimodal RAG contributions; Pix2Evidence is the stronger must-read, VisR-RAG-Fin a skim for the benchmark angle.
- **safety:** Securing the Agent is the clear safety pick (authorization vs. relevance, cross-tenant leakage, ABAC gating).

### Runner-up themes
- Q-RAG also fits **reasoning** (multi-step search) and **long-context** angles.
- MetaRAG also touches **evaluation/reproducibility**.
- Pix2Evidence also overlaps **evaluation** (benchmark construction).
- VisR-RAG-Fin also fits **evaluation/benchmarks** squarely.
- LoRA trade-offs also relate to **evaluation** (benchmark construction) and **long-context** (token-level F1).

## Recent Developments (web chatter, 2026)

- The dominant narrative for 2025–2026 is the merger of RAG with agent loops: static retrieve-then-generate monoliths are being replaced by tool-using, multi-step agents (Medium, Oct 2026).
- Agentic RAG surveys and data-centric overviews are proliferating (e.g., ACL 2026 Findings "Data-Centric Perspectives on Agentic Retrieval"; arXiv:2501.09136 v4), noting that evaluation still lags domain-specific curated benchmarks.
- Benchmarks are expanding: AIM-Agentic RAG Benchmark (70+ LLMs, 759 questions over 11 SQL databases, Oct 2026), workplace-question agentic RAG benchmarking, and multimodal financial-document benchmarks like VisR-RAG-Fin.
- Market estimates put the RAG platforms market at ~USD 4.0B (2025) growing to ~USD 5.52B (2026).
- Notable omitted by the arXiv angles: acceleration/deployment angle (OpenVINO agentic RAG study) and the "kill the retrieve-then-generate monolith" paradigm shift mentioned in industry commentary.

## One-Line Takeaways

- Q-RAG shows multi-step retrieval can be made resource-efficient by training the embedder with RL instead of a small LLM.
- MetaRAG's reproducibility confirms relative gains but flags hidden implementation drift.
- Pix2Evidence demonstrates that fusing image + transcription at the tile level beats text-only screenshot retrieval.
- VisR-RAG-Fin provides a rigorous benchmark for visually rich financial documents.
- Securing the Agent turns retrieval-time authorization gating into a practical safety layer for multi-tenant agents.
- LoRA on q/v projections dominates the quality-latency-resource trade-off frontier for docs RAG.
