# RAG Reading Group — Weekly Literature Scan (2026-10-25)

- **Date:** 2026-10-25
- **Scope:** Recent arXiv preprints on retrieval-augmented generation, scanned from **seven angles**: (1) core RAG methods, (2) agentic / multi-step retrieval, (3) long-context vs. retrieval, (4) RAG evaluation / benchmarks, (5) RAG efficiency (cost, compression, indexing), (6) multimodal RAG, (7) safety.
- **Volume:** the scans returned about **70 raw hits** (seven angles × up to ten each), which after de-duplication came down to **~55 unique preprints**. From those I selected **six**, placing each in exactly one of four themes: **efficiency, reasoning, multimodality, safety**.
- **Convention:** every paper is flagged **must-read** (a few sentences drawn from its arXiv page), **worth skimming** (one-liner), or **background** (one-liner). Each flag carries a named *runner-up* theme (with its arXiv ID) where the paper arguably spans two themes.

---

## How the theme assignment worked

1. **Primary-axis test.** For each candidate I extracted the paper's *primary question* — the problem it changes — not its application area. Where a paper runs on medical, legal, financial or scientific text, or uses a particular model, that was treated as evidence only.
2. **Grid mapping.** Efficiency = new trade-offs in compute, latency, token cost, index size or memory; reasoning = retrieval interleaved with multi-step thought; multimodality = grounding text answers in images, visuals or vision-language models; safety = attacks, guardrails, and secure-deployment properties of the retrieval path.
3. **Exhaustive and mutually exclusive.** Each paper is placed in exactly one row of the grid below; the grid is the whole set of candidates, so nothing is double-counted.
4. **Runner-up management.** Where a paper arguably answers two questions, I named a *runner-up* theme (with its arXiv ID) and still assigned it to one theme. The runner-up notes appear inline with each pick.
5. **Selection filter.** Recency (October 2026 window), arXiv-verified titles / IDs / dates from the abstract pages, and best representative per scan angle. Papers whose primary axis was evaluation tooling or another dimension were excluded from the six even when they ranked high within an angle.

---

## Theme grid

| Theme | Picks |
|---|---|
| **Efficiency** | UNREAL (must-read), Agentic AutoRAG (worth skimming) |
| **Reasoning** | Where and Why Search-Augmented LLMs Fail When Reasoning over Rapidly Evolving Knowledge (must-read), Beyond Retrieval Failure (worth skimming) |
| **Multimodality** | VisR-RAG-Fin (background) |
| **Safety** | Protection Is Not One Event: A Survey of RAG Protection Research by Measured Endpoint (must-read) |

---

## The scans (angle → best 2–3 of the hits)

1. **Core RAG methods** — rethink-knowledge-rag (2610.01936), analyzing-performance-RAG (2610.20419), graph-topology-energy-pathfinding (2610.29933), agentic-autoRAG (2610.08452)
2. **Agentic / multi-step retrieval** — agentic-retrieval-legal-reasoning (2610.18611), performance-costs-of-agentic-retrieval (2610.05750), multi-hop-evidence-miss (2610.21184), reasoning-search-augmented-LLMs (2610.29189)
3. **Long-context vs. retrieval** — UNREAL (2610.08463), long-context-online-textual-memory (2610.31284), prefill-pressure-scheduling (2608.15171), reasoning-language-alignment (2610.03136)
4. **Evaluation / benchmarks** — RAGStress (2610.04691), RAG-PIBench (2610.08571), How-Ground-Truth-Shapes-Retrieval-Scores (2610.31606), Decomposing-Unbounded-Prompt-Injection (2610.24999), RAGScope (2609.39075)
5. **Efficiency** — UNREAL (2610.08463), learning-to-repair-cross-chunk-context (2609.35139), agentic-autoRAG (2610.08452), energy-footprint-of-tokens (2610.19819), making-visual-evidence-count (2610.21318)
6. **Multimodal RAG** — VisR-RAG-Fin (2610.24822), making-visual-evidence-count (2610.21318), multimodal-agg-RAG (2610.11371)
7. **Safety** — Protection-Is-Not-One-Event (2610.30193), RAGStress (2610.04691), RAG-PIBench (2610.08571), agentic-safety-injection-red-teaming (2610.08951)

