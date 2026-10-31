# RAG Reading Group — Literature Scan Digest (2026-10-31)

- **Date:** 2026-10-31
- **Scope:** Recent arXiv preprints on retrieval-augmented generation, scanned from **seven angles**: (1) core RAG methods, (2) agentic / multi-step retrieval, (3) long-context vs. retrieval, (4) RAG evaluation / benchmarks, (5) RAG efficiency (cost, compression, indexing), (6) multimodal RAG, (7) safety.
- **Volume:** the scans returned **~27 unique preprints** (after de-duplication across seven angles plus arXiv-API lookups); from those I selected **six**, placing each in exactly one of four themes: **efficiency, reasoning, multimodality, safety**.
- **Convention:** every paper is flagged **must-read** (a few sentences drawn from its arXiv page), **worth skimming** (one-liner), or **background** (one-liner). Each flag carries a named *runner-up* theme (with its arXiv ID) where the paper arguably spans two themes.

---

## How the theme assignment worked

1. **Primary-axis test.** For each candidate I extracted the paper's *primary question* — the problem it changes — not its application area or model choice. Medical/legal/financial/scientific corpora and particular models were treated as evidence only.
2. **Grid mapping.** Efficiency = new trade-offs in compute, latency, token cost, index size or memory; reasoning = retrieval interleaved with multi-step thought; multimodality = grounding text answers in images, visuals or vision-language models; safety = attacks, guardrails and secure-deployment properties of the retrieval path.
3. **Exhaustive and mutually exclusive.** Each paper is placed in exactly one row of the grid below; the grid is the whole candidate set, so nothing is double-counted.
4. **Runner-up management.** Where a paper arguably answers two questions, I named a *runner-up* theme (with its arXiv ID) and still assigned it to one theme. Runner-up notes appear inline with each pick.
5. **Selection filter.** Recency (favouring October 2026, then 2025–2026), arXiv-verified titles / IDs / dates from the abstract pages, and best representative per scan angle. Papers whose primary axis was evaluation tooling or another dimension were excluded from the six even when they ranked high within an angle.

---

## Theme grid

| Theme | Picks |
|---|---|
| **Efficiency** | Glance: The Generator Is Its Own Reranker (must-read); Is Agentic RAG worth it? (worth skimming) |
| **Reasoning** | LLM-guided Hierarchical Search for End-to-end Reasoning Intensive Retrieval / LATTICE (must-read); SoK: Agentic Retrieval-Augmented Generation (background) |
| **Multimodality** | GARRET: Generative Feedback for Region Retrieval in Visual Documents (must-read) |
| **Safety** | A Survey of Secure Retrieval-Augmented Generation (must-read) |

---

## The scans (angle → best 2–3 of the hits)

1. **Core RAG methods** — RAG for LLM Efficiency (2402.19473), RAG for AI Agents (2501.09136), RAG for Knowledge-Intensive NLP (2005.11401), A Survey of Multimodal RAG (2504.08748).
2. **Agentic / multi-step retrieval** — SoK: Agentic RAG (2603.07379), Agentic RAG: Architectures, Controls and Real Costs, Is Agentic RAG worth it? (2601.07711).
3. **Long-context vs. retrieval** — Long-Context LLMs Meet RAG (2410.05983), Long Context RAG Performance (2411.03538), Long Context vs. RAG for LLMs (2501.01880), Agri-Query: RAG vs. Long-Context LLMs (2508.18093).
4. **Evaluation / benchmarks** — RAGBench (2407.11005), Benchmarking RAG for Medicine / MIRAGE (2402.13178), RGB (2309.01431), A RAG Evaluation Framework (2605.27445), Evaluating RAG (2605.14488).
5. **Efficiency** — Glance: The Generator Is Its Own Reranker (2610.40454), Decompose Estimate Select: Coverage-Aware Context Construction for Long-Form RAG (2610.40314), Retrieving from Your Own Mistakes: On-Policy Training of Embedding Models for Multi-Hop RAG (2610.40409), Is Agentic RAG worth it? (2601.07711).
6. **Multimodal RAG** — GARRET: Generative Feedback for Region Retrieval in Visual Documents (2610.27829), A Survey of Multimodal RAG (2504.08748), Ask in Any Modality (2502.08826), Multi-RAG (2505.23990).
7. **Safety** — A Survey of Secure RAG (2604.08304), RAG Safety: Exploring Knowledge Poisoning Attacks (2507.08862), RAG LLMs are Not Safer (2504.18041), Knowledge Poisoning Attack on RAG (2505.11548).

---

## The six picks

### 1. Efficiency — **must-read**

