# RAG Reading Group — Literature Scan Digest

**Theme:** Retrieval-Augmented Generation (RAG)
**Scope:** Recent arXiv preprints scanned from four angles: core RAG methods, agentic/multi-step retrieval, long-context vs. retrieval, and RAG evaluation/benchmarks.
**Selected:** 6 preprints, each assigned to exactly one theme (efficiency, reasoning, multimodality, safety).

---

## Selected Papers

### 1. When Is Additional Retrieval Worthwhile? A Cost-Aware Study of Evidence Gain and Answer Reliability in RAG
- **arXiv:** 2610.37358 (submitted Tue, 27 Oct 2026)
- **Theme:** Efficiency
- **Flag:** MUST-READ
- **Detail:** This reproducible empirical study separates two distinct problems in RAG: retrieving relevant evidence efficiently versus improving the reliability of the generated answer. It shows that evidence recovery does not proportionally reduce total error — premature resolutions and abstentions increase as missing-evidence failures decrease, shifting the bottleneck from guiding search toward required evidence to verifying that the retrieved evidence is sufficient. Useful for anyone tuning retrieval (retriever vs. generator failure attribution, cost-aware retrieval).

### 2. Beyond Retrieval Failure: Understanding Why LLMs Miss Evidence in Multi-Hop RAG
- **arXiv:** 2610.21184 (submitted Thu, 15 Oct 2026)
- **Theme:** Reasoning
- **Flag:** MUST-READ
- **Detail:** Investigates why LLMs miss evidence in multi-hop RAG. Finds that evidence recovery does not produce a proportional reduction in total error: premature resolutions and abstentions increase as missing-evidence failures decrease. The central finding is a shift in the remaining bottleneck, from guiding search toward required evidence to verifying that the retrieved evidence is sufficient. Accepted by DAI 2026 Oral.

### 3. Pix2Evidence: A Multimodal RAG System for Text and Visual Evidence
- **arXiv:** 2610.41335 (submitted Fri, 30 Oct 2026)
- **Theme:** Multimodality
- **Flag:** MUST-READ
- **Detail:** A multimodal RAG system that uses image descriptions to adapt the retriever, then reranks retrieved candidates before answer generation. Extensive experiments show it outperforms state-of-the-art methods: across five widely-used Wikipedia QA benchmarks, non-reranked Pix2Evidence leads the main comparison in answer accuracy on four, and on MMSearch it reaches 26.0%, 4.4 percentage points above PixelRAG. Code and derived data to be released where licensing/privacy permits.

### 4. Retrieved But Not Reliable: A Survey on Attacks, and Defenses in Retrieval-Augmented Generation
- **arXiv:** 2608.24977 (submitted Tue, 25 Aug 2026; v2 Thu, 27 Aug 2026)
- **Theme:** Safety
- **Flag:** MUST-READ
- **Detail:** A 24-page survey (accepted to Findings of ACL EMNLP 2026, peer-reviewed through ARR) summarizing attacks and defenses in RAG, including robustness benchmarks and explainability methods for evaluating and explaining RAG robustness. Covers the security meta-model angle as well as adversarial retrieval, backdoors, and privacy.

### 5. On the Effectiveness of Proposed Techniques to Reduce Energy Consumption in RAG Systems: A Controlled Experiment
- **arXiv:** 2601.02522 (v1 Mon, 5 Jan 2026; v2 Sun, 11 Jan 2026)
- **Theme:** Efficiency
- **Flag:** SKIM
- **Detail:** Presents what appears to be the first comprehensive empirical study on energy-efficient design techniques for RAG systems, with guidance for developers and researchers building sustainable RAG applications. Accepted at ICSE-SEIS'26.

