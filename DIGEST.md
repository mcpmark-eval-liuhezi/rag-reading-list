# RAG Reading Group — Literature Scan Digest (2026-10-22)

Weekly literature scan for the retrieval-augmented generation reading group.
Please comment directly on this PR (or open issues) — this digest is meant to be argued with.

## 1. Scan scope and method

Eight arXiv searches were run, covering the four agreed scan angles plus four theme-targeted follow-ups:

- **Requested angles:** (1) core RAG methods, (2) agentic / multi-step retrieval, (3) long-context vs retrieval, (4) RAG evaluation and benchmarks.
- **Theme-targeted follow-ups:** efficiency (latency / cost / caching), reasoning (retrieval + chain-of-thought / inference-time), multimodality (vision-language RAG), safety (poisoning / privacy / prompt injection / hallucination).

**Yield:** 77 raw scan hits → **60 unique preprints** after de-duplication. 55 of those were posted within the last four weeks (late Sept – Oct 22, 2026); 5 are older items that search dragged in (an Apr 2026 secure-RAG survey, a Feb 2026 agents eval, a Jun 2026 agent-memory systems paper, an Aug 2026 poisoned-context study, and a Jul 2025 artwork-understanding pipeline). Shortlisted candidates had their arXiv abstract pages read in full before selection; six were chosen.

## 2. How themes were assigned

Each pick lands in exactly one of the four themes (efficiency / reasoning / multimodality / safety). The rules used:

1. **Theme = the problem the paper attacks, not the domain it is applied to.** (A benchmark over financial documents is multimodality, not finance.)
2. **Primary axis = the contribution that survives if you swap the other axis out.** A paper about token budgets *for* visual documents is multimodal in substrate but about capacity economics in contribution — check which claim still stands if you changed the substrate.
3. **Ties broken toward the theme with fewer strong representatives** this cycle, so the shortlist doesn't collapse into one bucket.
4. **Where two themes genuinely compete, the runner-up is named** in the entry and the summary table.

## 3. The six picks

### Efficiency

**UNREAL: Unifying Retrieval and Long-Context with a Single Model** — arXiv:2610.08463 — posted 2026-10-06 — **MUST-READ**
*Runner-up theme: reasoning (its distractor-removal gains show up on NoLiMa, an associative-reasoning benchmark) — but the headline claims are recall-per-parameter and serving cost, so efficiency wins.*

- Proposes model-native evidence selection that spans **corpus retrieval and long-context inference with one mechanism**: chunks are encoded and retrieval queries are derived directly from the frozen LLM's internal representations. It adds fewer than **500K trainable parameters** and leaves the backbone unchanged.
- On a **3B-token, 21M-chunk Wikipedia index**, all four dense and hybrid UNREAL backbones beat state-of-the-art retriever-reranker systems; the best raises recall from 49.1% to 73.2% on HotpotQA, 31.7% to 60.1% on 2WikiMultiHopQA, and 8.8% to 14.4% on MuSiQue.
- Reused as a long-context filter (removing distractors before generation), it lifts NoLiMa accuracy from 1.0% to 24.83% at 128K context and LV-Eval F1 from 49.97% to 54.66% at 256K — and **reduces FLOPs and time-to-first-token vs full-context inference from roughly 32K tokens onward**, with larger gains as context grows.
- Why it matters to us: this is the most direct answer this cycle to the "RAG vs long context" question — it argues they're the same evidence-selection problem at different scales, and gets efficiency wins as a side effect.

### Reasoning

**Where and Why Search-Augmented LLMs Fail When Reasoning over Rapidly Evolving Knowledge (TREK)** — arXiv:2610.25323 — posted 2026-10-18 — **MUST-READ**
*Runner-up theme: safety, via its trustworthiness/conflicting-evidence distractor axis — but the paper's core claim is a reasoning diagnosis, not a defense.*

- Introduces TREK, three components: **TREKTRACE** (a plug-and-play framework attributing failures to specific stages of retrieval vs reasoning), **TREKBENCH-WILD** (a meta-benchmark of real-world questions requiring complex reasoning over rapidly evolving knowledge), and **TREKBENCH-CTRL** (a controlled benchmark with distractors spanning temporality, relevance, and trustworthiness).
- Headline finding: **the main bottleneck is post-retrieval reasoning, not retrieval** — frontier models are often misled by conflicting evidence even after retrieving everything needed to answer.
- Second finding with evaluation-design teeth: **benchmarks dominated by outdated distractors substantially underestimate task difficulty** — a caution for anyone building or trusting temporal-RAG evals.
- Why it matters to us: it attacks the "improve the retriever" instinct directly, and it's the best methodological example this cycle of stage-attributed failure analysis (which pairs with ExecutionRAG below).

