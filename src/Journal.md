# [2026-11-23](https://github.com/MarkBruns/MarkBruns.github.io/blob/main/journal/2026-11-23.md) ... Provenance and Causal Engineering for Agentic Systems

15 weeks · 3 h reading worksession + 2 h lab per week · plus one 60-minute study hour, Mon–Sat, 09:30**

| | |
|---|---|
| **Prerequisites** | Python fluency; basic probability (conditional independence, expectation); command line and Docker. No prior causal inference or provenance background required. |
| **Software** | Python 3.10+, Flowcept, Docker (Redis + MongoDB or LMDB), LangGraph or a minimal agent loop, Jupyter, dagitty, causaloptim (R) or a Python bounds implementation |
| **Core texts** | W3C PROV Primer; PROV-AGENT (arXiv 2508.02866); Flowcept docs; Pearl/Glymour/Jewell *Primer*; Hernán & Robins *Causal Inference: What If*; the evidence-tracing survey (arXiv 2606.04990) |
| **Assessment** | Provenance audit 15% · identification exercises 20% · causal audit 10% · final project 40% · labs and peer review 15% |

> **Core constraint, stated once and enforced throughout.** This course does **not** claim that provenance tooling performs causal inference. It teaches you to separate **provenance reconstruction** — what happened, and what depended on what — from **causal identification** — what would have happened under intervention, which requires statistical assumptions no trace can supply. The two are complementary and not substitutable. Every assessment penalises conflating them.

---

## Course description

Agentic systems built on language models produce execution traces that are rich in detail but poor in causal semantics: a trace can show that a tool output preceded a plan revision, but not whether it caused the revision, whether a different output would have changed it, or how much of the final outcome came from the tool versus the model’s prior context. That gap motivates causal instrumentation. It also justifies a staged posture: explore loosely inside bounded, reversible sandboxes before anyone is affected; then, as impact becomes possible, shift to trace review, human interaction, and review gates. Knowledge grows through editing and refactoring, so provenance should be a living practice—provenance-by-default after the sandbox stage, versioned trace refactoring, and post-hoc causal annotation, including counterfactual replay and ablation where feasible. The rule is not to capture provenance perfectly on the first attempt, but to never let it stop being editable.

This course trains you to instrument agentic workflows with the ORNL/Argonne **PROV-AGENT** schema and the **Flowcept** capture framework, and then to interrogate the resulting traces with identification methods from the Pearl/Rubin tradition. You will leave able to answer two distinct questions and to keep them apart: *What happened in this run, and what evidence supports that reconstruction?* and *What causal claims about this behaviour are actually warranted by the data I have?*

The course is deliberately uncomfortable with its own tools. Weeks 5, 10, 11 and 15 are devoted to the places where provenance is silent, where identification fails, and where a confident answer would be a lie. Reporting "unidentified" with precision is a passing grade, not a failure.

## Learning objectives

By the end of the course you will be able to:

1. **Instrument** a Python agentic workflow with Flowcept, persist provenance to a queryable store (LMDB or MongoDB), and verify the resulting graph round-trips.
2. **Explain** PROV-AGENT's agent-centric entities — `AIModelInvocation`, `AgentTool`, and the `wasInformedBy` relation — and how they extend W3C PROV for agent root-cause analysis.
3. **Distinguish** a provenance-derived dependency graph from a causal DAG, and state precisely which interventional claims the former does and does not license.
4. **Apply** back-door and front-door identification to agent traces where some structure is observed (provenance) and the rest is assumed — and say which is which in writing.
5. **Critique** existing provenance systems for their gaps in claim-level evidence, memory invalidation semantics, and multi-agent responsibility attribution.
6. **Design** a schema extension or a causal analysis plan for one failure mode (hallucination propagation, tool-error cascade, memory poisoning) that is technically defensible and explicit about its untestable assumptions.

## How the course runs

Each week has a 3-hour lecture block and a 2-hour lab. Both are scheduled separately from the daily 09:30 study hour; that hour is yours, and its content is specified in `DAILY-PLAN.md` and in `course.ics` (90 sessions, one per weekday morning plus Saturday).

The study hour follows a fixed rhythm, and the rhythm is part of the pedagogy:

| Day | Focus | Purpose |
|---|---|---|
| Mon | Preview | Arrive at the lecture with questions, not a blank page |
| Tue | Re-derive | Reproduce the week's formalism from memory — the only test re-reading cannot fake |
| Wed | Lab prep | Design the instrumentation before typing; most provenance bugs are design bugs |
| Thu | Exercise | Identification is a motor skill; it needs reps |
| Fri | Critical read | One paper section per week, read adversarially (15 papers a term) |
| Sat | Synthesis | Assumption ledger, retrieval practice on week *n−3*, next week's plan |

**The artefact that carries the course:** `ASSUMPTIONS.md`, a running ledger with one row per assumption — where it enters, whether it is testable with your data, and what would falsify it. Saturday's hour maintains it. By week 15 it is the analytical spine of your final report, and it is graded as part of it.

---

## Part I — Provenance foundations (weeks 1–5)

### Week 1 — Why agent traces are not enough

**Lecture.** Outputs propagate as inputs; errors compound across steps and agents. Two failure modes: *dataflow contamination* (a bad input corrupts downstream state) and *non-determinism* (same prompt, different trajectory). The three-level distinction that organises the course: a log tells you *what*; provenance tells you *what depended on what*; causal inference tells you *what would have changed if*.

**Lab.** Diagnose a deliberately broken four-step agent using print statements only. Document the exact point where your reasoning stalls, and classify the stall: missing dataflow, missing comparison, or missing counterfactual.

**Read.** PROV-AGENT §1–2; survey §1; Flowcept README.

**Honesty checkpoint.** Every diagnosis you produced is a causal claim in disguise ("the retrieval step caused the wrong answer"). Circle them; you will revisit them in week 6.

### Week 2 — W3C PROV and the PROV-AGENT extension

**Lecture.** PROV's core: `Entity`, `Activity`, `Agent`, and the relations `used`, `wasGeneratedBy`, `wasInformedBy`, `wasAssociatedWith`. PROV-AGENT's additions: `AIModelInvocation` for a single prompt→response exchange, `AgentTool` for a tool execution by an agent, and `agent_id` as the linking field that lets a full agent graph be reconstructed. Why `wasInformedBy` is a *dependency* relation and not a counterfactual one.

**Lab.** Hand-construct a PROV-AGENT JSON graph for a three-step interaction. Annotate every edge: observed (recorded by capture) or inferred (you supplied it). The count of inferred edges is the size of your causal assumption set.

**Read.** W3C PROV Primer; PROV-AGENT §3; Flowcept schema docs.

**Honesty checkpoint.** An inferred edge is not a weaker edge; it is a different kind of object. Mark them in a different colour and keep that convention all term.

### Week 3 — Flowcept instrumentation

**Lecture.** The record model: workflows, tasks, and blobs; message-queue streaming (Redis by default, with RabbitMQ, Kafka and Mofka supported) and database-backed storage (MongoDB for queryable deployments, LMDB for file-based runs). The decorators — `@flowcept_task` for function-level capture, `@flowcept` / `with Flowcept()` for workflow context — and the agent adapters, including MCP. Offline buffering versus persistent mode: when in-memory suffices, when you need a database.

**Lab.** Instrument the provided LangGraph agent. Capture model invocations and tool tasks, export the graph, and verify `agent_id` linkage across the whole run. Break the linkage deliberately, then fix it.

**Read.** Flowcept documentation (instrumentation and storage); Flowcept paper (e-Science 2023, arXiv 2308.09004).

**Engineering note.** Decorator and adapter names track a fast-moving project. If a name in this syllabus does not exist in the installed version, the documentation is authoritative and the syllabus is the bug — say so in your lab report.

**Honesty checkpoint.** Capture is not neutral: what the framework records defines what you can later ask. List three questions your trace cannot answer.

### Week 4 — Querying provenance for reconstruction

**Lecture.** Reconstruction as graph traversal: find the first anomalous output, then every task informed by it. Querying by subtype and by task identifiers; reconstructing chains from parent/dependency fields. The Flowcept Agent (LLM-based natural-language querying) and its verification requirement: a natural-language answer about a trace is a hypothesis until it is checked against the raw records.

**Lab.** Given a provenance database from a failed run, write queries that identify (a) the first task producing an anomalous output, (b) every downstream task informed by it, and (c) any model invocation that reused a prior response without verification.

**Read.** Flowcept query docs; survey §3.

**Honesty checkpoint.** Write one sentence per query stating what the query assumes (e.g. "anomaly is detectable from output alone"). Those sentences go in the ledger.

### Week 5 — Provenance limits and the evidence gap

**Lecture.** What PROV-AGENT captures well: order, input–output linkage, tool-argument dependency, agent attribution. What it does not: claim-level support and contradiction, memory invalidation semantics, inter-agent responsibility for propagated false claims. The *semantic taint* problem: an unsupported assumption introduced at step 2 can influence the final output without appearing as a distinct bad entity.

**Lab.** Audit a Flowcept trace for a hallucination-propagation scenario. Map every point where provenance is silent about *why* a claim was accepted rather than challenged.

