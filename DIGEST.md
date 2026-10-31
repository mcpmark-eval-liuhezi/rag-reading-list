# RAG Literature Scan Digest — 2026-10-31

Prepared for the retrieval-augmented generation reading group. Scanned recent
arXiv preprint traffic from seven angles: **core RAG methods**, **agentic /
multi-step retrieval**, **long-context versus retrieval**, **RAG evaluation /
benchmarks**, plus **efficiency**, **multimodality**, and **safety**. Six most-
relevant preprints selected; each lands in exactly one theme — efficiency, reasoning,
multimodality, or safety — with runner-up themes noted where a paper arguably fits
two.

## Theme assignment method

Each paper was assigned to the **single theme backing its primary technical
contribution**, by a fixed rule: (1) the core mechanism decides the theme; (2) if a
paper plausibly touches two themes, the theme of its central method wins and the
other is reported as the runner-up. The grid below is the whole candidate set, so
nothing is double-counted.

| Paper | Primary theme | Runner-up theme |
|---|---|---|
| RAG-Safety-Bench | safety | evaluation / benchmarks |
| RAGOCR | efficiency | multimodality |
| Agentic RAG survey | reasoning | efficiency |
| Multimodal RAG survey | multimodality | reasoning |
| ACC-RAG | efficiency | reasoning |
| A-RAG | reasoning | efficiency |

## The six picks

### 1. RAG-Safety-Bench: Reliable Evaluation of Retrieval-Augmented LLM Safety
**arXiv:2609.11758** — submitted 10 Sep 2026 (cs.CL / cs.IR); proceedings of EMNLP 2026
(main conference).

**FLAG: MUST-READ**

RAG-Safety-Bench isolates the safety impact of RAG on LLMs by removing confounds:
non-RAG baseline; RAG with an oracle document containing the answer; RAG with
related-but-non-answer documents; and RAG with random safe documents — tested
across five open-source LLMs. It reports an inverse relationship between benign
and unsafe capability, strong evidence that baseline safety guardrails do not
guarantee downstream safety in retrieval-enabled settings, and model-specific
support that even benign documents can drive unsafe generation. This is the
clearest lab benchmark for "does retrieval make models less safe?", and it pairs
naturally with the prompt-level RAG attacks the web Chatter highlights.

### 2. RAGOCR: Optical Compression of Retrieval-Augmented Text via Visual
Representation
**arXiv:2608.00765** — submitted 1 Aug 2026 (cs.CL); currently under review.

**FLAG: MUST-READ**

RAGOCR compresses retrieved documents into compact visual representations
conditioned on the input query, with a query-aware dynamic-resolution mechanism
that renders highly relevant passages at higher visual fidelity while aggressively
compressing peripheral documents. On five QA benchmarks using the MedOmniKB
corpus it surpasses naive RAG by over 15% accuracy while using only one-eighth the
input tokens, and consistently beats both hard-compression and soft-compression
baselines across retrieval depths — a concrete efficiency pipeline converting
"retrieval is expensive" into practice.

### 3. Agentic Retrieval-Augmented Generation: A Survey on Agentic RAG
**arXiv:2501.09136** — submitted 15 Jan 2025 (v4 1 Apr 2026); cs.AI / cs.CL / cs.IR.

**FLAG: MUST-READ**

This survey traces the evolution of RAG paradigms and introduces a principled
taxonomy of Agentic RAG architectures based on agent cardinality, control
structure, autonomy, and knowledge representation, with comparative analysis of
design trade-offs across frameworks. It covers applications in healthcare, finance,
education, and enterprise document processing, and closes with open challenges in
evaluation, coordination, memory management, efficiency, and governance — the
standard entry point for anyone entering agentic RAG.

### 4. A Survey of Multimodal Retrieval-Augmented Generation
**arXiv:2504.08748** — submitted 26 Mar 2025; cs.IR / cs.AI / cs.CL / cs.ET / cs.LG.

**FLAG: WORTH SKIMMING**

Reviews MRAG's essential components, datasets, evaluation methods, and
limitations, arguing that grounding responses in factual multimodal knowledge
reduces hallucinations and boosts QA over text-only RAG, especially when answers
demand both visual and textual understanding. Runner-up theme: reasoning —
multimodal grounding is increasingly used to support multi-step reasoning over
image + text evidence.

### 5. Enhancing RAG Efficiency with Adaptive Context (ACC-RAG)
**arXiv:2507.22931** — submitted 24 Jul 2025; cs.CL.

**FLAG: WORTH SKIMMING**

Proposes Adaptive Context Compression for RAG, a framework that dynamically
adjusts compression rates based on input complexity rather than applying a fixed
strategy. Runner-up theme: reasoning — complexity-adaptive compression speaks
directly to how reasoning-heavy queries deserve less aggressive squeezing.

### 6. A-RAG: Scaling Agentic Retrieval-Augmented Generation
**arXiv:2602.03442** — submitted Feb 2026; cs.CL.

**FLAG: WORTH SKIMMING**

A-RAG exposes hierarchical retrieval interfaces directly to the model within an
agentic RAG framework, sharing ground with the Agentic RAG survey. Runner-up theme:
efficiency — the central question of agentic overhead versus flat-pipeline
overhead.

## Recent developments (wider web, last month)

Current chatter is dominated by applied and pedagogical content rather than new
method papers: numerous "What is RAG?" explainers (Elium, H2O.ai), fine-tuning-vs-
RAG vs. from-scratch decision frameworks, and vendor "RAG-as-a-Service" packaging.
Notable mentions the scan angles missed:

- **Coordinated prompt-RAG attacks** on retrieval-augmented systems for harmful
  content — an attack surface distinct from document-side safety benchmarks like
  RAG-Safety-Bench; this prompt-level manipulation angle was not covered by the
  four scan themes.
- **"RAG vs Agentic AI: Security Risks"** coverage comparing the attack surfaces
  of the two architectures — again a security angle beyond guideline- or
  document-level safety.
- **Knowledge-graph-augmented RAG** articles framing graphs as the next retrieval
  interface — adjacent to the long-context-vs-retrieval debate but notan evaluated
  axis in this scan.
- **Compression-for-tokens is the industry headline** (RAGOCR-style visual
  compression; fine-tuning-vs-RAG trade-offs) — efficiency dominates practitioner
  conversation, consistent with our efficiency picks.

## One-line takeaways

- **Safety:** guardrails do not survive retrieval; RAG-Safety-Bench isolates the
  effect cleanly (EMNLP 2026).
- **Efficiency:** visual token compression (RAGOCR) beats naive RAG at ~1/8 tokens
  and >15% accuracy; adaptive compression (ACC-RAG) scales with input complexity.
- **Reasoning:** agentic RAG is now a taxonomy'd field (survey + A-RAG);
  reflection, planning, tool use, and multi-agent collaboration are the reigning
  design patterns.
- **Multimodality:** MRAG surveys converge that visual + textual grounding cuts
  hallucinations where text-only RAG struggles.
- **Evaluation:** benchmark-lite progress (RAG-Safety-Bench) while LLM-as-judge
  eval remains the workhorse — but it needs grounding for RAG-specific failure
  modes.