**Beyond Retrieval Failure: Understanding Why LLMs Miss Evidence in Multi-Hop RAG (ExecutionRAG)** — arXiv:2610.21184 — posted 2026-10-15/16 (v1; search metadata dates submission 15 Oct, arXiv announcement 16 Oct) — **WORTH SKIMMING**
*Runner-up theme: none compelling — it is a training-free, low-overhead intervention, but that's incidental to its diagnosis.*

- A training-free "requirement register" that records open sub-questions and their supporting evidence shows that much of what looks like retrieval failure in multi-hop RAG is actually **search drift** (search no longer tracking an unanswered sub-question); recovering the missing evidence does not proportionally reduce error, because the bottleneck then shifts to verifying that retrieved evidence is sufficient (on 1,000 MuSiQue questions, unretrieved-required-evidence errors fall from 382 to 234 / 383 to 274 across two embedders).

### Multimodality

**Loud and Clear: Making Visual Evidence Count in Multimodal Document RAG (LoC)** — arXiv:2610.21318 — posted 2026-10-15 — **MUST-READ**
*Runner-up theme: efficiency — its "Loud" requirement is explicitly a visual-token-budget argument (how much capacity you spend per retrieved page) — but the contribution is about how VLMs read retrieved pages, so multimodality wins.*

- Locates the bottleneck **beyond retrieval**: on SciEGQA oracle pages, five prior methods hand the generator only 0.7K–2.7K visual tokens per query on average; raising the page-only budget from 1K to 32K improves accuracy by **15.22 points**, and at a fixed 16K budget adding ground-truth crops adds 3.75 points over page-only input.
- Distills what the generator needs into two requirements: **Loud** (use full visual token capacity — both budget and image resolution help with the other held fixed; full-page scaling beats repetition and tiling at matched budgets) and **Clear** (refine the page so evidence is prominent — suppressing surrounding content helps without enlarging regions, and OCR of query-relevant regions plus page images beats either alone).
- LoC combines higher-resolution pages with OCR from query-relevant regions, **without ground-truth annotations or additional training**, beating eight prior methods on SciEGQA, ViDoRe-v3, and MMLongBench-Doc — over the strongest (ColQwen3) by 8.88 / 3.09 / 4.22 points with the same retriever and generator.
- Why it matters to us: the mirror image of TREK — retrieval succeeded, the reader failed — applied to the visual side, with a cheap, training-free fix.

**VisR-RAG-Fin: Benchmarking Multimodal RAG over Visually Rich Financial Documents** — arXiv:2610.24822 — posted 2026-10-17 — **BACKGROUND**
*Runner-up theme: none close (among the four themes only multimodality fits; its evaluation/benchmark character is a scan angle, not a theme).*

- Open-source benchmark plus a systematic empirical study of text-only vs multimodal vs hybrid configurations for page-level QA over visually rich financial documents (accepted at ACM SIGIR-AP 2026) — useful reference if the group ever needs a realistic enterprise-document testbed.

### Safety

**Consistency Is the Attack Surface: Detecting Coordinated Retrieval Poisoning with Embedding Geometry (CoordGuard)** — arXiv:2610.24834 — posted 2026-10-17 — **WORTH SKIMMING**
*Runner-up theme: none close.*

- Shows the assumption behind consistency-based defenses is brittle: a coordinated campaign touching a **negligible fraction of the corpus** still reaches the reader's top-5 in 94.1% of targeted query-seed rows (and forms a retrieved majority in 52.9%), driving exposure-conditional attack success of 0.512–0.576 even for defended systems (RobustRAG, ReliabilityRAG) while degrading clean accuracy. Coordination leaves a fingerprint in embedding geometry, and CoordGuard audits that structure **without poison labels, correct answers, or reader gradients** — always-filtering cuts attack success to 0.167 at a 13.6-point clean cost, while a calibrated gate keeps clean accuracy 0.315 at attack success 0.331.

## 4. Summary table