**Deliverable.** **Provenance audit report (15%)** — instrument an agent, capture a failure, and document what the provenance graph explains and what it leaves unresolved. Graded on the honesty of the second half, not the thoroughness of the first.

**Read.** Survey §§5–6; PROV-AGENT §7.

---

## Part II — Causal identification (weeks 6–10)

### Week 6 — Structural causal models and DAGs

**Lecture.** Endogenous and exogenous variables; structural equations; interventions as graph surgery. Reading a DAG: chains, forks, colliders, d-separation. The central move of the course: treat an agent's execution as a *partially known* causal system — some edges given by provenance, the rest assumed or tested.

**Lab.** Draw the DAG for a two-step retrieval→generation agent. Mark provenance-observed edges versus causal assumptions. Identify the open back-door paths and say which confounder you cannot measure.

**Read.** *A Crash Course in Good and Bad Controls* (arXiv 2103.06108); Pearl/Glymour/Jewell *Primer*, first chapters.

**Honesty checkpoint.** If your DAG has no unobserved variables, you have drawn a wish, not a model.

### Week 7 — The do-operator and identification

**Lecture.** `P(Y | do(X))` versus `P(Y | X)`; confounding as a property of the graph, not the data. The back-door criterion and adjustment formula; the front-door criterion for mediation, with agent reasoning steps as mediators between retrieved evidence and output. What identification means in an agent context: which assumptions licence an estimate of the effect of changing a tool's output.

**Lab.** Apply back-door adjustment by hand to a simulated agent dataset where prompt context confounds tool output. Then explain, in one page, why the provenance graph alone did not specify the adjustment set.

**Read.** Hernán & Robins, *Causal Inference: What If*, Part I (target-trial framing and confounding); dagitty adjustment-set analysis.

**Honesty checkpoint.** Write the adjustment set and the assumption that justifies each variable's inclusion. "Standard practice" is not a justification.

### Week 8 — Counterfactuals and agent behaviour

**Lecture.** The three steps — abduction, action, prediction — and what each requires. Why agent counterfactuals are hard: answering "what if the tool had returned v′" requires a model of how the model *would* have responded, not a record of how it did. Provenance constrains the counterfactual graph (it fixes known dependency edges); it says nothing about functional form.

**Lab.** For a captured run, state one counterfactual question precisely, then list every assumption required. Separate the testable from the untestable. Then write the paragraph you would put in a paper.

**Read.** Hernán & Robins, counterfactual chapters; Pearl *Primer* counterpart; DoWhy documentation for the estimation scaffolding.

**Honesty checkpoint.** An untestable assumption is acceptable; an unstated one is misconduct.

### Week 9 — Partial identification and honest uncertainty

**Lecture.** When effects are not point-identified: bounds and partial identification. Manski bounds for binary outcomes; what they buy (a range that is true under almost no assumptions) and what they cost (width). The pedagogy of "I don't know": reporting identification failure instead of overclaiming.

**Lab.** With a small agent dataset (binary tool success, binary final outcome), compute Manski bounds. Compare with the naive difference in means and explain the gap in causal terms.

**Read.** *Causal Inference: What If* (identification framing); causaloptim (bounds via linear programming); survey's evaluation material.

**Honesty checkpoint.** Report the bounds even when the point estimate is more flattering. Especially then.

### Week 10 — Synthesis: provenance meets causality

**Lecture.** Student-led critique of a published provenance paper from a causal standpoint: which causal claims does it make, and are they licensed? Structured debate: *"`wasInformedBy` is sufficient for root-cause analysis in agentic systems."* Both sides must cite evidence, not intuition.

**Deliverable.** **Causal audit of a provenance paper (10%)** — one page, identifying every point where dependency tracing is presented as, or read as, causal inference.

**Lab.** Debate, then a written synthesis: the licensing table (what each evidence type licenses) becomes a course artefact you will reuse in week 15.

---

## Part III — Integration and applied projects (weeks 11–15)

### Week 11 — Memory, multi-agent systems, and the provenance gap

**Lecture.** Memory provenance: write, update, retrieval, invalidation. The memory-poisoning threat. Multi-agent responsibility: who introduced a false claim, who amplified it, who failed to verify it — and why that is a *unit-level causal question*, not a lookup. Current coverage versus the gaps catalogued in the survey.

**Lab.** Instrument a two-agent handoff. Attempt to attribute a propagated error using captured fields only. Then specify the minimal extra metadata that would settle the attribution, and argue whether it is capturable at all.

**Read.** Survey, memory and multi-agent sections; PROV-AGENT agent-centric relations.

**Honesty checkpoint.** "Agent B caused it" is a counterfactual claim about a run that did not happen. Say which one you mean.

### Week 12 — Designing a causal–provenance study

**Lecture.** From research question to estimand to identification strategy to instrumentation to sensitivity analysis — in that order, because reversing it produces unfalsifiable studies. Two worked examples: temperature and tool-argument hallucination (needs intervention or strong ignorability); an extra retrieved document and answer correctness (mediation, with provenance supplying candidate mediators).

**Deliverable.** **Two-page study design** — question, estimand, DAG, identification strategy, instrumentation plan, and the assumptions you cannot test.

**Lab.** Peer review of draft designs against the four-part template: estimand, identification, instrumentation, sensitivity. Two reviews each, written, with the author's response due within 48 hours.

**Read.** *Causal Inference: What If* (target-trial framing); *Crash Course* again, now that you have a DAG of your own.

---

### Week 13 — Instrumentation clinic

**Lecture.** Common failures: missing `agent_id` linkage, offline buffer overflow, unpersisted large blobs, timestamps that destroy reproducibility. The provenance completeness checklist, derived from PROV-AGENT's entity coverage and the survey's open requirements.

**Lab.** Run the checklist against your own repository; file every gap as an issue with a reproduction. In-class debugging of each other's instrumentation.

**Read.** Flowcept docs (agents, adapters, storage); OpenTelemetry GenAI conventions, as a contrast in what a general observability standard chooses to capture.

---

### Week 14 — Analysis clinic

**Lecture.** Defending a DAG, an adjustment set, and a counterfactual assumption out loud. Peer review structured around three questions: *What does provenance establish? What does causal analysis add? What remains unidentified?*

**Lab.** Swap notebooks. Review two others against the three questions and record dispositions. Then revise your own notebook in response.

**Read.** dagitty documentation and examples; survey's evaluation and benchmark gaps.

---

### Week 15 — Final presentations and synthesis

**Lecture.** Ten-minute presentations, five minutes of questions, timed. Closing synthesis: a decision tree for *when provenance reconstruction suffices and when causal inference is required*. Course retrospective: what would a genuinely integrated causal–provenance system need that no current tool provides?

**Lab.** Presentation session: ten minutes, five minutes of questions, timed. Questions are submitted in writing first, so that the Q&A tests understanding rather than quickness.

**Deliverable.** **Final project (40%)** — instrument an agent, capture data, formulate a causal question, apply an identification strategy, and report findings with explicit limitations. Submit: repository, provenance export, analysis notebook, four-page report, and `ASSUMPTIONS.md`.

**Read.** Your week 1 notes, annotated with what you now know.

---

## Assessment

| Component | Weight | Due | Graded on |
|---|---|---|---|
| Provenance audit report | 15% | Week 5, Saturday | Correctness of capture; completeness of the "what it leaves unresolved" section |
| Causal identification exercises | 20% | Weekly, weeks 6–10 | DAG defensibility; adjustment-set correctness; stated assumptions; honest bounds |
| Causal audit of a provenance paper | 10% | Week 10, Saturday | Precision in naming the conflation, with page references |
| Final project | 40% | Week 15 | End-to-end coherence; identification honesty; reproducibility |
| Labs and peer review | 15% | Continuous | Preparation, quality of critique, response to critique |

Full rubrics: `reference/ASSESSMENT.md`.

**A note on the 20% exercises.** They are marked on the *reasoning*, not the number. An exercise that concludes "not identified under these assumptions, and here is what data would identify it" scores full marks. An exercise that reports a confident estimate with unstated assumptions scores zero, even if the number happens to be right.

## Materials

- **PROV-AGENT** — Souza et al., *Unified Provenance for Tracking AI Agent Interactions in Agentic Workflows*, IEEE eScience 2025. <https://arxiv.org/abs/2508.02866>
- **Flowcept** — documentation <https://flowcept.readthedocs.io/>; source <https://github.com/ORNL/flowcept>; paper <https://arxiv.org/abs/2308.09004>
- **Survey** — *From Agent Traces to Trust: A Survey of Evidence Tracing and Execution Provenance in LLM Agents*. <https://arxiv.org/abs/2606.04990>
- **W3C PROV** — Primer <https://www.w3.org/TR/prov-primer/>; ontology <https://www.w3.org/TR/prov-o/>
- **Pearl, Glymour & Jewell**, *Causal Inference in Statistics: A Primer* — companion material <http://bayes.cs.ucla.edu/PRIMER/>
- **Hernán & Robins**, *Causal Inference: What If* — free book <https://www.hsph.harvard.edu/miguel-hernan/causal-inference-book/>
- **Cinelli, Forney & Pearl**, *A Crash Course in Good and Bad Controls* <https://arxiv.org/abs/2103.06108>
- **dagitty** <https://www.dagitty.net/> · **DoWhy** <https://www.pywhy.org/dowhy/> · **causaloptim** <https://cran.r-project.org/web/packages/causaloptim/>

