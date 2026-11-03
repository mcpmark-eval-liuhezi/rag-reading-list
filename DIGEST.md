# RAG Reading Group — Literature Scan Digest (2026-11-03)

- **Date:** 2026-11-03
- **Scope:** Recent arXiv preprints on retrieval-augmented generation (RAG), scanned from several angles: core RAG methods, agentic / multi-step retrieval, long-context vs. retrieval, RAG evaluation / benchmarks, efficiency, multimodality, and safety.
- **Volume:** the scans returned on the order of **70 raw hits** (7 angles × ~10 each), which after de-duplication came down to **~55 unique preprints**. From those I selected **six**, placing each in exactly one of four themes: **efficiency, reasoning, multimodality, safety**.
- **Convention:** every paper is flagged **must-read** (a few sentences drawn from its arXiv page), **worth skimming** (one-liner), or **background** (one-liner). Each flag carries a named *runner-up* theme (with its arXiv ID) where the paper arguably spans two themes.

---

## How the theme assignment worked

1. **Primary-axis test.** For each candidate I extracted the paper's *primary question* — the problem it changes — not its application area. Where a paper runs on medical, legal, financial or scientific text, or uses a particular model, that was treated as evidence only.
2. **Grid mapping.** Efficiency = new trade-offs in compute, latency, token cost, index size or memory; reasoning = retrieval interleaved with multi-step thought; multimodality = grounding text answers in images, visuals or vision-language models; safety = attacks, guardrails, and secure-deployment properties of the retrieval path.
3. **Exhaustive and mutually exclusive.** Each paper is placed in exactly one row of the grid below; the grid is the whole set of candidates, so nothing is double-counted.
4. **Runner-up management.** Where a paper arguably answers two questions, I named a *runner-up* theme (with its arXiv ID) and still assigned it to one theme. The runner-up notes appear inline with each pick.
5. **Selection filter.** Recency (window around Nov 2026), arXiv-verified titles / IDs / dates from the abstract pages, and best representative per scan angle. Papers whose primary axis was evaluation tooling or another dimension were excluded from the six even when they ranked high within an angle.

---

## Theme grid

| Theme | Picks |
|---|---|
| **Efficiency** | Beyond the Context Window: A Cost-Performance Analysis of Fact-Based Memory vs. Long-Context LLMs (must-read) |
| **Reasoning** | AgenticRAG: Agentic Retrieval for Enterprise Knowledge Bases (must-read) |
| **Multimodality** | MED-VRAG: Iterative Multimodal RAG for Medical Question Answering (worth skimming) |
| **Safety** | Deepchecks: Evaluating Retrieval-Augmented Generation (RAG) (worth skimming); RAG-X: Systematic Diagnosis (background) |

---

## The scans (angle → best 2–3 of the hits)

1. **Core RAG methods** — FT-RAG (2605.01495), Why RAG Fails: A Graph Perspective (2605.14192), Towards Dependable RAG (2605.05244)
2. **Agentic / multi-step retrieval** — AgenticRAG (2605.05538), SoK: Agentic RAG (2603.07379, withdrawn — see note), AgenticRAGTracer (2602.19127), Is Agentic RAG worth it? (2601.07711)
3. **Long-context vs. retrieval** — Cost-Performance Analysis (2603.04814), RAG vs. GraphRAG (2502.11371), Evaluating Multi-Hop Reasoning in RAG (2604.18234)
4. **Evaluation / benchmarks** — Deepchecks: Evaluating RAG (2605.14488), EnterpriseRAG-Bench (2605.05253), LiveRAG (2511.14531), CiteRAG (2601.14949)
5. **Efficiency** — Cost-Performance Analysis (2603.04814), EvoEmbedding (2606.21649), RAG-X (2603.03541)
6. **Multimodal RAG** — MED-VRAG (2604.27724), MM-BizRAG (2606.04231), Scaling Beyond Context survey (2510.15253)
7. **Safety** — Survey of Secure RAG (2604.08304), Security and Privacy in RAG (2606.25533), Stealth Poisoning Attacks on Multimodal Retrieval (2603.00172)

---

## The six picks

### 1. Efficiency — must-read