| # | Paper | arXiv ID | Posted | Theme | Flag | Runner-up theme |
|---|-------|----------|--------|-------|------|-----------------|
| 1 | UNREAL: Unifying Retrieval and Long-Context | 2610.08463 | 2026-10-06 | Efficiency | **Must-read** | Reasoning |
| 2 | TREK: Where/Why Search-Augmented LLMs Fail | 2610.25323 | 2026-10-18 | Reasoning | **Must-read** | Safety |
| 3 | LoC: Loud and Clear (Multimodal Document RAG) | 2610.21318 | 2026-10-15 | Multimodality | **Must-read** | Efficiency |
| 4 | ExecutionRAG: Multi-Hop Evidence Misses | 2610.21184 | 2026-10-15/16 | Reasoning | Worth skimming | — |
| 5 | VisR-RAG-Fin (Financial Documents Benchmark) | 2610.24822 | 2026-10-17 | Multimodality | Background | — |
| 6 | CoordGuard: Coordinated Retrieval Poisoning | 2610.24834 | 2026-10-17 | Safety | Worth skimming | — |

Flags: **must-read** = read the full paper before the session; **worth skimming** = read abstract + figures, know the one claim; **background** = know it exists, cite when relevant.

## 5. Recent developments (what the wider web is saying about RAG)

- **"Context rot" and the hybrid consensus.** Chroma's 18-model Context Rot report (performance degrading long before the window fills) is the reference point in current discussions; the practical conclusion is that classic top-5 RAG as the *only* pattern is outdated, and the current default is **hybrid — retrieve a bounded set, then reason over all of it**. Vendors behave as if they agree: Anthropic's threshold compaction defaults to 150K on 1M-token models, OpenAI reprices requests above 272K input tokens, and Google charges more for Gemini 3.1 Pro prompts above 200K.
- **"MCP vs RAG" is being called the wrong question.** Current enterprise commentary argues Model Context Protocol and RAG are not competing architectures: MCP for real-time data, write access, multi-system coordination, and a standardized integration layer for agents; RAG for grounding in unstructured knowledge — with most enterprise architectures combining both according to data-access pattern.
- **RAG vs agentic AI decision frameworks.** Multiple practitioner guides this month compare the two on architecture, cost, auditability, and risk, and promote the "agentic RAG" hybrid pattern rather than a binary choice. The security-flavored versions of this conversation emphasize that agentic loops that retrieve untrusted content and act through tools inherit indirect prompt-injection risk.
- **Enterprise adoption numbers.** One architecture report making the rounds claims **51% of enterprise generative AI deployments run on RAG vs 9% built primarily on fine-tuning** — the "RAG vs fine-tuning" framing is still alive in practitioner media.
- **Conceptual hygiene around RAG vs long context.** Blog-level explanations stress that RAG and context windows solve overlapping problems in fundamentally different ways — the context window is static at inference time — which is roughly the framing UNREAL (above) now challenges from the research side.

## 6. What the chatter flags that our scan angles missed

- **Model Context Protocol / tool-protocol integration.** None of the eight arXiv queries surfaced MCP-related work; it's an interoperability and architecture story that lives mostly outside the methods literature, but it's shaping how retrieval gets wired into agents in practice.
- **Vendor pricing and compaction defaults as a de facto long-context tax.** The OpenAI >272K repricing, Gemini 3.1 Pro >200K pricing, and Anthropic 150K compaction default are serving-economics facts our efficiency scan didn't capture (it surfaced KV-cache papers, not the pricing landscape).
- **The RAG vs fine-tuning enterprise split (51% vs 9%).** This comparison barely appears in the arXiv methods literature but dominates practitioner discussion of where RAG sits in the stack.
- **"Context rot" as a named, benchmarked phenomenon.** It originates from a vendor study rather than arXiv, so our benchmark angle never saw it.
- **Agentic-AI security as its own frame.** Our safety scan covered RAG-specific poisoning/injection, but the wider web discusses indirect prompt injection for tool-using agents generally — a superset that our RAG-scoped queries under-sample.

## 7. Discussion questions for the session

1. UNREAL claims one model-internal mechanism spans corpus retrieval and long-context inference. Does that **dissolve** the RAG-vs-long-context debate, or just relocate it (to the question of who trains and hosts the selection head)?
2. TREK and ExecutionRAG both conclude the bottleneck is **post-retrieval** (conflict resolution; evidence-sufficiency verification). If that holds, where should the group spend its next project — retriever work or reader/verifier work?
3. LoC argues much of multimodal RAG's remaining gap is **visual-token economics**. Is that a systems problem (budgets, resolution) or a modeling problem (what the VLM attends to)?
4. CoordGuard pays a 13.6-point clean-accuracy cost in always-filter mode. When is trading clean accuracy for attack-surface reduction acceptable, and who gets to decide in a deployed system?
