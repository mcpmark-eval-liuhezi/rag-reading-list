# RAG Reading-Group Digest — Literature Scan (arXiv, 2026)

**Prepared for:** reading group on retrieval-augmented generation
**Scan window:** preprints posted 2025–2026 (current date 2026-10-31)
**Scan angles:** core RAG methods • agentic / multi-step retrieval • long-context vs. retrieval • RAG evaluation & benchmarks • multimodality • safety

---

## 1. How the scan was run and how themes were assigned

Six arXiv searches were run, one per angle (distinct preprints; 18 in total across the angles; overlap removed). From that pool the **six most relevant preprints overall** were chosen, then assigned to exactly one of the four themes — **efficiency, reasoning, multimodality, safety** — using a strict priority rule:

1. **Efficiency** first (cost / FLOPs / time-to-first-token, retriever-reranker compression, parameter-efficient unification).
2. **Reasoning** next (multi-hop reasoning chains, agentic deliberation, benchmark diagnostics of step allocation).
3. **Multimodality** then (text plus image / audio / video retrieval and generation).
4. **Safety** last (attack / defense, knowledge poisoning, and safety measurement of retrieved output).

Where a paper arguably fits two themes, the runner-up theme is noted in italics. The theme assignment is a forced one-theme归位 to keep the list balanced; every paper's primary contribution drove the placement.

## 2. The six papers

### Efficiency
** Must-read — UNREAL: Unifying Retrieval and Long-Context with a Single Model**
`arXiv:2610.08463` · posted 6 Oct 2026 (cs.CL; cs.IR; cs.LG)
Model-native evidence selection that spans corpus retrieval and long-context inference: chunks are encoded and retrieval queries are derived directly from the frozen LLM's internal representations, adding fewer than 500K trainable parameters while leaving the backbone unchanged. On a 3B-token / 21M-chunk Wikipedia index all four dense and hybrid backbones outperform SOTA retriever-reranker systems, raising recall from 49.1%→73.2% on HotpotQA, 31.7%→60.1% on 2WikiMultiHopQA, and 8.8%→14.4% on MuSiQue; the same selection mechanism lifts NoLiMa accuracy from 1.0% to 24.83% at 128K tokens and LV-Eval F1 from 49.97% to 54.66% at 256K, while cutting FLOPs and time-to-first-token versus full-context inference from roughly 32K tokens onward. Runner-up theme: **reasoning** (evidence selection across scales is itself a form of restricted reasoning).

### Reasoning
** Worth skimming — AgenticRAGTracer: A Hop-Aware Benchmark for Diagnosing Multi-Step Retrieval Reasoning in Agentic RAG**
`arXiv:2602.19127` · posted 22 Feb 2026 (v2 2 Jul 2026; cs.CL)
First Agentic RAG benchmark primarily auto-constructed by LLMs with step-by-step hop-level validation: 1,305 data points, no overlap with mainstream benchmarks. Even GPT-5 reaches only 22.6% EM on the hardest portion; hop-aware diagnosis shows failures come from distorted reasoning chains that collapse prematurely or wander into over-extension — i.e., an inability to allocate steps consistent with task logic. Runner-up theme: **evaluation** (the benchmark itself is an evaluation contribution).

** Background — Agentic Retrieval-Augmented Generation: A Survey on Agentic RAG**
`arXiv:2501.09136` · posted 15 Jan 2025 (v4 1 Apr 2026; cs.AI; cs.CL; cs.IR)
Analytical survey with a principled taxonomy of Agentic RAG architectures by agent cardinality, control structure, autonomy, and knowledge representation; covers applications in healthcare, finance, education, and enterprise document processing, and closes with open challenges in evaluation, coordination, memory management, efficiency, and governance. Useful orientation, not a deep read. Runner-up theme: **efficiency** (the survey explicitly weighs efficiency trade-offs across frameworks).

