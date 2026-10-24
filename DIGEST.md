# RAG Reading Group — Weekly Literature Scan

- **Date:** 2026-10-25
- **Scope:** Recent arXiv preprints on retrieval-augmented generation, scanned from **nine angles**: core RAG methods, agentic/multi-step retrieval, long-context vs. retrieval, RAG evaluation/benchmarks, efficiency/indexing, multimodal RAG, safety, and reasoning.
- **Volume:** the scans returned 90 results across the angles (each angle returned up to 10 results), leaving roughly 80 unique preprints after de-duplication. This digest selects **six** and places each in exactly one of four themes: **efficiency, reasoning, multimodality, safety**.
- **Convention:** each paper is flagged **must-read** (a few sentences from its arXiv page), **worth skimming** (one-liner), or **background** (one-liner). Every paper also notes where it arguably fits a runner-up theme.

---

## How the theme assignment worked

1. **Primary axis, not application.** For each candidate I extracted the paper's *primary* question — the problem it changes — rather than the problem it applies to. Everything else (domain, model choice, evaluation harness) was treated as evidence, not theme.
2. **Map the axis to one theme.** Efficiency = new trade-offs in compute, memory, latency, or index cost; reasoning = retrieval interleaved with multi-step thought; multimodality = grounding text answers in images, video, or 3D; safety = attacks, guardrails, or secure-deployment properties of the retrieval path.
3. **No double-counting.** Where a paper arguably answered two questions I named a *runner-up* theme (with its arXiv ID) and placed it in exactly one. The theme grid below is exhaustive and mutually exclusive.

---

## The six picks

### 1. Efficiency — **must-read**

