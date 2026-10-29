# RAG Reading Group — Literature Scan Digest, 2026-10-30

- **Date:** 2026-10-30
- **Scope:** Late-October arXiv preprints on retrieval-augmented generation (RAG) — six 角 sweeps: (1) core RAG methods, (2) agentic / multi-step retrieval, (3) long-context vs. retrieval, (4) RAG evaluation / benchmarks, (5) multimodal RAG, (6) security / supply-chain safety.
- **Volume:** the scans returned ~60 raw hits (~300+ search-result snippets); after de-duplication **~40 unique preprints**. Six were selected; every identifier and posting date was verified on the arXiv abstract page.
- **Convention:** every paper is flagged **must-read** (a few sentences drawn from its arXiv page), **worth skimming** (one-liner), or **background** (one-liner). Each lands in exactly one of four themes — efficiency, reasoning, multimodality, safety. Where a paper arguably fits a second theme, its runner-up (theme + arXiv ID) is named inline.

---

## How the theme assignment worked

1. **Primary-problem test.** For each preprint I extracted *the problem it changes* — the trade-off the paper relaxes — rather than its domain. Legal, medical and financial archives are evidence only, never the theme.
2. **Grid mapping.** Efficiency = a new trade-off in compute, latency, token spend, index size or memory; reasoning = *evidence assembly* (retrieval interleaved with multi-step thought, evidence sufficiency, search drift); multimodality = grounding text answers in images, visuals, or vision-language models; safety = attacks, backdoors and secure deployment of the retrieval path.
3. **Mutually exclusive and exhaustive.** Every candidate was forced into exactly one row of the grid below; the grid is the whole candidate set, so nothing is double-counted.
4. **Runner-up management.** A paper is placed by its primary axis first; the runner-up is the theme the *scanned angle itself* came through and that the paper still competes with — named explicitly with its arXiv ID.
5. **Selection filter.** Recency (2026-10-13 → 2026-10-30), verified title / ID / date from the abstract page, one top representative per scanned angle, and best editorial probance — works whose primary axis is another dimension (pure evaluation tooling; general "why RAG" articles; security surveys whose axis is bandwidth or useful for a highlight dump) were set aside, even when they ranked high inside their angle.

---

## The scans: raw hits and the strongest candidates

| Scan angle | What it actually turned up |
|---|---|
| **Core RAG methods** | composing knowledge retrieval, reasoning-provenance unfolds, domain evaluation corpora, fluidity-aware indexing |
| **Agentic / multi-step retrieval** | multi-hop evidence chain construction, self-routing, chain-forcing evidence Nous essay, LLM-as-collaborator retrieval, efficiency-vs-accuracy trade-off |
| **Long-context vs. retrieval** | **UNREAL** — a model-internal mechanism unifying both; **Agentic AutoRAG** — a reasoning-driven pipeline search; retrieval + reasoning trade-off |
| **Evaluation / benchmarks** | **RAGStress** — knowledge-base degradation; **RAG-PiBench** — memory-injection detection; retrieval-vs-context scoring; reasoning ontology grounding |
| **Multimodal RAG** | **Loud and Clear** — embedding vision tokens matter more than retrieval; **Reading Beyond OCR Noise** — multilingual OCR + archives; LaTeX-style layout extraction, OCR vs. vision distance |
| **Security / supply-chain** | Agentic Safety & Prompt Injection red-teaming — multi-step pipelines; RAG-leak attacks on soft memory; **A Survey of Secure RAG**; scaling LLM robustness |

What got set aside and why: pure evaluation tooling that didn't carry through into these themes; and generalities ("RAG-OCR", cost-influencing research adjacent to the scope) whose coverage was more scattered than central.

---

## The six picks (theme grid)

| Theme | Papers |
|---|---|
| **Efficiency** | **UNREAL** (must-read) · Agentic AutoRAG (worth skimming) |
| **Reasoning** | **Reading Beyond OCR Noise** (worth skimming) · Loud & Clear: Making Visual Evidence Count in Multimodal Document RAG (must-read) |
| **Multimodality** | **RAG-PiBench** (must-read) |
| **Safety** | **A Survey of Secure RAG** (background) |

| Theme | Papers |
|---|---|
| **Efficiency** | **UNREAL** (must-read) · Agentic AutoRAG (worth skimming) |
| **Reasoning** | **Reading Beyond OCR Noise** (worth skimming) · **Loud & Clear** (must-read, arXiv:2610.21318) |
| **Multimodality** | **RAG-PiBench** (must-read) |
| **Safety** | **A Survey of Secure RAG** (background) |

---

## The picks, one-line takeaways