### Multimodality
** Must-read — Multi-RAG: A Multimodal Retrieval-Augmented Generation System for Adaptive Video Understanding**
`arXiv:2505.23990` · posted 29 May 2025 (v2 14 Jun 2025; cs.AI)
Multimodal RAG integrating and reasoning over video, audio, and text to reduce cognitive load in dynamic, information-rich human-assistance scenarios; benchmarked on MMBench-Video and reports superior performance over open-source Video-LLMs and LVLMs while using fewer resources and less input data, positioning multimodal understanding as a foundation for adaptive human-robot assistance. Runner-up theme: **efficiency** (the paper's own claim is resource efficiency alongside multimodal gains).

** Background — A Survey of Multimodal Retrieval-Augmented Generation**
`arXiv:2504.08748` · posted 26 Mar 2025 (cs.IR; cs.AI; cs.CL; cs.LG)
Reviews MRAG components, datasets, evaluation methods, and limitations, arguing that grounding responses in factual multimodal knowledge reduces hallucinations and outperforms text-only RAG where visual and textual understanding both matter. Useful as orientation rather than a new method. Runner-up theme: **evaluation** (the survey catalogues evaluation methods for MRAG).

### Safety
** Must-read — RAG-Safety-Bench: Reliable Evaluation of Retrieval-Augmented LLM Safety**
`arXiv:2609.11758` · posted 10 Sep 2026 (cs.CL; cs.IR; proceedings of EMNLP 2026 main conference)
Introduced a benchmark that removes the confounding effect of retriever quality and cleanly separates four conditions — non-RAG; RAG with an oracle document containing the answer; RAG with related-but-non-answer documents; RAG with random safe documents — across five open-source LLMs. It reports an inverse relationship between benign and unsafe capability, strong evidence that baseline safety guardrails do not yield downstream safety guarantees once retrieval is enabled, and model-specific support for the finding that even benign documents can drive unsafe generation. Runner-up theme: **evaluation** (itself an evaluation benchmark for safety).

## 3. One-line takeaways

- **Efficiency:** A single model-native evidence-selection mechanism can do the job of both a retriever-reranker and a long-context attention mask, raising recall and distractor removal at a fraction of the FLOPs (`2610.08463`).
- **Reasoning:** Even the best LLMs fail multi-step agentic retrieval at the hop level — premature collapse or over-extension — and auto-constructed hop-aware diagnostics expose it (`2602.19127`).
- **Reasoning (survey):** Agentic RAG is now a taxonomy problem more than a retrieval problem; coordination, memory, and governance are the open frontiers (`2501.09136`).
- **Multimodality:** Video/audio/text RAG beats Video-LLMs on MMBench-Video with fewer resources, showing multimodal grounding helps wherever vision and language jointly determine the answer (`2505.23990`).
- **Multimodality (survey):** MRAG components, datasets, and evaluation recipes are mature enough to survey; the remaining gap is unified evaluation across modalities (`2504.08748`).
- **Safety:** RAG's retrieval step actively trades benign capability for unsafe outputs, and vanilla guardrails do not save you; clean experimental design (oracle vs. related vs. random docs) is what isolates the effect (`2609.11758`).

## 4. Recent developments (wider web, last month)

- **Market momentum:** the global RAG-platforms market was valued at ~USD 4.00B in 2025 and is estimated at ~USD 5.52B in 2026 (Yahoo Finance, 30 Oct 2026).
- **"Killing the retrieve-then-generate monolith":** mainstream commentary argues that wiring a static vector DB directly into a generator is legacy software; 2026 framing is an ecosystem of specialized patterns for different workloads (Medium, Noumannawaz, 2026).
- **RAGE-KG 2026 workshop at ISWC, Bari (26 Oct 2026):** 22 research presentations on RAG + knowledge graphs, keynote by Filip Ilievski — the KG-grounding trend my angle scan under-weighted.
- **Enterprise positioning:** HCLTech frames the future as Agentic RAG plus multi-modal retrieval for grounded, auditable enterprise answers (8 Oct 2026).
- **RAG vs. agentic AI security:** a contrast piece notes RAG grounds answers via retrieval while agentic AI plans and executes multi-step tool use — each with distinct security risk profiles (15 Oct 2026).
- **Effectiveness critique:** *RAG in the Wild: On the (In)effectiveness of LLMs with RAG* (Xu et al. 2026, cited by 7) questions whether retrieval genuinely helps in realistic settings.
- **Tooling normalize:** "13 RAG tools for 2026" splits frameworks, managed services, and search infrastructure with real pricing for a 50k-page workload (2 Oct 2026).

## 5. Notable chatter items my angles missed

1. **Knowledge-graph grounding (RAGE-KG / "Enhancing RAG with Knowledge Graphs"):** KG-enhanced RAG was a live workshop track with rich blog coverage; my scans touched RAG+KG only indirectly.
2. **The "RAG in the Wild" effectiveness critique:** the field is splitting between benchmark gains and deployment reality — worth a dedicated session.
3. **Guardrail-vs-agentic security contrast:** the web is separating RAG's retrieval-amplification risk from agentic tool-use risk as distinct engineering problems; my safety angle covered poisoning but not this RAG/agentic security split.

## 6. Scan inventory

- **Distinct preprints turned up across the six angle searches: 18** (overlap removed; 2026-heavy: `2610.08463`, `2609.11758`, `2602.19127`, `2501.09136`; 2025: `2505.23990`, `2504.08748`; earlier classics retained for context: `2005.11401`, `2312.10997`, `2402.19473`).
- **Selected for the digest: 6** (3 must-reads, 1 worth-skimming, 2 background).