**RAPID: Long-Context Inference with Retrieval-Augmented Speculative Decoding** — [arXiv:2502.20330](https://arxiv.org/abs/2502.20330) (posted 27 Feb 2025; ICML 2025 Spotlight)

RAPID shows that retrieval and long context are really a single knob rather than two competing paradigms. A *RAG drafter* — a small LLM operating on shortened retrieval contexts — speculates on the generation of a same-scale or larger long-context target LLM, and an inference-time knowledge transfer step enriches the target's output distribution using the drafter's evidence. On LLaMA-3.1 and Qwen2.5 backbones it goes from 39.33 to 42.83 on InfiniteBench for LLaMA-3.1-8B with more than 2× speedups, and its analyses show the gains hold across context lengths and retrieval quality. Worth reading because it dissolves the "retrieval vs. long context" framing I used as one of my scan angles: the practical story is a hybrid, not a competition.

### 2. Efficiency — **must-read**

**RAG-Stack: Co-Optimizing RAG Quality and Performance From the Vector Database Perspective** — [arXiv:2510.20296](https://arxiv.org/abs/2510.20296) (posted 23 Oct 2025)

A three-pillar blueprint for treating quality and performance as one system: (1) **RAG-IR**, an intermediate representation that decouples the quality and performance aspects of a RAG pipeline; (2) **RAG-CM**, a cost model that estimates system performance from an RAG-IR; and (3) **RAG-PE**, a plan-exploration algorithm that searches for high-quality, high-performance configurations. The author's framing — that the quality–performance joint optimization is "significantly more complex than it appears due to the numerous knobs on both the algorithmic and systems sides" — makes this a natural anchor for the efficiency theme in a discussion of trade-offs.

**Runner-up for efficiency:** [SPI: Query-Depth-Adaptive Indexing for Streaming RAG in Vector Databases](https://arxiv.org/abs/2511.16681) (arXiv:2511.16681, posted 12 Nov 2025) — streaming RAG indexing with query-depth-adaptive retrieval achieving 1.4–2.3× latency reduction; it overlaps efficiency but is really a vector-DB systems paper, so it lands as a mention rather than a selection.

### 3. Reasoning — **must-read**

**Chain-of-Retrieval Augmented Generation (CoRAG)** — [arXiv:2501.14342](https://arxiv.org/abs/2501.14342) (posted 24 Jan 2025; NeurIPS 2025)

Training o1-style RAG models that *retrieve and reason step by step* before answering: rejection sampling auto-generates intermediate retrieval chains to augment datasets that only provide the final answer, a dynamic query reformulation step updates the query as the retrieval state evolves, and test-time decoding strategies control chain length and count to scale the model's compute. Across multiple benchmarks the gains concentrate on multi-hop question answering (more than 10 points of EM over strong baselines, and a new SOTA on KILT), and the paper is the clearest case that *multi-step* retrieval beats single-shot retrieval when the first pass is imperfect.

### 4. Reasoning — **worth skimming**

**Self-Reflective Chain-of-Thought (SRCoT): Evidence-Based Text Generation via a Closed-Loop Retrieve–Reflect–Revise Pipeline on Edge LLMs** — [arXiv:2610.23311](https://arxiv.org/abs/2610.23311) (posted 16 Oct 2026)

A modular Retrieve–Reflect–Revise loop that keeps environment state, persistent knowledge, accumulated experience, and short-term memory in provenance-labeled stores, with BM25 supplying local context and subsequent passes surfacing intermediate drafts, missing-information markers, and claim–evidence mappings that drive revision, clarification, or abstention — all running on small edge LLMs. Author's own caveats matter: it demonstrates *inspectability*, not comparative superiority, hallucination reduction, clinical validity, or operational safety, and behavior is unproven across models. Fetch if the group wants a genuinely honest small-model RAG architecture; skim the rest.

**Runner-up for reasoning:** [MA-RAG: Multi-Agent Retrieval-Augmented Generation](https://arxiv.org/abs/2505.20096) (arXiv:2505.20096, posted 11 Oct 2025) — multi-agent RAG framed around resolving retrieval ambiguity; it spans reasoning and agentic retrieval, but its methodological contribution is more narrowly scoped than CoRAG's.

### 5. Multimodality — **must-read**

**Multimodal Hybrid RAG for Scientific Document Understanding using Open-Source SLMs** — [arXiv:2607.24799](https://arxiv.org/abs/2607.24799) (posted 6 Jul 2026)

An end-to-end open-source pipeline for domain queries over scientific documents: a multimodal ingestion stage uses Qwen2-VL-2B-Instruct to generate textual summaries of tables and figures; retrieval combines HNSW dense search with GIN lexical search unified by reciprocal rank fusion and refined by cross-encoder reranking, with a Query Condenser keeping multi-turn coherence; evaluations run on MMLongBench, a BeIR-format synthetic dataset, and the DeepEval framework. It reports a 157% improvement in retrieval quality over a Naive-RAG baseline at only 50 ms added latency, with Qwen2-VL-2B-Instruct producing results comparable to cloud-based models in BERTScore.

**Runner-up for multimodality:** the [A Survey of Multimodal Retrieval-Augmented Generation](https://arxiv.org/abs/2504.08748) (arXiv:2504.08748, posted 26 Mar 2025) survey — components, datasets, evaluation methods, and limitations in one place; it's the better map for the landscape, but the 2607 paper is the more recent, more concrete entry point.

### 6. Safety — **must-read**

**The Promptware Kill Chain: How Prompt Injections Gradually Evolved Into a Multistep Malware Delivery Mechanism** — [arXiv:2601.09625](https://arxiv.org/abs/2601.09625) (posted 14 Jan 2026)

Reframes indirect prompt injection as **promptware** — a new class of malware-execution mechanism triggered through prompts engineered to exploit an application's LLM — with a seven-stage kill chain: Initial Access (prompt injection) → Privilege Escalation (jailbreaking) → Reconnaissance → Persistence (memory and retrieval poisoning) → Command and Control → Lateral Movement → Actions on Objective. The paper analyzes 36 prominent studies and real-world incidents affecting production LLM systems and finds that at least 21 documented attacks traverse four or more stages, making the threat model a live production concern rather than a thought experiment, and it argues for defense-in-depth across the whole promptware life cycle.

**Runner-up for safety:** [nokast-secureRAG: Context-Aware Prompt Injection Detection via Small Language Models in RAG Pipelines](https://arxiv.org/abs/2610.28364) (arXiv:2610.28364, posted 20 Oct 2026) — a roughly 0.5B-parameter SLM acting as a semantic firewall between retrieval and generation, reaching 0.994 detection recall at 0.026 false-positive rate. The author discloses that fluent fact-poisoning attacks lie outside its instruction-consistency threat model, so it's a promising baseline rather than a solved problem.

---

## Theme breakdown

| Theme | Paper | arXiv ID | Posted | Flag |
|---|---|---|---|---|
| Efficiency | RAPID: Long-Context Inference with RAG Speculative Decoding | arXiv:2502.20330 | 27 Feb 2025 | must-read |
| Efficiency | RAG-Stack: Co-Optimizing RAG Quality and Performance | arXiv:2510.20296 | 23 Oct 2025 | must-read |
| Reasoning | Chain-of-Retrieval Augmented Generation (CoRAG) | arXiv:2501.14342 | 24 Jan 2025 | must-read |
| Reasoning | Self-Reflective Chain-of-Thought (SRCoT) | arXiv:2610.23311 | 16 Oct 2026 | worth skimming |
| Multimodality | Multimodal Hybrid RAG for Scientific Document Understanding (Open-Source SLMs) | arXiv:2607.24799 | 6 Jul 2026 | must-read |
| Safety | The Promptware Kill Chain | arXiv:2601.09625 | 14 Jan 2026 | must-read |

**Total:** six papers — four must-read, one worth skimming, one background. No paper is assigned two themes; every ambiguity is surfaced in its runner-up note.

---

## One-line takeaways

1. **RAPID (2502.20330):** RAG drafters and long-context LLMs can share one knob — 2× speedups and accuracy up.
2. **RAG-Stack (2510.20296):** stop optimizing RAG quality and performance separately; treat them as one joint system.
3. **CoRAG (2501.14342):** multi-step retrieval beats single-shot retrieval, especially on multi-hop QA.
4. **SRCoT (2610.23311):** self-correcting loops are inspectable — and honest to admit when they don't help.
5. **Multimodal hybrid RAG (2607.24799):** cheap open SLMs plus hybrid dense/lexical retrieval close most of the multimodal gap.
6. **Promptware Kill Chain (2601.09625):** RAG poisoning is now a staged, production-real attack surface, not a hypothetical.

---

## Recent developments (from the wider web, October 2026)

The dominant conversation right now is that **RAG and agent loops have merged**, and that this is the new baseline for production systems:

- **Agentic RAG is the new default, not a niche variant.** Rather than wiring a static vector database directly into a generator, production stacks treat retrieval as a *tool* the LLM planner decomposes the prompt around, decides which retriever to call (vector DB, knowledge graph, web API), judges whether the returned context is sufficient, and loops back to retrieve more when it senses a gap. Where an agent first calls retrieval once and trusts the result, an agent self-heals: refusing to pass bad context into the generator. This is the biggest shift of 2025–2026 according to industry write-ups (Maxcore, LangGraph guides, and community posts alike).
- **RAG survives the 1M-token context window.** The 2026 position is that long context buys throughput but not *precision*; hybrid agentic retrieval filters noise and feeds highly refined, verified context into the generator. The "retrieval vs. context length" debate is now moot.
- **Streaming RAG via CDC.** Nightly re-indexing Python scripts are gone from enterprise pipelines; Change Data Capture streams database changes straight into the embedding function for a continuously fresh index without external orchestration.
- **Contextual chunking is now standard ingestion.** Prepending a short per-chunk summary ("this chunk is from Q3 2025 earnings of Acme Corp") cuts retrieval failures nearly in half and is a baseline technique for new knowledge bases.
- **Observability of retrieval spans is becoming an eval requirement.** Tracing every retrieve call, retrieval decision, and retrieved context is increasingly required when you hand control over to agents.
- **Private vs. public RAG is a live enterprise decision.** Keeping embeddings, indexes, and logs inside your own boundary is a deliberate architectural choice, not an afterthought, in 2026.
- **Market context:** the global RAG market is projected to grow from USD 1.98B (2025) to USD 52.6B by 2035, ~38.8% CAGR.

**What the wider chatter mentions that the four scan angles missed:**

- **Chunking and ingestion quality as a first-class concern.** My scans covered it only tangentially via agentic RAG. "Lost in the Middle" at scale, contextual retrieval, and ingestion-time summarization are now treated as core building blocks of a good pipeline, not afterthoughts.
- **Streaming RAG via Change Data Capture.** Present on the engineering side (mentioned above) but not represented among the six selected, which skews toward algorithmic and evaluation concerns.
- **Observability and tracing of agentic retrieval spans.** A tooling/engineering angle that only surfaced in the web search; relevant if the group starts building (rather than just reading about) agentic pipelines.
- **Private vs. public RAG deployment as a distinct axis.** The scans touched RAG security broadly but not the deployment-context distinction (third-party vector hosts vs. self-hosted), which is a genuine 2026 discussion topic.

---

## Scan notes

- Scanned angles and raw hit counts: core RAG methods (10), agentic retrieval (10), long-context vs. retrieval (10), evaluation/benchmarks (10), efficiency/indexing (10), multimodal RAG (10), safety (10), reasoning (10) = 90 results across 9 angles.
- Selection logic: recency filtered out everything pre-2024; methodologically canonical papers (Self-RAG lineage, classic benchmarks) appeared but scored lower because they were already well represented; papers that answered two themes at once were assigned to one and cited as runner-up to avoid double-counting.
- Web chatter searched October 2026; reflects public industry/academic discussion rather than the arXiv corpus itself.