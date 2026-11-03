# RAG Reading Group — Literature Scan Digest

**Theme angles:** core RAG methods, agentic / multi-step retrieval, long-context vs. retrieval, RAG evaluation & benchmarks.
**Selected papers:** 6 (posted Oct 2026)

---

## Selected Papers

### 1. UNREAL: Unifying Retrieval and Long-Context with a Single Model
- **arXiv:** 2610.08463 — submitted Tue, 6 Oct 2026
- **Theme:** Efficiency (also long-context vs. retrieval)
- **Flag:** MUST-READ
- **Detail:** Proposes model-native evidence selection that spans corpus retrieval and long-context inference, adding fewer than 500K trainable parameters with a frozen LLM. On a 3B-token / 21M-chunk Wikipedia index all four dense and hybrid backbones beat retriever-reranker systems: recall 49.1%→73.2% on HotpotQA, 31.7%→60.1% on 2WikiMultiHopQA, 8.8%→14.4% on MuSiQue; applied to long-context tasks the same mechanism raises NoLiMa accuracy 1.0%→24.83% at 128K tokens and LV-Eval F1 49.97%→54.66% at 256K, while reducing FLOPs and time-to-first-token vs. full-context inference from ~32K tokens onward.

### 2. Beyond Retrieval Failure: Understanding Why LLMs Miss Evidence in Multi-Hop RAG
- **arXiv:** 2610.21184 — submitted Thu, 15 Oct 2026
- **Theme:** Reasoning
- **Flag:** MUST-READ
- **Detail:** Introduces ExecutionRAG, a training-free requirement register that records open sub-questions and their supporting evidence, changing search guidance without altering evidence access. On 1,000 MuSiQue questions, wrong answers with unretrieved required evidence drop from 382→234 (all-MiniLM-L6-v2) and 383→274 (Qwen3-Embedding-0.6B), i.e. 69%→44% and 66%→48% of each system's errors respectively — but recovery does not proportionally cut total error, since premature resolutions and abstentions increase. Accepted by DAI 2026 Oral.

### 3. RouteDRAG: Learning to Route and Control Agentic Execution for Multimodal Document RAG
- **arXiv:** 2610.36444 — submitted Tue, 27 Oct 2026
- **Theme:** Multimodality (also reasoning / agentic efficiency)
- **Flag:** MUST-READ
- **Detail:** For long multimodal documents (pages, tables, figures), RouteDRAG learns when agentic execution is worth it: a Unified Document Index (graph-backed), Adaptive Path Routing predicting the benefit of Agent over shorter paths, Dynamic Agent Execution with an evolving workspace, and Sequential Policy Learning trained from observed outcomes. Average accuracy improvement of 3.47 pp over shorter-path-only execution while assigning only 79.3% of queries to the Agent, and surpassing uniform Agent execution on both benchmarks with fewer answering calls.

### 4. RAGLeak: Supply-Chain Privacy Backdoors in Retrieval-Augmented Generation
- **arXiv:** 2610.25937 — submitted Mon, 19 Oct 2026
- **Theme:** Safety
- **Flag:** MUST-READ
- **Detail:** Supply-chain privacy backdoor attack that decouples information leakage from direct textual exposure, avoiding the stealthiness/fidelity trade-off of prior extraction attacks that rely on prompt injection or paraphrased backdoors. Relevant for anyone shipping RAG over untrusted or third-party knowledge bases.

### 5. When Is Additional Retrieval Worthwhile? A Cost-Aware Study of Evidence Gain and Answer Reliability in RAG
- **arXiv:** 2610.37358 — submitted Tue, 27 Oct 2026
- **Theme:** Efficiency
- **Flag:** SKIM
- **Detail:** Cost-aware two-action policy choosing between dense-retrieval-plus-reranking and hybrid lexical-dense retrieval, with a regularized linear model and threshold selected via document-grouped cross-validation. On 188 QASPER questions (169 evidence-evaluable) it triggers hybrid retrieval on 46 (24.5%) with the same Hit@10 as always-hybrid (78.70% vs 76.92%), and 4-bit Qwen3-4B answer-level assessments show no clear correctness/faithfulness gain despite the evidence gain — retrieval efficiency and answer reliability are distinct.