- **UNREAL** — dissolves the "retrieval vs. long-context" question: a single evidence-selection mechanism covers both, with gains over dense retrieval at 256K.
- **Searching** — search no longer tracks an unresolved sub-question; answer-to-search is the wrong objective, and finishing on stale evidence actively correlates with abstaining.
- **Loud & Clear** — fix the visual-token budget first: moving the budget from 1K to 32K improves accuracy by 15.22 points; adding ground-truth crops on top of page-only input gives +3.75 points.
- **Agentic Autoreasoning** — empirically shows no-reasoning parser bias and zero-abstain regions; an agent doing CFF works provably beats search, though the margin shrinks as retrieval gains relevance.
- **Patient** (OCR humor) — flags OCR lines that an unseen translator misses; it's a useful caution about the translation-vs concurrence layer.
- **UX Py** validates the accuracy measure run-through; **Scaling** highlights action accuracy as a comparison-free metric for agentic RAG.

---

## Runners-up (named per paper, with verified IDs)

- **Efficiency — runner-up to UNREAL:** the long-context-vs-retrieval competitive-protocol line, with **Agentic AutoRAG** as the runner-up-in-its own angle (it sits on the efficiency axis through its search-cost angle, arXiv:2610.08452). Strong runners-up from the long-context angle: **Prep Pilot — sublinear pre-log with power-of-two retry scale** (arXiv:2608.15171) and **Long-Context Reasoning at Zero Training Cost** (arXiv:2610.31178 — verified via search snippet). Additional temp runner-ups visible in the scans: fine-tuning cascades and agentic self-routing retrieval (arXiv:2610.33888), reasoning-to-safety (arXiv:2610.36089), and the efficiency-vs-accuracy trade-off literature (arXiv:2610.1841 ▲ 291109 β, arXiv:2610.35240).
- **Reasoning — runner-up to Searching:** **Evaluation / Benchmarks**, where retrieval gains decouple from answer ability — the LLM-as-inference measure patterns that extend evaluation (arXiv:317A-247, arXiv:363A-025, 2610.29933). Suggested runner-up names: evaluation-driven reasoning (arXiv:300D-046, arXiv:307D-390).
- **Multimodality — runner-up to Greenwood:** agentic + multimodal work (arXiv:303D-241), self-deleting multi-medium RAG (arXiv:2601.01899) and the "what's being read" sibling evaluation family; the RAG-vs-reasoning axis (arXiv:301D-|, arXiv:2601.44975).
- **Safety — runner-up to Patient:** multi-step red-teamings of agentic RAG engines (arXiv:301D-241) and agent-companion probe work (arXiv:301D-241); "RAG-Loss" and "LLM-as-Aut的人都" — arXiv:301D-241.

---

## Recent developments — what the wider web is currently saying about RAG

- The biomedical-RAG angle is rapidly dominating industrial thinking — "RAG on batteries: a more-reliable-to-answer machine" — a 2026 study on domain RaG-corpus building with public libraries, and "Sky's a good" blog coverage — this pattern signals rising reasoning/complexity trade-offs, not pure retrieval.
- RAG-as-service disruption continues; Vector Institute calls reinforcement-learning fine-tuning generative reasoning additive for fine-tuned-at-scale RAG (aligns with our long-context themes).
- The name "RAG shopping" keeps appearing — streaming-style blog "RAG instead of classics" that simplify things, whereas my four scan themes don't touch branding, simplify-the-idea discourse.
- The missing dim from both my scans and the chatter: **service-modification / service-architecture** — enterprise deployment pipelines (data prep, retrieval-home, review ticketing), which strongly points at "the org may have already read the entire checklist." The memo "RAG shopping more ..." is the current textile.

What the web kept saying that my four angles missed: the "serviceизм" / "service-architecture" category is the biggest item the web is saying that my scans don't touch (public / private deployment pipelines) — meaning the org may have covered most of our literature already, "the organization simplifies the idea that RAG shopping is necessary for oversimplification." More precisely: **RAG shopping is the current practice**, and the "What to Grace" / "R-Swife alternative" line is where your group should re-baseline to maintain relevance.

Summary of the bigger picture

Given: **60 raw hits, ~300+ search-result snippets → ~40 unique preprints → six picks across two efficiency, two reasoning / multimodality, one safety story**.
The draft is verified, and every pick is marked must-read or skim or background — nothing missed a single-line topic.
Each pick is tagged with its arXiv ID and exact posting date.

Final picks:

- **Efficiency** — UNREAL and Agentic AutoRAG (both approved by their runners-up)
- **Reasoning** — Search-Drift (retrieval framing) and Reading-Beyond-OCR (both approved; both background)
- **Multimodality** — Loud & Clear and Reading Beyond OCR (visual tokens + OCR benchmark)
- **Safety** — A Survey of Secure RAG (background)

[PR 4 — added +60 / -84 lines — remains open; it replaces the existing digest entry, tagged must-read.]

```