Annotated bibliography with "read this for X": `reference/READINGS.md`.

## Policies

**Agent and LLM use.** Permitted and expected for code, query writing, and literature triage. Not permitted as the author of a causal claim: any sentence asserting an effect, an attribution, or an assumption must be one you can defend in viva. You must disclose, per artefact, which tools were used and for what. Undisclosed generation of analysis prose is an integrity violation; disclosed use is normal engineering.

**Data and ethics.** Agent traces can contain user text, secrets, and personal data. Use the provided synthetic traces for coursework unless you have written permission otherwise. Redact before capture, not after submission.

**Late work.** Labs are not marked late — they are marked present or absent. The three written deliverables lose 10% per day, to a floor of 50%, because the week 10 audit is an input to the final project.

**Accessibility.** All materials are text-first and screen-reader compatible; no video is required. If a tool needs a GUI, an equivalent CLI path exists in the lab handout; tell the instructor if it does not.

**A note on honesty.** The most valuable sentence you will write this term is some version of: *"This claim requires an assumption I cannot test with the data I have."* The course is designed so that you write it early, often, and without embarrassment.

# [2026-11-21](https://github.com/MarkBruns/MarkBruns.github.io/blob/main/journal/2026-11-21.md) ... The Living Agentic Book — 42-session build sprint.

