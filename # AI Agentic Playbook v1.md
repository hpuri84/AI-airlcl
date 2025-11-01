# AI Agentic Playbook v1.1

### CargoX — Air & LCL Orchestrated Intelligence

**Purpose:**
Enable the next generation of freight operations: from assisted UIs to orchestrated, AI-driven workflows.
CargoX acts as the intelligence layer over CargoWise One (CW1), delivering Booking → Quotation → Consol → Invoice via modular, trusted agents.

---

## 1. Vision & Principles

| Principle                        | Description                                                                                                                |
| -------------------------------- | -------------------------------------------------------------------------------------------------------------------------- |
| **Transparency by Design**       | Every AI decision surfaces sources, confidence, and reasoning.                                                             |
| **Human-in-the-Loop (HITL)**     | Operators always retain control: override, approve, correct.                                                               |
| **Continuous Learning**          | Feedback from real interactions flows back into the system (REACT loop: Recognize → Evaluate → Act → Communicate → Track). |
| **Trust through Explainability** | Confidence badges, source citations, and process visibility build user trust.                                              |
| **Governance & Safety**          | Every action logged, auditable, and reversible; policy/guardrails built-in.                                                |
| **Experience-Driven Adoption**   | Success not just accuracy — measure usability, adoption, and impact.                                                       |

---

## 2. Architecture Overview

**CargoX Agent Stack**

```
[User (Operator, Customer, Vendor)]
          ↓
  [CargoX Orchestrator Agent]
          ↓
 ├── Booking Validator Agent  
 ├── Quotation Agent  
 ├── Rate / Route Engine (RAG + Reasoning)  
 ├── Forecast Agent  
 ├── Invoice Validator Agent  
 ├── Learning Agent  
 └── Evaluation Agent (LLM-as-Judge)  
```

**Key architectural elements**

* **Orchestrator**: Central hub that routes intents, maintains state, enforces contract.
* **Toolset**: APIs, retrieval, agent actions, escalation pathways.
* **Knowledge Graph / Freight Graph**: Unified vector + metadata layer (CW1 logs, EDI events, contracts, SOPs, email records) accessible to agents.
* **Feedback & Evaluation Loop**: Capture operator corrections → update models/pipelines → monitor drift.
* **Guardrails**: Loop limits, confidence thresholds, human handover, audit trails.

---

## 2.1 Agent Design Patterns

