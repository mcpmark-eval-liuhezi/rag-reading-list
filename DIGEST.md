# RAG Reading Group — Literature Scan Digest (2026-11-03)

- **Date:** 2026-11-03
- **Scope:** Recent arXiv preprints on retrieval-augmented generation (RAG), scanned from four angles: (1) core RAG methods, (2) agentic / multi-step retrieval, (3) long-context vs. retrieval, (4) RAG evaluation / benchmarks. Multimodality and safety were covered as well given the theme grid.
- **Volume:** the scans returned about **35 raw hits** (four angles x up to ten each), which after de-duplication came down to **~30 unique preprints**. From those I selected **six**, placing each in exactly one of four themes: **efficiency, reasoning, multimodality, safety**.
- **Convention:** every paper is flagged **must-read** (a few sentences drawn from its arXiv page), **worth skimming** (one-liner), or **background** (one-liner). Each flag carries a named *runner-up* theme (with its arXiv ID) where the paper arguably spans two themes.

---

## How the theme assignment worked

1. **Primary-axis test.** For each candidate I extracted the paper's primary question — the problem it changes — not its application area. Where a paper runs on medical, legal, financial or scientific text, or uses a particular model, that was treated as evidence only.
2. **Grid mapping.** Efficiency = new trade-offs in compute, latency, token cost, index size or memory; reasoning = retrieval interleaved with multi-step thought; multimodality = grounding text answers in images, visuals or vision-language models; safety = attacks, guardrails, and secure-deployment properties of the retrieval path.
3. **Exhaustive and mutually exclusive.** Each paper is placed in exactly one row of the grid below; the grid is the whole set of candidates, so nothing is double-counted.
4. **Runner-up management.** Where a paper arguably answers two questions, I named a *runner-up* theme (with its arXiv ID) and still assigned it to one theme. The runner-up notes appear inline with each pick.
5. **Selection filter.** Recency (Oct 2025-Oct 2026 window), arXiv-verified titles / IDs / dates from the abstract pages, and best representative per scan angle. Papers whose primary axis was evaluation tooling or another dimension were excluded from the six even when they ranked high within an angle.

---

## The scans (angle -> best hits)

1. **Core RAG methods** — SoK: Agentic RAG (2603.07379), FT-RAG (2605.01495), RAG Must Move Beyond (2604.12138), Why RAG Fails: A Graph (2605.14192), Differentially Private RAG (2602.14374).
2. **Agentic / multi-step retrieval** — AgenticRag-R1 (2608.29622), A-RAG: Scaling Agentic RAG (2602.03442), AgenticRAG: Enterprise Knowledge (2605.05538), Is Agentic RAG worth it? (2601.07711), Q-RAG (2511.07328).
3. **Long-context vs. retrieval** — Unifying Retrieval and Long-Context with a Single Model (2610.08463), Route Before Retrieve: Activating Latent Routing (2605.10235), MLDocRAG (2602.10271), Q-RAG (2511.07328), DF-RAG (2601.17212).
4. **Evaluation / benchmarks** — RAGPerf (2603.10765), Deepchecks: Evaluating RAG (2605.14488), Generating Leakage-Free Benchmarks (2605.08838), Towards Global RAG (2510.26205), RAGMark (2609.05760), ViDoRe V3 (2601.08620).
5. **Multimodality** — VLD-RAG (2607.24748), MLDocRAG (2602.10271), ViDoRe V3 (2601.08620).
6. **Safety** — A Survey of Secure RAG (2604.08304, EMNLP 2026), Security and Privacy in RAG (2606.25533), Towards Secure RAG (2603.21654), AuthorityBench (2603.25092).

---

## The six picks

### 1. Efficiency — must-read