### 6. Agentic AutoRAG: RAG Pipeline Optimization through Reasoning-Driven Agents
- **arXiv:** 2610.08452 (submitted Tue, 6 Oct 2026)
- **Theme:** Reasoning
- **Flag:** SKIM
- **Detail:** An LLM-agent optimizer for multi-objective RAG hyperparameter optimization with retrieval-versus-generation failure attribution. In cost-aware mode on a real-world healthcare corpus it reaches median exam accuracy of 77%, above the strongest baseline's 71.5%, at about 58% of that baseline's cost per query, and matches 70.5% at about 22% of the cost. Accepted at REALM (EMNLP 2026) and ML for Systems Workshop (NeurIPS 2026).

---

## Theme Assignment Rationale

Each paper was assigned to exactly one theme:

- **Efficiency (2 papers):** 2610.37358 (cost-aware retrieval study) and 2601.02522 (energy consumption experiment). Both directly target cost/reliability trade-offs in RAG deployment.
- **Reasoning (2 papers):** 2610.21184 (why LLMs miss evidence in multi-hop RAG) and 2610.08452 (agentic pipeline optimization with failure attribution). Both concern multi-step reasoning over retrieved evidence.
- **Multimodality (1 paper):** 2610.41335 (Pix2Evidence). Directly addresses text + visual evidence retrieval and generation.
- **Safety (1 paper):** 2608.24977 (survey on attacks and defenses). Focused on security/privacy robustness of RAG.

**Runner-up themes (papers that arguably fit two themes):**
- 2610.08463 (UNREAL: Unifying Retrieval and Long-Context with a Single Model) — could be efficiency (FLOPs/time-to-first-token) or reasoning; assigned to efficiency as it unifies retrieval and long-context inference.
- 2610.37826 (DeFT-RAG: Incrementally Decomposing Multi-Hop) — reasoning vs. efficiency; assigned to reasoning.
- 2610.25937 (RAGLeak: Supply-Chain Privacy Backdoors) and 2604.08304 (Survey of Secure RAG) — safety, but also relevant to efficiency/privacy; assigned to safety.
- 2510.15253 (Scaling Beyond Context: Multimodal Retrieval Survey) — multimodality, but also efficiency; assigned to multimodality.

---

## Recent Developments (Web Chatter)

- The RAG platforms market was valued at ~USD 4.00 billion in 2025 and is estimated to reach ~USD 5.52 billion in 2026 (Yahoo Finance, Oct 2026), reflecting industrial adoption.
- Evaluation tooling remains a hot topic: Confident AI, DeepEval, Ragas, lm-evaluation-harness and UK AI Security Evaluation are among the leading open-source RAG evaluation frameworks in 2026, with ongoing debate about LLM-based scoring calibration and adversarial question pairs.
- Knowledge-graph-enhanced RAG is frequently cited in industry chatter (e.g., Vector Institute), bridging the graph-choice and retrieval-hybridization angles.
- Clinical/medical RAG for evidence-based question answering is an active apply domain (Nature Sci Rep 2026).
- Notable absence from the arXiv scans: agentic RAG surveys (e.g., 2501.09136) and the Generative-to-Agentic AI survey (2504.18875) are older than the core recent results; the chatter also mentions long-context vs. retrieval trade-offs (e.g., TrekBench-Ctrl, "The Bottleneck Is Retrieval, Not Reading") that complement the UNREAL paper.

---

## One-Line Takeaways

- Cost-aware retrieval (2610.37358) decoupling evidence gain from answer reliability is key for practical RAG tuning.
- Multi-hop RAG failures shift from retrieval to verification (2610.21184) — verify sufficiency, don't just retrieve more.
- Pix2Evidence (2610.41335) shows text+visual evidence reranking beats text-only SOTA on Wikipedia QA and MMSearch.
- RAG security is maturing into a survey-level field (2608.24977) covering attacks, defenses, benchmarks and explainability.
- Energy-efficient RAG techniques are now empirically characterized (2601.02522), and agentic AutoRAG (2610.08452) delivers ~58% cost with comparable accuracy.

---

*Scan prepared for the reading group. Papers listed under "Selected Papers" are the six most relevant preprints across the four scan angles, each assigned to a single theme.*
