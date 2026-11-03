# RAG Reading Group — Literature Scan Digest (2026-11-03)

- **Date:** 2026-11-03
- **Scope:** Recent arXiv preprints on retrieval-augmented generation, scanned from seven angles: (1) core RAG methods, (2) agentic / multi-step retrieval, (3) long-context vs. retrieval, (4) RAG evaluation / benchmarks, (5) efficiency (cost, token budget, latency), (6) multimodal RAG, (7) safety / security.
- **Volume:** the scans returned ~45 raw hits across the seven angles; after de-duplication ~35 unique preprints. From those I selected six, placing each in exactly one of four themes: efficiency, reasoning, multimodality, safety.
- **Convention:** every paper is flagged must-read (a few sentences drawn from its arXiv page), worth skimming (one-liner), or background (one-liner). Each flag carries a named runner-up theme (with arXiv ID) where the paper arguably spans two themes.

---

## How the theme assignment worked

1. Primary-axis test: for each candidate I extracted the paper's primary question — the problem it changes — not its application area. Domain (medical, legal, video, etc.) or model choice was treated as evidence only.
2. Grid mapping: Efficiency = new trade-offs in compute, latency, token cost, index size or memory; reasoning = retrieval interleaved with multi-step thought / search; multimodality = grounding answers in images, visuals or vision-language models; safety = attacks, guardrails, and secure-deployment properties of the retrieval path.
3. Exhaustive and mutually exclusive: each paper is placed in exactly one row; the grid below is the whole candidate set, so nothing is double-counted.
4. Runner-up management: where a paper arguably answers two questions, I named a runner-up theme (with its arXiv ID) and still assigned it to one theme. Runner-up notes appear inline with each pick.
5. Selection filter: recency (October 2026 window), arXiv-verified titles / IDs / dates from the abstract pages, and best representative per scan angle. Papers whose primary axis was evaluation tooling or another dimension were excluded from the six even when they ranked high within an angle.

---

## Theme grid

| Theme | Picks |
|---|---|
| Efficiency | When Is Additional Retrieval Worthwhile? (must-read), SpectRAG (worth skimming) |
| Reasoning | Frustratingly Easy Agentic RAG via Portable Skills (must-read), Beyond Retrieval Failure (worth skimming) |
| Multimodality | EC-RAG: Event Chain RAG for Long Video Understanding (must-read) |
| Safety | Prevented is Not Protected: What Attack Success Rate Hides about RAG (must-read) |

---

## The scans (angle -> best 2-3 of the hits)

1. Core RAG methods: Retrieval Augmented Generation Compositionality (2610.29722), Private RAG via Random (2610.22297), MAPS: Macro-Adaptive Parallel Reasoning (2610.29792), When Is Additional Retrieval Worthwhile (2610.37358)
2. Agentic / multi-step retrieval: Frustratingly Easy Agentic RAG via Portable Skills (2610.14428), RouteDRAG (2610.36444), Understanding Why LLMs Miss Evidence in Multi-Hop RAG (2610.21184), Agentic AutoRAG (2610.08452)
3. Long-context vs. retrieval: Unifying Retrieval and Long-Context with a Single Model (2610.08463), From Long Context to Selective Memory (2610.21165), Rethinking Retrieval in the Long-Context Era (2610.34146), Coverage-Aware Context Construction (2610.40314)
4. Evaluation / benchmarks: RAGStress (2610.04691), RAG-PIBench (2610.08571), What Attack Success Rate Hides about RAG (2610.40742), Better Retrievers Worse Labels (2610.40966), How Ground Truth Shapes Retrieval Scores (2610.31606)
5. Efficiency: When Is Additional Retrieval Worthwhile (2610.37358), SpectRAG token-budgeted context selection (2610.36991), LURE-RAG lightweight reranking (2601.19535)
6. Multimodal RAG: EC-RAG event-chain for long video (2610.08674), MG2-RAG multi-granularity graph (2604.04969), Scaling Beyond Context: A Survey of Multimodal Retrieval (2510.15253)
7. Safety: Prevented is Not Protected (2610.40742), RAG-PIBench (2610.08571), A Survey of Secure RAG (2604.08304), Stealth Poisoning Attacks on Multimodal RAG (2603.00172)

---

## The six picks

### 1. Efficiency — must-read

