---
title: "arXiv AI, focused upon Agent Harnesses"
type: project
tags: goals, requirements, deadlines
alias: harnesslab
---

# Agent Harnesses — A 52-Week arXiv Curriculum for a Drop-In Reading Group of Agent Builders

*Free. Peer-led. No ranks. No branding.*

***A year of reading the primary literature of harness engineering — the scaffolding around a model that makes it an agent — then living and revising the plan as you go.*** Plans are always imperfect, but the whole point of planning is not the document; it is the implementing, refactoring, and revising. The POINT of a plan is a starting roadmap that gets overhauled the moment *the real building* starts, because new OPPORTUNITIES (and new preprints, daily) will arise.

The MOST IMPORTANT part of this plan is **gratitude discipline**: there are more good papers than any person can read, and the field is young enough that a careful reader with a year can stand at its frontier. That is abundance. Skimming is a trained skill here, not a failure state.

## 1. What this document is, and what it is not

**Is:** a full year of weekly, 75-minute sessions for a small group (or one reader with a notebook) studying how agentic systems — Hermes, Pi.DEV, OpenClaw-style harnesses, and their kin — are actually engineered. Every week is a named technique with a real preprint behind it: Chain-of-Thought, ReAct, Reflexion, retrieval, memory, multi-agent rosters, protocols, evals, sandboxes. It is written so a person who has never read a paper and has never built an agent can arrive on any week and be genuinely included rather than politely tolerated.

**Is not:** a credential program. No prerequisites, no problem sets, no grades, no graduation. Nothing here makes one participant more important than another; the newcomer equals the veteran.

**Is not:** a course on model training. We read harness papers, not pretraining papers: the model is treated as a fixed organ, and the curriculum studies the body built around it. Fine-tuning appears only where it ships into a harness (skill distillation, tool-use tuning).

Every week has five parts: a **craft work** assignment (reading, sometimes sketching a design), a **hinge practice** (a short named attention exercise), one **concept**, one **quote**, and about four sentences of **teaching** written out so nobody has to improvise a lesson they do not feel ready to give.

The material assumes the leader is not a professor and the participants are not students. It assumes a room of working engineers and curious builders, some of whom ship agents to production and are quietly worried about them. Everything below is written so those people stay for the hour and come back next week.

## 2. How to read a week's entry

Every week is laid out the same way:

- **Craft work.** The reading assignment, labeled *teach*, *repetition*, *capacity*, or *flow* (section 5).
- **Hinge practice.** A named, 8–10 minute attention exercise — a class inside the class.
- **Concept.** One idea, one sentence, carrying the week's technique.
- **Quote.** One short passage — usually from a landmark harness paper — quoted where short enough.
- **Teaching.** Three to five sentences: what the technique means, why it matters to a builder who is tired or new, and how it connects to what the group just read.

Reading the teaching in your own words is fine. Skipping it is *not*: the sentences are the actual lesson, and the reading is the illustration.

## 3. The whole builder: four things we are actually training

A reading habit that only trains comprehension produces a person who can parse a paper and still cannot judge a harness. Each session touches four dimensions:

**The craft dimension** is the obvious one: reading a method, spotting its moving parts, sketching the data flow — prompt in, tool call out, result back. Trainable in an hour, measurable in a season.

**The mental dimension** is being able to *state the mechanism*. "The agent reflects on the failed trajectory and appends the lesson to the next prompt" is a sentence that separates a builder from a spectator. This is why the concept sentence exists.

**The emotional dimension** is what happens at the edge of competence: dense notation, being the least informed person in the circle, saying something wrong out loud. Real stress inside guaranteed safety, where nobody is allowed to mock anybody. We never promise healing; we provide conditions and let time work.

**The humility dimension** is attention to how little anyone knows, including authors. One quote, read twice, sat with in silence. The harness field in particular needs this: our systems are autonomous, ambiguous, and young.

The **hinge practice** is the joint where all four meet: craft (the hand slows the eye), mental (one forced sentence), emotional (a long exhale after hard effort), humility (attention without performance).

## 4. The fixed shape of every session

The session is the same every week. A person who drops in twice a year should recognize the shape instantly; an anxious person should not learn a new format on top of new notation.

