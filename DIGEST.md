# RAG Reading Group — Literature Scan Digest

**Prepared:** 2026-10-31 (UTC) • **Author:** HeziLiu • **Scope:** recent arXiv preprints on retrieval-augmented generation (roughly Last 30 days: 2026-09-30 → 2026-10-31)

## How the scan was done

Four search angles, each run separately over arXiv and cross-checked against the arXiv API export feed for precise dates and abstracts:

1. **Core RAG methods** — compositionality, chunking, reranking, parallelABER reasoning topico.
2. **Agentic / multi-step retrieval** — ReAct-style loops, when retrieval fails silently.
3. **Long-context vs. retrieval** — does the model preferthe full context or selected evidence?
4. **RAG evaluation / benchmarks** — controlled corruption, ground-truth sensitivity, scale laws.

Six most relevant preprints overall were then assigned to exactly one of four themes — **efficiency, reasoning, multimodality, safety** — using a simple fit grid (primary contribution → closest theme; runner-up theme recorded where a paper arguably fits two). Each paper is flagged **MUST-READ**, **WORTH SKIMMING**, or **BACKGROUND**.

---

## The six preprints

### 1. Efficiency — MUST-READ

- **arXiv:2610.40454** — *Glance: The Generator Is Its Own Reranker* (Metinov & Arziev, cs.CL/cs.IR, 29 Oct 2026)
  Generator-based reranking with one resident 9B backbone: a lightweight decision adapter + pointer head scores candidate passages from a shared prefill, adding ~0.1 GiB per decision skill. On SciFact nDCG@10 = 0.741 and NFCorpus = 0.345, beating bge-reranker-v2-m3 (0.721 / 0.326); on 300 HotpotQA the selected context improves answer F1 by 0.045 over cross-encoder context. Reranking quality keeps rising up to 200 candidates (43k tokens) from one shared prefill, exceeding the cross-encoder by 0.058 nDCG@10. Where a paper arguably fits two themes: **runner-up theme = reasoning** — reranking becomes endogenous decoding-time inference rather than a separate model.

### 2. Reasoning — MUST-READ

- **arXiv:2610.40409** — *Retrieving from Your Own Mistakes: On-Policy Training of Embedding Models for Multi-Hop RAG-Augmented Generation* (Qiu, Zeng, Shi, Chen, Luo, Xu; cs.AI, 29 Oct 2026)
  Chain embedding retrievers that re-encode the question with retrieved passages are already strong, but at test time they condition on their own retrievals: by the third step roughly half or more of visited states hold a wrong passage,淋巴 lowering gold-passage recall beyond state difficulty. The fix is on-policy state training — label each reached state with the earliest still-missing gold passage while masking the others, and update contrastively so the encoder's training distribution follows itself. The retriever then recovers from its own mistakes far more often and transfers without further training to longer-chain HotpotQA and 2WikiMultiHopQA variants. Runner-up theme: **efficiency** (training cheaper than graph-based systems / search agents; related line: *How CoT Reasoning Improves Long-Context Counting*, 2609.38958).

### 3. Multimodality — WORTH SKIMMING

- **arXiv:2610.10183** — *VideoEvolve: Co-Evolving Memory and Retrieval for Long Video Understanding* (Yongchao Xu et al., cs.CV/cs.AI, 7 Oct 2026)
  Starts from a coarse low-frame-rate overview and couples a Memory Evolver (selective memory augmentation) with a Retrieval Evolver (adaptive retrieval over evolving memory), co-evolving them through alternating agentic reinforcement learning, steered by Bottleneck-Aware Evolution Feedback (which side is the bottleneck?) and Capability-Aware Evolution Feedback (avoid over-specializing on training questions). Experiments on long-video understanding benchmarks show the co-evolution helps; fuller detail and numbers are worth a skim pass. Runner-up theme: **reasoning** (downstream reasoning over long-video understanding) / efficiency (cost of co-evolution).

### 4. Safety — MUST-READ

- **arXiv:2610.22297** — *Private Retrieval Augmented Generation via Random Projection* (Yao, Rabbani, Li; cs.AI/cs.CR, 15 Oct 2026)
  Applies the same random projection to both datastore embeddings and query embeddings, provably preserving semantic similarity between queries and retrieved items while substantially mitigating data-extraction attacks. Across multiple RAG architectures and datasets it achieves superior retrieval and generation performance versus methods relying on formal differential privacy, with comparable empirical privacy under strong attack models — the first indication that random projection is a competitive, practical baseline for privacy-preserving RAG. Runner-up theme: **efficiency** (projection overhead is small; the trade-off is privacy rather thanbers).