When Is Additional Retrieval Worthwhile? A Cost-Aware Study of Evidence Gain and Answer Reliability in RAG — arXiv:2610.37358 (submitted Tue, 27 Oct 2026).

A cost-aware two-action retrieval policy that chooses between a dense-retrieval-plus-reranking baseline and a hybrid lexical-dense retriever, estimating the question-specific incremental evidence benefit from features available before the routing decision. On 60 unseen QASPER articles (188 questions, 169 evidence-evaluable) the policy triggers hybrid retrieval on 46 questions (24.5%) and matches always-hybrid evidence Hit@10 (78.70% vs 76.92% for always-keep); paired bootstrap intervals do not establish a reliable utility advantage, and 4-bit Qwen3-4B answer-level assessments show no clear correctness/faithfulness improvement despite the evidence gain. The takeaway: retrieving relevant evidence efficiently is not the same as improving reliable answer quality — a reproducible empirical study with document-grouped cross-validation frozen before held-out evaluation.

Runner-up theme: reasoning / answer reliability (it expressly distinguishes evidence-retrieval gain from answer reliability); runner-up angle best pick is Beyond Retrieval Failure (arXiv:2610.21184), which quantifies how much apparent retrieval failure is search drift vs. genuine un-retrievability.

### 2. Efficiency — worth skimming

SpectRAG: Weighted Chunk Graphs for Token-Budgeted Context Selection in Multi-Hop Retrieval-Augmented Generation — arXiv:2610.36991 (submitted Tue, 27 Oct 2026, v3 30 Oct 2026).

Spectral graph-augmented retrieval combining hybrid candidate seeding, weighted chunk graph construction, graph-based expansion, spectral relevance propagation, and token-budgeted context selection. Experiments on MultiHopRAG, UltraDomain and long-document QA show improved broad evidence recovery and competitive generation quality vs. dense, hybrid, HyDE, LightRAG and NaiveRAG baselines; graph-spectral structure is especially useful for inference-oriented and cross-document retrieval, with trade-offs in early precision, compute cost and domain-dependent performance. 26 pages, 5 figures, 10 tables; intended for an IEEE journal.

Runner-up theme: reasoning (multi-hop); runner-up angle best pick is RouteDRAG (arXiv:2610.36444, 28 Oct 2026), which learns to route and control agentic retrieval.

### 3. Reasoning — must-read

Frustratingly Easy Agentic RAG via Portable Skills: A Case Study in Customer Support — arXiv:2610.14428 (submitted Sat, 10 Oct 2026; accepted EMNLP 2026 Industry Track).

A deployment case study of a portable skill: a natural-language instruction, lightweight tools (retrieval API, format-checking scripts) and a corpus enriched with an LLM-generated Wikipedia-style navigation layer. It performs strongly on challenging customer-support resolution workflow generation, achieving 99.2% procedural equivalence to human-approved ground truth and 83.3% evidence sufficiency, but is roughly an order of magnitude slower per case than the deployed production assistant (~90 s vs ~8-9 s). Claim is scoped to that setting: mature curated corpus, latency-tolerant workflow, human review of every case.

Runner-up theme: efficiency (deployment cost/latency); runner-up angle best pick is When Is Additional Retrieval Worthwhile (arXiv:2610.37358) for the cost-aware routing angle.

### 4. Reasoning — worth skimming

Beyond Retrieval Failure: Understanding Why LLMs Miss Evidence in Multi-Hop RAG — arXiv:2610.21184 (submitted Thu, 15 Oct 2026; accepted DAI 2026 Oral).

ExecutionRAG, a training-free requirement register that records open sub-questions and supporting evidence, changing search guidance but not evidence access, so each recovered gold passage certifies that it was reachable by the original retriever. On 1,000 MuSiQue questions, wrong answers with unretrieved required evidence fall from 382 to 234 (all-MiniLM-L6-v2) and 383 to 274 (Qwen3-Embedding-0.6B), i.e. 69% to 44% and 66% to 48% of each system's wrong answers; evidence recovery does not proportionally reduce total error since premature resolutions and abstentions increase. Central finding: the bottleneck shifts from guiding search toward required evidence to verifying that the retrieved evidence is sufficient.

