# RAG Reading Group — Literature Scan Digest (2026-11-03)

**Prepared:** 2026-11-03 (Hong Kong time)  
**Scope:** Recent arXiv preprints on Retrieval-Augmented Generation (RAG), scanned from multiple angles: core RAG methods, agentic / multi-step retrieval, long-context vs. retrieval, and RAG evaluation / benchmarks / safety.

## Selected Papers (6 total)

Each paper is assigned to exactly one theme: **efficiency**, **reasoning**, **multimodality**, or **safety**.

### 1. Efficiency — MUST-READ
- **Title:** When Is Additional Retrieval Worthwhile? A Cost-Aware Study of Evidence Gain and Answer Reliability in RAG
- **arXiv: 2610.37358** (submitted Tue, 27 Oct 2026)
- **Detail:** Reproducible empirical study distinguishing efficient evidence retrieval from answer-reliability gains; shows retrieving relevant evidence efficiently is not the same as improving generated-answer reliability. Useful baseline for any cost-aware RAG design.

### 2. Efficiency — WORTH SKIMMING
- **Title:** Enhancing Knowledge Density via Hierarchical Context Pruning for Retrieval-Augmented Repository-Level Code Completion
- **arXiv: 2508.10068** (v3 Thu, 15 Oct 2026)
- **Detail:** Hierarchical context pruning that boosts knowledge density without increasing token usage; solid for code-RAG efficiency discussions. Runner-up theme: long-context retrieval.

### 3. Reasoning — MUST-READ
- **Title:** MAPS: Macro-Adaptive Parallel Reasoning for Regulating Search Momentum in Retrieval-Augmented Generation
- **arXiv: 2610.29792** (submitted Wed, 21 Oct 2026)
- **Detail:** Extends sequential RAG reasoning into parallel retrieval with complementary sub-queries and state consolidation; consistently outperforms representative RAG methods across six QA benchmarks and backbones. Runner-up theme: agentic RAG (e.g., RouteDRAG 2610.36444).

### 4. Reasoning — WORTH SKIMMING
- **Title:** RouteDRAG: Learning to Route and Control Agentic Execution for Multimodal Document RAG
- **arXiv: 2610.36444** (submitted Tue, 27 Oct 2026)
- **Detail:** Learned routing between short-path and agentic execution for multimodal document RAG; 3.47 pt avg improvement over short-path-only with only 79.3% of queries sent to an Agent. Runner-up theme: multimodality.

### 5. Multimodality — MUST-READ
- **Title:** Loud and Clear: Making Visual Evidence Count in Multimodal Document RAG
- **arXiv: 2610.21318** (submitted Thu, 15 Oct 2026)
- **Detail:** Shows the bottleneck in multimodal document RAG is often beyond retrieval — how retrieved pages are given to the generator. Outperforms eight prior methods on SciEGQA, ViDoRe-v3, and MMLongBench-Doc by 8.88 / 3.09 / 4.22 points over ColQwen3 with the same retriever and generator. Runner-up theme: long-video RAG (EC-RAG 2610.08674).

### 6. Safety — MUST-READ
- **Title:** Prevented is Not Protected: What Attack Success Rate Hides about RAG
- **arXiv: 2610.40742** (submitted Thu, 29 Oct 2026)
- **Detail:** Studies retrieval-corpus poisoning for RAG defense evaluation; existing defenses can introduce unexpected target-positive answers and evaluation criteria can change defense rankings. Motivates more comprehensive assessment of RAG poisoning defenses. Runner-up themes: supply-chain privacy backdoors (RAGLeak 2610.25937) and leakage-aware prompt-injection benchmarks (RAG-PIBench 2610.08571).

## Theme Assignment Methodology

Papers were scanned from four angles: core RAG methods, agentic/multi-step retrieval, long-context vs. retrieval, and RAG evaluation/benchmarks/safety. Each candidate was mapped to exactly one theme by its primary contribution:
- **Efficiency:** cost/token/top-k tradeoffs, pruning, knowledge density (2610.37358, 2508.10068).
- **Reasoning:** parallel/adaptive/multi-step reasoning over retrieved evidence (MAPS 2610.29792, RouteDRAG 2610.36444).
- **Multimodality:** vision-language document RAG, visual evidence handling (2610.21318; EC-RAG 2610.08674 as runner-up).
- **Safety:** poisoning, injection, privacy backdoors, evaluation blind spots (2610.40742; RAGLeak 2610.25937 and RAG-PIBench 2610.08571 as runners-up).

Papers fitting two themes (e.g., RouteDRAG: agentic routing + multimodality; EC-RAG: event chains + long-video/long-context) are noted with their runner-up theme.

## Recent Developments (web chatter, ~Nov 2026)

- **Agentic RAG vs. retrieve-then-generate monoliths:** the dominant 2025–2026 narrative is the merger of RAG with agent loops; blind vector-store retrieval is being replaced by iterative, tool-using agents (reflects MAPS, RouteDRAG, Librarian Agents 2610.22273 in this scan).
- **Market growth:** RAG platforms market valued ~USD 4.0B in 2025, estimated ~USD 5.52B in 2026 (Yahoo Finance, Oct 2026).
- **Agentic RAG market:** projected 35.1% CAGR 2026–2032 (OpenPR, Oct 2026).
- **Evaluation concerns:** chatter increasingly flags that CAS-based RAG benchmarks (e.g., HotpotQA, Natural Questions) may overstate robustness; controlled stress tests (RAGStress 2610.04691) and poisoning-evaluation critiques (2610.40742) align with this.
- **Notable misses from the academic scans:** long-context scaling surveys (e.g., Gong Scaling beyond context) and multimodal RAG for document understanding surveys (2610.31385) appear in the web/surveys space but were not among the top-6 picks; guardian/RED-team tooling for RAG injection (RAG-PIBench 2610.08571) is gaining traction in industry chatter.

## One-Line Takeaways

- Cost-aware RAG (2610.37358) separates efficient retrieval from reliable answers.
- Parallel macro-adaptive reasoning (MAPS, 2610.29792) beats sequential RAG across benchmarks.
- Multimodal document RAG bottlenecks are often generation-side, not retrieval-side (2610.21318).
- Agentic routing (RouteDRAG, 2610.36444) cuts calls while improving accuracy.
- Visual evidence presentation matters more than raw retrieval gains (2610.21318).
- Attack Success Rate hides defense blind spots; poisoning eval needs reforging (2610.40742).