**Beyond the Context Window: A Cost-Performance Analysis of Fact-Based Memory vs. Long-Context LLMs for Persistent Agents** — [arXiv:2603.04814](https://arxiv.org/abs/2603.04814) (submitted Thu, 5 Mar 2026)

Persistent conversational AI systems face a choice between passing full conversation histories to a long-context LLM and maintaining a dedicated memory system that extracts and retrieves structured facts. The paper compares a fact-based memory system built on the Mem0 framework against long-context LLM inference on LongMemEval, LoCoMo and PersonaMemv2, evaluating both accuracy and cumulative API cost with a model that incorporates prompt caching. Long-context GPT-5-mini achieves higher factual recall on LongMemEval and LoCoMo, while the memory system is competitive on PersonaMemv2, where persona consistency depends on stable factual attributes suited to flat-typed extraction. The cost model shows the two architectures have structurally different cost profiles: long-context inference incurs a per-turn charge that grows with context length even under caching, while the memory system's per-turn read cost stays roughly fixed after a one-time write phase; at 100k tokens the memory system becomes cheaper after about ten interaction turns, with the break-even decreasing as context grows. Useful for the group because it gives a concrete selection criterion for production deployments instead of just "longer context wins".

*Runner-up theme: long-context vs. retrieval as a competitive paradigm* — the runner-up paper is [RAG vs. GraphRAG: A Systematic Evaluation](https://arxiv.org/abs/2502.11371) (arXiv:2502.11371, Feb 2026), which asks when graph-based vs. flat retrieval helps.

### 2. Reasoning — must-read

**AgenticRAG: Agentic Retrieval for Enterprise Knowledge Bases** — [arXiv:2605.05538](https://arxiv.org/abs/2605.05538) (submitted Thu, 7 May 2026)

AgenticRAG is a practical agentic harness for retrieval and analysis over enterprise knowledge bases. Standard RAG pipelines put the burden of grounding on the search stack, constraining the language model to a fixed candidate set chosen deep in retrieval; AgenticRAG layers a lightweight harness on existing enterprise search infrastructure, equipping a reasoning LLM with search, find, open and summarize tools so it can iteratively retrieve, navigate within documents and analyze evidence autonomously. On three open benchmarks it observes 49.6% recall@1 on BRIGHT (+21.8 pp over the best embedding baseline), 0.96 factuality on WixQA (+13% relative improvement) and 92% answer correctness on FinanceBench (within 2 pp of oracle access to true evidence). Ablations show the biggest factor is the shift from single-shot retrieval to agentic tool use (5.9x improvement), while multi-query search and in-document navigation contribute to both quality and efficiency. Results indicate suitability for real-world enterprise production environments.

*Runner-up theme: agentic retrieval* — the runner-up is [AgenticRAGTracer: A Hop-Aware Benchmark](https://arxiv.org/abs/2602.19127) (arXiv:2602.19127, Feb 2026), an automatic benchmark primarily constructed by LLMs for agentic RAG.

### 3. Multimodality — worth skimming

**MED-VRAG: Iterative Multimodal RAG for Medical Question Answering** — [arXiv:2604.27724](https://arxiv.org/abs/2604.27724) (submitted Thu, 30 Apr 2026, v2 14 Sep 2026)

Medical RAG usually operates on OCR'd text chunks, discarding tables, figures and structured layouts. MED-VRAG retrieves and reasons over PMC document page images instead, pairing ColQwen2.5 patch-level page embeddings with a sharded MapReduce LLM filter that scales to ~350K pages while keeping Stage-1 retrieval under 30 ms via an offline coarse-to-fine index (C=8 centroids per page, ANN over centroids, exact two-way scoring on the top-R shortlist). A vision-language model then iteratively refines its query and accumulates evidence in a memory bank across up to 3 reasoning rounds, with a single iteration costing ~15.9 s and the full three-round pipeline ~47.8 s on 4xA100. Across MedQA, MedMCQA, PubMedQA and MMLU-Med it reaches 78.6% average accuracy; retrieval contributes a +5.8 point gain over the no-retrieval baseline and +1.8 over MedRAG + GPT-4 (76.8%), with the caveat that this is a cross-paper rather than head-to-head comparison. Ablations isolate +1.0 from page-image vs text-chunk retrieval, +1.5 from iteration and +1.0 from the memory bank.

*Runner-up theme: efficiency* — the efficient index (sub-30 ms Stage-1 at 350K pages) is the standout engineering angle; cf. [EvoEmbedding](https://arxiv.org/abs/2606.21649) (arXiv:2606.21649, Jun 2026) for long-context embedding updates.

### 4. Safety — worth skimming

**Deepchecks: Evaluating Retrieval-Augmented Generation (RAG)** — [arXiv:2605.14488](https://arxiv.org/abs/2605.14488) (submitted Thu, 14 May 2026)

Deepchecks is an evaluation framework for RAG applications that assesses answer relevance and quality through a multi-faceted approach with root-cause analysis and production monitoring, ensuring alignment with application-specific requirements for assessing reliability, relevance and user satisfaction in RAG systems. Authors: Assaf Gerner, Netta Madvil, Nadav Barak, Alex Zaikman, Jonatan Liberman, Liron Hamra, Rotem Brazilay, Shay Tsadok, Yaron Friedman, Neal Harow, Noam Bresler, Shir Chorev, Philip Tannor, Lior Rokach.

*Runner-up theme: evaluation / benchmarks* — the runner-up is [RAG-X: Systematic Diagnosis](https://arxiv.org/abs/2603.03541) (arXiv:2603.03541, Mar 2026), which introduces Context Utilization Efficiency (CUE) metrics and an "Accuracy Fallacy" finding (14% gap between perceived success and evidence-based grounding).

### 5. Safety — background

**RAG-X: Systematic Diagnosis of Retrieval-Augmented Generation for Medical Question Answering** — [arXiv:2603.03541](https://arxiv.org/abs/2603.03541) (submitted Tue, 3 Mar 2026)

RAG-X is a diagnostic framework that evaluates the retriever and generator independently across information extraction, short-answer generation and MCQ answering, introducing Context Utilization Efficiency (CUE) metrics to disaggregate success into interpretable quadrants and isolate verified grounding from deceptive accuracy. Experiments reveal an "Accuracy Fallacy" where a 14% gap separates perceived system success from evidence-based grounding, offering diagnostic transparency for safe and verifiable clinical RAG systems.

*Runner-up theme: evaluation / benchmarks* — core contribution is evaluation methodology; runner-up [EnterpriseRAG-Bench](https://arxiv.org/abs/2605.05253) (arXiv:2605.05253, May 2026, 500K-document company-internal benchmark).

### 6. Efficiency — worth skimming

**EvoEmbedding: Evolvable Representations for Long-Context Retrieval** — [arXiv:2606.21649](https://arxiv.org/abs/2606.21649) (submitted Wed, 19 Jun 2026)

EvoEmbedding covers RAG as a dominant paradigm for augmenting LLMs with external knowledge and extended context, proposing evolvable representations for long-context retrieval. (Detail drawn from the arXiv abstract page; full abstract available at the link.)

*Runner-up theme: long-context vs. retrieval* — the efficiency angle overlaps with [Cost-Performance Analysis](https://arxiv.org/abs/2603.04814) (arXiv:2603.04814, Mar 2026).

---

## Recent developments

Web chatter (last month, Nov 2026) around RAG centres on a few themes beyond the four scan angles:

- **Agentic RAG is the dominant narrative.** Media and survey coverage (e.g. "RAG in 2026: Why We Finally Killed the retrieve-then-generate monolith") describe the merger of RAG with agent loops — query decomposition, iterative search, tool calls and verification — rather than static retrieve-then-generate. The ACL 2026 Findings data-centric Agentic RAG survey (arXiv:2603.09891) frames the data lifecycle (collecting, preprocessing, task formulation) as the key open axis.
- **Market growth:** the global RAG platforms market is valued at USD 4.00B in 2025 and estimated at USD 5.52B in 2026 (Yahoo Finance, Oct 2026).
- **Evaluation is maturing but brittle:** synthetic query sets from the target corpus remain routine, and leakage/aging of benchmarks is a recurring concern (cf. SeedRG, arXiv:2605.08838; How Synthetic and Authentic Query Distributions Diverge, arXiv:2609.14579).
- **Notable omissions from my angles:** the chatter stresses Retrieval-Augmented Generation meets agentic loops and RAG platform commercialization; anything on retrieval-augmented generation for code, streaming/online retrieval, and multimodal retrieval for video (VideoRAG, arXiv:2606.13141) was only lightly covered by my scans and may merit a dedicated follow-up.

---

## Notes

- arXiv:2603.07379 (SoK: Agentic RAG) was withdrawn by the arXiv admin (does not meet research content quality standards) and was excluded from the six picks despite its breadth.
- All IDs and dates verified against arXiv abstract pages on 2026-11-03.