Runner-up theme: evaluation; runner-up angle best pick is RAGStress (arXiv:2610.04691) for controlled KB-corruption testing.

### 5. Multimodality — must-read

EC-RAG: Event Chain Retrieval-Augmented Generation for Long Video Understanding — arXiv:2610.08674 (submitted Tue, 6 Oct 2026).

Event-centric RAG for long video: frames are usually processed independently, losing temporal event structure; EC-RAG organizes video content into explicit event chains, with structured multi-modal fusion aggregating speech, text and visual cues at the event level, plug-and-play compatible with existing LVLM backbones (no additional training, no proprietary models). On Video-MME, MLVU and LongVideoBench the event-centric design consistently outperforms frame-level retrieval baselines, highlighting the importance of modeling temporal structure for long-video understanding. 12 pages, 7 figures, 7 tables.

Runner-up theme: efficiency (long-video retrieval at scale); runner-up angle best pick is Librarian Agents (arXiv:2610.22273) for training LLMs to curate long-context references.

### 6. Safety — must-read

Prevented is Not Protected: What Attack Success Rate Hides about RAG — arXiv:2610.40742 (submitted Thu, 29 Oct 2026).

Existing RAG poisoning defenses are primarily evaluated with attack success rate (ASR), which obscures defense-induced failures and the mechanisms behind apparent attack prevention. The paper introduces Aligned RAG Evaluation, a matched-query protocol jointly examining clean and poisoned responses with and without defense, combining matched-conditions analysis, LLM-judge endorsement and retrieval-dependence controls to distinguish prevented from introduced failures, target mentions from LLM-judge endorsement, and single-passage influence from evidence composition. Experiments on HotpotQA and Natural Questions reveal that existing defenses can introduce unexpected target-positive answers (while preventing some attacks), and evaluation criteria can also change defense rankings; code and evaluation artifact available.

Runner-up theme: evaluation; runner-up angle best pick is RAG-PIBench (arXiv:2610.08571) for leakage-aware prompt-injection detection in RAG-contextual inputs.

---

## Recent developments

- Market and adoption: the global RAG platforms market was valued at about USD 4.00 B in 2025 and is estimated at about USD 5.52 B in 2026; agentic RAG solutions are projected to surge at about 35.1% CAGR through 2032 (Oct 2026 trade press).
- TREC RAG Track 2026 is launching as a large-scale, community-driven benchmark for agentic retrieval, multi-hop reasoning and retrieval-augmented generation — directly relevant to the agentic RAG and evaluation angles.
- LongEval at CLEF 2026 results show that the highest retrieval capabilities in a RAG system do not necessarily lead to the best end-to-end performance, echoing the evidence recovery vs. answer reliability finding in 2610.37358.
- Security chatter: OWASP LLM Top 10 (2025/2026) repeatedly flags RAG-specific risks — poisoning of indexed content, weak tenant isolation in vector stores, embedding inversion and cross-tenant leakage; coordinated prompt-RAG attacks and practical poisoning attacks (SACMAT '26) are actively studied. This matches pick #6 (arXiv:2610.40742).
- Notable misses vs. my angles: the wider web emphasizes enterprise deployment narratives (portable skills, RAG-as-a-service) and market growth rather than new retrieval algorithms; the ASQ dataset (about 1M agentic multi-step search traces) and How AI agents search work surface agentic-search evaluation that my scans touched but did not center; knowledge-graph-augmented RAG (KAG-style) also appears frequently in industry comparisons (RAG vs KAG vs CAG), which my safety/eval angles did not deeply cover.

---

## One-line takeaways

- When Is Additional Retrieval Worthwhile (2610.37358): extra retrieval often buys evidence, not correct answers — route cheaply, do not assume hybrid wins.
- SpectRAG (2610.36991): graph spectral context selection with token budgets beats flat ranking for multi-hop evidence recovery.
- Portable Skills (2610.14428): simple, portable agentic RAG can match human procedure quality at about 90 s/case — latency, not accuracy, is the limit.
- Beyond Retrieval Failure (2610.21184): recover evidence without proportionally cutting errors; verify sufficiency, not just recall.
- EC-RAG (2610.08674): event chains, not frames, are the right unit for long-video grounding.
- Prevented is Not Protected (2610.40742): ASR hides introduced failures — use matched-query evaluation for RAG poisoning defenses.