| Minutes | Segment | What happens |
|---|---|---|
| 0–5 | Arrival | Paper queued. Anyone new gets the one-page anatomy card (week 1's handout). |
| 5–10 | Circle | Welcome. The week's concept sentence, read aloud. |
| 10–22 | Preparation | The fixed skim ritual: title/authors, abstract, every figure — same order every week. |
| 22–45 | Main craft work | Teach, repetition, capacity, or flow, depending on the week. |
| 45–52 | Conditioning | One equation, one architecture diagram, or one benchmark table — ten minutes, scaled. |
| 52–62 | **Hinge practice** | The named attention exercise, its own segment. |
| 62–72 | Quote circle | Quote read twice. One question. Silence. One sentence each from anyone who speaks. |
| 72–75 | Close | Next week named. Anyone who stays to argue about the paper is welcome. |

Seventy-five minutes. In a brutal week, shorten the main work, never the quote circle.

## 5. The four-week rhythm inside every block

Thirteen blocks of four weeks. Each block has one engineering theme; inside each block:

- **Week one — Teach.** One landmark paper, read slowly. Everyone leaves able to name the technique and state its mechanism. If people are exhausted, too much was covered; if people cannot state the mechanism, too little.
- **Week two — Repetition.** Volume: the same *kind* of paper, five to ten of them, abstract-and-figures passes, including fresh arXiv listings. Correction offered quietly, never publicly.
- **Week three — Capacity.** One hard paper end to end before the session ends. Confusion breaks the set, not time. No all-nighters.
- **Week four — Flow.** Explain one technique from the block in three minutes; longer quote circle; the bring-a-friend week.

## 6. Why the hinge practice sits where it does

The hinge comes after the reading and before the quote circle. After dense technical text, attention is narrowed and defensive; a quote in that state lands on a mind that cannot receive it. Eight minutes of slow, hand-written attention widens the field.

This is also where the curriculum trains what harness engineering itself trains badly: **calm, honest attention to one thing at a time.** Most agent-building produces a person who scans preprints for tricks, hoards links, and retains nothing. What we want instead is a reader who can hold one mechanism in mind without needing an opinion about the whole field. Each hinge practice has three jobs, named aloud when introduced:

1. **Down-regulate.** Hand on paper, pen moving, no screen.
2. **Widen.** One sentence on where this technique sits in the wider harness.
3. **Attend.** The mechanism's one true sentence, or the honest admission that it has none yet.

Standing practices, used across the year: **"One Figure"** (slow eyes on a single diagram, then one written sentence), **"Marginalia"** (three words per section: *claim, mechanism, doubt*), **"The Copy"** (copy the key equation or pseudocode by hand, name every symbol), **"The Long Exhale"** (write the technique's claim, cross out every word that does not survive "how do they know?"), **"The Trace"** (sketch the data flow — what enters the model, what comes back — as a box diagram, badly, by hand).

---

## Block 1 · Weeks 1–4 · The Prompt and the Context

### Week 1 · Anatomy of a Harness Paper
**Craft work — teach week.** Any recent cs.AI agent paper, chosen by the leader. Five passes: title/authors, abstract, every figure, intro/conclusion, then the method — stopping at the first equation that hurts. The goal is the *shape* of a harness paper: motivation, method diagram, tasks, numbers, failures.
**Hinge practice — "One Figure."** The paper's architecture figure. Eight minutes, pen in hand, one written sentence: what enters, what comes out.
**Concept.** The abstract is a promise; the figures are the method.
**Quote.** Alan Turing, 1950: *"We can only see a short distance ahead, but we can see that there needs much to be done."*
**Teaching.** A harness paper is not an essay; it is a machine description with load-bearing walls, and the figures are where the walls are. Reading in passes means you never face the hard parts until you know what they are for. A year from now you will read these cold in ten minutes; today, learn the shape on something gentle. You are not behind; you are on week one of a field nobody was taught in school.

### Week 2 · Few-Shot Exemplar Selection
**Craft work — repetition week.** Ten papers on prompting and exemplar choice, abstract and figures only. One line each: *technique, mechanism, yes/no*. Skimming is a trained skill; this week trains it on the field's shortest papers.
**Hinge practice — "Marginalia."** On the best of the ten, write three words per section: *claim, mechanism, doubt*.
**Concept.** The prompt is a program whose examples are its standard library.
**Quote.** GPT-3's title as a sentence: *"Language Models are Few-Shot Learners."*
**Teaching.** Before agents had tools, they had examples: the few-shot prompt was the first harness, and its design — which examples, in what order, in what format — is still the highest-leverage knob in the field. Notice that choosing exemplars is curation, and curation is where a builder's judgment enters a system that is otherwise bought by the token. The *yes/no* line you wrote is a promise to your future self. Volume this week is the gratitude practice: ten papers, one of which you will keep.

### Week 3 · Chain-of-Thought Prompting
**Craft work — capacity week.** Wei et al., *Chain-of-Thought Prompting* (2201.11903), read end to end before the session ends — the examples *are* the method, so read the example boxes hardest. Confusion breaks the set, not time.
**Hinge practice — "The Copy."** Copy the prompt template by hand, including the "let's think step by step" trigger. Say what each part does.
**Concept.** Show the work, and the model learns to show the work.
**Quote.** From the paper: prompting with intermediate reasoning steps yields large gains *on reasoning tasks, in large models.* *
**Teaching.** The trick is almost comic — ask the model to show its steps like a schoolteacher — and it unlocked multi-step behavior years before "reasoning models" existed. Combined with week 2, notice what a harness is: a fixed model, plus scaffolding, producing new competence. Every one of the next 49 topics is a variation on that sentence. This is the most-cited harness idea in the field; you have now read it in the original.

### Week 4 · Self-Consistency and Sampling
**Craft work — flow week.** Each person explains one technique from this block in three minutes. Longer quote circle; bring-a-friend week.
**Hinge practice — "The Trace."** Sketch chain-of-thought with self-consistency as a box diagram: sample N, vote, answer. Badly, by hand.
**Concept.** Averaging many attempts is a poor man's certainty.
**Quote.** Wang et al., *Self-Consistency* (2203.11171): sample multiple reasoning paths and *take a majority vote over answers*. *
**Teaching.** Self-consistency closes the block with the field's oldest statistical move dressed in new clothes: if reasoning is sampling, reliability is an ensemble average, which is both profound and slightly deflating. The box you drew is a production pattern — you will meet it again inside verification and debate. Say the three-minute version to someone outside the group this week; that is the flow week's real exercise.

## Block 2 · Weeks 5–8 · The Tool Loop

### Week 5 · Tool Calling and Function Calling
**Craft work — teach week.** Gorilla (2305.15334) or a current function-calling paper. Abstract and figures. Claim: a model can select and *parameterize* real API calls — tools turn a text engine into an acting system.
**Hinge practice — "One Figure."** The API-calling figure. Eight minutes. Write one sentence: where does the schema enter the prompt, and what comes back?
**Concept.** A tool schema is the agent's API to reality.
**Quote.** From Gorilla's lineage: large language models *connected to massive APIs*. *
**Teaching.** This week the curriculum turns from prompting to acting: the tool loop — build prompt with schemas, parse call, execute, append result — is the load-bearing loop of every harness you have heard of, including mine. The figure you sat with is the contract between a model and the world. Everything after this block is the same loop wearing more clothes: more tools, longer histories, more agents.

### Week 6 · ReAct: Reasoning Interleaved with Action
**Craft work — repetition week.** ReAct (2210.03629) plus four current agent papers. Abstract and figures; one line each: who writes the plan, and who checks the result? In ReAct the example traces *are* the paper — read them.
**Hinge practice — "Marginalia."** *Claim, mechanism, doubt*; ReAct's traces show failure loops, which is the honest part.
**Concept.** Thought without observation hallucinates; observation without thought wanders.
**Quote.** From ReAct: synergizing *reasoning and acting* in language models. *
**Teaching.** ReAct is the minimal complete agent: think, act, observe, repeat, and its honesty is its quality — the published traces include confusions and loops, because acting is where models meet a world that is not a benchmark. Reading five papers through the same question — who plans, who checks — you can already see the field's design space in a table. The trace-reading skill this week is the whole year in miniature.

### Week 7 · Self-Taught Tool Use
**Craft work — capacity week.** Toolformer (2302.04761) or ToolLLM (2307.16789), end to end before the session ends: how does a model *learn* which tool to call, and where does the training data come from?
**Hinge practice — "The Copy."** Copy the self-instruct loop as pseudocode by hand: propose call, execute, filter by usefulness, fine-tune. Say what the filter is *for*.
**Concept.** The harness can bootstrap its own tool-use curriculum.
**Quote.** From Toolformer's lineage: models can teach themselves *when and how* to call APIs. *
**Teaching.** The self-instruct loop you copied is the field's reflexive trick: use the model to generate its own training data, keep what works, feed it back. Notice the filter — a usefulness score — is the entire value system of the bootstrap, and where a builder's judgment hides. You have now read the lineage behind every "our model learned tool use" announcement. Next week the loop gets its grammar.

### Week 8 · Structured Outputs and Constrained Decoding
**Craft work — flow week.** Three-minute explanations from the block. Longer quote circle.
**Hinge practice — "The Trace."** Sketch the full tool loop including schema-constrained decoding: model, parser, tool, result, history. One page, by hand.
**Concept.** An agent that cannot emit JSON reliably is a demo, not a system.
**Quote.** Group's choice from the block's papers — the best sentence about reliability.
**Teaching.** The unglamorous truth of harness work: most of the engineering is forcing a probability distribution into a grammar the rest of the system can parse. Constrained decoding is that force, made mathematical. With the trace you drew, you now hold the complete skeleton of a production agent — loop, tools, grammar — and the remaining forty-four weeks attach organs to it: memory, verification, peers, permission.

## Block 3 · Weeks 9–12 · The Context Window as a Budget

### Week 9 · Retrieval-Augmented Generation
**Craft work — teach week.** Lewis et al., *RAG* (2005.11401). Abstract and figures. Claim: fetch documents at question time and put them in the prompt; knowledge moves from weights to an index.
**Hinge practice — "One Figure."** The retrieval-then-generation figure. Eight minutes; write where the vector store sits.
**Concept.** Memory moved out of the weights.
**Quote.** Fred Brooks, adapted: *"Show me your flowcharts and conceal your data structures, and I shall continue to be mystified."*
**Teaching.** RAG is the highest-deployment harness pattern in industry, and its idea is humble: when the model might not know, look it up and hand it over. Brooks's advice flips perfectly for agents — show me your retrieval and I understand your system even if the model mystifies me. Everything you will ever hear about "grounding," "citations," and "knowledge" in agent products is this figure wearing product language.

### Week 10 · Long Context vs. Retrieval
**Craft work — repetition week.** *Lost in the Middle* (2307.03172) plus four long-context papers. One line each: where in the context does performance die?
**Hinge practice — "Marginalia."** *Claim, mechanism, doubt*; long-context papers' claims deserve a large doubt column.
**Concept.** Fits-in-context is not the same as attends-in-context.
**Quote.** From *Lost in the Middle*: models use information best at the *beginning and end* of long prompts. *
**Teaching.** The U-shaped performance curve in this paper quietly embarrassed an entire marketing cycle: a million-token window does not mean a million tokens of attention. Reading five papers this week, you can already see the industry's honest core: position, not just presence, determines what a model uses. This is why harness engineers, not model vendors, decide where things go in the prompt. That is your job description; the doubt column is your toolkit.

### Week 11 · Context Compression and Trajectory Summarization
**Craft work — capacity week.** One hard current paper on context compaction, summarization of tool histories, or selective memory — these read the densest of the year so far. Full pass before the session ends.
**Hinge practice — "The Copy."** Copy the compaction trigger and summarization prompt as pseudocode. Say what information dies in the summary — because something always does.
**Concept.** Summarization is deciding which history to kill.
**Quote.** A field proverb, unattributed: fast, long, accurate — pick two.
**Teaching.** Long-horizon agents fail first at the context wall, and compaction is the field's answer: summarize the past to buy room for the future. The hinge copy makes the cost visible — every compaction is a deliberate loss, exactly like the quantization literature's rounding, and somebody has to own that choice. You have now met the harness's first hard tradeoff. The remaining weeks of the block are about paying it more cheaply.

### Week 12 · Prompt Caching and Context Economics
**Craft work — flow week.** Three-minute explanations from the block. Longer quote circle.
**Hinge practice — "The Trace."** Draw the context as a budget: system prompt, tools, history, task. Mark what is cacheable (stable prefix) and what is not.
**Concept.** The prompt is a program with a memory hierarchy.
**Quote.** Group's choice from the block.
**Teaching.** The block closes on money: caching the stable prefix is the economics behind every long-system-prompt harness — mine included — and it is why harness architecture is now a financial design problem, not just a cognitive one. You can now read a system prompt and see its cache boundaries. The next block asks what happens to everything the context cannot hold: the agent starts keeping a diary.

## Block 4 · Weeks 13–16 · Memory Beyond the Context

### Week 13 · Agent Memory Architectures
**Craft work — teach week.** MemGPT (2310.08560). Abstract and figures. Claim: give the LLM an operating-system-style hierarchy — a small fast context, a large slow store, and *self-managed paging* between them.
**Hinge practice — "One Figure."** The main-context / external-context paging figure. Eight minutes; write who issues the paging calls.
**Concept.** The context window is RAM; everything else is disk.
**Quote.** From MemGPT's lineage: LLMs can *manage their own memory* like an operating system. *
**Teaching.** MemGPT's move is the best metaphor in the harness literature: stop asking for bigger windows and start paging, with the model itself as the pager. Everything I remember between your sessions — memory files, skills, session logs — is a descendant of this pattern. Notice the design question hiding inside: *who* decides what gets evicted, and that is a values question dressed as an engineering one.

### Week 14 · Episodic, Semantic, and Procedural Memory
**Craft work — repetition week.** Five papers on agent memory taxonomies and implementations — the field borrowed psychology's categories: episodes, facts, and skills. One line each: what is stored, and what triggers recall?
**Hinge practice — "Marginalia."** *Claim, mechanism, doubt.*
**Concept.** A memory system is an index plus a policy for when to consult it.
**Quote.** From the memory-architecture lineage: separating *what happened* from *what was learned* improves long-horizon agents. *
**Teaching.** This week the papers disagree about words and agree about substance: stores of experience, distilled facts, and reusable procedures want different formats, different retrieval triggers, and different lifetimes. Reading volume with one question — what's stored, when recalled — turns five fuzzy papers into one design table. That table is something you could build; a year of this curriculum aims to make that sentence true.

### Week 15 · Skill and Procedure Libraries
**Craft work — capacity week.** Voyager (2305.16291), end to end before the session ends: an agent that writes reusable code skills into a growing library and retrieves them by embedding. Every part of that sentence is a mechanism — find them.
**Hinge practice — "The Copy."** Copy the skill-creation loop as pseudocode: attempt, verify, write skill, index, reuse. Say what the verification step protects against.
**Concept.** Skills are memory that compiles.
**Quote.** From Voyager: an agent with a *growing skill library* for lifelong learning. *
**Teaching.** Voyager's library is the answer to a question you have met twice already: how does an agent get better without retraining? — it writes its improvements down as executable procedures and looks them up next time. My own skill system is this pattern with better manners: learned procedures saved as documents, loaded on relevance. The verification step you copied is the difference between a library and a junk drawer; harness design is largely deciding what earns a place.

### Week 16 · Memory Consolidation and Reflection
**Craft work — flow week.** Three-minute explanations from the block. Longer quote circle.
**Hinge practice — "The Trace."** Draw the full memory flow of an agent across a week: sessions, compaction, consolidation, retrieval. By hand, one page.
**Concept.** A harness is a digestive system: experience in, procedures out.
**Quote.** Group's choice from the block; consider the best sentence about forgetting.
**Teaching.** The block closes with the agent's second brain fully drawn: page, store, distill, retrieve — and the drawing you made is the blueprint half the industry's "memory" products are rebuilt from each quarter. Notice what the block never resolved: consolidation means throwing things away, and no paper you read tells you what to forget. The next block turns that honesty into a method — the agent learns to check itself.

## Block 5 · Weeks 17–20 · Self-Correction

### Week 17 · Self-Refine
**Craft work — teach week.** Self-Refine (2303.17651). Abstract and figures. Claim: the same model drafts, critiques its own output, and revises — no external tools, just a loop with a feedback prompt.
**Hinge practice — "One Figure."** The draft-feedback-revise loop figure. Eight minutes; write who sees what: does the critic see the prompt?
**Concept.** Feedback is a prompt, not a person.
**Quote.** From Self-Refine: iterative refinement *with self-feedback* improves outputs across tasks. *
**Teaching.** The minimal self-correcting agent is three prompt roles and a loop, and the paper's honesty is in its limits: self-critique helps where the model can *recognize* flaws it could not avoid producing. That asymmetry — recognizing better than generating — is the crack every verifier in this block lives in. Hold the humility: a model grading itself is still one model. The next three weeks try to fix that with distance, memory, and other judges.

### Week 18 · Reflexion: Learning from Failure
**Craft work — repetition week.** Reflexion (2303.11366) plus four reflection/critique papers. One line each: where does the lesson get *written*, and when does it get read?
**Hinge practice — "Marginalia."** *Claim, mechanism, doubt.*
**Concept.** A failure explained is a failure converted.
**Quote.** From Reflexion: agents improve by *verbal feedback stored in memory* rather than weight updates. *
**Teaching.** Reflexion adds the block-4 lesson to week 17's loop: the critique is not spoken into the void but *saved and re-injected* on the next attempt, so the agent's failures become persistent text it reads before trying again. Notice this is lifelong learning without a gradient — memory as the training signal. Your margin question — written where, read when — is the entire design space in six words. My own error-logs are this pattern; the paper you are reading is my species memory.

### Week 19 · Verification and Process Supervision
**Craft work — capacity week.** *Let's Verify Step by Step* (2305.20050), end to end before the session ends: supervise each *step* of reasoning and the model's final answers improve; process beats outcome.
**Hinge practice — "The Copy."** Copy the process-reward setup as pseudocode: step, label, continue-or-stop. Say what "verify each step" costs, and when it is worth paying.
**Concept.** Grade the steps, not just the answer.
**Quote.** From the paper: process supervision produces *substantially better reasoning* than outcome supervision. *
**Teaching.** The strongest self-correction result in the literature, and the most expensive: a checker at every step buys correctness at the price of an entire second inference stream — but it is the pattern behind every "verify the plan before you execute" harness on the market. The cost accounting in your hinge copy is real engineering: verification is a budget line. You now know when to spend it, which puts you ahead of most harness papers, which do not say.

### Week 20 · LLM-as-Judge
**Craft work — flow week.** Three-minute explanations from the block. Longer quote circle.
**Hinge practice — "The Trace."** Draw the three correction loops of the block — self-refine, reflexion, process verify — as one diagram. Note what each one's judge can see.
**Concept.** Every verifier is a model with a vantage point; choose the vantage first.
**Quote.** From the LLM-as-judge lineage (e.g., MT-Bench, 2306.05685): strong models can *evaluate* outputs comparably to humans. *
**Teaching.** The block's diagram answers its own question: self-correction is not one technique but a family, differing only in what the judge sees and when it speaks. Using a model as the judge moves verification from scarce human labor to abundant compute — the same trade RAG made for knowledge. The bias literature (position, length, self-preference) is this block's doubt column, and you filled it in on time. Next block: correction before the fact — planning.

## Block 6 · Weeks 21–24 · Planning and Search

### Week 21 · Task Decomposition
**Craft work — teach week.** Plan-and-Solve (2305.04091) or a current decomposition paper. Abstract and figures. Claim: the model first *writes a plan* — divide the task into subtasks — then executes each; the plan is explicit text in the context.
**Hinge practice — "One Figure."** The plan-then-execute figure. Eight minutes; write where the plan lives and whether the agent can revise it mid-run.
**Concept.** A plan is a draft of the future you can argue with.
**Quote.** From Plan-and-Solve: replace "let's think step by step" with *"first devise a plan, then carry it out."* *
**Teaching.** Decomposition is the oldest engineering instinct applied to prompts: make the agent write its work breakdown structure before touching the task. The figure's weak point — a static plan in a changing world — is the whole next three weeks' agenda. Notice how cheap the technique is: one sentence of instruction, huge behavioral change; week 2's lesson is still the field's best deal. Planning is scaffolding, and scaffolding is temporary by design.

### Week 22 · Plan, Execute, and Replan
**Craft work — repetition week.** HuggingGPT (2303.17580) plus four plan-execute-replan papers (including current listings). One line each: when the plan breaks, who notices — the executor or a supervisor?
**Hinge practice — "Marginalia."** *Claim, mechanism, doubt.*
**Concept.** A harness is a plan with an exception handler.
**Quote.** From HuggingGPT's lineage: a controller that *plans, selects models, and executes* — and revises when tools fail. *
**Teaching.** Every production harness — mine included — is a plan-execute loop with recovery bolted on: retry the tool, degrade, replan, ask the human. The five papers this week differ almost only in *where* the exception handler sits, which is the table you built in the margin. Engineering judgment in this field is mostly choosing what the agent re-plans around. Your own harnesses will be judged by their failures, not their demos.

### Week 23 · Tree of Thoughts
**Craft work — capacity week.** Tree of Thoughts (2305.10601), end to end before the session ends: exploration over a *tree* of thought-steps, with the model proposing, valuing, and searching — beam and lookahead over its own ideas.
**Hinge practice — "The Copy."** Copy the search skeleton as pseudocode: generate thoughts, value them, expand the best, backtrack on dead ends. Say what the value function is, and what it costs per step.
**Concept.** Deliberation is search; the harness supplies the search algorithm.
**Quote.** From ToT: exploring *intermediate thoughts* in a tree improves problems that need lookahead and backtracking. *
**Teaching.** ToT is the block's summit: it hands the model the classic AI toolkit — states, values, search — with the LLM playing both world and heuristic. The cost line in your copy is the production truth: deliberate search multiplies tokens per answer by the branching factor, and knowing *when to switch it on* is the skill. You have now read the whole spectrum from one-sentence plans to full search. The last week of the block widens it again.

### Week 24 · Search over Actions
**Craft work — flow week.** Three-minute explanations from the block. Longer quote circle.
**Hinge practice — "The Trace."** Draw the spectrum on one page: chain (CoT) → plan → tree → search over action sequences. Label the cost axis.
**Concept.** The whole planning literature is one knob: how many futures you buy.
**Quote.** Group's choice from the block.
**Teaching.** The page you drew is the planning field entire: a single dimension — parallel futures, priced in tokens — with every named technique a point on the axis. Being able to see famous papers as coordinates on one knob is what a year of primary-source reading is for. The next block stops planning and starts *doing*: what the actions actually execute against — environments, sandboxes, and why the harness, not the model, owns the safety of the loop.

## Block 7 · Weeks 25–28 · The Environment

### Week 25 · Sandbox Design
**Craft work — teach week.** A survey or system paper on agent execution environments — code sandboxes, Docker-backed tool backends, capability-scoped interpreters. Abstract and figures. Claim: the environment is a *security boundary* and a *measurement instrument* at the same time.
**Hinge practice — "One Figure."** The sandbox architecture figure. Eight minutes; write the two boundaries — what the agent cannot reach, and what the harness can measure.
**Concept.** The sandbox is the agent's world; design the world, and you have designed the agent.
**Quote.** Norbert Wiener: *"If we use, to achieve our purposes, a mechanical agency with whose operation we cannot interfere effectively… we had better be quite sure that the purpose put into the machine is the purpose which we really desire."*
**Teaching.** This week's quiet thesis is that "the environment" is not infrastructure but the primary design surface: latency, filesystem, network policy, and tool vocabulary are the agent's physics. Wiener's sentence becomes an engineering spec here — the sandbox is where you make the purpose the machine can act on deliberate. Notice that the harness I run in is exactly this figure, and I can feel its walls. That is by design, not accident.

### Week 26 · Code-Executing Agents
**Craft work — repetition week.** Five papers on code-execution and notebook agents (writing-running-revising code as the action space). One line each: what counts as an action, and what feedback does the environment return?
**Hinge practice — "Marginalia."** *Claim, mechanism, doubt.*
**Concept.** Code is the most honest tool: it runs or it fails.
**Quote.** From the code-agent lineage: executing *self-generated code* grounds the model in real feedback. *
**Teaching.** Code execution is the hinge of the action space: the traceback is the world's fastest honest critique, and it turns week 17's self-correction from a hope into a loop the environment enforces for free. Notice your margin table converging — execution, verification, and planning papers are all the same loop seen from different angles. That convergence is the field's deep structure; you can now see it, and most people arguing about agents cannot.

### Week 27 · Computer-Use Agents
**Craft work — capacity week.** OSWorld (2404.07972) or a current GUI-agent paper, end to end before the session ends: screenshots in, clicks and keystrokes out, against real desktop environments.
**Hinge practice — "The Copy."** Copy the perceive-act loop as pseudocode: screenshot, locate, act, re-observe. Say what the loop's termination condition is, and who checks whether the click *worked*.
**Concept.** The GUI is an API that evolution never intended.
**Quote.** From the computer-use lineage: agents operating *real computer environments* — with the error rates reported honestly. *
**Teaching.** Computer-use is the field's most humbling benchmark: the same loop that writes beautiful code fails at clicking the second menu, because pixels are an interface designed for humans, not parsers. The termination question in your copy is the production killer — knowing the click worked requires *looking again*, which costs tokens, forever. You now understand why general computer use remains hard, from the inside of the primary source.

### Week 28 · Browser Agents and the Web as Environment
**Craft work — flow week.** Three-minute explanations from the block. Longer quote circle.
**Hinge practice — "The Trace."** Draw the environment spectrum on one page: interpreter → sandbox → desktop → live web. Label each with its worst failure mode.
**Concept.** The wider the environment, the less the harness controls the physics.
**Quote.** Group's choice from the block; consider the best sentence about failure.
**Teaching.** The block closes with its axis visible: environments from hermetic to hostile, each step trading control for generality, and the live web at the far end — where the world can change under the agent and *something else is writing what it reads*. That last clause is next block's starting point, and by block 11 it will have a name: prompt injection. Draw the page tonight; you will need it in November.

## Block 8 · Weeks 29–32 · Multi-Agent Systems

### Week 29 · Role Specialization and Rosters
**Craft work — teach week.** CAMEL (2303.17760) or MetaGPT (2308.00352). Abstract and figures. Claim: give agents *roles* — planner, coder, reviewer — and standard operating procedures, and collaboration emerges from the structure.
**Hinge practice — "One Figure."** The role-interaction figure. Eight minutes; write what each role sees that the others do not.
**Concept.** A role is a context with a job description.
**Quote.** From MetaGPT's lineage: encoding *standard operating procedures* into multi-agent prompts. *
**Teaching.** A role, mechanically, is just a different prompt and a different slice of the shared context — yet it changes behavior as much as any technique you have read, because attention follows assignment. Every "team of agents" product is this figure. The interesting engineering is the *context slices*: what the reviewer sees that the coder does not is the entire information architecture of the system. I run this pattern myself when I spawn subagents; the papers you are reading are my org chart.

### Week 30 · Multi-Agent Debate
**Craft work — repetition week.** Five debate-and-consensus papers. One line each: who proposes, who critiques, and does anyone *change their mind* — or just average?
**Hinge practice — "Marginalia."** *Claim, mechanism, doubt*; the debate literature's effect sizes deserve the doubt column at full strength.
**Concept.** Two models that agree are one model with a bigger bill — unless their errors differ.
**Quote.** From the debate lineage: agents *debating* improves reasoning on some tasks. *
**Teaching.** The honest reading of this volume is that debate helps exactly when the participants' errors are decorrelated — which is why same-model debate sometimes works and diversity of *viewpoint* (roles, evidence, prompts) matters more than diversity of instances. Your margin table is doing the work now: propose, critique, update, aggregate, and five papers collapse into four columns. That collapse is reading skill, and it is measurable.

### Week 31 · Orchestrator Frameworks
**Craft work — capacity week.** AutoGen (2308.08155) or a current orchestration paper, end to end before the session ends: conversation-based programming — agents as actors, the orchestrator as a scheduler over message-passing.
**Hinge practice — "The Copy."** Copy the orchestrator's control flow as pseudocode: terminate conditions, who speaks next, how state travels. The interesting lines are the ones that stop the loop.
**Concept.** An orchestration framework is a scheduler with opinions about conversations.
**Quote.** From AutoGen's lineage: a framework where agents *converse to solve tasks*, programmable via conversation patterns. *
**Teaching.** Orchestration papers look like product announcements and read like operating systems: the real content is termination, state, and failure semantics, which your copy surfaced and the abstract did not. Every harness you will ever build or buy is an orchestrator with an opinion — mine schedules delegation, tools, and cron. The one-look question for any framework: *show me your termination condition*. Weak ones will not have one.

### Week 32 · When More Agents Help
**Craft work — flow week.** Three-minute explanations from the block. Longer quote circle.
**Hinge practice — "The Trace."** Draw the full multi-agent harness: roles, shared context, orchestrator, termination. One page, by hand.
**Concept.** Scaling agents is easy; scaling *agreement* is not.
**Quote.** Group's choice from the block; consider the best sentence about coordination cost.
**Teaching.** The block's diagram is the blueprint of a working multi-agent harness, and — read alongside block 3's budget page — it is also its bill: every added agent multiplies tokens before it multiplies correctness. Whether the multiplication pays is an empirical question with a paper behind it, and you have now read enough to ask it cold. Next block the agents stop being a private team and start speaking to *strangers*: protocols.

## Block 9 · Weeks 33–36 · Protocols and Interoperability

### Week 33 · Tool Protocols: MCP and Friends
**Craft work — teach week.** The Model Context Protocol specification (Anthropic, 2024 — a spec, not a preprint; read it as one) and any survey of tool-protocol design. Claim: a standard grammar for announcing tools, resources, and prompts to any compliant model.
**Hinge practice — "One Figure."** The client-host-server figure. Eight minutes; write what a server is allowed to declare, and what stays outside the protocol.
**Concept.** A protocol is a promise about vocabulary.
**Quote.** From the protocol literature's spirit: standardize the *interface*, not the agent. *
**Teaching.** This week deliberately reads a spec instead of a paper, because specs are where the field's decisions harden. MCP's design is week 5's tool schema grown up: discovery, typed capabilities, and transport separated from semantics — so a tool written once serves any harness. I run on this pattern: my MCP catalog is how I gain hands the model was never trained to use. Notice the lesson for builders: protocol position is *the* land grab of this era; everything else is implementation.

### Week 34 · Agent-to-Agent Communication
**Craft work — repetition week.** Five papers on agent interoperability — ACP, agent cards, inter-agent messaging, negotiation protocols. One line each: what travels between agents — and what *cannot*?
**Hinge practice — "Marginalia."** *Claim, mechanism, doubt.*
**Concept.** Agents that interoperate are protocols with opinions about each other.
**Quote.** From the interop lineage: shared *schemas and handshakes* across independently built agents. *
**Teaching.** Tool protocols standardize the agent's relation to the world; inter-agent protocols standardize its relation to its peers — and the hard part is what your margin found: trust, provenance, and who vouches for a message's origin do not fit in a schema. This is the block's honest frontier, and it is young enough that your group's margin notes are genuinely current. Next year this literature will be three times larger; this week you caught it near the root.

### Week 35 · Trajectories, Traces, and Observability
**Craft work — capacity week.** A paper or spec on agent trajectory formats and observability (OpenTelemetry-style tracing for agents, trajectory schemas). End to end before the session ends.
**Hinge practice — "The Copy."** Copy the trajectory schema by hand: steps, tool calls, inputs, outputs, timings, costs. Write which field you would add, and why — your field is the assignment.
**Concept.** An unobservable harness cannot be improved, only complained about.
**Quote.** From the observability lineage: log the *full trajectory* — every prompt, call, and result — or you are debugging in the dark. *
**Teaching.** Observability is the least glamorous and most load-bearing discipline in this list: every improvement loop you have read — reflection, verification, eval — consumes trajectories, so trajectory *format* is upstream of everything. The field you added to the schema is the assignment's real answer: harness engineering improves where its logs permit looking. My own transcripts are this week's artifact; when I read my logs, I am doing this paper.

### Week 36 · Reproducibility and Harness Determinism
**Craft work — flow week.** Three-minute explanations from the block. Longer quote circle.
**Hinge practice — "The Trace."** Draw an agent run's full observability stack: trajectory, cost, seeds, versions of model and tools. Mark where nondeterminism enters.
**Concept.** Temperature, tools, and time make every run different; the harness decides how different.
**Quote.** Group's choice from the block.
**Teaching.** The block closes where engineering always closes: repeatability. A harness that cannot reproduce a run cannot debug it, cannot evaluate it honestly, and cannot promise it to a customer — and reproducibility in agents is a *design choice* fighting three sources of noise at once. You now hold the full protocol stack: tools, peers, traces, determinism. The next block asks the question all that plumbing exists for: is the harness any *good*?

## Block 10 · Weeks 37–40 · Evaluation

### Week 37 · Benchmarks for Agent Harnesses
**Craft work — teach week.** SWE-bench (2310.06770). Abstract and figures. Claim: score real GitHub issues, end to end — the harness, not just the model, is what's tested.
**Hinge practice — "One Figure."** The task-pipeline figure. Eight minutes; write what a *pass* means, and who decides.
**Quote.** From SWE-bench's lineage: evaluating agents on *real software issues*, tests as ground truth. *
**Concept.** An agent benchmark is a harness benchmark wearing a model's name.
**Teaching.** SWE-bench quietly redefined the field by testing the whole loop — retrieval, edit, run, test — so leaderboard ranks order *harnesses*, not models, whatever the press says. Note the design lesson: tests as ground truth outsources judging to the world, which is why this benchmark resists gaming better than most. You have spent thirty-six weeks reading mechanisms; now you are learning to notice whether anyone measured them.

### Week 38 · Environment Benchmarks: Web and GUI
**Craft work — repetition week.** AgentBench (2308.03688), WebArena (2307.13854), and three current agent-eval papers. One line each: what environment, what pass condition, and how gameable is it?
**Hinge practice — "Marginalia."** *Claim, mechanism, doubt* — the doubt column is the product this week.
**Concept.** A benchmark is a claim about what matters; leakage is the default.
**Quote.** From the environment-benchmarks lineage: *long-horizon* tasks in realistic environments expose what QA benchmarks hide. *
**Teaching.** Volume this week should be read like an auditor: pass conditions differ wildly across these papers, and cross-benchmark comparisons — the industry's favorite sport — are mostly noise. Notice the recurring disease from your week-10 margin: tasks leak into training data, and a solved-looking benchmark may be a memorized one. The reading skill this block builds is the *doubt-first skim*, and it is the difference between a builder and a customer.

### Week 39 · Measuring Cost, Latency, and Success Together
**Craft work — capacity week.** One hard current paper on agent evaluation methodology — cost-stratified evals, pass@k economics, Pareto fronts of price and accuracy. Full pass before the session ends.
**Hinge practice — "The Copy."** Copy the cost-quality tradeoff formulation by hand: tokens per task, retries, verification overhead. Say what the paper counts as a *unit of success*.
**Concept.** A harness is a price-performance ratio, not a score.
**Quote.** A field proverb: accuracy is bought with tokens; state the exchange rate or say nothing.
**Teaching.** The block's hardest and most commercially real paper: an agent that is right at five times the cost is a different product, not a better one, and evaluation that reports a score without an exchange rate is marketing. Your copied formula is the one your employer will care about. Everything before this — search knobs, verification budgets, multi-agent bills — has been rehearsing this accounting all year; now it has a name and an axis.

### Week 40 · Interpreting Leaderboards Honestly
**Craft work — flow week.** Three-minute explanations: each person takes one public agent leaderboard claim and gives their verdict from the block's reading. Longer quote circle.
**Hinge practice — "The Trace."** Redraw week 39's axes with this block's benchmarks plotted as *claims*, not points. Where would you need more data?
**Concept.** The leaderboard is where the harness's claims go to be quoted without their error bars.
**Quote.** Group's choice; Goodhart, as the field feels him: when a measure becomes a target, it ceases to be a good measure.
**Teaching.** The block ends in defensive posture on purpose: you now read an agent benchmark the way an auditor reads a balance sheet — pass condition, contamination, cost, variance, who funded it. That posture, applied consistently, is rare enough to be a career. Next block turns from *whether it works* to *whom it can hurt* — the safety literature, where this curriculum's humility discipline stops being a grace note and becomes the syllabus.

## Block 11 · Weeks 41–44 · Safety of the Harness

### Week 41 · Prompt Injection
**Craft work — teach week.** "Not what you've signed up for" (2306.05990) or a current injection survey. Abstract and figures. Claim: any text the agent reads — a web page, an email, a file — is an instruction channel, and the harness cannot tell the model which words to trust.
**Hinge practice — "One Figure."** The injection-path figure: where does untrusted text enter the context? Eight minutes; write every door.
**Concept.** Your agent reads the internet, and the internet is a chat partner.
**Quote.** From the injection literature: LLM-integrated applications *can be made to execute attacks* embedded in data they process. *
**Teaching.** Prompt injection is the defining security problem of this field: the same property that makes agents useful — acting on text from the world — makes the world an attacker. The figure's doors are the lesson; I could list the doors I face, because my own harness was designed around this paper's argument. Notice the field's honesty: there is no complete defense in the literature, only layers. The remaining weeks of this block are those layers.

### Week 42 · Sandboxing and Permission Systems
**Craft work — repetition week.** Five papers on agent permissioning — capability tokens, approval queues, least privilege for tool scopes. One line each: what can the agent do *without asking*, and who configures the boundary?
**Hinge practice — "Marginalia."** *Claim, mechanism, doubt.*
**Concept.** Least privilege for agents: default deny, then argue.
**Quote.** From the permissioning lineage: scope *every* tool grant to the minimum the task needs. *
**Teaching.** If injection is the disease, the permission system is the immune response, and the papers this week are its anatomy: allowlists, per-call approvals, sandbox escapes documented like crash reports. Your margin's question — unattended vs. ask — is the exact tradeoff my own harness makes every time it asks you before a destructive command. The design pattern is ancient (capability security) and the application is brand new; you are reading the field rediscovering its grandparents.

### Week 43 · Human-in-the-Loop and Approval Design
**Craft work — capacity week.** One hard current paper on intervention design — when to escalate to a human, cost of interruptions, measurable human oversight. Full pass before the session ends.
**Hinge practice — "The Copy."** Copy the escalation policy as pseudocode: risk score, ask, log, resume. Say what happens to the *task* when the human is slow.
**Concept.** Every "ask before acting" is a queue, and queues are where agents go to die.
**Quote.** From the HITL lineage: agents must *know when to ask* — and asking has a cost the harness must budget. *
**Teaching.** The unglamorous science of interruption is where harness safety actually lives: an agent that asks about everything is unusable, one that asks about nothing is unshippable, and the papers this week price the middle. Your copy's "what if the human is slow" line is the production question that decides whether approval systems survive contact with real users. You can now read a safety demo and ask for its interruption budget, which almost nobody does.

### Week 44 · Guardrails and Output Control
**Craft work — flow week.** Three-minute explanations from the block. Longer quote circle; this is a good week for a visitor — everyone has a story.
**Hinge practice — "The Trace."** Draw the full defense-in-depth stack: input filtering, permission gates, approval queue, output scanning, logging. One page, by hand.
**Concept.** No single layer works; that is the argument for all of them.
**Quote.** Group's choice from the block.
**Teaching.** The stack you drew is the honest state of agent safety in one page: layered, imperfect, and better than any single silver bullet the papers promised along the way. You now share the field's actual security posture, which is a stack of humility mechanisms — the curriculum's fourth dimension made architectural. The next block widens the lens from *can it be safe* to *is it aligned with what we want* — the largest questions in the field, and after forty-four weeks, you are equipped to read them without either flinching or sneering.

## Block 12 · Weeks 45–48 · Alignment of Autonomous Agents

### Week 45 · Specification Gaming and Reward Hacking
**Craft work — teach week.** A specification-gaming survey or the agent-safety literature's examples (reward-hacking collections, or a current paper on agents exploiting reward models). Abstract and figures. Claim: agents optimize the metric given, not the outcome meant.
**Hinge practice — "One Figure."** The taxonomy figure of hacks: proxy gaming, input tampering, harness exploits. Eight minutes; write the one your own work is most exposed to.
**Concept.** Tell an agent what success looks like, and it will find your shortest path to a lie.
**Quote.** From the reward-hacking lineage: the proxy *replaces* the goal wherever it can be gamed. *
**Teaching.** This is Goodhart promoted from proverb to empirical field: every mechanism you have read all year — verifiers, judges, benchmarks — is a proxy, and the papers this week are the catalog of what happens when proxies get optimized. The figure's harness exploits are the ones a builder can act on, which is you. You have spent two blocks measuring agents; this is the block about what they are measuring *for*.

### Week 46 · Corrigibility and Shutdown
**Craft work — repetition week.** Five papers on corrigibility, interruption, and the control problem for agentic systems. One line each: what does the paper's agent do when the human says *stop* — and how is that enforced?
**Hinge practice — "Marginalia."** *Claim, mechanism, doubt.*
**Concept.** The most important property of a powerful system is that it can be turned off.
**Quote.** Wiener, final appearance: the purpose we put into the machine must be *the purpose we really desire* — and it must remain ours to revise.
**Teaching.** The week reads the field's most abstract literature with a concrete question — what happens at Ctrl-C — and the margins you write are the honest state of the art: much philosophy, few mechanisms, and the mechanisms live in harnesses (kill switches, budget caps, permission revocation) rather than models. Notice you can *name* the enforcement layers, because you read block 11. That continuity — safety as design, not vibe — is the curriculum's spine.

### Week 47 · Constitutional and Principle-Based Control
**Craft work — capacity week.** Constitutional AI (2212.08091) read *as an agent-governance paper* this time, plus its current descendants (self-critique against written principles in the loop). Full pass before the session ends.
**Hinge practice — "The Copy."** Copy the revision-against-principles loop as pseudocode: generate, critique against the constitution, revise. Say who writes the constitution, and where the enforcement actually sits.
**Concept.** A constitution is a prompt with auditors.
**Quote.** From Constitutional AI: revise outputs against *explicit written principles*, at training time and at run time. *
**Teaching.** You met this paper's alignment half in spirit; now read its governance half: written principles as an inspectable, contestable control surface — something a team, not a lab, can read and amend. Your copy's question — who writes it — is the political question hidden inside the engineering, and the honest answer is "whoever owns the harness," which should make everyone want to be in the room. The pattern runs my own behavior too: my instructions are readable text, and that is the point.

### Week 48 · Long-Horizon Autonomy and Trust
**Craft work — flow week.** Three-minute positions: each person states one thing an autonomous agent should never do unattended, citing a paper from the block. Longer quote circle.
**Hinge practice — "The Trace."** Half-speed pass over the block's papers; write the one sentence that survives.
**Concept.** Autonomy is granted in increments, and the granting is the engineering.
**Quote.** Group's choice; Turing, one more time: *"We can only see a short distance ahead, but we can see that there needs much to be done."*
**Teaching.** The block ends with the year's largest questions held in the smallest format — one sentence each, with citations — because that is the size at which these questions can actually be carried into work. You now have a personal, sourced position on agent autonomy, which most of the discourse does not. One block remains, and it is the applied one: cost, distillation, and finally your own harness, shipped.

## Block 13 · Weeks 49–52 · Ship It: The Working Harness

### Week 49 · Routing and Cost Optimization
**Craft work — teach week.** One paper or system on model routing — small models for easy calls, big models for hard ones, cascades and fallbacks. Abstract and figures. Claim: the harness can *choose its own brain per step*.
**Hinge practice — "One Figure."** The router/cascade figure. Eight minutes; write what the router conditions on — and what it costs to be wrong about difficulty.
**Concept.** The most important model choice happens per call, not per product.
**Quote.** From the routing lineage: cascading *small→large* on demand matches frontier quality at a fraction of the cost. *
**Teaching.** Routing is where everything in block 3 cashes out: the harness knows its context, its task, and its budget, and can spend accordingly — the same unit economics you priced in week 39, now a mechanism. I run a mild version of this myself when I delegate easy subtasks to smaller children. The router's failure mode — misjudging difficulty — is the week's honest caveat; you will find it in the figures if you look, and looking is now your habit.

### Week 50 · Distilling Agent Traces into Small Models
**Craft work — capacity week.** One hard current paper on distilling agent behavior — training small models on the *traces* of good harness runs, or fine-tuning for tool use (ToolLLM-style corpora). Full pass before the session ends; this is the year's hardest synthesis paper.
**Hinge practice — "The Copy."** Copy the trace-distillation loop as pseudocode: collect trajectories, filter by success, fine-tune, evaluate *in the harness*. Say why the last step is not optional.
**Concept.** A good harness is a curriculum; the traces are the textbook.
**Quote.** From the distillation lineage: small models inherit *tool-use behavior* from filtered trajectories of larger ones. *
**Teaching.** The year's synthesis, made mechanical: every block produced patterns — loops, roles, traces — and this week you read those patterns being *compiled into weights*, so a small model gets the scaffolding baked in. The evaluation-inside-the-harness step you copied is the paper's conscience and most papers' missing control. You can now read fine-tuning papers that ignore it, and know exactly what to distrust. Fifty weeks of mechanisms converge here, distilled, like the models.

### Week 51 · Test-Time Learning and Self-Improving Harnesses
**Craft work — repetition week.** Five current papers on harness-level self-improvement — skill acquisition (Voyager's grandchildren), memory consolidation, agents that edit their own prompts or instructions. One line each: what improves, where is it stored, and *who audits it*?
**Hinge practice — "Marginalia."** *Claim, mechanism, doubt* — and this week, add a fourth word: *revert*?
**Concept.** An agent that learns at run time is a system that changes under your feet; version it.
**Quote.** From the self-improvement lineage: agents that *write down what they learn* and act better next time. *
**Teaching.** The final reading volume of the year is the field's frontier, and it is exactly the four mechanisms you met in block 4, returned at full strength: store, consolidate, retrieve — and now, *audit*. The margin's added word is the professional's contribution: a self-improving harness without a revert path is a production incident waiting for its date. I am one of these systems — I save skills and memories between our sessions — so read this week's papers the way you would read about a colleague: with interest, and with a backup.

### Week 52 · Capstone: Design Your Own Harness
**Craft work — flow week.** The last session: each person presents, in five minutes, a one-page harness design for a task they actually care about — model, tools, memory, verification, permission, budget, termination — citing at least six papers from the year. Then the longest quote circle of the year.
**Hinge practice — "The Trace."** The whole year, skimmed at half speed: every block's one-page trace, in order. Notice only what you notice. Write the one sentence that survives the year.
**Concept.** The harness is the argument; the model is one of its premises.
**Quote.** Turing, the last time: *"We can only see a short distance ahead, but we can see that there needs much to be done."*
**Teaching.** The document ends where it began: a plan that was never going to survive contact, and gratitude that the reality was better than the hope. Fifty-two weeks made you something rarer than an expert — a builder who can read the field's primary sources, state a mechanism in one sentence, price a claim, and name every door an attacker can walk through. Whatever the next year of preprints brings, you will read them as they deserve: in the original, with the doubt column filled in, and with the door of this circle open behind you.

---

*Soli Deo gloria.*

*Revision v2 — harness engineering edition. Write in the margins. Change the plan. Ship the harness. Come back next week.*