| Pattern               | Description                                               | Example for Air/LCL                                        | Evaluation Focus                                 |
| --------------------- | --------------------------------------------------------- | ---------------------------------------------------------- | ------------------------------------------------ |
| **Information Agent** | Summarise / forecast / explain based on data              | “Why is this consol delayed?”                              | Accuracy of explanation, source grounding        |
| **Action Agent**      | Execute tasks via APIs or workflows                       | “Rebook this HAWB under next available consol.”            | API success, SLA hit rate                        |
| **Decision Agent**    | Suggest optimal decisions based on multi-factor reasoning | “Recommend routing based on margin & transit time.”        | Decision acceptance rate, margin improvement     |
| **Learning Agent**    | Improve over time via feedback/corrections                | Operator correction “incorrect pickup code” → update model | Learning velocity (# errors dropped / iteration) |
| **Evaluation Agent**  | Judges other agents for factuality, compliance, alignment | “Judge if AI quote aligns with our rate sheet.”            | Alignment score, false positives/negatives       |

---

## 2.2 Retrieval & Knowledge Layer

**Lessons from Contextual Retrieval / Beyond Naive RAG (Anthropic)**

| Principle                        | Air/LCL Adaptation                                                          | Outcome                                |
| -------------------------------- | --------------------------------------------------------------------------- | -------------------------------------- |
| **Late Interaction Models**      | Token-level semantic search across HAWB docs, invoices, logs                | Better precision, fewer hallucinations |
| **Multi-Representation RAG**     | Separate vector maps for emails, rate sheets, SOPs                          | Domain-specific retrieval, less noise  |
| **Reasoning-enhanced Retrieval** | Promptriever: follow operator intent, dynamic tool-selection                | Smarter retrieval, better UX           |
| **FreshStack-style Evaluation**  | Evaluate retrieval not just by recall but by grounding, coverage, diversity | Higher trust/accuracy metrics          |
| **Agents as Routers**            | Orchestrator dynamically chooses retrieval index (Rate DB, CW1 logs, Email) | Faster & context-aware responses       |

**Freight Graph** – Cognitive map of operations

```
[CW1 Logs] – operational truth  
[EDI Events] – real-time milestones  
[Customer Contracts] – pricing & SLAs  
[Rate Repository] – procurement data  
[SOPs / Manuals] – policy & process knowledge  
[Emails / Notes] – human context  
```

Each node is vectorized and tagged with metadata (source system, date, product/region, business domain) so agents can reason across the full operational context.

**Retrieval Pipeline (CargoX Standard)**

1. Intent detection by Orchestrator
2. Route to correct index (Freight Graph partition)
3. Semantic + sparse retrieval (embeddings + BM25)
4. Reranking & reasoning layer
5. Candidate context passed to generation/agent
6. Evaluation Agent checks grounding → response or escalate

**Evaluation Metrics for RAG layer**

| Metric                 | Description                                       | Target |
| ---------------------- | ------------------------------------------------- | ------ |
| Grounding@K            | % of answer tokens supported by retrieved sources | ≥ 85%  |
| Coverage@K             | % of relevant facts retrieved                     | ≥ 80%  |
| Diversity@K            | Non-redundant doc sources in retrieval            | ≥ 75%  |
| Latency SLO            | Average response time from query to output        | < 6s   |
| Feedback Adoption Rate | % of operator corrections used for model update   | > 70%  |

**References**

* “Introducing Contextual Retrieval” by Anthropic, Sept 19 2024. ([anthropic.com][1])
* “Beyond Naive RAG: Practical Advanced Methods” (mini-book). ([hamelhusain.substack.com][2])
* “Beyond Basic RAG: A Practical Guide…” (Towards AI, Oct 7 2025) ([Towards AI][3])

---

## 3. UX Framework – Trust, Transparency & Control

### Confidence & Source Visualization

| Confidence | Colour | Message Example                          | User Action               |
| ---------- | ------ | ---------------------------------------- | ------------------------- |
| High       | Green  | “Verified using CW1 log & Supplier API.” | Auto-approve agent action |
| Medium     | Orange | “Partial data – requires user review.”   | Prompt user review        |
| Low        | Red    | “Unable to verify – missing data.”       | Escalate to human         |

Show source badges: e.g., “Source: CW1 Audit Log (updated 5 min ago)”
Avoid icon overload — use clear text + neutral colour emphasis.

### Interaction Patterns

| Pattern                 | Description                            | Example                                                |
| ----------------------- | -------------------------------------- | ------------------------------------------------------ |
| Embedded Feature        | Inline in CW1/ALP workflow             | “Auto-fill MOF” on booking screen                      |
| Embedded Chat Assistant | Side-panel conversational aid          | “Why was this shipment rejected?”                      |
| Teams / Outlook Agent   | Conversational AI for asynchronous ops | “@CargoX show yesterday’s exception summary”           |
| Autonomous Worker       | Background multi-agent workflow        | Booking Validator → Rate Agent → Planner collaboration |
| Voice Agent (future)    | Voice-first for warehouse or airport   | “CargoX, confirm cargo arrival at AMS warehouse.”      |

### Evaluation Framework (aligned with conversational UX)

| Metric Type       | Key Metrics                                   | Application                   |
| ----------------- | --------------------------------------------- | ----------------------------- |
| Usage & Behaviour | MAU, Drop-off rate, Clarification loops       | Adoption & friction           |
| Performance       | Fallback rate, latency, error rate            | Technical health              |
| Per Interaction   | 👍/👎 feedback + optional comment             | Real-time sentiment           |
| Monthly UX        | UMUX-Lite (“meets my needs”, “easy to use”)   | Lightweight usability         |
| Quarterly UX      | BUS-11 (conversation clarity, responsiveness) | Deep usability                |
| System-level      | Grounding@K, Diversity@K, Eval pass rate      | Retrieval & reasoning quality |
| Learning Velocity | Accuracy improvement per iteration            | Training effectiveness        |

---

## 4. Human-Agent Collaboration Principles

| Guideline                          | Implementation                                                                     |
| ---------------------------------- | ---------------------------------------------------------------------------------- |
| Always show agent’s reasoning step | “Validating rate using Supplier API…”                                              |
| Offer three levels of autonomy     | 1) Passive log mode <br> 2) Confirm mode <br> 3) Autonomous mode (high confidence) |
| Allow override/cancel              | Inline “Edit before sending” / “Send to operator”                                  |
| Escalate sensitive cases           | Low confidence + emotional/validation triggers → human                             |
| Record all interactions            | Audit logs in ALP for traceability & retraining                                    |

---

## 5. Capability → Agent → UX → Evaluation Mapping

| Capability                | Agent              | UX Pattern                  | Eval Metric                          | Confidence Signal |
| ------------------------- | ------------------ | --------------------------- | ------------------------------------ | ----------------- |
| Booking Validation        | Booking Validator  | Inline + Chat assist        | Touchless % + 👍/👎 feedback         | 🟢 High           |
| Quotation Automation      | Quotation Agent    | Side panel suggestion       | Quote accuracy + UMUX                | 🟠 Medium         |
| Order Planner / Consol    | Planner Agent      | Dashboard + feedback form   | Margin improvement + user acceptance | 🟠 Medium         |
| Forecast / ETA Prediction | Forecast Agent     | Chat + “Why this forecast?” | Accuracy vs real-event               | 🟠 Medium         |
| Invoice Validation        | Invoice Validator  | Inline diff/highlight view  | Error detection rate                 | 🟢 High           |
| Customer Communication    | Customer Assistant | Teams/Email chat            | CSAT + latency + BUS-11              | 🟠 Medium         |