### 5. Efficiency — WORTH SKIMMING

- **arXiv:2610.05750** — *Beyond Semantic Similarity: Performance and Costs of Agentic Retrieval for Complex Tasks* (Esfandiarpoor et al., cs.IR/cs.AI, 5 Oct 2026)
  Agentic retrieval = LLM reasoning plus efficient corpus exploration in a ReAct loop; nDCG@10 improve by 8.7 points with the same embedding model, and the pipeline is highly generalizable across ViDoRe v3 and BRIGHT. The catch: ~107.4 s per query (vs 0.67 s for standard retrieval) and ~764.1K input / 5.8K output tokens per query — effectiveness clearly not free. Runner-up theme: **reasoning** (agentic loop reasoning) / **multimodality** (ViDoRe videor benchmark).

### 6. Reasoning — BACKGROUND

- **arXiv:2610.31606** — *How Ground Truth Shapes Retrieval Scores: Evidence-Aware Evaluation of a Retrieval-Augmented Generation System for Breast Lesions* (Mochizuki Silva et al., cs.CL/cs.AI, 22 Oct 2026, v2 23 Oct 2026)
  18-document corpus + 18-query development benchmark; hybrid retriever (dense + BM25 + cross-encoder) with 384-token chunks and 20% overlap reaches Recall@3 / R-Precision / MRR@3 / nDCG@3 ≈ 0.94, with cross-encoder reranking scoring highest; expanded relevance annotations increased recognized evidence spans (25→37) and accepted chunk targets (36→51) without changing rankings — retrieval scores are annotation-sensitive. Runner-up theme: **safety** (clinical evidence sufficiency / decision-support accountability).

---

## Scans turned up

Across the four angles plus the arXiv API cross-check and web chatter: **~18 distinct preprints** surfaced; **6 selected** for the digest.

---

## Recent developments (web)

- **The paradigm is merging, not shrinking.** Medium piece "RAG in 2026: Why We Finally Killed the Retrieve-Then-Generate Monolith" frames the biggest 2025–2026 shift as RAG merging into agent loops — we no longer blindly pass a query to a vector store and hope the right chunks come back.
- **Security surveys are appearing.** "A Survey of Secure Retrieval-Augmented Generation" (2026) catalogs RAG's distinct security risks versus training-time LLM risks: prompt-injection detection, model alignment, privacy auditing, and source attribution.
- **Attack taxonomy maturing.** ACM Gould 2026 "Coordinated Prompt-RAG Attacks" notes existing RAG attacks see effectiveness decline and identifies gaps in robustness testing; "Decomposing the Unbounded Prompt Injection Attack Space" (2610.24999) extends the attack vocabulary.
- **Multimodal VLM RAG is active.** Patho-AgenticRAG targets multimodal agentic RAG for pathology VLMs via reinforcement learning; MedGemma is being fine-tuned for clinical captioning with multimodal RAG over Malaysian CPGs.
- **Market rhetoric:** RAG-platform market cited at ~USD 4.00B (2025) → ~USD 5.52B (2026).

**What the chatter mentions that my four angles missed:** (1) the agentic-RAG *merger* as a design-paradigm shift (my angles treated agentic retrieval as an efficiency/reasoning question, not aDirections architecturally); (2) coordinated prompt-RAG attacks as a first-class adversarial category; (3) multimodal medical-VLM agentic RAG as a distinct subfield; (4) the commercial-market growth narrative.

---

## One-line takeaways

1. **Glance (2610.40454)** — one 9B backbone can rerank from a shared prefill at near-zero marginal memory.
2. **On-Policy chain retrievers (2610.40409)** — train on the states you reach, including your own mistakes.
3. **VideoEvolve (2610.10183)** — co-evolve memory and retrieval with alternating agentic RL for long video.
4. **Private RAG via random projection (2610.22297)** — random projection preserves相似ity while mitigating extraction attacks, competitive with DP.
5. **Agentic retrieval costs (2610.05750)** — +8.7 nDCG@10 but ~107 s and 764K tokens per query.
6. **Ground-truth sensitivity (2610.31606)** — bigger relevance annotation sets change nothing in rankings — annotation design is the lever.