### 6. A Security Meta-Model for Retrieval-Augmented Generation Systems
- **arXiv:** 2610.11893 — submitted Thu, 8 Oct 2026
- **Theme:** Safety
- **Flag:** SKIM
- **Detail:** Security meta-model capturing causal relationships among RAG surfaces, attacks, weaknesses, risks and CIA impact; instantiated as a catalog from 43 publications (2023–2026) with an interactive graph visualizer and stakeholder-specific views. Analysis reveals an imbalance between attack-focused and defense-focused research, threat concentration at ingestion, and coverage gaps for output integrity; assessed against OWASP LLM Top-10 and covering textual, graph-based and multimodal RAG configurations.

---

## Runner-up / Notable Omissions

- **RAGStress (2610.04691, 3 Oct 2026):** controlled benchmark for KB degradation (factual corruption, numeric typo, relevance poisoning, contradiction injection) over 52,500 eval conditions; semantic-fidelity corruptions far more harmful than signal-utility perturbations. Evaluation-angle runner-up.
- **Metacognitive Reliability Supervision (2610.41738, 30 Oct 2026):** reliability-aware process reward for GRPO balancing search vs. no-search; accuracy-efficiency trade-off over 7 QA benchmarks. Efficiency/reasoning runner-up.
- **Agentic AutoRAG (2610.08452, 6 Oct 2026):** LLM-agent optimizer with retrieval-vs-generation failure attribution, Pareto accuracy/cost on 3 multi-hop QA benchmarks and 58% cost of healthcare-corpus baseline at 77% median exam accuracy. Efficiency runner-up.
- **EC-RAG (2610.08674, 6 Oct 2026):** event-centric retrieval for long-video understanding (Video-MME, MLVU, LongVideoBench) — multimodality runner-up.
- **DeFT-RAG (2610.37826, 27 Oct 2026):** incremental decomposition for multi-hop — reasoning runner-up.

---

## Recent Developments (web chatter, ~Oct 2026)

- The dominant narrative is the merger of RAG with agent loops: the "retrieve-then-generate monolith" is being killed in favor of iterative, tool-using agents (Medium, Oct 2026; Scalacode guide).
- ACL 2026 Findings includes a data-centric survey on Agentic RAG (Deng et al.), cataloging training datasets and benchmarks across QA, web and software engineering, motivated by data scarcity for interactive agent trajectories.
- RAG platforms market valued at ~USD 4.00B (2025), estimated USD 5.52B (2026) — industrial traction continuing.
- Knowledge-graph-enhanced RAG is a recurring theme (Vector Institute, Oct 2026).
- Chatter mentions RAG evaluation metrics (hit/answer-level) and self-citation collapse in knowledge bases as open issues.

**Notable calls not covered by the four top angles:** retrieval-augmented generation for clinical/medical QA (Nature Sci Rep 2026) and RAG + knowledge graphs, which the selected papers only partly touch (EC-RAG for videos, meta-model for graph RAG).

---

## One-Line Takeaways

- UNREAL: one model-native mechanism can do both corpus retrieval and long-context evidence selection, cutting FLOPs while boosting recall and long-context accuracy.
- ExecutionRAG: much apparent retrieval failure is search drift, not unreachable evidence; a requirement register recovers 44–48% of errors without proportional total-error gain.
- RouteDRAG: route to an agent only when beneficial (79.3% of queries skip it) for multimodal documents.
- RAGLeak: supply-chain backdoors can leak data without的直接 textual exposure.
- Cost-aware routing: extra retrieval helps evidence retrieval but not necessarily answer correctness (24.5% of queries need it; no clear quality gain).
- Security meta-model: structure RAG risk as surfaces→attacks→CIA impact, with OWASP LLM Top-10 coverage and output-integrity gaps.