**RAGPerf: An End-to-End Benchmarking Framework for Retrieval-Augmented Generation Systems** — [arXiv:2603.10765](https://arxiv.org/abs/2603.10765) (submitted Wed, 11 Mar 2026)

RAGPerf gives end-to-end benchmarking of RAG systems with negligible performance overhead; the authors open-source the codebase and demonstrate it through a comprehensive set of experiments. It fits the efficiency theme because it targets the cost/quality trade-space of full RAG pipelines (indexing, retrieval, generation) rather than any single component, and it sits alongside the long-context-vs-retrieval angle by situating RAG among other inference strategies. For the group: practical, reproducible, and a good baseline for "how much does RAG actually cost" discussions.

Runner-up theme: evaluation / benchmarks (it is itself a benchmarking framework paper) — the strongest runner-up here is [Deepchecks](https://arxiv.org/abs/2605.14488) (arXiv:2605.14488, May 2026), which adds root-cause analysis and production monitoring on top of classic retrieval/generation metrics.

### 2. Reasoning — must-read

**Q-RAG: Long Context Multi-step Retrieval via Value-based Embedder Training** — [arXiv:2511.07328](https://arxiv.org/abs/2511.07328) (submitted Mon, 10 Nov 2025; v2 Mon, 4 May 2026)

Q-RAG tackles the gap between single-step retrieval and multi-step search in long-context settings: it trains embedders with a value-based objective so that query embeddings focus on the parts of the context that are actually relevant across multiple retrieval hops. Experiments report multi-hop retrieval gains over eight baselines on both retrieval and generation (V-RAGBench). For the group: a direct answer to "when one retrieval is not enough" with a train-time fix rather than a test-time sampler.

Runner-up theme: long-context vs. retrieval (the angle it came from) — the strongest runner-up is [Route Before Retrieve: Activating Latent Routing Abilities of LLMs for RAG vs. Long-Context Selection](https://arxiv.org/abs/2605.10235) (arXiv:2605.10235, May 2026), which picks RAG or long-context per query for cost-effectiveness.

### 3. Multimodality — worth skimming

**VLD-RAG: Agentic Vision-Language Retrieval-Augmented Generation for Long, Visually-Rich Multi-Page Documents** — [arXiv:2607.24748](https://arxiv.org/abs/2607.24748) (submitted Thu, 21 May 2026)

VLD-RAG studies multimodal RAG for question answering over visually-rich long documents where retrieval must select evidence scattered across pages; it shows that coordinated agent verification and multimodal hybrid retrieval are crucial for reliable grounding when correct answers depend on cross-page evidence. For the group: concrete evidence that hybrid retrieval + agent verification beats pure captioning or pure OCR pipelines on long documents.

Runner-up theme: reasoning — the strongest runner-up is [Q-RAG](https://arxiv.org/abs/2511.07328) (arXiv:2511.07328), which is multi-step retrieval with a long-context flavor.

### 4. Multimodality — worth skimming

**MLDocRAG: Multimodal Long-Context Document Retrieval Augmented Generation** — [arXiv:2602.10271](https://arxiv.org/abs/2602.10271) (submitted Tue, 10 Feb 2026; v3 Fri, 13 Feb 2026)

MLDocRAG consistently improves retrieval quality and answer accuracy over baselines on MMLongBench-Doc and LongDocURL, demonstrating effectiveness for multimodal long-context understanding. For the group: a solid empirical result on combining multimodality with long-context retrieval.

Runner-up theme: efficiency — the strongest runner-up is [RAGPerf](https://arxiv.org/abs/2603.10765) (arXiv:2603.10765), which covers cost/overhead of RAG systems.

### 5. Safety — must-read

**A Survey of Secure Retrieval-Augmented Generation** — [arXiv:2604.08304](https://arxiv.org/abs/2604.08304) (submitted Thu, 9 Apr 2026; v5 Mon, 12 Oct 2026; accepted at EMNLP 2026)

This survey covers the security risks opened by RAG's access path to external knowledge — prompt injection through retrieved documents, toxic/outdated content propagation, and membership inference — and surveys defenses. For the group: the current canonical survey to start for the safety theme, updated through Oct 2026 with five revisions.

Runner-up theme: evaluation — the strongest runner-up is [RAGMark](https://arxiv.org/abs/2609.05760) (arXiv:2609.05760, Sep 2026), a modular benchmarking framework for advanced RAG on small-scale multi-GPU environments.

### 6. Reasoning — worth skimming

**AgenticRag-R1: Agentic Reinforcement Learning with Stack Memory for Multi-Step Reasoning, Retrieval and Memorizing** — [arXiv:2608.29622](https://arxiv.org/abs/2608.29622) (submitted Sun, 30 Aug 2026)

AgenticRag-R1 applies agentic reinforcement learning with stack memory to multi-step reasoning, retrieval and memorizing, learning robust, interpretable, memory-aware reasoning behaviors via fine-grained action modeling and information-aware optimization for long-horizon reasoning. For the group: RL + memory angle on agentic RAG; code anon. available.

Runner-up theme: safety — the strongest runner-up is [A Survey of Secure RAG](https://arxiv.org/abs/2604.08304) (arXiv:2604.08304), whose memory/summarization components intersect with agentic retention risks.

---

## Recent developments (wider web, Oct 2026)

- "Killing the retrieve-then-generate monolith": the dominant 2025-2026 production shift is merging RAG with agent loops — retrieval exposed as a tool, with the LLM decomposing the prompt, choosing the retriever (vector DB / Neo4j GraphRAG / web API), judging sufficiency, and looping back on gaps.
- GraphRAG is the other big strand: flat vector similarity misses structural/entity relationships; knowledge graphs (often Neo4j) traversed at query time help answer global questions over large corpora.
- Corrective / self-healing RAG: an explicit relevance evaluator triggers noise stripping, fact filtering, or web-search fallback instead of passing bad context to the generator.
- Contextual chunking (Anthropic-style: LLM-prepended chunk summaries) cuts retrieval failure rates roughly ~50%.
- Streaming RAG via CDC (Change Data Capture) keeps embedding indexes fresh without nightly re-indexing.
- Market/industrial: RAG platform market estimated ~USD 4.00B (2025) -> ~USD 5.52B (2026); RAGE-KG 2026 workshop at ISWC Bari; RAG-in-the-wild effectiveness critiques; RAG-vs-agentic security contrast.
- Items the academic angles missed: KG grounding (e.g., SPLIT-RAG with question-driven graph partitioning, ACL EMNLP 2026), deployment effectiveness, and the guardrail-vs-agentic security split.

---

## One-line takeaways

- RAGPerf (2603.10765) — end-to-end RAG benchmarking with negligible overhead; efficiency baseline for cost/quality trade-spaces.
- Q-RAG (2511.07328) — value-based embedder training for multi-step long-context retrieval.
- VLD-RAG (2607.24748) — agent verification + multimodal hybrid retrieval for cross-page visual grounding.
- MLDocRAG (2602.10271) — multimodal long-context document retrieval with consistent gains on MMLongBench-Doc / LongDocURL.
- Survey of Secure RAG (2604.08304) — EMNLP 2026 survey of RAG security risks and defenses.
- AgenticRag-R1 (2608.29622) — agentic RL with stack memory for multi-step reasoning, retrieval and memorizing.