---

## The six picks

### 1. Efficiency — **must-read**

**UNREAL: Unifying Retrieval and Long-Context with a Single Model** — [arXiv:2610.08463](https://arxiv.org/abs/2610.08463) (submitted Tue, 6 Oct 2026)

Long-context inference and RAG handle evidence selection at vastly different scales — a single long prompt versus an entire corpus — and UNREAL asks whether one model-internal mechanism can span that range. It derives retrieval queries directly from the frozen LLM's own internal representations and encodes chunks, then scores candidate chunks against the query embedding; in practice this replaces the dense-retrieval layer of a long-context model, raising HotpotQA recall from 49.1% to 73.2% and LV-Eval F1 from 49.97% to 54.66% at 256K tokens, while cutting time-to-first-token relative to full-context inference from roughly 32K tokens onward, with larger gains as context grows. For the group this matters because it dissolves the "retrieval vs. long context" framing that drove several of my scan angles: the practical story is a unified evidence-selection mechanism, not two competing paradigms, and it overlaps directly with the efficiency theme I assigned it.

*Runner-up theme: long-context vs. retrieval as a *competitive* paradigm* (the angle it came from) — the strongest runner-up paper is [P-PAS: Prefill-Pressure Adaptive Scheduling for Long-Context LLMs](https://arxiv.org/abs/2608.15171) (arXiv:2608.15171, submitted 9 Aug 2026), which targets inference-time efficiency of long-context LLM applications including RAG.

### 2. Efficiency — **worth skimming**

**Agentic AutoRAG: RAG Pipeline Optimization through Reasoning-Driven Agents** — [arXiv:2610.08452](https://arxiv.org/abs/2610.08452) (submitted Tue, 6 Oct 2026)

Retrieving a good chunk is only half the problem; the other half is finding good hyperparameters among the many interacting choices (chunking, embedding, reranking, generation). Agentic AutoRAG turns that into a search an LLM agent drives: after each trial a **Diagnoser** attributes each failed question to retrieval or generation, and a **Proposer** — grounded in a knowledge base of model rankings and pricing — traces a Pareto frontier of accuracy versus cost. On three multi-hop QA benchmarks it matches the strongest baseline's 30-trial judge accuracy within its first 10 trials, and on a real-world healthcare corpus hits 77% exam accuracy at ~58% of the baseline's per-query cost (matching the baseline's 71.5% at ~22% of cost). Accepted at REALM@EMNLP 2026 and the ML-for-Systems Workshop@NeurIPS 2026.

*Runner-up theme: agentic retrieval* (its optimizer is itself an agentic loop for choosing pipeline configs); the runner-up angle's best pick is [Agentic Retrieval for Evidence-Based Legal Reasoning](https://arxiv.org/abs/2610.18611) (arXiv:2610.18611, submitted 13 Oct 2026), which asks *when* an agent should even retrieve.

### 3. Reasoning — **must-read**

**Where and Why Search-Augmented LLMs Fail When Reasoning over Rapidly Evolving Knowledge** — [arXiv:2610.25323](https://arxiv.org/abs/2610.25323) (submitted Wed, 18 Oct 2026)

As the world changes, new information piles up while older records stay online, and this complicates reasoning: the model must retrieve evidence *and* resolve conflicts over which record remains valid. To pin down the bottleneck the authors build **TREKBENCH-CTRL**, a controlled benchmark with distractors spanning temporality, relevance and trustworthiness, and show that benchmarks dominated by outdated distractors substantially *underestimate* task difficulty. The headline finding: the main bottleneck is no longer retrieval but *post-retrieval reasoning* — frontier models are often misled by conflicting evidence even after retrieving the right passage. The design rewards models for simply selecting the latest evidence and fails to capture the complexity of real-world information seeking, so it diagnoses rather than scores.

*Runner-up theme: evaluation / benchmarks* — the benchmark paper that sits on this boundary is [RAGScope](https://arxiv.org/abs/2609.39075) (arXiv:2609.39075, submitted 30 Sep 2026), a leakage-controlled, cost-aware evaluation protocol for local evidence gates.

### 4. Reasoning — **worth skimming**

**Beyond Retrieval Failure: Understanding Why LLMs Miss Evidence in Multi-Hop RAG** — [arXiv:2610.21184](https://arxiv.org/abs/2610.21184) (submitted Thu, 15 Oct 2026)

Multi-hop RAG is usually evaluated as "did the answer cite the required passage?", but in a long chain a missing passage may simply be unreachable, or the agent may have issued a query that doesn't retrieve it — two distinct failure modes that standard evaluation conflates. This paper formalizes multi-hop RAG as retrieval plus reasoning and finds that **search drift** — the query no longer tracking the unanswered sub-question — explains most apparent retrieval failure. Its surprising result: recovering missing evidence does *not* proportionally reduce total error; as missing-evidence failures drop, premature resolutions and abstentions rise, so the remaining bottleneck has shifted from guiding search toward required evidence to verifying that the retrieved evidence is sufficient. The paper also includes a retrieval-efficiency analysis (retrieved tokens, API cost across methods and embedding backbones).

*Runner-up theme: efficiency* — the runner-up paper here is [P-PAS](https://arxiv.org/abs/2608.15171) (arXiv:2608.15171), again, since the efficiency axis cuts across the efficiency and reasoning angles.

### 5. Multimodality — **background**

**VisR-RAG-Fin: Benchmarking Multimodal RAG over Visually Rich Financial Documents** — [arXiv:2610.24822](https://arxiv.org/abs/2610.24822) (submitted Sat, 17 Oct 2026)

Open benchmark for page-level QA over visually rich financial documents, built with a general pipeline that preserves original layout and visual content; it systematically compares retrieval and generation behavior under text-only, multimodal and hybrid configurations, giving the group a concrete testbed for multimodal RAG. Accepted at the main research track of ACM SIGIR-AP 2026 (Singapore, Dec 13–15, 2026).

*Runner-up theme: evaluation / benchmarks* — the runner-up multimodal benchmark is [Making Visual Evidence Count in Multimodal Document RAG](https://arxiv.org/abs/2610.21318) (arXiv:2610.21318, submitted 15 Oct 2026), whose angle is the vision-language model's accuracy-cost trade-off in reading visual evidence, and [Multimodal Reranking Is a System One Decision](https://arxiv.org/abs/2610.28435) (arXiv:2610.28435, submitted 21 Oct 2026), which reframes multimodal reranking as a single design decision.

### 6. Safety — **must-read**

**Protection Is Not One Event: A Survey of RAG Protection Research by Measured Endpoint** — [arXiv:2610.30193](https://arxiv.org/abs/2610.30193) (submitted Wed, 21 Oct 2026)

RAG systems face content leakage, source reconstruction, unauthorized access, data poisoning and prompt injection, yet the literature uses incompatible metrics, datasets and threat models, and no two papers call the same thing a "defense". This paper presents a systematic survey and human-coded evidence map of **118 full-text-confirmed RAG defense papers**, organized by measured endpoint — content disclosure, formal privacy proxies, access control and suppression, corpus-use detection, and pipeline integrity and attribution — rather than by claimed goal or mechanism. The controlled testbed result is the part to carry into the group: an 8-gram guard that reduces 20-token copying to 0.0% does *not* prevent private-fact recovery — a three-query adaptive attacker recovers 48.3% of hidden facts on Qwen3-8B. It also argues that existing evaluations don't match the systems being evaluated. Released: taxonomy, dataset, coding protocols and testbed. Recommended companion to [RAGStress](https://arxiv.org/abs/2610.04691) (arXiv:2610.04691) if the group wants a runner-up safety-adjacent benchmark.

*Runner-up theme: evaluation / privacy* — the runner-up for safety is [RAGStress](https://arxiv.org/abs/2610.04691) (arXiv:2610.04691, submitted 3 Oct 2026), which stresses RAG under four KB-corruption types (factual, numeric-typography, relevance-poisoning, contradiction) across 52,500 evaluations — a robustness benchmark rather than a defense.

---

## Recent developments (from the wider web, Oct 2026)

1. **Agentic RAG is the new production baseline.** The biggest reported shift is the merger of RAG with agent loops: retrieval is exposed as a *tool* an LLM planner decomposes the prompt, selects which retriever to call (vector DB, knowledge graph or web API), judges whether context is sufficient, and loops back when it senses a gap. Maxcore's October piece goes further, calling corrective RAG (CRAG) self-healing pipelines the pattern separating demos from enterprise products — explicit relevance evaluators that refuse to pass bad context. That is my agentic/multi-step angle in deployment form, not just research form.
2. **Streaming RAG is the infrastructure story the angles missed.** Streaming-ingestion posts are appearing alongside the research papers — the "nightly re-index Python script is dead" claim backed by CDC (Change Data Capture) pipelines that stream database changes straight into embedding functions for real-time index freshness — alongside a second trend: contextual chunking (originally Anthropic-pioneered) becoming the standard ingestion step because plain chunking loses meaning the moment a passage is split in isolation.
3. **Negative results are now published results.** The LASAGNA study (huggingface, Oct 2026) is the clearest such: the three top techniques predicted a combined **+47%** gain but delivered **+17%** stacked — a 63% shortfall across 358,215 individual query evaluations. Retrievability quality and answer faithfulness are essentially *uncorrelated* (Pearson r = -0.01, p = 0.91; different pipeline stages drive each metric); a rank crossover between RAG profiles sits somewhere between 15K and 25K documents; even a 2019 MS-MARCO MiniLM-L6 cross-encoder ranked above all four recent rerankers tested; at 200K documents the "Balanced" profile beats "Standard" by 13.7% (p = 0.003). Roughly $5,200 of compute across ~310 wall-clock hours. This directly informs both the efficiency and evaluation angles and undercuts any "tune one lever" mindset that papers like Agentic AutoRAG embody.
4. **The budgeting conversation has moved on from accuracy.** One enterprise architecture report (Oct 2026) claims RAG outperforms fine-tuning on factual recall by 28–41%; knowledge-graph-augmented RAG is the other structural move, per the Vector Institute's October overview.

**What the chatter mentions that my angles missed:** (a) the *pipeline-ops layer* — streaming ingestion via CDC, self-healing pipelines, contextual chunking, and multi-agent retrieval-as-tool-loop as the new production baseline; and (b) *empirical anti-patterns* — the non-additivity of RAG techniques and the near-zero correlation between retrieval quality and faithfulness — that the evaluation angle only covered as "benchmarks", not as things people are actively publishing against. The RAG-vs-fine-tuning comparison is a management-level question no arXiv angle was designed to catch.

---

## One-line takeaways

- **UNREAL** — retrieval and long-context are one evidence-selection knob; a unified model-native mechanism beats patching either side.
- **Where and Why** — the bottleneck in search-augmented reasoning has moved from retrieval to post-retrieval reasoning: verify sufficiency, don't just recover evidence.
- **Protection Is Not One Event** — verbatim-blocking ≠ private-fact protection: an 8-gram guard still leaks 48.3% of hidden facts to a three-query adaptive attacker on Qwen3-8B.
- **Agentic AutoRAG** — agentic diagnostics turn RAG tuning from a 30-trial brute force into a ~10-trial Pareto search.
- **Beyond Retrieval Failure** — search drift is the dominant "retrieval failure" cause, and recovering missing evidence doesn't proportionally help.
- **VisR-RAG-Fin** — multimodal finance QA needs its own benchmark; text-only baselines are not a fair comparison.

---

*Scan angles, candidate counts and full abstracts are available in the arXiv search log for this cycle. Prepared by Hezi Liu for the RAG reading group, 2026-10-25.*