**Glance: The Generator Is Its Own Reranker** — [arXiv:2610.40454](https://arxiv.org/abs/2610.40454) (submitted Thu, 29 Oct 2026; authors Adilet Metinov, Chingiz Arziev; cs.CL/cs.IR).

RAG traditionally serves separate models for reranking and answering, duplicating model residency and passage processing. Glance equips the generator with a lightweight decision adapter and pointer head to score candidate passages from a shared prefill: short relevance probes branch from the cached context, producing one score per passage without separately prefilling each query-passage pair. A single resident 9B backbone supports generation, general decisions and reranking, with roughly 0.1 GiB of additional memory per decision skill. After 39 minutes of MS MARCO fine-tuning it reaches nDCG@10 of 0.741 on SciFact and 0.345 on NFCorpus versus 0.721 and 0.326 for bge-reranker-v2-m3; on 300 HotpotQA questions its selected context improves answer F1 by 0.045 over cross-encoder-selected context under the same base generator (paired bootstrap 95% CI [0.014, 0.076]). A scaling study shows reranking quality keeps rising up to 200 candidates (43k tokens) scored from one shared prefill, exceeding the cross-encoder by 0.058 nDCG@10. For the group: reranking need not be a separate model — this is the efficiency argument in its purest modern form.

*Runner-up theme: long-context vs. retrieval as a competitive paradigm* (the angle it came from) — strongest runner-up paper is [Decompose, Estimate, Select: Coverage-Aware Context Construction for Long-Form RAG](https://arxiv.org/abs/2610.40314) (arXiv:2610.40314, Oct 2026), which targets answer completeness rather than reranking quality.

### 2. Efficiency — **worth skimming**

**Is Agentic RAG worth it? An experimental comparison of RAG approaches** — [arXiv:2601.07711](https://arxiv.org/abs/2601.07711) (submitted Mon, 12 Jan 2026; v2 20 Apr 2026; authors Pietro Ferrazzi et al.; cs.CL; accepted at ACL 2026 Industry Track).

An experimental cost/performance comparison of agentic versus naive RAG; the results offer practical guidance on selecting the most effective RAG design for real-world applications considering both performance and tokens/costs. Worth skimming for the efficiency angle's cost side; the reasoning-side companion is [LLM-guided Hierarchical Search for End-to-end Reasoning Intensive Retrieval](https://arxiv.org/abs/2510.13217) (arXiv:2510.13217).

### 3. Reasoning — **must-read**

**LLM-guided Hierarchical Search for End-to-end Reasoning Intensive Retrieval (LATTICE / LATTICE++)** — [arXiv:2510.13217](https://arxiv.org/abs/2510.13217) (submitted Wed, 15 Oct 2025; v2 Mon, 25 May 2026; authors Nilesh Gupta et al.; cs.IR/cs.LG).

This paper explores LLM-guided hierarchical search in which an LLM interacts with the corpus directly via search, rather than treating retrieval as a one-shot chunk fetch. With a single off-the-shelf LLM, base LATTICE reaches 46.7 nDCG@10 on the reasoning-intensive BRIGHT benchmark — matching the best fine-tuned ensemble baseline overall — and a lightweight ensemble LATTICE++ that fuses LATTICE with cheap retrieval reaches 49.1 nDCG@10. A controlled same-LLM comparison against sliding-window reranking shows reranking offers a better tradeoff at low token budgets, but LATTICE converges to a higher asymptote after a moderate budget; it also works with open-weight LLMs and remains competitive on traditional IR benchmarks (NQ, SciFact, SciDocs). For the group: the model searches its own reasoning structure, which is exactly the reasoning-theme story the raw retrieval misses.

*Runner-up theme: efficiency* — reranking tradeoff at low token budgets; runner-up paper [Is Agentic RAG worth it?](https://arxiv.org/abs/2601.07711) (arXiv:2601.07711).

### 4. Reasoning — **background**

**SoK: Agentic Retrieval-Augmented Generation (RAG): Taxonomy, Architectures, Evaluation, and Research Directions** — [arXiv:2603.07379](https://arxiv.org/abs/2603.07379) (2026; authors S. Mishra et al.).

The first unified framework treating agentic RAG as a sequential decision-making system; it traces architectures by agent cardinality, control and memory, plus evaluation methodologies and unresolved reliability risks. Useful orienting background before deeper dives; the efficiency runner-up paper is [Is Agentic RAG worth it?](https://arxiv.org/abs/2601.07711) (arXiv:2601.07711) and the multimodal runner-up is [GARRET](https://arxiv.org/abs/2610.27829) (arXiv:2610.27829).

### 5. Multimodality — **must-read**

**GARRET: Generative Feedback for Region Retrieval in Visual Documents** — [arXiv:2610.27829](https://arxiv.org/abs/2610.27829) (updated 20 Oct 2026; authors Weijian Jian, Siyang Chen, Yuguang Yang et al.; cs.CV/cs.IR).

Multimodal RAG over visually rich documents needs evidence at finer granularity than entire pages; training region-level retrievers usually needs costly query-to-region annotations or noisy model-generated labels. GARRET introduces a region-retrieval framework trained from (page, question, answer) triplets through differentiable generative feedback: a shared context-preserving retriever produces page and region multi-vector representations, retrieval scores define a soft routing distribution over candidate region crops, an auxiliary vision-language model attends to each crop separately and aggregates crop contexts using routing weights, and gradients through the routing distribution assign query-conditioned credit to indexed region representations without query-to-region annotations; the auxiliary model is removed at inference. It introduces ViDoRe-V3-Region, a corpus-wide benchmark of 200,682 fixed candidate regions across eight domains; GARRET reaches macro nDCG@10 of 0.4126, outperforming the strongest visual baseline by 2.94 points, while indexing 47.8% fewer vectors per page than ColQwen2.5-v0.2. For the group: region-level grounding is where multimodal RAG is actually getting its harder retrieval problems.

*Runner-up theme: agentic retrieval* (an auxiliary model attends crops and aggregates them — a light retrieval agent); runner-up paper [SoK: Agentic RAG](https://arxiv.org/abs/2603.07379) (arXiv:2603.07379). Efficiency runner-up: [47.8% fewer vectors indexed per page](https://arxiv.org/abs/2610.27829) (arXiv:2610.27829).

### 6. Safety — **must-read**

**A Survey of Secure Retrieval-Augmented Generation** — [arXiv:2604.08304](https://arxiv.org/abs/2604.08304) (submitted Thu, 9 Apr 2026; v5 Mon, 12 Oct 2026; authors Haoyang Li et al.; cs.CR/cs.AI; accepted at EMNLP 2026).

RAG improves LLMs with external knowledge, but this access path creates security risks distinct from standard LLM deployment: poisoning and manipulation of retrieved evidence, leakage of retrieved content and logs, cross-tenant and multi-user threats in shared indexes, and the tension between retrieval completeness and exposure. The survey systematizes these risks against secure-deployment boundaries (keeping embeddings, indexes and logs inside the boundary) and connects them to agentic RAG reliability questions. Web chatter echoes this from the vendor side: single-document knowledge-poisoning attacks, RAGForensics-style traceback tooling, CPA-RAG covert poisoning, and enterprise guides on private-RAG data-leakage prevention. For the group: if your RAG answers are auditable, this is the frame for why "retrieval quality" and "retrieval safety" cannot be separated.

*Runner-up theme: evaluation* — the survey's defenses are evaluated largely via benchmarks; runner-up papers [A RAG Evaluation Framework](https://arxiv.org/abs/2605.27445) (arXiv:2605.27445) and [Evaluating RAG](https://arxiv.org/abs/2605.14488) (arXiv:2605.14488). Attack runner-up: [RAG Safety: Exploring Knowledge Poisoning Attacks](https://arxiv.org/abs/2507.08862) (arXiv:2507.08862).

---

## Recent developments

The wider web in October 2026 keeps converging on a few themes that the academic scans above partly miss:

- **Agentic RAG is merging with agent loops.** The dominant narrative is that the "retrieve-then-generate" monolith is being replaced by agentic loops where the model decides when to search, which tools to call, and when to re-check context — RAG is increasingly treated as one tool inside an agent rather than the whole pipeline.
- **RAG vs. long-context remains unresolved and contested.** Practitioner chatter repeatedly notes that agentic RAG puts the model in charge of retrieval rather than treating chunks as fixed, and that long-context recall behavior is environment-dependent — the theoretical "RAG always wins with enough context" story is fading in production discussions.
- **Security is the loudest operational theme.** Single-document knowledge-poisoning attacks, RAGForensics traceback, CPA-RAG covert poisoning, and enterprise private-RAG guides on document-level access controls and leakage prevention are all trending; the survey above (2604.08304) is the academic counterpart.
- **Cost and real-world overhead are finally first-class concerns.** Beyond token cost, there is chatter about agentic-RAG latency, retry loops and "architectures, controls and real costs" — efficiency is shifting from index compression to end-to-end overhead.
- **The market is scaling fast:** the global RAG platforms market was valued ~USD 4.00B in 2025 and estimated ~USD 5.52B in 2026.

Notable things the wider chatter mentions that my academic angles missed: (1) **operational cost and latency profile of agentic RAG** as a management problem, not just a metric; (2) **private-RAG data security and governance** (access controls, cross-tenant isolation) as a deployment requirement; (3) **enterprise adoption scale and vendor guidance** (platform market growth, CISO-style RAG security checklists) — my scan was preprint-focused, so adoption-scale and ops framing are the externalities the group may want to flag separately.

---

## One-line takeaways

- **Efficiency:** Glance (2610.40454) shows one 9B backbone can do generation, decisions and reranking from a shared prefill — reranking need not be a second model.
- **Reasoning:** LATTICE (2510.13217) lets an off-the-shelf LLM search hierarchically and match fine-tuned ensembles on reasoning-intensive benchmarks.
- **Multimodality:** GARRET (2610.27829) retrieves by image region from (page, question, answer) triplets, beating visual baselines while indexing 47.8% fewer vectors per page.
- **Safety:** The Secure RAG survey (2604.08304) frames retrieval-path risks as distinct from standard LLM risks and maps them to secure-deployment boundaries.
- **Overarching:** the current conversation is agentic RAG inside agent loops, with safety and real cost rising alongside retrieval quality.