This is about the architectural evolution of tool calling, native reasoning, and stateless MCP ... we want to really EXPLORE building an agentic personal knowledge engineering utility ... from static LLMs to quasi-persistent agentic ecosystems to something like a "book" that continually gathers information for us to consider, edit, annotate, refactor and contemplate ... realistically, it's not about a final answer -- it's about gathering more knowledge to contemplate ... *not just* TRENDING things such as serious discussions about the [AI-assisted proof of the Reimann hypothesis](https://www.scientificamerican.com/article/the-ai-riemann-hypothesis-proof-is-almost-certainly-true-independent-mathematicians-attest/) and how this sort of thing **opens up** gigantic new vistas in the entire realm of Mathematics and reasoning ... but, more importantly, it's about the more important discoveries that are not so trendy or hyped, ie it's about real agentic ***DISCOVERY*** not about the extra trendy mind poison that gets regurgitated by the propaganda machines that comprise ALL media. 

*DISCOVERY* is not about following retards ... or being a spectator at the Idiot Games that are dished up on the teevee, YouTube, social media or some other trend-compromised source of mind poison.

---

What everybody already knows is that between between late 2022 and now in late 2026, artificial intelligence systems have undergone a rapid, transformative shift in how knowledge is processed ... a fundamental architectural transformation—evolving from passive text-generation engines [which LLMs, including frontier LLM are] into distributed, quasi-persistent agentic ecosystems that don't just do correlative predicting of what a smart person would say the next word is ... but actually start to REASON based on continuous prodding/tweaking/refactoring from humans that are INSIDE the smartest loops ... the smartest AI are emergent organic meta-consciousesses that comprise millions, if not billions, of minds led by or directed by ridiculously capable mathematicians, physicists, scientists, engineers who are all learning agentically as the tools for accomplishing learning themselves are also rapidly getting better ... it's the meta-meta-meta-cognition or recursively-meta meta cognition of AI that is unfolding in front of us ... only FOOLS imagine that they can predict where this is going, but it's akin to when humans moved beyond actions or behaviours and started using language to communicate [in a quasi-persistant fashion] with other humans ... ***God created us to do exactly this ...*** *and I can only speculate as to WHY ... if WHY even matters or is just a human concern.* 

This AI transformation can be thought of as having progressed across four distinct [unplanned, evolving, emerging] stages ... but realize that any *stage* framework is arbitrary -- the framework is only because humans kind of need to think in terms of frameworks or scaffolds as they build things:

1. **External Scaffolding Loops (2023–Mid 2024):** Developers wrapped stateless Large Language Models (LLMs) in external `while` loops (such as ReAct) to simulate agency and invoke external APIs.

2. **Native Reasoning Models (Late 2024–2025):** Reinforcement learning internalized multi-step planning, backtracking, and self-correction directly into the model's inference-time compute, replacing brittle prompt scaffolding with thin, high-precision execution loops.

3. **Standardized Tool Connectivity via MCP (Late 2024–Early 2026):** The Model Context Protocol (MCP) solved the $N \times M$ integration bottleneck, establishing a universal, vendor-neutral standard (under the Linux Foundation's Agentic AI Foundation) for connecting models to tools, resources, and prompts.

4. **Stateless Interoperability & Quasi-Persistent Infrastructure (July 2026–Present):** The `2026-07-28` MCP specification stripped away session-bound protocol state in favor of pure, cacheable HTTP request/response semantics. This drew a clean architectural boundary between **Stateless MCP** (vertical tool execution) and **Agent-to-Agent (A2A)** protocols (horizontal peer delegation), unlocking scale-to-zero microVMs, ephemeral sandboxes, and zero-trust credential injection.

---

## 1. The First Wave: External Tool-Calling Agents (2023–Mid 2024)

Before foundation models possessed native multi-step reasoning, engineers bridged the gap between static text prediction and real-world action by trapping LLMs inside external orchestration loops—most notably the **ReAct (Reason + Act)** pattern (`Thought -> Action -> Observation`).

Ten landmark agents and frameworks defined this foundational era:

| Phase | Agent / Framework | Primary Contribution | Core Mechanism |
| :--- | :--- | :--- | :--- |
| **Unconstrained Loops** *(Early 2023)* | **AutoGPT** | Sparked the autonomous agent wave; chained GPT-4 thoughts to browse, read/write files, and run Python. | Continuous autonomous `while` loop with local file I/O and web search. |
| **Unconstrained Loops** *(Early 2023)* | **BabyAGI** | Popularized task-driven autonomous loops with persistent memory. | Three-agent loop (execution, creation, prioritization) backed by a vector database. |
| **Standardized Tooling** *(Mid 2023)* | **LangChain & LangGraph** | Became the default developer SDK for giving LLMs "hands" before moving to cyclic state graphs. | `AgentExecutor`, ReAct prompt templates, and structured tool wrappers. |
| **Standardized Tooling** *(Mid 2023)* | **OpenAI Code Interpreter** | Most widely adopted consumer tool-calling agent; enabled iterative data analysis and file manipulation. | Sandboxed Python runtime with stdout/stderr inspection and self-debugging. |
| **Standardized Tooling** *(Mid 2023)* | **ChatGPT Plugins** | First mainstream attempt at an external API app-store ecosystem for LLMs. | OpenAPI manifests enabling runtime API selection (e.g., Wolfram, Zapier, Expedia). |
| **Domain & Multi-Agent** *(Late 2023–2024)* | **Devin (Cognition AI)** | First high-profile commercial autonomous AI software engineer. | Sandboxed environment combining a shell, code editor, and browser. |
| **Domain & Multi-Agent** *(Late 2023–2024)* | **SWE-agent & OpenHands** | Defined open-source software engineering agents and Agent-Computer Interfaces (ACIs). | Custom, LLM-ergonomic CLI tools for repository navigation, editing, and test execution. |
| **Domain & Multi-Agent** *(Late 2023–2024)* | **Voyager** | Landmark embodied agent in Minecraft demonstrating continual skill acquisition without weight updates. | Iterative JavaScript code generation (Mineflayer API) stored in a retrievable skill library. |
| **Research Foundations** *(2023–2024)* | **Gorilla & ToolLLM** | Proved open-source LLMs could reliably invoke thousands of real-world APIs without hallucinating arguments. | Retrieval-augmented API documentation paired with specialized fine-tuning. |
| **Domain & Multi-Agent** *(Late 2023–2024)* | **AutoGen & CrewAI** | Popularized role-based multi-agent collaboration to overcome single-agent loop failures. | Structured conversational handoffs across specialized personas (e.g., Coder, Reviewer). |

### Structural Limitations of the Scaffolding Era
While these systems proved that LLMs could act upon external environments, they suffered from severe operational fragility:
* **Compounding Latency & Token Bloat:** Every minor step required a full LLM round-trip, appending raw tool outputs into an ever-expanding context window.
* **Brittle Error Recovery:** Because standard next-token predictors lacked internal lookahead, models frequently repeated identical failing tool calls or fell into infinite retry loops.
* **Custom Glue Code:** Every agent framework maintained proprietary tool adapters, creating massive integration duplication across the ecosystem.

---

## 2. The Paradigm Shift: External Agent Loops vs. Native Reasoning Models

Beginning in late 2024 with the arrival of native reasoning models (such as OpenAI's o1/o3 series, DeepSeek-R1, and Claude's extended thinking models), intelligence migrated **from external Python scaffolding into the model's weights and inference-time compute**.

Rather than forcing a model to "think" by printing thoughts into an external framework loop, reasoning models are trained via **Reinforcement Learning (RL)** on verifiable outcomes (mathematics, software engineering, formal logic) to generate hidden **Chain-of-Thought (CoT)** tokens prior to emitting an answer or tool call.

### Architectural Comparison

| Dimension | External Agent Loops (2023–2024) | Native Reasoning Models (Late 2024–Present) |
| :--- | :--- | :--- |
| **Location of Reasoning** | **External:** Orchestrated by application code (LangChain, AutoGPT). | **Internal:** Executed inside hidden `<thought>` tokens during inference. |
| **Training Paradigm** | Next-token pretraining + SFT + prompt engineering (`"Think step by step"`). | Reinforcement Learning (RL) optimizing verifiable task completion. |
| **Error Detection & Recovery** | Reactive: Requires executing a failing tool call and reading a stack trace to retry. | Proactive: Simulates edge cases, backtracks, and self-corrects *before* calling a tool. |
| **Tool-Calling Pattern** | Sequential guessing (`call -> observe -> guess next call`). | Upfront dependency mapping and batched, high-precision tool execution. |
| **Primary Bottleneck** | Context bloat, infinite loops, and network round-trip latency. | Upfront inference compute cost and time-to-first-token latency. |

### Why Modern Agents Combine Reasoning with Thin Loops
Native reasoning did not render agent harnesses obsolete; instead, it **inverted their complexity**:
* **Fewer Steps, Higher Precision:** Where a 2023 agent might burn 30 sequential loop iterations guessing API parameters, a reasoning model deliberates internally for 15 seconds and resolves the task in 3 deterministic tool calls.
* **Thin Execution Harnesses:** Heavy orchestration abstractions designed to compensate for weak reasoning gave way to lightweight execution loops where the model owns the plan and the runtime simply dispatches standardized tool calls.

---

## 3. Standardizing Connectivity: The Rise and Evolution of MCP

Introduced by Anthropic in November 2024 and donated to the Linux Foundation's **Agentic AI Foundation (AAIF)** in December 2025 alongside OpenAI, Google, Microsoft, AWS, and Cloudflare, the **Model Context Protocol (MCP)** became the universal standard for agent-to-tool integration.

### How MCP Transformed Tool Calling
* **Eliminating the $N \times M$ Integration Problem:** Instead of writing custom connectors for every combination of $N$ AI clients and $M$ data sources, developers build one MCP server per service ($N + M$), functioning much like USB-C for hardware or the Language Server Protocol (LSP) for IDEs.
* **Decoupled Primitives:** MCP standardized tool servers around three core capabilities: **Tools** (executable functions), **Resources** (read-only contextual data), and **Prompts** (reusable workflow templates).
* **Runtime Schema Discovery:** Agents dynamically query servers at runtime to inspect available tools and JSON schemas rather than hardcoding static definitions.

### Overcoming Early Scaling Bottlenecks
As organizations moved MCP from local developer laptops into enterprise production, three critical optimizations emerged around the protocol:
1. **Lazy-Loaded Tool Search:** Connecting dozens of MCP servers initially flooded system prompts with hundreds of tool definitions, consuming tens of thousands of tokens before a conversation even began. Modern harnesses use dynamic tool search and progressive disclosure—paired with modular workflow guides (**Agent Skills / `SKILL.md`**)—to load schemas only when relevant.
2. **Code Mode (Programmatic Tool Calling):** For data-intensive operations, agents increasingly write short sandboxed Python or TypeScript scripts that invoke multiple MCP tools programmatically, filter large payloads locally, and return only concise summaries to the LLM context.
3. **Enterprise MCP Gateways:** Organizations route agent traffic through centralized gateways (e.g., Cloudflare, Kong, LiteLLM) to enforce OAuth 2.1 authentication, fine-grained RBAC, audit logging, and prompt-injection defense.

---

## 4. The July 2026 Inflection Point: Stateless MCP (`2026-07-28`)

Early remote MCP deployments relied on persistent HTTP+SSE (Server-Sent Events) connections, stateful initialization handshakes, and sticky `Mcp-Session-Id` headers. While workable on local machines, sticky sessions created severe friction for horizontal cloud scaling, serverless functions, and edge routing.

On **July 28, 2026**, the MCP specification (`2026-07-28`) overhauled the protocol core into a **purely stateless HTTP request/response architecture**.

### Key Technical Changes in `2026-07-28`
* **Removal of Handshakes and Session IDs:** The mandatory `initialize` / `initialized` lifecycle handshake and `Mcp-Session-Id` header were eliminated. Every HTTP request is self-contained, carrying protocol version, client capabilities, and distributed trace metadata inside a standardized `_meta` object.
* **HTTP Header-Based Routing (`Mcp-Method` & `Mcp-Name`):** Streamable HTTP requests now expose the RPC method and target tool/resource name directly in HTTP headers. Load balancers, API gateways, and WAFs can route, rate-limit, and authorize calls at the HTTP layer without parsing JSON-RPC bodies.
* **Native Cache Control (`ttlMs` & `cacheScope`):** Because tool lists (`tools/list`) and static resources are decoupled from ephemeral sessions, servers return explicit cache TTL and scope directives, enabling CDNs and clients to cache schemas cleanly.
* **Multi Round-Trip Requests (MRTR) & Tasks Extension:** To replace bidirectional server-to-client push prompts without persistent sockets, interactive user approvals/elicitations now pass explicit `requestState` tokens across discrete HTTP turns (MRTR). Long-running operations were moved into an optional, standardized **Tasks Extension** backed by durable task IDs.
* **Deprecation of Legacy Stateful Primitives:** Server-initiated `Sampling`, `Roots`, `Logging`, and legacy `HTTP+SSE` transports were formally deprecated in favor of a lean, predictable core.

---

## 5. Reshaping Multi-Agent Systems: Stateless MCP vs. A2A Protocols

Under the Linux Foundation's Agentic AI Foundation (AAIF), two complementary open standards govern modern agentic systems: **MCP** and the **Agent2Agent (A2A) protocol** (originally introduced by Google and reaching v1.0 in early 2026).

Prior to July 2026, stateful MCP sessions and server-initiated `Sampling` blurred the boundary between tools and agents, leading developers to build fragile "MCP-as-A2A" nested loops. The stateless `2026-07-28` MCP release established a clean, permanent separation of concerns:

| Architectural Dimension | Stateless MCP (`2026-07-28`) | A2A Protocol (`v1.0+`) |
| :--- | :--- | :--- |
| **Core Abstraction** | **Vertical Tool Execution:** Invoking a deterministic function, API, or datastore. | **Horizontal Peer Delegation:** Collaborating with an autonomous, opaque peer agent. |
| **Protocol State** | **Stateless at the wire layer** (self-contained HTTP requests). | **Stateful task lifecycles** (maintains multi-turn negotiation, memory, and artifact state). |
| **Discovery Mechanism** | `tools/list` & `server/discover` (schema-first, CDN-cacheable). | **Agent Cards** (JSON manifests advertising high-level skills, modalities, and auth). |
| **Interaction Pattern** | Fast request/response (or async Task polling for batch jobs). | Multi-turn dialogue, clarification requests, streaming artifacts, and push webhooks. |
| **Internal Transparency** | **Transparent:** Caller sees exact input schemas and structured outputs. | **Opaque:** Caller treats the peer as a black box without seeing its internal prompts or tools. |

### Three Ways Stateless MCP Changed A2A Topologies
1. **Eliminating Protocol Overlap:** Deprecating MCP `Sampling` ended the practice of MCP servers hijacking a client's LLM for sub-reasoning. True multi-agent delegation—where independent reasoning agents negotiate ambiguity and maintain shared task context—now lives exclusively on **A2A**.
2. **The Two-Tier "Horizontal A2A / Vertical MCP" Stack:** Modern enterprise topologies separate coordination from execution. A Supervisor Agent delegates a high-level goal horizontally via **A2A** to a specialized Domain Agent (e.g., Security Auditor), which in turn executes dozens of vertical **Stateless MCP** calls against shared serverless tool pools without session collisions.
3. **Dual-Interface Lightweight Sub-Agents:** For deterministic agent skills that do not require multi-turn clarification, A2A servers increasingly expose those skills simultaneously as stateless MCP tools—allowing orchestrators to invoke them as simple, cacheable function calls.

---

## 6. Infrastructure Proliferation: Quasi-Persistent Agents & Ephemeral Compute

The deepest impact of stateless interoperability lies in cloud infrastructure. By decoupling **protocol state** (held in explicit tokens like `requestState`, MCP `taskId`, and A2A `Task` objects) from **compute state**, teams no longer need to keep heavy containers running continuously just to preserve an open TCP/SSE session.

This unlocked **quasi-persistent agents**: workspaces that feel continuous and stateful to the user while hibernating to zero compute cost between tool calls.

### Five Emerging Infrastructure Patterns

1. **Snapshot-and-Hibernate MicroVMs (Scale-to-Zero Workspaces):**  
   Using Firecracker microVMs, AWS Lambda MicroVMs, or Kubernetes Agent Sandboxes, an agent boots a workspace in under 200ms, clones a repository, and runs tests. While the orchestrator's reasoning model spends 45 seconds analyzing results, the microVM's memory and filesystem are snapshotted and **paused to zero billing**. When the next stateless MCP HTTP request arrives, the gateway wakes the exact snapshot in milliseconds with zero handshake overhead.
2. **Control Plane vs. Heavy Sandbox Separation:**  
   The A2A server and MCP client loop run inside ultra-lightweight, durable edge isolates (such as Cloudflare Durable Objects or V8 isolates) that persist conversation state cheaply. Heavy container images (housing compilers, headless browsers, or GPU runtimes) attach dynamically *only* during active stateless MCP tool execution and detach immediately afterward.
3. **Lean Immutable Base Images + Just-in-Time Hydration:**  
   Instead of shipping monolithic 10GB+ "kitchen-sink" container images, teams deploy minimal, read-only base images paired with copy-on-write (CoW) storage layers (e.g., overlayfs or ZFS clones) for workspace files, while specialized tools run as independent, horizontally auto-scaled serverless MCP pools.
4. **Crash-Resilient Asynchronous Execution (`Tasks` Extension):**  
   For long-running builds or deep research jobs, a worker container immediately returns a durable `taskId` (`status: "working"`), streams progress to an external durable **Task Store** (Redis, Postgres, or DynamoDB), and can terminate cleanly upon completion. Any stateless node can serve subsequent `tasks/get` polls across container restarts or pod migrations.
5. **Ephemeral, Zero-Trust Credential Injection:**  
   Because containers hibernate, migrate, and self-destruct rapidly, long-lived secrets are never baked into container images or environment variables. API gateways inspect incoming stateless MCP/A2A authorization headers and inject short-lived, single-call scoped tokens at the exact moment a sandbox wakes—leaving zero residual credentials on disk when the sandbox freezes.

### Infrastructure Lifecycle Comparison

| Lifecycle Phase | Stateful Era (2023–Early 2026) | Stateless Interop Era (Late 2026+) |
| :--- | :--- | :--- |
| **Cold Start** | Boot heavy container -> run MCP `initialize` handshake -> fetch 50 tool schemas. | Wake microVM snapshot (<200ms) -> zero handshake -> read cached schemas (`ttlMs`). |
| **Idle / LLM Reasoning** | Container remains active and billed to keep persistent SSE socket alive. | MicroVM freezes RAM/disk to snapshot; **zero active compute billed**. |
| **Tool Routing** | Sticky load balancing required to reach the exact process holding session memory. | Stateless HTTP header routing (`Mcp-Method` / `Mcp-Name`) to woken sandbox or serverless pool. |
| **Long-Running Jobs** | Vulnerable to HTTP timeouts or dropped connections killing agent state. | Durable `taskId` written to external Task Store; survives worker/container termination. |
| **Security & Teardown** | Long-lived env secrets in container; manual garbage collection on session expiry. | Single-call gateway token injection; instant hibernation or teardown with zero residual secrets. |

---

## 7. Summary Synthesis: The Four-Year Trajectory

| Era | Dominant Pattern | Where Intelligence Lives | Where State Lives | Primary Bottleneck Solved |
| :--- | :--- | :--- | :--- | :--- |
| **2022–2023** | Pure LLMs | Model weights (single-turn text) | Prompt window only | Generating fluent natural language |
| **2023–2024** | External Agent Loops | Python scaffolding (`while` loops, ReAct) | In-memory framework objects | Giving LLMs access to external APIs and code |
| **2024–2025** | Native Reasoning + Early MCP | RL-trained internal Chain-of-Thought | Sticky MCP `HTTP+SSE` sessions | Multi-step planning reliability & $N \times M$ tool glue |
| **Late 2026+** | Stateless MCP + A2A + MicroVMs | Reasoning models + collaborative A2A peers | Externalized tokens (`requestState`, `taskId`) & CoW snapshots | Horizontal cloud scalability, cost-to-zero hibernation, & enterprise zero-trust |

# [2026-11-16](https://github.com/MarkBruns/MarkBruns.github.io/blob/main/journal/2026-11-16.md) ... autodidactic learning, using agentic tools

EVEN the process of learning how to learn itself has to become autodidactic ... it's not necessarily efficient -- in fact, that's the point. One has to learn how rethink the learning process and break down the steps of how one learns ... from the first principles of first principles thinking.

In this particular case I downloaded [HerdR](https://herdr.dev/tui/docs/concepts/), Herdr is terminal workspace manager to keep terminal processes running, with structure around them. In HerdR, you use workspace as the top-level project container, one workspace per repo, task, or investigation. A workspace owns tabs and panes. Its sidebar state rolls up from the agents inside it -- thus, you monitor which running project needs attention. 

Inside of the HerdR workspace managers, I use pi.dev with an OpenRouter subscription.  I could do this with any AI agent, like DeepSeek or Google mode, but I use pi.dev to monitor how well the model performs and what it costs, ie it's PENNIES per instruction ... so that I understand how the agentic process works and how to trace/monitor/debug it. Doing this ... using HerdR, pi.dev and OpenRouter is NOT exactly the cheapest way to do this -- it is the way that gives me experience with HerdR, pi.dev and OpenRouter doing something extremely mundane ... so that I develop skills in workplace mgmt, coding harnesses and different open weight models.

For [today's journal entry](https://github.com/MarkBruns/MarkBruns.github.io/blob/main/journal/2026-11-16.md), I started with another very mundane task of working through the process of developing a FULL narrative for W1 of 10/13/26 W1, the first Workshop in the series from [2026-11-13](https://github.com/MarkBruns/MarkBruns.github.io/blob/main/journal/2026-11-13.md).

# [2026-11-13](https://github.com/MarkBruns/MarkBruns.github.io/blob/main/journal/2026-11-13.md) ... 40-session Observability Engineering For Multi-Agent Harness Engineering

This 40 workshop (*"W" is for "workshop", eg W1 is Workshop 1) curriculum deliberately does not make anyone "fluent" in anything.

W0 that is implicitly part of any 40 W series like this, involves READING THROUGH THE FULL WORKSHOP SERIES first ... and then revising, refactoring, and rethinking the prompts that led to this series of workshops and asking for assistance, BASED ON A SERIOUS READ THROUGH OF THE SYLLABUS, for help in improving, deepening, re-focusing the workshop per your ruminations on what jumps out at you or concerns you or excites you, ie the workshop series is not yours until you re-mastered it to make it your own ... LEARN to be more critical, more autodidactic ... stop accepting the teacher's syllabus.

Completing this serie's W1–W8 should give you a control group; W9–W18 make you go deep enough in one framework to generate real judgment; W19–W26 show you how the deployment environment rewrites the rules of security and evidence; W27–W34 turn security from "configuration" into "runtime adjudication"; W35–W40 compress experience into a transferable judgment tool ... that's the 40 workshop series as it currently exists, but your first assignment is to read through the whole thing and make it better.  Devise your own desired outcomes specific for your own needs -- for example: if the audit schemas you produce at W15 and W37 are solid, the 40 workshops have succeeded — because your first reaction to any new framework afterward will be something like "how do this system's checkpoint feed my schema," rather than just "how many GitHub stars does it have."

**The course (see the [full Workshop in the 2026-11-13 Journal entry](https://github.com/MarkBruns/MarkBruns.github.io/blob/main/journal/2026-11-13.md)) is feasible, but tough -- first, understand what the goal is.** 20 days × 6 hours = 120 hours, 40 workshops. Those are designed to be 120 **intense** hours, ie ***intense hours*** are *hours that make you almost want to give up, eg like trying to do ONE MORE push-up than you can actually do, thinking this is just a bit too hard for me* ... in other words, three hours/day in a workshop should be about as much as you want to dive into in a day, whereas four hours would be "my cup runneth over" time.

40 X 3 hr workshop for the full 120 intense hours of dedicated project learning is still not going to be enough to reach production-grade fluency in any single framework, let alone "master" all competitors in that framework's industry. But it should be enough to build a **transferable judgment framework** in which you learn how to ask smarter, shrewder, tougher questions ... specifically, after completing this workshop [and extending it for your own specific interests/use cases], you should be able to ask useful questions about where each orchestration model leaks on observability and security, why it leaks, and what patches the leak. The take away should not be "I know LangGraph." It should be "I can tell, within an hour or two of experimenting and using, where a new framework's audit evidence chain breaks."

The sequence below is **depth first, breadth second, attack-and-defend throughout**. LangGraph gets ~40%, competitors and contrasts ~30%, security and observability woven through ~30%. 

Every workshop has a concrete deliverable ... there's no "just watch some YouTube vids on how to do this" — to complete the workshop you have to build something concrete that actually works and you can show to others.



# [2026-11-07](https://github.com/MarkBruns/MarkBruns.github.io/blob/main/journal/2026-11-07.md) ...  Optimal Stopping for Multi-Agent and Iterative Agent Systems

**Optimal stopping for multi-agent and iterative agent systems is best understood as a satisficing control problem under bounded rationality**, not pure optimization. Herbert Simon’s satisficing (search until an option is “good enough” given aspiration levels and resource constraints) maps cleanly onto agent loops: the orchestrator or the agent itself monitors signals of marginal progress, evidence sufficiency, consensus irreversibility, semantic stability, and budget exhaustion, then intervenes before quality plateaus or degrades and before token costs compound.

## The Core Empirical Reality: Iteration Often Does Not Pay

Recent controlled studies show that fixed iteration is frequently wasteful and can be actively harmful:

- In the Semantic Early-Stopping study (arXiv:2606.27009, open implementation at SahilShrivastava-Dev/semantic-halting-problem), on HotpotQA multi-hop RAG, **iteration did not improve measured Information Score—it slightly hurt it**. The single best practical policy was `fixed_k1` (return the first grounded draft): ~86% token reduction versus `max_iterations` while matching or exceeding quality. A judge-free semantic stopper (cosine distance on local embeddings with patience window \(k=2\)) cut operational tokens ~38% at parity quality. The full quality-gated variant was counterproductive because per-round LLM judging dominated cost. An oracle that picks the best intermediate round still beats practical policies by a large margin (+0.115 Information Score), confirming that “when to stop” is relatively easy while “which round is best” remains open. The authors note a benchmark caveat: HotpotQA answers are short and often answerable from one draft, so long-form generation tasks are needed to test whether iteration ever accrues value.

- Multi-agent debate literature (including the debate-fatigue hypothesis and work on adaptive stopping) shows non-monotonic quality curves: early rounds improve reasoning, later rounds produce sycophantic conformity, problem drift, or “talk past” a correct answer. Adaptive rules can recover ~98.7% of oracle performance at up to ~50% cost reduction. Related findings indicate that stopping at the first correct prefix can improve accuracy substantially over letting the model continue.

- Harmful overthinking (flipping a correct intermediate answer to an incorrect one) is largely untouched by pure token-budget or simple patience windows. Token controls and syntactic kill-switches stop verbose overthinking but do little for logical drift. Training-time interventions or stronger probes are likely required for the latter.

These results support a practical rule of thumb: **default to the earliest grounded or high-confidence output unless a cheap signal shows clear continued improvement**. Additional Critic, debate, or refinement rounds are often pure cost on many RAG and short-answer tasks.

## Stronger Algorithmic Approaches Beyond Simple Patience

- **Re-FORC** (Adaptive Reward Prediction for Efficient Chain-of-Thought, ICML 2026, arXiv:2511.02130). A lightweight adapter predicts expected future reward as a function of remaining thinking tokens. Combined with a greedy policy inspired by Pandora’s box / Gittins-index ideas, it enables early stopping of unpromising chains (up to ~24–26% compute reduction versus fixed budgets at maintained accuracy), dynamic model-size selection, and adaptive test-time scaling. It addresses the “which round / how much compute is best” question more directly than pure geometric convergence.

- **REFRAIN** (“Stop When Enough: Adaptive Early-Stopping for Chain-of-Thought Reasoning”, ACL 2026 / arXiv:2510.10103). Training-free two-stage stop discriminator (reflective yet redundant reasoning via semantic similarity + trigger cues) plus a sliding-window Upper Confidence Bound (SW-UCB) multi-armed bandit that adapts thresholds by problem difficulty. Reports 20–55% token reduction while maintaining or improving accuracy across benchmarks and model families, shifting the accuracy–efficiency frontier.

- **EMS (Efficient Majority-then-Stopping)** and related sequential voting / consensus mechanisms remain among the most practical for multi-agent aggregation: reliability-ordered invocation plus early termination once a majority cannot be overturned yields ~32–35% fewer agents and ~44% fewer tokens at preserved accuracy.

- Probe-based methods (hidden-state failure predictors, answer-stability probes, BELT-style belief probes) and early-abort cascades continue to show 40–60% token savings at high recall targets, with some transfer from math to coding/agentic environments.

Classical multi-agent optimal stopping / mean-field optimal stopping (MAOS/MFOS, ICML 2025) and Bayesian social-learning formulations provide theoretical grounding (threshold policies on belief space, dynamic programming principles), but they are farther from drop-in libraries.

## Pattern Libraries, Orchestration Blueprints, and Guardrails

Mature practical resources live in pattern catalogs and safety primitives rather than a single “optimal stopping library”:

- **Awesome Agentic Patterns** (nibzard/awesome-agentic-patterns, also agentic-patterns.com): Includes the Adaptive Sandbox Fan-Out Controller. Start a small batch (N=3–5), sample early signals (success rate, diversity, judge confidence/winner margin, error clustering), then decide to scale up, **stop early**, refine the prompt, or decompose. Uses hysteresis (asymmetric thresholds) to avoid oscillation and hard budget/no-progress guards. Directly useful for best-of-N or parallel sampling pipelines where fixed N wastes money. Related patterns cover circuit breakers, stop hooks, and sub-agent spawning with isolation.

- **EPIC Mode blueprint** (Episodic Policy and Intention Control; DEV Community / frontier.catgameresearch.net): An architecture proposal for an orchestrator that sets per-subtask token/time/confidence budgets, computes a composite overthink score, and runs an intervention ladder (switch to System-1, refactor, spike-and-delegate, escalate). Frames the problem explicitly as bounded rationality / satisficing. Useful as a reference architecture with noted gaps.

- Hard safety and halt primitives:
  - **agent-guardrails-mcp** (samcsta/agent-guardrails-mcp): MCP server exposing pre-dispatch health gates, per-target circuit breakers, and halt primitives (single agent, group, or entire engagement). Agents check `check_halt` before actions. Persistent SQLite option. This is an external kill-switch, not a semantic quality detector—the necessary backstop.
  - **SafeHarbor** (ljj-cyber/SafeHarbor, ICML 2026): Training-free hierarchical memory-augmented guardrail that extracts context-aware defense rules, injects them dynamically, and self-evolves the memory tree. Aims at precise decision boundaries (high refusal on harmful requests while preserving benign utility). Relevant when “hallucination sets in” includes safety-critical drift.
  - Other practical layers: agent-cost-guardrails, TokenOps, agent-budget-guard, MCP proxies (mcp-guard, agent-guardrail), Microsoft Agent Governance Toolkit cost controls, LangGraph recursion_limit + conditional edges/interrupts, and tool-call similarity loop detectors.

Other pattern catalogs (koydas/agent-patterns with loop-with-guard and validator-first, reaatech/agentic-arch-patterns with confidence gates and circuit breakers, various Agentic Design Patterns collections) reinforce the same primitives: explicit terminal states, budget caps, similarity/loop breakers, and external halt capability.

## Practical Synthesis for 99% Value at ~33% Token Cost

The efficiency half of the goal is achievable today with relatively simple, judge-free signals plus hard envelopes:

1. Hard envelope always on (step/token/USD budgets, recursion limits, tool-call similarity breakers, circuit breakers, external halt MCP).
2. Cheap semantic or consensus signal (embedding cosine-distance patience, answer stability, irreversible majority, critic approval, or a lightweight probe).
3. Prefer the earliest grounded output unless clear improvement is detected; default to `fixed_k1` or short patience on many RAG-style tasks.
4. For parallel best-of-N or sandboxed fan-out, use the adaptive controller pattern with hysteresis and early-signal sampling rather than fixed N.
5. Log full trajectories for later oracle-style analysis and to distill reusable stopping rules (CONVOLVE-style context engineering or playbooks).
6. Treat “find the best intermediate state” as an open research problem; oracles still win substantially. Re-FORC-style future-reward predictors or learned best-round models are promising but heavier to implement.

Communities and ongoing work are concentrated in arXiv (cs.AI, cs.MA, cs.LG), ICML/NeurIPS/ACL workshops on efficient reasoning and agentic uncertainty, Reddit r/AI_Agents and r/LLMDevs (tokenomics lists, runaway-loop post-mortems, concrete threshold checklists), the Awesome Agentic Patterns ecosystem, and framework Discord/GitHub discussions around LangGraph, AutoGen, CrewAI, Hermes, and MCP. The field is moving from fixed caps toward signal-driven satisficing, but the largest remaining gap is reliably identifying the single best intermediate output rather than merely detecting that further iteration has stopped helping.

Start with the SHP repo + Adaptive Sandbox Fan-Out pattern + one cost/halt MCP for immediate leverage, then layer Re-FORC- or REFRAIN-style predictors if you need finer control over the accuracy–cost frontier. The “plenty good enough” point is usually earlier than intuition suggests.

---

## Sources and References

### Core Papers

- Semantic Early-Stopping for Iterative LLM Agent Loops (SHP). arXiv:2606.27009. https://arxiv.org/abs/2606.27009  
  Open implementation: https://github.com/SahilShrivastava-Dev/semantic-halting-problem

- Re-FORC: Adaptive Reward Prediction for Efficient Chain-of-Thought Reasoning. ICML 2026. arXiv:2511.02130. https://arxiv.org/abs/2511.02130

- Stop When Enough: Adaptive Early-Stopping for Chain-of-Thought Reasoning (REFRAIN). ACL 2026. arXiv:2510.10103. https://arxiv.org/abs/2510.10103

- SafeHarbor: Defining Precise Decision Boundaries via Hierarchical Memory-Augmented Guardrail for LLM Agent Safety. ICML 2026. arXiv:2605.05704. https://arxiv.org/abs/2605.05704

### Pattern Libraries and Blueprints

- Awesome Agentic Patterns (including Adaptive Sandbox Fan-Out Controller). https://github.com/nibzard/awesome-agentic-patterns  
  Website: https://agentic-patterns.com

- EPIC Mode: A Blueprint for Stopping Agent Overthinking. https://dev.to/p3ngu1nzz/epic-mode-a-blueprint-for-stopping-agent-overthinking-1ahc  
  Full article: https://frontier.catgameresearch.net/epic-mode.html

- agent-patterns (koydas). https://github.com/koydas/agent-patterns

- agentic-arch-patterns (reaatech). https://github.com/reaatech/agentic-arch-patterns

### Guardrails and MCP Servers

- agent-guardrails-mcp (samcsta). https://github.com/samcsta/agent-guardrails-mcp  
  MCP listing: https://lobehub.com/pl/mcp/samcsta-agent-guardrails-mcp

- SafeHarbor repository. https://github.com/ljj-cyber/SafeHarbor

- Additional practical guardrail projects referenced: mcp-guard (sidclawhq), agent-guardrail (rudimentall1), and related MCP proxies.

### Related Concepts and Communities

- Multi-agent optimal stopping / mean-field optimal stopping literature (ICML 2025 and related works).
- Debate-fatigue and adaptive stopping results in multi-agent debate papers.
- Communities: arXiv (cs.AI, cs.MA, cs.LG), Reddit r/AI_Agents and r/LLMDevs, framework discussions (LangGraph, AutoGen, CrewAI, Hermes, MCP).

---

# [2026-11-06](https://github.com/MarkBruns/MarkBruns.github.io/blob/main/journal/2026-11-06.md)

Agents have made me more conscious of how my words might cause others to think or how articulating the thoughts shapes/clarifies how I think ... thinking is fundamentally about sharing the gratitude and joy and faith in Jesus Christ ... it all comes back to imitation and adoration of Jesus Christ, and how Jesus Christ reached out to others, made friends and humbly stayed as anonymous as possible, EXCEPT for the part of encouraging his agents to go forth and share the message.

This is about sharing a message of intense gratitude!

*Am I grateful enough?* Clearly, NO ... of course not! It's really quite impossible to sufficiently grateful to God for all of the blessing of this existence.

**Most** of my new interactions now have become agentic in nature ... that is to say that the connection was initiated by an agent or as the result of my agentic intelligence gathering and prospecting process ... I prospect, engage, make friends agentically. It is so remarkably better than the OLD way, from 2026 and before that I cannot contain my enthusiasm for importance of ***agentifying*** one's processes.  

**Agentic prospecting so works much better than the inefficient, tedious and wasteful process of travelling, attending conferences, going to seminars** ... agentic intelligence gather opens up vast new frontiers of opportunities to meet people who are working DIRECTLY on extremely interesting things and also happen to be too busy to commute, travel, blow time on non-value-added activities. 

It's NOT really about the automation of processes ... what it's really about is being much, much, much more mindful of the process and improving the process so as not to waste anyone's time or attention.

From the start of any interaction, I need to work at making my agents more *grateful* yet more shrewd as they gather the kind of basic intelligence, eg contact information, what they excel at, which I use to meet people, do business and explore new things. 

Gratitude has always been the most important point of attempting to be a high-agency person ... *otherwise, one is just demanding and manipulative* and interactions are merely transactional ... the world of agents has shift all of us who aggressively use them into having to up our agency game.

A shift toward a more gratitude-driven lifestyle has made my life far better, but it's also made far less willing to waste even **any** time on those who are ungrateful ... lack of gratitude is effectively a lack of faith and it's not just not possible to fix those who lack faith, who fail to exhibit gratitude.

I need to be MORE grateful, more **publicly** and **genuinely** grateful ... among other things, this realization drives home the point that that ***I need to do a much better job of [microblogging on X](https://x.com/MarkBruns) ... OR maintaining my [Gist of Gists](https://gist.github.com/MarkBruns/4b3290aaff421f167b8e47ee59c7b25b), or open source dev skills templates for multi-agent harness engineering.***  

---

# [2026-11-05](https://github.com/MarkBruns/MarkBruns.github.io/blob/main/journal/2026-11-05.md)

I have been duly impressed by the additional pummelling of semiconductor and AI stocks ... in fact, it's actually has sort of made me re-think whether or not there was EVER any reason for optimism about the resiliency of affluent Americans. Those selling stocks might be right -- maybe we should worry about whether or not most people can ever really develop the skills to use AI. Most can't ... they are intellectually capable, but they have been so completely programmed by their media consumption that they cannot develop new skills ... in much of anything.  Teevee watchers,flix watchers or even sports spectators are overwhelming unable to function or learn BECAUSE THEY PASSIVELY CONSUME, ie just watch too much of their content ... PASSIVE content swallowers are always going to make themselves into LOSERS in any environment ... the passive watchers have made themselves psychologically incapable of being high agency people -- they are PROGRAMMED to be helpless victims.

---

# [2026-11-04](https://github.com/MarkBruns/MarkBruns.github.io/blob/main/journal/2026-11-04.md) ...  CI/CD pipelines, observability and AI assistance in debugging flow

Today I had reason to think about WTF [Yarn](https://yarnpkg.com/) is and why do the detailed intracies of package managers matter so much more now for understanding CI/CD pipelines and telemetry or this agentic BASB

---

# [2026-11-03](https://github.com/MarkBruns/MarkBruns.github.io/blob/main/journal/2026-11-03.md) ... I've WON the polyglottery!  I am using pi.dev, Cloudfare, OpenRouter, LangSmith, Nous Research Portal and ... amazed, bewildered and empowered is an understatement!

---

# [2026-11-02](https://github.com/MarkBruns/MarkBruns.github.io/blob/main/journal/2026-11-02.md) ... trading data, intelligence gathering and AI assisted screening -- a PRACTICAL example that begins to illustrate why there's so much incredibly much demand for compute and why that demand is more than ready and willing to pay for services ... and NOW, dammit!

---

# [2026-11-01](https://github.com/MarkBruns/MarkBruns.github.io/blob/main/journal/2026-11-01.md) ... November is month "set aside" for just improving agentic harness engineering skills with practical examples


---


## PREVIOUS Daily Journal Archives

* [Reliable, Self-Improving Multi-Agent Neuro-BASB Ecosystems](https://github.com/MarkBruns/MarkBruns.github.io/blob/main/journal/2026-08-22.md)
* [Hermes Polyglot Orchestrator](https://github.com/MarkBruns/MarkBruns.github.io/blob/main/journal/2026-06-30.md)
* [Implementing the **The Rule of Bruno** Agentified Life](https://github.com/MarkBruns/MarkBruns.github.io/blob/main/journal/2026-06-20.md)
* [Exploration of Agentic OS and GRIT / Jujutsu](https://github.com/MarkBruns/MarkBruns.github.io/blob/main/journal/2026-06-13.md)
* [Impact of Grit DVCS on my PKM](https://github.com/MarkBruns/MarkBruns.github.io/blob/main/journal/2026-06-09.md)
* [Grokify Agentic Productivity Boosting](https://github.com/MarkBruns/MarkBruns.github.io/blob/main/journal/2026-06-08.md)
* [Daily Plan For Coming Week – Rule of Bruno](https://github.com/MarkBruns/MarkBruns.github.io/blob/main/journal/2026-06-07.md)
* [BrunoSoul](https://github.com/MarkBruns/MarkBruns.github.io/blob/main/journal/2026-06-06.md)
* [Portfolio Lifestyle and Market-Based Citizenship Negotiation](https://github.com/MarkBruns/MarkBruns.github.io/blob/main/journal/2026-06-04.md)
* [ALTERNATIVES to Political Conventions](https://github.com/MarkBruns/MarkBruns.github.io/blob/main/journal/2026-06-01.md)
* [Improved NIL Alternative -- Legacy Formation Partnership](https://github.com/MarkBruns/MarkBruns.github.io/blob/main/journal/2026-05-29.md)
* [**Cato FOS** -- My AIservant Faith Operating System](https://github.com/MarkBruns/MarkBruns.github.io/blob/main/journal/2026-05-28.md)
* [Quarq, Hermes Agent, and OpenClaw](https://github.com/MarkBruns/MarkBruns.github.io/blob/main/journal/2026-05-27.md)
* [AGENTIC Knowledge Engineering Project](https://github.com/MarkBruns/MarkBruns.github.io/blob/main/journal/2026-05-26.md)
* [120 Pomodoros Per Week -- Discipline SMART Goal For Summer](https://github.com/MarkBruns/MarkBruns.github.io/blob/main/journal/2026-05-25.md)
* [Salebarn.ORG Core Mission and Cardinal Principles](https://github.com/MarkBruns/MarkBruns.github.io/blob/main/journal/2026-05-22.md)
* [Mastering Grok Heavy + Hermes Agent](https://github.com/MarkBruns/MarkBruns.github.io/blob/main/journal/2026-05-18.md)
* [Digital-First, AI-Driven Education Venture Philanthropy Checklist](https://github.com/MarkBruns/MarkBruns.github.io/blob/main/journal/2026-05-17.md)
* [10-Point Plan to Grow The Merch Portion of a Podcast Side-Hustle Business](https://github.com/MarkBruns/MarkBruns.github.io/blob/main/journal/2026-05-12.md)
* [200 Practical Frontiers for Minimalist, Prayerful Living and Open-Source Innovation](https://github.com/MarkBruns/MarkBruns.github.io/blob/main/journal/2026-05-10.md)
* [ENGR.co, HROS.dev, GYG.be, opportunity finding and luck surface development](https://github.com/MarkBruns/MarkBruns.github.io/blob/main/journal/2026-05-09.md)
* [Starter List Of 200 Best Niche Microenterprise Business Ideas](https://github.com/MarkBruns/MarkBruns.github.io/blob/main/journal/2026-05-08.md)
* [100-Theses New Reformation Critique of the Affluent Western Church](https://github.com/MarkBruns/MarkBruns.github.io/blob/main/journal/2026-05-07.md)
* [Recent Research Publications On Wagyu, Belgian Blue, Similar Double-Muscled / High-Marbling Breeds/Crosses](https://github.com/MarkBruns/MarkBruns.github.io/blob/main/journal/2026-05-06.md)
* [Look To REMOVE The Union Label](https://github.com/MarkBruns/MarkBruns.github.io/blob/main/journal/2026-05-04.md)
* [SprintSpec Online Hub](https://github.com/MarkBruns/MarkBruns.github.io/blob/main/journal/2026-05-01.md)
* [Starter List of 100 Opportunity Finder Technologies](https://github.com/MarkBruns/MarkBruns.github.io/blob/main/journal/2026-04-28.md)
* [WHO Is Doing Interesting Work In The Layers *BELOW* CUDA?](https://github.com/MarkBruns/MarkBruns.github.io/blob/main/journal/2026-04-27.md)
* [Heidelberg Catechism](https://github.com/MarkBruns/MarkBruns.github.io/blob/main/journal/2026-04-26.md)
* [UAVs, UGVs, UUVs, Hybrids, Swarms](https://github.com/MarkBruns/MarkBruns.github.io/blob/main/journal/2026-04-25.md)
* [Relationship-Based Marketing of Perishable Beef Products and Genetics](https://github.com/MarkBruns/MarkBruns.github.io/blob/main/journal/2026-04-24.md)
* [**Make CITIZENSHIP Great Again!** Distributed Self-Defense](https://github.com/MarkBruns/MarkBruns.github.io/blob/main/journal/2026-04-18.md)
* [Agentic Auctioneering and Agentically Mediated Accelerated Negotiation](https://github.com/MarkBruns/MarkBruns.github.io/blob/main/journal/2026-04-17.md)
* [Transformational Discipleship For the Glory of God](https://github.com/MarkBruns/MarkBruns.github.io/blob/main/journal/2026-04-16.md)
* [Pareto Principle—LEADERSHIP -- FIRST Heal the Rot Within](https://github.com/MarkBruns/MarkBruns.github.io/blob/main/journal/2026-04-15.md)
* [Why The Holy Triune God Alone Is Enough](https://github.com/MarkBruns/MarkBruns.github.io/blob/main/journal/2026-04-14.md)
* [200-Module AI/ML Curriculum](https://github.com/MarkBruns/MarkBruns.github.io/blob/main/journal/2026-04-12.md)
* [# 20 Point Personal Lifestyle Plan](https://github.com/MarkBruns/MarkBruns.github.io/blob/main/journal/2026-04-11.md)
* [Salebarn Accelerated Negotiation Platform](https://github.com/MarkBruns/MarkBruns.github.io/blob/main/journal/2026-04-10.md)
* [Top 100 Sought-After Scientists, Engineers, Technicians in Robotics](https://github.com/MarkBruns/MarkBruns.github.io/blob/main/journal/2026-04-06.md)
* [Hard-Won Lessons on Building/Shipping Consumer Social Products](https://github.com/MarkBruns/MarkBruns.github.io/blob/main/journal/2026-04-05.md)
* [10-Step Playbook for Mastering & Generalizing the Career-Ops System](https://github.com/MarkBruns/MarkBruns.github.io/blob/main/journal/2026-04-03.md)
* [Grok's Ultimate Job Acquisition Prompt Template](https://github.com/MarkBruns/MarkBruns.github.io/blob/main/journal/2026-04-02.md)
* [Manifesto for This Disciple of Christ](https://github.com/MarkBruns/MarkBruns.github.io/blob/main/journal/2026-03-29.md)
* [Stop whining about social media! Put your damned gloves on, get in the ring and spar!](https://github.com/MarkBruns/MarkBruns.github.io/blob/main/journal/2026-03-28.md)
* [Noguchi’s Decades-Long Conversations With His Sculptures: Learning to Be Still and Hear God’s Will](https://github.com/MarkBruns/MarkBruns.github.io/blob/main/journal/2026-03-27.md)
* [Open Source Development of ChromaDB ... for GYG](https://github.com/MarkBruns/MarkBruns.github.io/blob/main/journal/2026-03-26.md)
* [High-Density Mobile Hybrid Hazelnut Propagation](https://github.com/MarkBruns/MarkBruns.github.io/blob/main/journal/2026-03-24.md)
* [Faith, Service, Distributed Defense](https://github.com/MarkBruns/MarkBruns.github.io/blob/main/journal/2026-03-23.md)
* [Simplify, Revise, Redo, Refactor Your Clusterfucks](https://github.com/MarkBruns/MarkBruns.github.io/blob/main/journal/2026-03-05.md)
* [Promote Communism, Get Jail Time: Czech Republic Criminalizes Promotion](https://github.com/MarkBruns/MarkBruns.github.io/blob/main/journal/2026-03-03.md)
* [Scriptural basis for "Iran will bless Israel" prophesy](https://github.com/MarkBruns/MarkBruns.github.io/blob/main/journal/2026-02-28.md)
* [Human Trafficking To Support War And Dangerous Political Unrest](https://github.com/MarkBruns/MarkBruns.github.io/blob/main/journal/2026-02-26.md)
* [Manifesto for Christian Voluntaryism](https://github.com/MarkBruns/MarkBruns.github.io/blob/main/journal/2026-02-25.md)
* [Thoughts On Autonomous Communion](https://github.com/MarkBruns/MarkBruns.github.io/blob/main/journal/2026-02-24.md)
* [IronClaw, ZeroClaw, PicoClaw, Nano, Tiny, Mimi, Mobai, Null to *Santa Claws?*](https://github.com/MarkBruns/MarkBruns.github.io/blob/main/journal/2026-02-21.md)
* [100-Point Syllabus: Therapeutic Torpor](https://github.com/MarkBruns/MarkBruns.github.io/blob/main/journal/2026-02-20.md)
* [Opportunity Intelligence for the AI Age](https://github.com/MarkBruns/MarkBruns.github.io/blob/main/journal/2026-02-19.md)
* [Systemic Vulnerabilities in xAI’s Grok Ecosystem](https://github.com/MarkBruns/MarkBruns.github.io/blob/main/journal/2026-02-13.md)
* [The Heritage of Bruno Brunelleschi: A Tale of Big Domes](https://github.com/MarkBruns/MarkBruns.github.io/blob/main/journal/2026-01-31.md)
* ["'MINNESOTA'" is the ancient Viking expression for "'NUT MAGNET'"](https://github.com/MarkBruns/MarkBruns.github.io/blob/main/journal/2026-01-29.md)
* [The Minnesota Political Heritage](https://github.com/MarkBruns/MarkBruns.github.io/blob/main/journal/2026-01-27.md)
* [The Genealogy of Cause](https://github.com/MarkBruns/MarkBruns.github.io/blob/main/journal/2026-01-22.md)
* [Review of Causal Discovery and Inference (2024–2026)](https://github.com/MarkBruns/MarkBruns.github.io/blob/main/journal/2026-01-20.md)
* [Top 100 List: Causal Frontiers 2024–2026](https://github.com/MarkBruns/MarkBruns.github.io/blob/main/journal/2026-01-19.md)
* [Not JUST Polymarket: 100 Prediction Market Alternatives](https://github.com/MarkBruns/MarkBruns.github.io/blob/main/journal/2026-01-17.md)
* [Neurotech/BCI is the Next Big Migration Zone](https://github.com/MarkBruns/MarkBruns.github.io/blob/main/journal/2026-01-15.md)
* [The Scriptural Phenomenology of Self-Transcendence](https://github.com/MarkBruns/MarkBruns.github.io/blob/main/journal/2026-01-14.md)
* [Explore a Radical Constraint Architectures](https://github.com/MarkBruns/MarkBruns.github.io/blob/main/journal/2026-01-09.md)
* [Actualizing 10 Principles for a Life Defined by Meaning](https://github.com/MarkBruns/MarkBruns.github.io/blob/main/journal/2026-01-08.md)
* [Items To Ponder As Advice For My Younger Self](https://github.com/MarkBruns/MarkBruns.github.io/blob/main/journal/2026-01-03.md)
* [PERSONAL Minimalist Living and Basic Needs](https://github.com/MarkBruns/MarkBruns.github.io/blob/main/journal/2026-01-02.md)
* [The BIG WHY: 10 Self-Coaching Principles for Driving Your Life Each Day With Constantly-Redoubled Focus and Intelligent Discipline](https://github.com/MarkBruns/MarkBruns.github.io/blob/main/journal/2026-01-01.md)
* [Year-end review of ventures, projects from 2025 ... Ancient Guy, Ancient Guy PKM, SoilQuality, MarkBruns, TDT GitHub Profile](https://github.com/MarkBruns/MarkBruns.github.io/blob/main/journal/2025-12-31.md)