---

## 6. Feedback & Learning Loop

1. Collect 👍/👎 for each AI message + optional comment
2. Cases scored low auto-flagged for human review
3. Human corrections feed labelled data set → model retrain + RAG retrain
4. Monthly UX survey (UMUX-Lite) + quarterly BUS-11 survey
5. Dashboard shows: Eval pass rate, Confidence distribution, Learning velocity
6. Visible feedback: “Your correction helped improve booking detection for future cases.”

---

## 7. Governance & Observability

| Pillar               | Implementation                               | Tool / Asset         |
| -------------------- | -------------------------------------------- | -------------------- |
| Auditability         | Log every decision, action, source           | CargoX Audit Trail   |
| Explainability       | Tooltip / “Why” link for each suggestion     | UI Metadata panel    |
| Policy & Risk Engine | Drift alerts, unauthorized action prevention | Governance dashboard |
| Model Oversight      | Versioning, performance dashboards, drift    | MLOps Portal         |
| Cost Management      | Token / API cost tracking, optimization      | Azure Cost Dashboard |

---

## 8. Visual & Copy Guidelines

| Element          | Format Example                             | Notes                        |
| ---------------- | ------------------------------------------ | ---------------------------- |
| Confidence Badge | “High confidence (87%)”                    | Text + colour only           |
| Tooltip          | “Based on rate contracts + EDI + CW1 logs” | Transparent source reasoning |
| Status Message   | “Analyzing supplier discrepancy…”          | Keep user informed           |
| Error Message    | “Unable to verify shipper name.”           | Plain, direct language       |
| Tone             | “Let’s verify this together.”              | Collaborative voice          |

---

## 9. Timeline: 6-Week Agentic Rollout (Pilot)

| Week     | Focus                              | Deliverables                                    |
| -------- | ---------------------------------- | ----------------------------------------------- |
| Week 0   | Prep & Data Access                 | Design doc, CW1 log access, retrieval schema    |
| Week 1-2 | MVP Booking Validator              | Parser, rule-based validation, shadow mode      |
| Week 3-4 | Orchestrator + Guardrails          | Retrieval pipeline, guardrail checks, HITL flow |
| Week 5   | Refund & Terms Tool + Eval Harness | Refund stub, terms tool, LLM-as-Judge tests     |
| Week 6   | Live Pilot + Dashboard             | KPI baseline, operator training, pilot launch   |

---

## 10. Success Metrics

| Category     | Metric                             | Target           |
| ------------ | ---------------------------------- | ---------------- |
| Efficiency   | Touchless % per file               | +20%             |
| Adoption     | Active operators/month             | ≥ 80%            |
| Accuracy     | Eval pass rate                     | ≥ 85%            |
| Trust        | UMUX-Lite score                    | > 75             |
| Satisfaction | BUS-11 overall score               | > 80 (Very Good) |
| Learning     | Accuracy improvement per iteration | +10%/quarter     |

---

## 11. References & Further Reading

* “Introducing Contextual Retrieval” (Anthropic, Sept 19 2024) — blog post explaining how to dramatically improve retrieval failure rates. ([anthropic.com][1])
* “Beyond Naive RAG: Practical Advanced Methods” — open mini-book on advanced retrieval techniques. ([hamelhusain.substack.com][2])
* “Beyond Basic RAG: A Practical Guide to Advanced Indexing Techniques” (Towards AI, Oct 7 2025) — deep dive on chunking/indexing strategies. ([Towards AI][3])
* “RAFT: Adapting Language Model to Domain Specific RAG” (ArXiv, Mar 2024) — research on fine-tuning retrieval for domain tasks. ([arXiv][4])
* “A New HOPE: Domain-agnostic Automatic Evaluation of Text Chunking” (ArXiv, May 2025) — research on evaluation of chunking strategies. ([arXiv][5])

---

### Tagline

**CargoX + CW1 + Azure AI = The Learning Freight Network**
From *Assisted UI* → *Orchestrated Intelligence* → *Autonomous Freight*.

---


[1]: https://www.anthropic.com/news/contextual-retrieval?utm_source=chatgpt.com "Contextual Retrieval in AI Systems"
[2]: https://hamelhusain.substack.com/p/beyond-naive-rag-a-new-free-mini?utm_source=chatgpt.com "Beyond Naive RAG: A new, free mini-book on advanced ..."
[3]: https://pub.towardsai.net/beyond-basic-rag-a-practical-guide-to-advanced-indexing-techniques-a3efe7c6d78c?utm_source=chatgpt.com "Beyond Basic RAG: A Practical Guide to Advanced ..."
[4]: https://arxiv.org/abs/2403.10131?utm_source=chatgpt.com "RAFT: Adapting Language Model to Domain Specific RAG"
[5]: https://arxiv.org/abs/2505.02171?utm_source=chatgpt.com "A New HOPE: Domain-agnostic Automatic Evaluation of Text Chunking"
