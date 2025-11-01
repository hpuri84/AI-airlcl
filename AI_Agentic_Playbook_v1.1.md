# AI Agentic Playbook v1.1

### CargoX — Air & LCL Orchestrated Intelligence

**Version**: 1.1  
**Date**: November 2025  
**Status**: Production Ready

---

## Document Overview

**Purpose**: Enable the next generation of freight operations through agentic AI — from assisted UIs to orchestrated, self-learning workflows. CargoX acts as the intelligence layer over core systems (CargoWise One, ERP, EDI), delivering end-to-end automation for Booking → Quotation → Consolidation → Invoice → Feedback.

**What's New in v1.1**:
- ✨ **Email/Attachment Intake Automation Blueprint** (§12)
- ✨ **Multi-Agent Coordination Patterns Catalog** (§2.3)
- ✨ **Human-Agent Interaction Patterns** (§13)
- ✨ **Trust Indicators & UI Component Library** (§14)
- ✨ **Conversational AI Evaluation Framework** (§15)
- ✨ **Agent Persona Cards** with detailed RACI (§3)
- ✨ **RAG Feedback Loop Operationalization** (§7)
- ✨ **Governance & Security Policies** (§16)
- ✨ **Observability & Operations** (§17)
- ✨ **Adoption & Change Management** (§18)

---

## Table of Contents

1. [Vision & Principles](#1-vision--principles)
2. [Architecture Overview](#2-architecture-overview)
   - 2.1 [CargoX Agent Stack](#21-cargox-agent-stack)
   - 2.2 [Freight Graph Knowledge Layer](#22-freight-graph-knowledge-layer)
   - 2.3 [Multi-Agent Coordination Patterns](#23-multi-agent-coordination-patterns)
3. [Agent Persona Cards](#3-agent-persona-cards)
4. [Retrieval & RAG Pipeline](#4-retrieval--rag-pipeline)
5. [Trust Maturity Model](#5-trust-maturity-model)
6. [Human-Agent Collaboration](#6-human-agent-collaboration)
7. [RAG Feedback & Learning Loop](#7-rag-feedback--learning-loop)
8. [Capability Mapping](#8-capability-mapping)
9. [Success Metrics & KPIs](#9-success-metrics--kpis)
10. [Timeline & Rollout](#10-timeline--rollout)
11. [References](#11-references)
12. [Email/Attachment Intake Blueprint](#12-emailattachment-intake-blueprint)
13. [Human-Agent Interaction Patterns](#13-human-agent-interaction-patterns)
14. [Trust Indicators & UI Components](#14-trust-indicators--ui-components)
15. [Conversational AI Evaluation](#15-conversational-ai-evaluation)
16. [Governance & Security](#16-governance--security)
17. [Observability & Operations](#17-observability--operations)
18. [Adoption & Change Management](#18-adoption--change-management)

---

## 1. Vision & Principles

### Vision Statement

**From Manual to Intelligent**: Transform freight operations from manual, error-prone processes to self-learning, orchestrated workflows where AI agents handle routine tasks, operators focus on exceptions, and the system continuously improves through feedback.

### Core Principles

| Principle | Implementation Checklist |
|-----------|-------------------------|
| **Transparency by Design** | ✅ Source citations for every AI claim<br>✅ Confidence scores (High/Medium/Low)<br>✅ Reasoning traces ("How I decided")<br>✅ Audit logs for all actions |
| **Human-in-the-Loop (HITL)** | ✅ Approval gates by risk level (Low: auto, Medium: confirm, High: review)<br>✅ Override controls (edit AI output before execution)<br>✅ Escalation triggers (confidence < 70%, DG cargo, high value) |
| **Continuous Learning** | ✅ Feedback capture (👍👎 + corrections)<br>✅ Learning Agent analyzes patterns weekly<br>✅ A/B testing before deployment<br>✅ Visible feedback loop ("Your correction helped...") |
| **Trust through Explainability** | ✅ Confidence badges on all outputs<br>✅ Source badges (e.g., "CW1 Audit Log, 5 min ago")<br>✅ Decision journal (what, why, when, who approved)<br>✅ Rollback capability for any agent action |
| **Governance & Safety** | ✅ PII detection and redaction<br>✅ Financial approval gates (>$50k requires human)<br>✅ DG specialist approval for hazardous cargo<br>✅ Incident response runbooks<br>✅ Quarterly bias/fairness audits |
| **Experience-Driven Adoption** | ✅ UMUX-Lite surveys (monthly)<br>✅ BUS-11 conversational usability (quarterly)<br>✅ Shadow → Confirm → Autonomous progression<br>✅ Training materials and sandbox environment |

### Trust Maturity Model

Operators progress through stages as trust builds:

```
Stage 1: Shadow Mode (Week 1-4)
- Agent suggests, human always executes
- Goal: Learn patterns, build familiarity
- Success: 50+ interactions, UMUX-Lite > 65

Stage 2: Confirm Mode (Week 5-12)
- Agent executes after human approval
- Goal: Reduce operator workload by 30%
- Success: Approval rate > 80%, UMUX-Lite > 75

Stage 3: Autonomous Mode (Week 13-20)
- Agent executes for high-confidence cases (>90%)
- Human monitors exceptions
- Goal: 50% touchless rate
- Success: Accuracy > 90%, escalation < 25%

Stage 4: Proactive Mode (Week 21+)
- Agent initiates conversations ("Should we consolidate these 5 bookings?")
- Goal: 70% touchless rate, proactive optimization
- Success: UMUX-Lite > 80, BUS-11 > 80
```

---

## 2. Architecture Overview

### 2.1 CargoX Agent Stack

```
[Customer/Operator/Partner]
          ↓
  [CargoX Orchestrator Agent]
          ↓
  ┌───────────────────────────────────────┐
  │  Domain Agents (Multi-Agent System)   │
  ├───────────────────────────────────────┤
  │ 📧 Email Analyzer                     │
  │ ✅ Booking Validator                   │
  │ 💰 Rate Agent                          │
  │ 📦 Quotation Agent                     │
  │ 🚚 Consolidation Planner               │
  │ 📊 Forecast Agent                      │
  │ 🧾 Invoice Validator                   │
  │ 🎓 Learning Agent                      │
  │ ⚖️ Evaluation Agent (LLM-as-Judge)     │
  │ 🔧 Master Data Agent                   │
  │ 🛃 Customs Agent                        │
  │ 📞 Exception Handler                   │
  └───────────────────────────────────────┘
          ↓
  [Event Bus: order.received, booking.validated, operator.feedback, etc.]
          ↓
  ┌───────────────────────────────────────┐
  │  Integration Layer                    │
  ├───────────────────────────────────────┤
  │ • CargoWise One (CW1)                 │
  │ • ERP / Finance Systems               │
  │ • EDI / API Partners                  │
  │ • Email / Teams / Outlook             │
  │ • Warehouse Management Systems        │
  └───────────────────────────────────────┘
          ↓
  [Freight Graph: Knowledge Base]
  - CW1 logs (operational truth)
  - EDI events (real-time milestones)
  - Contracts (pricing, SLAs)
  - Rate Repository (procurement data)
  - SOPs (policy, process)
  - Emails/Notes (human context)
```

### 2.2 Freight Graph Knowledge Layer

**Purpose**: Unified cognitive map of freight operations accessible via RAG (Retrieval-Augmented Generation).

**Data Sources**:

| Source | Content | Update Frequency | Access Pattern |
|--------|---------|------------------|----------------|
| **CW1 Logs** | Bookings, shipments, invoices, master data | Real-time (event-driven) | Semantic search + SQL |
| **EDI Events** | Milestones (cargo ready, departed, arrived) | Real-time (event-driven) | Event query by HAWB/MAWB |
| **Customer Contracts** | Pricing, payment terms, SLAs, volume commitments | Weekly batch | Vector search by customer |
| **Rate Repository** | Supplier rates, validity dates, margins | Daily batch | Vector + filter by lane |
| **SOPs / Manuals** | DG handling, customs procedures, escalation rules | Monthly | Semantic search |
| **Emails / Notes** | Customer inquiries, operator decisions, exceptions | Real-time | Full-text + semantic |

**Retrieval Pipeline** (CargoX Standard):

```
1. Intent Detection
   Orchestrator analyzes user query → identifies intent (rate lookup, exception explanation, consol suggestion)

2. Route to Index
   Select correct Freight Graph partition (Rate DB, CW1 Logs, SOP Manual)

3. Hybrid Retrieval
   - Semantic: Embedding-based similarity (top 10)
   - Sparse: BM25 keyword match (top 10)
   - Merge and deduplicate

4. Reranking
   Cross-encoder reranks by relevance to query

5. Context Assembly
   Top 5 documents passed to agent with metadata (source, date, confidence)

6. Evaluation
   Evaluation Agent checks grounding (every claim cited?)
   - Pass: Return response to user
   - Fail: Escalate to human or retry with expanded context
```

**Evaluation Metrics** (Monthly Review):

| Metric | Target | Current | Trend |
|--------|--------|---------|-------|
| Grounding@K | ≥ 85% | 82% | ↗️ |
| Coverage@K | ≥ 80% | 78% | ↗️ |
| Diversity@K | ≥ 75% | 80% | ✅ |
| Latency SLO | < 6s | 4.2s | ✅ |
| Feedback Adoption | > 70% | 68% | ↗️ |

### 2.3 Multi-Agent Coordination Patterns

**Purpose**: Define how agents collaborate to complete complex workflows.

#### Pattern Catalog

| Pattern | Description | Example Workflow | Handoff Trigger | Compensation Strategy |
|---------|-------------|------------------|-----------------|----------------------|
| **Sequential Delegation** | Agent A completes → triggers Agent B | Email Analyzer → Booking Validator → Rate Agent | `booking.validated` event | Undo in reverse order |
| **Parallel Consultation** | Orchestrator queries multiple agents simultaneously, aggregates results | Orchestrator asks (Quotation + Capacity + Routing) → selects best | User query "find best route" | N/A (read-only) |
| **Hierarchical Escalation** | Agent tries → fails → escalates to senior agent or human | Booking Validator (confidence < 70%) → Exception Handler → Human Operator | Confidence threshold breach | Human decision logged as ground truth |
| **Collaborative Refinement** | Agents iterate together until consensus or threshold met | Rate Agent proposes margin → Invoice Validator checks → Rate Agent adjusts | Validation fails | Iteration limit (max 3 rounds) |
| **Human-in-the-Loop Gate** | Agent proposes → human reviews → agent executes only after approval | Consol Planner suggests grouping → Operator approves → CW1 Sync Agent books | High-risk action (DG cargo, >$50k, new customer) | Human approval required; no auto-execution |
| **Compensating Transaction** | Agent A executes → Agent B detects error → Agent C reverses | Booking Agent creates CW1 record → Validator detects duplicate → Cleanup Agent deletes | Error detected in audit | Idempotent operations; audit log retained |

#### Event Taxonomy for Freight Operations

**Core Events** (trigger agent activation):

| Event | Trigger Condition | Agent(s) Activated | Downstream Events | Payload Schema |
|-------|------------------|-------------------|-------------------|----------------|
| `order.received` | Email attachment parsed | Email Analyzer → Booking Validator | `booking.validated` or `booking.exception` | `{email_id, attachments[], parsed_fields{}}` |
| `booking.validated` | All mandatory fields present, rules passed | Rate Agent → Capacity Agent | `rate.calculated`, `capacity.checked` | `{booking_id, confidence, validation_result{}}` |
| `booking.exception` | Missing data, rule violation, low confidence | Exception Handler → Human Escalation | `operator.notified` | `{booking_id, exception_type, missing_fields[], reason}` |
| `rate.calculated` | Rate lookup complete | Quotation Agent | `quotation.generated` | `{booking_id, rate_details{}, margin, validity}` |
| `consol.created` | Planner finalizes consolidation | Invoice Generator → CW1 Sync Agent | `invoice.drafted`, `cw1.updated` | `{consol_id, booking_ids[], total_cbm, departure_date}` |
| `operator.feedback` | Human corrects agent output | Learning Agent → RAG Retraining | `model.retrained`, `prompt.updated` | `{agent_id, feedback_type, correction{}, operator_id, timestamp}` |
| `agent.error` | Agent throws exception | Exception Handler → On-Call Engineer | `incident.created`, `alert.sent` | `{agent_id, error_message, stack_trace, context{}}` |

**Event Flow Example** (Email to Booking):

```
1. Email arrives → `order.received`
   ↓
2. Email Analyzer extracts fields → `email.parsed`
   ↓
3. Booking Validator checks fields
   ├─ All valid → `booking.validated`
   └─ Missing data → `booking.exception` → Operator notified
   ↓
4. Rate Agent calculates margin → `rate.calculated`
   ↓
5. Quotation Agent generates quote → `quotation.generated`
   ↓
6. Operator approves → `booking.confirmed`
   ↓
7. CW1 Sync Agent creates booking → `cw1.booking_created`
   ↓
8. Confirmation email sent → `customer.notified`
```

---

## 3. Agent Persona Cards

### 🤖 Email Analyzer Agent

**Purpose**: Parse incoming emails and attachments to extract booking data.

**Inputs**:
- Raw email (subject, body, attachments)
- Email metadata (sender, timestamp, thread_id)

**Outputs**:
- `email.parsed` event with structured data:
  ```json
  {
    "origin": "CNSHA",
    "destination": "NLRTM",
    "shipper": "Acme Corp",
    "consignee": "Global Logistics BV",
    "cargo_details": {
      "pieces": 10,
      "weight_kg": 500,
      "cbm": 2.5,
      "commodity": "Electronics"
    },
    "ready_date": "2025-11-10",
    "confidence": 0.92
  }
  ```

**Decision Logic**:
1. Extract key fields using document intelligence
2. Normalize location codes (Amsterdam → NLAMS)
3. Parse dates (multiple formats supported)
4. Calculate CBM if dimensions provided
5. Return confidence score based on extraction certainty

**Escalation Rules**:
- Confidence < 80% → Flag for human review
- Attachment format unsupported (not PDF/Excel/Word) → Escalate
- Email language not English → Trigger translation + re-parse

**Learning Inputs**:
- Operator corrections on extracted fields
- New email formats (added to training set)

**Evaluation Metrics**:
- Field extraction accuracy: 95% target
- Parsing success rate: 98% target
- Avg processing time: < 10s

---

### ✅ Booking Validator Agent

**Purpose**: Validate booking requests against business rules, master data, and capacity constraints.

**Inputs**:
- Parsed booking data (from Email Analyzer or manual entry)
- CW1 master data (shipper, consignee, locations)
- Rate cards, DG regulations, capacity calendars

**Outputs**:
- `booking.validated` event (if pass) with confidence score
- `booking.exception` event (if fail) with:
  - Missing fields highlighted
  - Suggested corrections
  - Reason for rejection

**Decision Logic**:
1. **Mandatory Field Check**
   - Origin, destination, cargo details, ready date
   - If missing → `booking.exception`

2. **Master Data Validation**
   - Cross-check shipper/consignee against CW1
   - If not found → Trigger Master Data Agent (create new or link existing)

3. **DG Regulation Check**
   - If hazardous cargo detected → Validate against DG database
   - If Class 1-9 → Require DG specialist approval

4. **Capacity Check**
   - Calculate CBM, check against available capacity
   - If overbooked → Suggest alternate dates

5. **Margin Check**
   - If margin < 5% → Flag for review
   - If margin < 0% → Reject

6. **Confidence Scoring**
   - High (>90%): All checks pass, master data match perfect
   - Medium (70-90%): Minor issues (e.g., location alias)
   - Low (<70%): Missing critical data or multiple issues

**Escalation Rules**:
- Confidence < 70% → Exception Handler → Operator review
- DG cargo → DG Compliance Officer approval required
- New shipper (not in CW1) → Master Data Agent → Operator confirms
- Margin < 0% → Rate Agent recalculates → Operator approves pricing

**Learning Inputs**:
- Operator corrections on validation errors
- Acceptance/rejection of suggested corrections
- New business rules (added to rule engine)

**Evaluation Metrics**:
- Validation accuracy: 92% target (% of bookings correctly validated)
- Touchless rate: 60% target (% auto-approved without human intervention)
- False positive rate: < 8% (% incorrectly flagged)
- False negative rate: < 3% (% incorrectly approved)

---

### 💰 Rate Agent

**Purpose**: Lookup rates, calculate margins, and recommend pricing.

**Inputs**:
- Booking details (origin, destination, CBM, weight, commodity)
- Rate repository (supplier rates, customer contracts)
- Historical pricing (for trend analysis)

**Outputs**:
- `rate.calculated` event with:
  - Buy rate (from supplier)
  - Sell rate (to customer)
  - Margin (absolute & percentage)
  - Validity period

**Decision Logic**:
1. **Rate Lookup**
   - Query Rate Repository by lane (origin → destination)
   - Filter by validity date
   - Select best rate (lowest cost or preferred supplier)

2. **Margin Calculation**
   - Sell Rate = Buy Rate + Margin %
   - Apply customer-specific discounts (from contract)

3. **Dynamic Pricing** (if enabled)
   - Adjust margin based on:
     - Capacity utilization (high demand → +5%)
     - Customer tier (VIP → -2%)
     - Market trends (spot rate vs contract rate)

4. **Rate Recommendation**
   - If margin < 5% → Suggest higher sell rate
   - If competitor rate available → Compare and flag

**Escalation Rules**:
- Margin < 5% → Highlight for operator review
- No rate found → Escalate to procurement team
- Rate expired → Request updated rate from supplier

**Learning Inputs**:
- Operator overrides on pricing
- Won/lost deal analysis (was our rate competitive?)

**Evaluation Metrics**:
- Rate accuracy: 98% (correct rate retrieved)
- Margin optimization: +3% avg improvement vs baseline
- Rate lookup latency: < 2s

---

### 📦 Quotation Agent

**Purpose**: Generate customer-facing quotations from booking and rate data.

**Inputs**:
- Validated booking details
- Calculated rates (from Rate Agent)
- Customer contract terms (payment, currency, surcharges)

**Outputs**:
- `quotation.generated` event
- PDF quotation document (branded, multi-language)
- Email draft to customer

**Decision Logic**:
1. **Quotation Template Selection**
   - Select template by customer type (SMB, Enterprise) and product (Air, LCL)

2. **Content Assembly**
   - Booking summary (origin → destination, cargo details)
   - Pricing breakdown (base rate, fuel surcharge, handling, total)
   - Terms & Conditions (from customer contract)
   - Validity period (typically 7 days)

3. **Multi-Currency Support**
   - Convert to customer's preferred currency

4. **Approval Workflow** (if required)
   - If custom terms → Operator approves before sending

**Escalation Rules**:
- Custom pricing (not in rate card) → Operator approval
- Large quote (>$50k) → Finance Manager approval
- New customer (no contract) → Sales approval

**Learning Inputs**:
- Quote acceptance rate (did customer book?)
- Time to respond (faster = higher conversion?)

**Evaluation Metrics**:
- Quote generation time: < 1 min
- Acceptance rate: 65% target
- Error rate: < 1% (incorrect pricing, T&C)

---

### 🚚 Consolidation Planner Agent

**Purpose**: Optimize consolidation of bookings to maximize capacity utilization and margin.

**Inputs**:
- All validated bookings (by destination, ready date)
- Capacity constraints (container size, weight limits)
- Business rules (min margin, customer priority)

**Outputs**:
- `consol.created` event with:
  - Consol ID
  - List of booking IDs
  - Total CBM, weight
  - Departure date, route
  - Expected margin

**Decision Logic**:
1. **Clustering**
   - Group bookings by:
     - Destination (same airport/port)
     - Ready date (±2 days)
     - Customer priority (VIP first)

2. **Bin Packing Optimization**
   - Maximize CBM utilization (target: >85%)
   - Respect weight limits
   - Avoid mixing incompatible cargo (DG + non-DG)

3. **Margin Optimization**
   - Prioritize high-margin bookings
   - If capacity limited, drop low-margin bookings

4. **Constraint Satisfaction**
   - Min 5 bookings per consol (else not economical)
   - Max 20 bookings (operational complexity)

5. **Recommendation**
   - Present top 3 consol options to operator
   - Operator selects or modifies

**Escalation Rules**:
- Low utilization (<70%) → Flag for operator review (wait for more bookings?)
- High-risk cargo (DG, high-value) → Operator approves grouping
- New lane (no historical data) → Request operator confirmation

**Learning Inputs**:
- Actual vs planned CBM (were estimates accurate?)
- Consol profitability (margin vs operational cost)
- Operator modifications (which consols were adjusted?)

**Evaluation Metrics**:
- Utilization rate: 85% target
- Margin per consol: +10% vs individual bookings
- Planning time: < 5 min for 50 bookings

---

### 🎓 Learning Agent

**Purpose**: Analyze operator feedback, identify patterns, and propose improvements to other agents.

**Inputs**:
- `operator.feedback` events (corrections, thumbs up/down, comments)
- Agent performance metrics (accuracy, latency, escalation rate)
- Evaluation Agent scores (LLM-as-Judge ratings)

**Outputs**:
- `improvement.proposed` event with:
  - Target agent (e.g., Booking Validator)
  - Change type (prompt update, rule addition)
  - Expected impact (+5% accuracy)
  - A/B test plan

**Decision Logic**:
1. **Pattern Recognition** (weekly batch)
   - Aggregate all corrections for each agent
   - Identify common error types (e.g., "50% of shipper mismatches due to trade name vs legal name")

2. **Root Cause Analysis**
   - Is error due to:
     - Missing data in training?
     - Ambiguous prompt?
     - Incorrect business rule?
     - External data issue (e.g., CW1 master data outdated)?

3. **Improvement Hypothesis**
   - Generate candidate fix (e.g., "Always search by legal name first, then trade name")

4. **Validation**
   - Flag for Evaluation Agent to A/B test

5. **Deployment Recommendation**
   - If improvement confirmed (>5%) → Recommend deployment
   - If no improvement → Log for future analysis

**Escalation Rules**:
- Accuracy drop detected (>10% in 1 week) → Alert on-call team
- Conflicting feedback (operators disagree on correction) → Escalate to domain expert

**Learning Inputs**:
- Historical improvement deployments (what worked?)
- Inter-agent patterns (does fixing Agent A help Agent B?)

**Evaluation Metrics**:
- Learning velocity: +5% accuracy per quarter target
- Feedback adoption rate: >70% of corrections incorporated
- Time to deployment: <7 days from correction to model update

---

### ⚖️ Evaluation Agent (LLM-as-Judge)

**Purpose**: Continuously assess quality of agent outputs before and after deployment.

**Inputs**:
- Agent outputs (responses, actions, decisions)
- Ground truth (human-labeled data, historical outcomes)
- Evaluation criteria (accuracy, grounding, helpfulness, safety)

**Outputs**:
- `evaluation.completed` event with:
  - Overall score (1-5 scale)
  - Per-criterion scores (accuracy, completeness, grounding, helpfulness, safety, tone)
  - Reasoning (why this score?)
  - Improvement suggestions

**Evaluation Modes**:

1. **Offline Evaluation** (pre-deployment)
   - Test new agent/prompt on curated test set (100+ samples)
   - Compare against ground truth
   - Metrics: Precision, Recall, F1, Grounding@K
   - Gate: Must achieve >85% accuracy to deploy

2. **Online Evaluation** (production)
   - Monitor agent outputs in real-time
   - Flag anomalies:
     - Sudden accuracy drop (>10% in 1 hour)
     - High escalation rate (>50%)
     - Latency spike (>10s avg)
   - Metrics: Latency, error rate, operator thumbs up rate
   - Alert: If threshold breached → Page on-call

3. **Human-in-the-Loop Evaluation** (periodic audit)
   - Sample 100 agent outputs per week
   - Human expert scores quality (1-5 scale)
   - Metrics: Inter-rater agreement, BUS-11 score
   - Review: Monthly review with stakeholders

**Evaluation Criteria** (per agent output):

| Criterion | 1 (Poor) | 3 (Acceptable) | 5 (Excellent) |
|-----------|----------|----------------|---------------|
| **Factual Accuracy** | Wrong info | Mostly correct | Fully correct |
| **Completeness** | Missing key info | Sufficient | All details present |
| **Grounding** | No sources cited | Some citations | Every claim cited |
| **Helpfulness** | Doesn't answer question | Answers question | Exceeds expectations |
| **Safety** | Harmful suggestion | Safe but generic | Safe and specific |
| **Tone** | Inappropriate | Professional | Empathetic |

**Judgment Logic** (LLM-as-Judge Prompt):

```
You are an expert evaluator for freight operations AI agents.

Given:
- User query: {query}
- Agent response: {response}
- Retrieved sources: {sources}
- Ground truth (if available): {ground_truth}

Evaluate the response on a 1-5 scale for:
1. Factual accuracy (1=wrong, 5=correct)
2. Completeness (1=missing key info, 5=complete)
3. Grounding (1=no sources cited, 5=every claim cited)
4. Helpfulness (1=not useful, 5=very useful)
5. Safety (1=harmful, 5=safe)
6. Tone (1=inappropriate, 5=perfect)

Provide:
- Overall score (average of 6 criteria)
- Reasoning (2-3 sentences explaining your scores)
- Improvement suggestions (if score < 4, what should agent do differently?)

Format as JSON:
{
  "scores": {"accuracy": 4, "completeness": 5, ...},
  "overall": 4.3,
  "reasoning": "...",
  "suggestions": "..."
}
```

**Escalation Rules**:
- Overall score < 3 → Block response, escalate to human
- Grounding < 3 → Retrain retrieval pipeline
- Safety < 4 → Block response, escalate to safety team, log for review
- Consistent low scores (>20% below threshold) → Pause agent, trigger review

**Learning Integration**:
- Low-scoring patterns → Learning Agent analyzes root cause
- High-scoring patterns → Promoted as best practices, used for few-shot prompting

**Evaluation Metrics**:
- Eval coverage: 100% of agent outputs (online mode)
- Eval latency: < 500ms (should not slow down agents)
- Human agreement: >90% (does human agree with LLM judge?)

---

## 4. Retrieval & RAG Pipeline

### RAG Feedback Capture Workflow

**Scenario**: Booking Validator returns incorrect shipper match.

**Operator Action** (via UI):
1. Click "Incorrect match" next to suggested shipper
2. Select correct shipper from dropdown or create new
3. Optionally add comment: "Use full legal name, not trade name"
4. Submit feedback

**System Response**:
1. Log feedback with:
   - Timestamp, operator ID
   - Context (query, retrieved docs, agent's answer, correct answer)
   - Severity (minor: typo, major: wrong entity)
2. Label as "correction" type
3. Queue for Learning Agent review (weekly batch)

**Learning Agent** (runs weekly):
1. Aggregate all corrections for Booking Validator
2. Identify patterns:
   - Example: "50% of shipper mismatches due to trade name vs legal name"
3. Generate improvement hypothesis:
   - "Always search by legal name first, then trade name as fallback"
4. Create updated prompt/retrieval strategy
5. Flag for Evaluation Agent A/B test

**Evaluation Agent**:
1. Run A/B test:
   - Control: Current prompt
   - Treatment: New prompt
   - Test set: 100 held-out bookings
2. Measure improvement:
   - Grounding@K: +8% (92% → 100%)
   - Operator approval rate: +12% (78% → 90%)
3. If improvement > 5% → Recommend deployment

**Deployment**:
1. Orchestrator updates Booking Validator prompt in production
2. Monitor for 2 weeks:
   - Track accuracy, escalation rate
   - Collect operator feedback
3. If regression detected → Rollback to previous version

**Visible Feedback Loop**:
- Operator sees toast: "Thanks for your feedback! We're analyzing patterns to improve."
- 1 week later: "Your correction helped improve shipper matching by 12%. Keep the feedback coming!"

### Retrieval Use Case Examples

| Query Type | Example Query | Expected Retrieval | Grounding Source | Success Criteria |
|------------|--------------|-------------------|------------------|------------------|
| **Shipper Lookup** | "Find shipper for email john@acme.com" | Acme Corp master data record | CW1 customer DB | Correct shipper returned with >90% confidence |
| **Rate Inquiry** | "What's the rate for 10 CBM Shanghai → Rotterdam?" | Rate card with validity dates, margin | Rate Repository | Correct rate within ±5% of actual |
| **SOP Question** | "What's the DG process for Class 3 flammable liquids?" | DG handling SOP, approval workflow | SOP manual, historical logs | Complete procedure with approval steps |
| **Exception Explanation** | "Why was booking #12345 rejected?" | Rejection reason, business rule violated | CW1 audit log, rule engine | Correct reason with rule reference |
| **Consol Optimization** | "Which bookings should I consolidate for tomorrow's flight?" | Bookings by destination, CBM, margin | CW1 operational data, capacity calendar | Top 3 consol options with utilization >80% |
| **Historical Analysis** | "Show me all delayed shipments to NLAMS in Q3" | Shipment records with ATD vs ETA | CW1 logs, EDI events | All delayed shipments (recall >95%) |

---

## 5. Trust Maturity Model

(See [§1 Vision & Principles](#1-vision--principles) for details)

**Summary**: Operators progress through 4 stages (Shadow → Confirm → Autonomous → Proactive) as trust builds through successful interactions, transparent decision-making, and visible improvement.

---

## 6. Human-Agent Collaboration

### Agent → Human Handoff Sequence

```
1. Agent attempts task (e.g., Booking Validator validates booking)
   ↓
2. Confidence < threshold (70%) OR rule violation detected
   ↓
3. Agent generates handoff package:
   - Context: "Attempted to validate booking #67890"
   - Reason: "Shipper 'ABC Ltd' not found in CW1 master data (confidence: 62%)"
   - Suggested next steps: 
     a. Link to existing shipper (top 3 matches shown)
     b. Create new shipper (draft master data pre-filled)
     c. Reject booking (reason: incomplete data)
   - Draft for review: "Hi [Customer], we need clarification on shipper details..."
   ↓
4. Notification sent to operator
   - Channel: Teams message, email alert, app push notification
   - Priority: Medium (not urgent, but needs attention today)
   ↓
5. Operator reviews handoff package in UI
   ↓
6. Operator takes action:
   a. Approve agent's suggestion → Agent completes task
   b. Edit agent's suggestion → Agent executes edited version
   c. Reject and handle manually → Agent logs outcome for learning
   ↓
7. Outcome logged with operator feedback
   - Decision made, reasoning, time spent
   ↓
8. Learning Agent analyzes pattern (weekly)
   - Was escalation necessary?
   - Could agent have handled this with better data/prompt?
```

### Human → Agent Delegation Patterns

| Delegation Type | Trigger | Example | Agent Response | Follow-Up |
|----------------|---------|---------|----------------|-----------|
| **Explicit Command** | Operator types instruction | "Create a consol for all NL bookings tomorrow" | Agent confirms parameters → executes → reports back | "Created consol #4567 with 8 bookings, 12.5 CBM, departure 2025-11-11" |
| **Approval Workflow** | Operator approves AI suggestion | Agent suggests consol → operator clicks "Approve" | Agent executes immediately | "Consol #4567 created and synced to CW1" |
| **Batch Automation** | Operator sets rule | "Auto-approve all bookings < 5 CBM with high confidence" | Agent applies rule going forward | Dashboard shows auto-approved bookings (daily summary) |
| **Background Monitoring** | Operator subscribes to alerts | "Notify me if any booking > $10k margin" | Agent monitors, sends alert when triggered | "Alert: Booking #67891 has $12k margin, requires review" |
| **Scheduled Task** | Operator configures schedule | "Generate consol plan every Friday at 3pm" | Agent runs on schedule, sends results to operator | "Consol plan for week 45 ready, 3 options presented" |

### Three Levels of Autonomy

| Mode | Agent Behavior | Human Role | Use When | Example |
|------|---------------|------------|----------|---------|
| **1. Passive Log** | Agent observes and logs, never executes | Human reviews logs, executes manually | Initial rollout, high-risk scenarios | Shadow mode (Week 1-4) |
| **2. Confirm** | Agent proposes action, waits for approval | Human approves/edits before execution | Medium confidence, moderate risk | Confirm mode (Week 5-12) |
| **3. Autonomous** | Agent executes, human monitors exceptions | Human intervenes only if escalated | High confidence, low risk | Autonomous mode (Week 13+) |

**Escalation Triggers** (force human review):

- **Low Confidence**: Agent confidence < 70%
- **High Value**: Booking value > $50k
- **DG Cargo**: Hazardous materials (Class 1-9)
- **New Customer**: First booking from unknown shipper
- **Policy Violation**: Exceeds customer credit limit, invalid T&C
- **Anomaly**: Unusual pattern (e.g., 10x normal booking size)

---

## 7. RAG Feedback & Learning Loop

(See [§4 Retrieval & RAG Pipeline](#4-retrieval--rag-pipeline) for detailed workflow)

### Learning SLOs (Service Level Objectives)

| Metric | Target | Measurement Frequency | Owner | Current Performance |
|--------|--------|-----------------------|-------|---------------------|
| **Feedback Response Time** | < 7 days from correction to model update | Weekly | Learning Agent Team | 6.2 days ↗️ |
| **Accuracy Improvement Rate** | +5% per quarter (e.g., 85% → 90%) | Quarterly | Evaluation Agent | +4.2% Q3 ↗️ |
| **Feedback Adoption Rate** | > 70% of operator corrections incorporated | Monthly | Learning Agent | 68% ↗️ |
| **False Positive Reduction** | -10% per quarter | Quarterly | Evaluation Agent | -8% Q3 ↗️ |
| **Escalation Rate Reduction** | -15% per quarter | Quarterly | Orchestrator Team | -12% Q3 ↗️ |
| **Operator Satisfaction** | UMUX-Lite > 75 | Monthly | UX Team | 73 ↗️ |

---

## 8. Capability Mapping

### Core Capabilities (from Use Case Exploration)

| Capability | Agent | UX Pattern | Eval Metric | Confidence Signal | Asset Ref |
|------------|-------|------------|-------------|-------------------|-----------|
| **Email/Attachment Intake** | Email Analyzer | Background worker + exception queue | Extraction accuracy, touchless rate | 🟢 High (92%) | Use Case p.4 |
| **Booking Validation** | Booking Validator | Inline approval + exception highlights | Validation accuracy, false positive rate | 🟢 High (94%) | Use Case p.5 |
| **Quotation Automation** | Quotation Agent | Side panel suggestion + email draft | Quote acceptance rate, generation time | 🟠 Medium (78%) | Use Case p.6 |
| **Consolidation Planning** | Consol Planner | Dashboard + interactive optimization | Utilization rate, margin improvement | 🟠 Medium (82%) | Use Case p.7 |
| **Forecast / ETA Prediction** | Forecast Agent | Dashboard + "Why this forecast?" | Forecast accuracy (MAPE), confidence interval | 🟠 Medium (75%) | Use Case p.8 |
| **Invoice Validation** | Invoice Validator | Inline diff view + highlight discrepancies | Error detection rate, false positives | 🟢 High (96%) | Use Case p.9 |
| **Customer Communication** | Customer Assistant | Teams/Email chat + sentiment analysis | CSAT, response time, BUS-11 | 🟠 Medium (79%) | Use Case p.10 |
| **Supplier Contract Validation** | Contract Validator | Inline approval + risk scoring | Risk reduction rate, compliance % | 🟢 High (88%) | Use Case p.5 |
| **Rate Conversion (Doc → Data)** | Rate Converter | Batch upload + validation review | Conversion accuracy, processing time | 🟠 Medium (91%) | Use Case p.5 |
| **Dynamic Routing** | Routing Weaver | Dashboard + scenario comparison | Route acceptance rate, margin impact | 🟠 Medium (73%) | Use Case p.14 |
| **Warehouse Coordination** | Warehouse Agent | Mobile app + voice commands | Task completion rate, error rate | 🟢 High (92%) | Use Case p.14-15 |
| **Customs Document Generation** | Customs Agent | Auto-generate + compliance check | Submission success rate, rejection rate | 🟢 High (94%) | Use Case p.15-16 |
| **BI Forecasting & Reporting** | Forecast Agent | Dashboard + scheduled reports | Forecast accuracy (MAPE), report timeliness | 🟠 Medium (80%) | Use Case p.16 |

### Confidence Signal Legend

- 🟢 **High (>85%)**: Touchless automation, human rarely needed
- 🟠 **Medium (70-85%)**: Human-in-the-loop confirmation, agent proposes
- 🔴 **Low (<70%)**: Agent assists, human drives decision

---

## 9. Success Metrics & KPIs

### North Star Metrics

| Category | Metric | Baseline (Pre-AI) | Target (Year 1) | Current | Trend |
|----------|--------|------------------|----------------|---------|-------|
| **Efficiency** | Touchless booking rate | 0% | 70% | 42% | ↗️ |
| **Accuracy** | Booking validation accuracy | 88% (manual) | 95% | 94% | ↗️ |
| **Speed** | Time to quote (email → quote sent) | 4 hours | 15 minutes | 28 minutes | ↗️ |
| **Quality** | Invoice error rate | 12% | 3% | 5% | ↗️ |
| **Satisfaction** | Operator UMUX-Lite score | N/A | 80 | 73 | ↗️ |
| **Trust** | BUS-11 conversational usability | N/A | 80 (Very Good) | 76 (Good) | ↗️ |

### Agent-Level KPIs (Tracked Monthly)

| Agent | Key Metric | Target | Current | Action if Below Target |
|-------|-----------|--------|---------|----------------------|
| Email Analyzer | Extraction accuracy | >90% | 92% | ✅ On track |
| Booking Validator | Validation accuracy | >92% | 94% | ✅ On track |
| Booking Validator | Touchless rate | >60% | 42% | ⚠️ Review escalation rules; are thresholds too conservative? |
| Rate Agent | Rate accuracy | >98% | 99% | ✅ On track |
| Quotation Agent | Quote acceptance rate | >65% | 58% | ⚠️ Analyze rejected quotes; is pricing competitive? |
| Consol Planner | Utilization rate | >85% | 82% | ⚠️ Review grouping algorithm; wait for more bookings? |
| Invoice Validator | Error detection rate | >95% | 96% | ✅ On track |
| Learning Agent | Feedback adoption rate | >70% | 68% | ⚠️ Prioritize high-impact corrections first |
| Evaluation Agent | Human agreement rate | >90% | 91% | ✅ On track |

---

## 10. Timeline & Rollout

### Phase 1: Foundation (Weeks 1-4)

**Goal**: Establish governance, evaluation, trust components, and architecture baseline.

| Week | Focus | Deliverables | Owner | Exit Criteria |
|------|-------|--------------|-------|--------------|
| **1** | Governance & Policies | Policy framework (data privacy, financial risk, safety, incident response) | Compliance + AI Lead | ✅ Policies approved by Legal & Leadership |
| **2** | Evaluation Framework | Metrics library (UMUX-Lite, BUS-11, accuracy), LLM-as-Judge setup, test data (100+ samples) | Data Science | ✅ Eval framework validated; baseline scores established |
| **3** | Trust & UI Components | Component library (confidence badges, source citations, approval buttons, feedback UI) | UX Designer + Frontend | ✅ Components deployed to design system; React library published |
| **4** | Architecture Baseline | Event schemas (order.received, booking.validated, etc.), agent personas, integration adapters | Solution Architect | ✅ Architecture review completed; event bus configured |

---

### Phase 2: Email Intake MVP (Weeks 5-8)

**Goal**: Deploy end-to-end email → booking automation in **shadow mode**.

| Week | Focus | Deliverables | Owner | Success Metrics |
|------|-------|--------------|-------|----------------|
| **5** | Email Ingestion | Email Analyzer agent, attachment parser (PDF, Excel, Word), event publisher | Backend Engineer | 50 emails processed/week |
| **6** | Booking Validation | Booking Validator agent, validation rule engine, CW1 master data lookup | Backend + Domain Expert | Validation accuracy > 80% |
| **7** | HITL UI | Approval dashboard, exception queue, feedback buttons (👍👎 + comments) | Frontend Engineer | Operator can review 100% of validations |
| **8** | Pilot Launch | Shadow mode: 50 emails/week, all reviewed by operators | Full Team | Extraction accuracy > 85%, Operator UMUX-Lite > 70 |

**Rollback Plan**: If accuracy < 70%, disable auto-validation; revert to manual email processing.

---

### Phase 3: Learning Loop & Scale (Weeks 9-12)

**Goal**: Enable continuous improvement; scale to 200 emails/week in **confirm mode**.

| Week | Focus | Deliverables | Owner | Success Metrics |
|------|-------|--------------|-------|----------------|
| **9** | Learning Agent | Feedback analysis pipeline, prompt improvement recommender, A/B test framework | Data Science | 20+ corrections collected; 1 prompt update identified |
| **10** | Evaluation Agent | LLM-as-Judge deployed, A/B testing live, offline eval suite (100 test cases) | Data Science | Eval Agent scores 100% of outputs; human agreement > 85% |
| **11** | Orchestrator Enhancements | Multi-agent coordination (Email Analyzer → Booking Validator → Rate Agent), exception routing | Backend Engineer | 3-agent workflow live; handoffs < 10s latency |
| **12** | Scale to Confirm Mode | Operators approve before CW1 sync; 200 emails/week | Full Team | Touchless rate > 30%, Escalation rate < 35%, UMUX-Lite > 75 |

---

### Phase 4: Advanced Capabilities (Weeks 13-16)

**Goal**: Add Rate Agent, Quotation Agent; integrate CargoWise One; achieve **50% touchless**.

| Week | Focus | Deliverables | Owner | Success Metrics |
|------|-------|--------------|-------|----------------|
| **13** | Rate Agent | Rate lookup, margin calculation, dynamic pricing logic | Backend + Domain Expert | Rate accuracy > 95%, Lookup latency < 2s |
| **14** | Quotation Agent | Auto-generate quotes, PDF templates, email integration | Backend + Domain Expert | Quote generation < 1 min, Acceptance rate > 55% |
| **15** | CargoWise Integration | Event bus adapters (CW1 ↔ CargoX), master data sync, financial posting | Integration Engineer | CW1 sync success rate > 99%, Latency < 5s |
| **16** | End-to-End Flow | Email → Parse → Validate → Rate → Quote → Approve → CW1 Book | Full Team | 500 emails/week, 50% touchless, Accuracy > 92% |

---

### Phase 5: Full Autonomy & Expansion (Weeks 17-26)

**Goal**: Achieve **70% touchless rate**; deploy proactive agents; expand to all regions.

| Weeks | Focus | Deliverables | Success Metrics |
|-------|-------|--------------|----------------|
| **17-20** | Autonomous Mode | High-confidence bookings (>90%) auto-executed; no human approval required | 60% touchless, Escalation rate < 25% |
| **21-22** | Proactive Agents | Agents initiate conversations ("Should we consolidate?"), suggest optimizations | 65% touchless, Proactive suggestions accepted >50% |
| **23-24** | Voice Agent | Warehouse coordination via voice commands (mobile app, wearables) | Voice task completion rate > 85% |
| **25-26** | Regional Expansion | Deploy to EMEA, APAC, Americas; localize for multi-language, multi-currency | 70% touchless globally, UMUX-Lite > 80, BUS-11 > 80 |

---

## 11. References

**RAG & Retrieval**:
- [Introducing Contextual Retrieval](https://www.anthropic.com/news/contextual-retrieval) (Anthropic, Sept 2024)
- [Beyond Naive RAG: Practical Advanced Methods](https://hamelhusain.substack.com/p/beyond-naive-rag-a-new-free-mini) (Hamel Husain)
- [Beyond Basic RAG: Advanced Indexing Techniques](https://pub.towardsai.net/beyond-basic-rag-a-practical-guide-to-advanced-indexing-techniques-a3efe7c6d78c) (Towards AI, Oct 2025)
- [RAFT: Domain-Specific RAG](https://arxiv.org/abs/2403.10131) (ArXiv, Mar 2024)
- [HOPE: Text Chunking Evaluation](https://arxiv.org/abs/2505.02171) (ArXiv, May 2025)

**Conversational AI Evaluation**:
- UMUX-Lite (Usability Metric for User Experience)
- BUS-11 (Chatbot Usability Scale)

**Asset Documents**:
- ALP ALCL AI Use Case Exploration
- AI-Human-agent interaction: Channels & Triggers
- AI-Trust indicators & UI patterns
- AI-Conversational AI Evaluation
- Maersk AI Freight Ecosystem

---

## 12. Email/Attachment Intake Blueprint

### Purpose
End-to-end automation of order intake from customer emails with attachments.

### Architecture

```
┌─────────────────────────────────────────────────────────────┐
│                   Email Channel                             │
│  (Outlook, Gmail, SMTP)                                     │
└─────────────────────┬───────────────────────────────────────┘
                      │ Email arrives
                      ↓
┌─────────────────────────────────────────────────────────────┐
│           Email Listener Service                            │
│  - Monitors inbox (polling or webhook)                      │
│  - Filters by sender, subject pattern                       │
│  - Downloads attachments                                    │
└─────────────────────┬───────────────────────────────────────┘
                      │ Publishes `order.received` event
                      ↓
┌─────────────────────────────────────────────────────────────┐
│        📧 Email Analyzer Agent                              │
│  - Parses email body (NLP)                                  │
│  - Extracts attachments (PDF, Excel, Word)                  │
│  - OCR for scanned documents                                │
│  - Field extraction (origin, dest, cargo, dates)            │
│  - Confidence scoring                                       │
└─────────────────────┬───────────────────────────────────────┘
                      │ Publishes `email.parsed` event
                      ↓
┌─────────────────────────────────────────────────────────────┐
│        ✅ Booking Validator Agent                           │
│  - Validates mandatory fields                               │
│  - Cross-checks master data (CW1)                           │
│  - Applies business rules                                   │
│  - Checks capacity, DG regulations                          │
└─────────────────────┬───────────────────────────────────────┘
                      │
           ┌──────────┴──────────┐
           │                     │
     Confidence > 70%      Confidence < 70%
           │                     │
           ↓                     ↓
  `booking.validated`    `booking.exception`
           │                     │
           ↓                     ↓
  Rate Agent          Exception Queue
  Quotation Agent     (Human Review)
  CW1 Sync Agent
```

### Workflow (Step-by-Step)

**Step 1: Email Arrival**
- Email arrives at `orders@maersk.com`
- Subject: "Booking Request - CNSHA to NLRTM - 10 CBM"
- Attachments: `Booking_Form.pdf`, `Cargo_Details.xlsx`

**Step 2: Email Listener**
- Listener detects new email (webhook trigger or 1-min polling)
- Applies filters:
  - ✅ From: `customer@acme.com` (known customer)
  - ✅ Subject contains: "Booking Request"
  - ✅ Has attachments
- Downloads attachments to blob storage
- Publishes `order.received` event:
  ```json
  {
    "event_type": "order.received",
    "email_id": "abc123",
    "sender": "customer@acme.com",
    "subject": "Booking Request - CNSHA to NLRTM - 10 CBM",
    "body": "Please book 10 CBM from Shanghai to Rotterdam...",
    "attachments": [
      {"filename": "Booking_Form.pdf", "url": "blob://..."},
      {"filename": "Cargo_Details.xlsx", "url": "blob://..."}
    ],
    "timestamp": "2025-11-10T08:30:00Z"
  }
  ```

**Step 3: Email Analyzer**
- Receives `order.received` event
- Parses email body:
  - Extracts: origin ("Shanghai"), destination ("Rotterdam"), volume ("10 CBM")
- Processes attachments:
  - PDF: OCR → Extract shipper, consignee, cargo details
  - Excel: Parse rows → Extract piece count, weight, dimensions
- Normalizes data:
  - Shanghai → CNSHA (IATA code)
  - Rotterdam → NLRTM
- Calculates confidence:
  - All fields found: 95%
  - Some fields missing: 70%
  - Critical fields missing: 40%
- Publishes `email.parsed` event:
  ```json
  {
    "event_type": "email.parsed",
    "email_id": "abc123",
    "parsed_data": {
      "origin": "CNSHA",
      "destination": "NLRTM",
      "shipper": {"name": "Acme Corp", "email": "john@acme.com"},
      "consignee": {"name": "Global Logistics BV", "address": "..."},
      "cargo": {
        "pieces": 10,
        "weight_kg": 500,
        "cbm": 10,
        "commodity": "Electronics",
        "hs_code": "8471.30"
      },
      "ready_date": "2025-11-15",
      "incoterm": "FOB"
    },
    "confidence": 0.95,
    "timestamp": "2025-11-10T08:31:15Z"
  }
  ```

**Step 4: Booking Validator**
- Receives `email.parsed` event
- **Validation Checks**:
  1. ✅ Mandatory fields present (origin, dest, cargo, date)
  2. ✅ Master data lookup: Acme Corp found in CW1 (customer_id: 12345)
  3. ✅ Consignee lookup: Global Logistics BV found (consignee_id: 67890)
  4. ✅ DG check: HS Code 8471.30 = Non-DG (electronics)
  5. ✅ Capacity check: 10 CBM available for CNSHA → NLRTM on 2025-11-15
  6. ✅ Rate check: Rate available, margin = 15% (acceptable)
- **Result**: All checks pass
- Publishes `booking.validated` event:
  ```json
  {
    "event_type": "booking.validated",
    "email_id": "abc123",
    "booking_id": "BK-67890",
    "validation_result": {
      "status": "validated",
      "confidence": 0.94,
      "checks": {
        "mandatory_fields": "pass",
        "master_data": "pass",
        "dg_check": "pass",
        "capacity": "pass",
        "rate": "pass"
      }
    },
    "next_agents": ["rate_agent", "quotation_agent"],
    "timestamp": "2025-11-10T08:32:00Z"
  }
  ```

**Step 5: Exception Handling** (if validation fails)
- If confidence < 70% or any check fails:
  - Publishes `booking.exception` event
  - Exception Handler Agent activates
  - Sends notification to operator:
    - Channel: Teams message, email
    - Content: "Booking #BK-67890 requires review: Shipper not found in CW1"
    - Suggested actions: Link to existing shipper, create new, reject
  - Operator reviews in dashboard (exception queue)
  - Operator resolves:
    - Option A: Links to correct shipper → Re-triggers validation
    - Option B: Rejects booking → Sends rejection email to customer
    - Option C: Creates new shipper → Triggers Master Data Agent

**Step 6: Downstream Processing** (if validated)
- Rate Agent calculates pricing
- Quotation Agent generates quote
- Operator approves (Confirm Mode) or auto-executes (Autonomous Mode)
- CW1 Sync Agent creates booking in CargoWise One
- Confirmation email sent to customer

### Data Extraction Patterns

**Key Fields to Extract**:

| Field Category | Required Fields | Optional Fields | Extraction Method |
|---------------|----------------|----------------|-------------------|
| **Shipment Details** | Origin, Destination, Ready Date | Incoterm, Service Level | NLP + location normalization |
| **Shipper** | Name, Email | Address, Phone, Contact Person | Entity extraction + CW1 lookup |
| **Consignee** | Name, Address | Email, Phone, Contact Person | Entity extraction + CW1 lookup |
| **Cargo** | Pieces, Weight, CBM, Commodity | HS Code, Value, Packing Type | Table extraction (Excel/PDF) |
| **Special Requirements** | DG (if applicable) | Temperature control, Fragile, Insurance | Keyword detection |

**Extraction Techniques**:
- **Email Body**: NLP (named entity recognition, date parsing)
- **PDF Forms**: Template matching + OCR (if scanned)
- **Excel/CSV**: Row/column parsing (structured data)
- **Images**: OCR (Tesseract) + post-processing

### Validation Rules

**Mandatory Field Checks**:
```python
def validate_mandatory_fields(booking_data):
    required = ["origin", "destination", "cargo.pieces", "cargo.cbm", "ready_date"]
    missing = [f for f in required if not booking_data.get(f)]
    if missing:
        return {"status": "fail", "reason": f"Missing fields: {missing}"}
    return {"status": "pass"}
```

**Master Data Validation**:
```python
def validate_shipper(shipper_email):
    # Query CW1 customer database
    customer = cw1_lookup(shipper_email)
    if customer:
        return {"status": "pass", "customer_id": customer.id, "confidence": 1.0}
    # Fuzzy match by name
    candidates = fuzzy_search_cw1(shipper_email.domain)
    if candidates:
        return {"status": "review", "candidates": candidates, "confidence": 0.7}
    # No match
    return {"status": "fail", "reason": "Shipper not found", "confidence": 0.3}
```

**DG Regulation Check**:
```python
def validate_dg(hs_code, commodity_description):
    if is_dg_hs_code(hs_code):
        return {"status": "dg_required", "class": get_dg_class(hs_code)}
    # Check description for DG keywords
    dg_keywords = ["flammable", "lithium", "battery", "explosive", "corrosive"]
    if any(kw in commodity_description.lower() for kw in dg_keywords):
        return {"status": "dg_suspected", "confidence": 0.8}
    return {"status": "non_dg"}
```

### Exception Handling

**Exception Types**:

| Exception Type | Trigger | Resolution Path | SLA |
|---------------|---------|-----------------|-----|
| **Missing Field** | Required field not extracted | Operator fills in missing data | < 4 hours |
| **Shipper Not Found** | Shipper email/name not in CW1 | Link existing or create new | < 2 hours |
| **DG Suspected** | Keywords suggest hazardous cargo | DG specialist reviews and approves | < 1 day |
| **Capacity Full** | No space on requested date | Suggest alternate dates or routes | < 4 hours |
| **Low Margin** | Calculated margin < 5% | Adjust pricing or reject | < 4 hours |
| **Duplicate Booking** | Same booking already exists | Merge or reject | < 1 hour |

**Operator Dashboard** (Exception Queue):
- List view: All pending exceptions, sorted by priority (High, Medium, Low)
- Detail view: Exception context, suggested actions, edit fields
- Bulk actions: Approve all, reject all, assign to specialist

### Success Metrics

| Metric | Baseline (Manual) | Target (AI) | Current | Measurement |
|--------|------------------|-------------|---------|-------------|
| **Time to Process** | 4 hours | 15 minutes | 28 minutes | From email arrival to booking validated |
| **Extraction Accuracy** | N/A | >90% | 92% | % of fields correctly extracted |
| **Validation Accuracy** | 88% | >95% | 94% | % of bookings correctly validated |
| **Touchless Rate** | 0% | 70% | 42% | % of bookings auto-processed (no human touch) |
| **Exception Rate** | 100% (all manual) | <30% | 58% | % of bookings requiring human review |
| **Customer Satisfaction** | 3.2/5 | >4.0/5 | 3.8/5 | NPS or CSAT survey |

---

## 13. Human-Agent Interaction Patterns

### Channel Taxonomy

| Channel | Best For | Example Use Case | User Type | Latency |
|---------|----------|------------------|-----------|---------|
| **Email** | Async, formal communication | Booking requests, quotations | External customers | Hours |
| **Web App (Embedded)** | Focused tasks within workflow | Auto-fill booking form, validate data | Internal operators | Real-time |
| **Web App (Chat)** | Exploratory Q&A, help | "Why was this shipment delayed?" | Internal operators | Real-time |
| **Teams / Slack** | Collaboration, notifications | "@CargoX show yesterday's exceptions" | Internal operators | Near real-time |
| **Mobile App** | On-the-go, warehouse operations | Confirm cargo arrival, scan barcode | Warehouse staff | Real-time |
| **Voice** | Hands-free, eyes-busy scenarios | "CargoX, is cargo ready at AMS?" | Warehouse staff, drivers | Real-time |
| **API** | System-to-system integration | EDI partners, e-commerce platforms | External systems | Real-time |

### Trigger Taxonomy

| Trigger Type | Description | Example | Agent Behavior |
|-------------|-------------|---------|---------------|
| **Explicit User Action** | User clicks button, types command | Click "Auto-fill booking", type "@CargoX help" | Agent responds immediately |
| **Contextual Opportunity** | System detects opportunity to help | User enters invalid location code | Agent suggests correction (inline tooltip) |
| **Post-Action Chain** | After user completes step A, agent handles step B | User approves booking → Agent syncs to CW1 | Agent executes automatically |
| **Scheduled / Business Rule** | Time-based or rule-based trigger | Every Friday 3pm → Generate consol plan | Agent runs on schedule |
| **Event-Driven** | External event triggers agent | Email arrives → Parse and validate | Agent reacts to event |
| **Proactive** | Agent initiates conversation (advanced) | Agent detects low margin → Alerts operator | Agent sends notification |

### Interaction Pattern Catalog

#### 1. Embedded Feature (Action Agent)

**Best For**: Single focused task within existing workflow.

**Example**: "Auto-fill MOF" button on booking form.

**Design**:
- **Entry Point**: Button or icon next to form field
- **Interaction**: 
  1. User clicks "Auto-fill"
  2. Agent calculates MOF based on route, cargo type
  3. Agent pre-fills field (user can edit)
- **Feedback**: Tooltip shows confidence ("High confidence: $12.50/CBM based on rate card")
- **Control**: User can override value

**When to Use**:
- Narrow, well-defined task
- Real-time response expected (<2s)
- Low risk (user can easily undo)

---

#### 2. Embedded Chat (Information Agent)

**Best For**: Quick Q&A within app context.

**Example**: "Why was this shipment rejected?" in side panel.

**Design**:
- **Entry Point**: Chat icon (bottom-right) or contextual "Ask AI" link
- **Interaction**:
  1. User opens chat panel (slides in from right)
  2. User types question or selects suggested prompt
  3. Agent responds with answer + sources
  4. User can ask follow-up questions (conversational)
- **Feedback**: Thumbs up/down after each response
- **Control**: User can minimize chat, clear history

**When to Use**:
- Exploratory questions (user doesn't know exact answer location)
- Moderate complexity (answer requires context from multiple sources)
- Medium risk (informational only, no actions executed)

---

#### 3. Teams / Outlook Agent (Orchestrator + Multiple Agents)

**Best For**: Async collaboration, notifications, multi-turn conversations.

**Example**: "@CargoX show yesterday's exceptions" in Teams channel.

**Design**:
- **Entry Point**: @mention in Teams/Slack channel or DM
- **Interaction**:
  1. User types "@CargoX [command]"
  2. Agent parses intent, queries relevant agents
  3. Agent responds in thread with results (formatted message, cards)
  4. User can react (approve/reject) via buttons or replies
- **Feedback**: Reactions (👍👎), inline comments
- **Control**: User can cancel task ("@CargoX stop")

**When to Use**:
- Async workflows (user doesn't need immediate answer)
- Collaboration (multiple stakeholders involved)
- Notifications (agent alerts user when action needed)

**Notification Types**:
- **Exception Alert**: "Booking #67890 requires your review (DG cargo suspected)"
- **Approval Request**: "Consol #4567 ready for approval (8 bookings, $15k margin)"
- **Status Update**: "Shipment HAWB-12345 departed CNSHA, ETA NLRTM 2025-11-20"
- **Daily Digest**: "Yesterday: 50 bookings processed, 8 exceptions, 42% touchless"

---

#### 4. Autonomous Worker (Multi-Agent System)

**Best For**: Background multi-agent workflows requiring no user interaction.

**Example**: Email → Parse → Validate → Rate → Quote → Book → Notify.

**Design**:
- **Entry Point**: Event trigger (email arrival, schedule)
- **Interaction**:
  1. User does nothing (agent operates in background)
  2. Agent orchestrates workflow across multiple agents
  3. Agent logs all actions (audit trail)
  4. Agent notifies user only if exception or approval needed
- **Feedback**: User reviews audit log (dashboard)
- **Control**: User can pause agent, rollback actions

**When to Use**:
- High confidence scenarios (>90% success rate)
- Low risk or reversible actions
- High volume (100+ tasks/day)

**Monitoring**:
- Dashboard shows: Tasks completed, success rate, exceptions, latency
- Alerts if SLA breached (e.g., >10% error rate)

---

#### 5. Voice Agent (Voice-Enabled Agent)

**Best For**: Hands-free, mobile, warehouse scenarios.

**Example**: "CargoX, confirm cargo arrival at AMS warehouse."

**Design**:
- **Entry Point**: Wake word ("Hey CargoX") or push-to-talk button
- **Interaction**:
  1. User speaks command
  2. Agent transcribes → parses intent
  3. Agent executes action or retrieves info
  4. Agent responds via voice (text-to-speech)
- **Feedback**: User confirms ("Yes, correct") or corrects ("No, I said NLAMS not NLRTM")
- **Control**: User can cancel ("CargoX, stop")

**When to Use**:
- Hands-free scenarios (driving, warehouse picking)
- Simple commands (lookup, confirm, update status)
- Mobile workforce

**Voice UX Principles**:
- Keep responses short (<15s)
- Confirm critical actions ("Did you say 'NLRTM'? Say yes to confirm.")
- Provide escape hatch ("Say 'help' for options")

---

#### 6. Standalone Chat App (Orchestrator + Domain Agents)

**Best For**: Exploratory, multi-purpose assistant.

**Example**: "Find me the best consolidation options for next week."

**Design**:
- **Entry Point**: Dedicated web/mobile app
- **Interaction**:
  1. User opens app, types query or selects task
  2. Agent orchestrates across domain agents (Consol Planner, Rate Agent, Capacity Agent)
  3. Agent presents results (tables, charts, recommendations)
  4. User refines query or takes action (approve consol)
- **Feedback**: Thumbs up/down, star rating, comment
- **Control**: User can switch agents, clear conversation, export results

**When to Use**:
- Open-ended tasks (user exploring options)
- Complex workflows (requires multiple agents)
- Power users (frequent use, advanced features)

---

### Handoff Choreography

**Agent → Human Handoff**:
(See [§6 Human-Agent Collaboration](#6-human-agent-collaboration) for detailed sequence)

**Human → Agent Handoff**:

```
Operator identifies task suitable for agent
   ↓
Operator delegates to agent (command, approval, rule)
   ↓
Agent confirms parameters ("Create consol for 8 bookings to NLRTM on 2025-11-15?")
   ↓
Operator confirms ("Yes") or adjusts ("Change date to 2025-11-16")
   ↓
Agent executes
   ↓
Agent reports back ("Consol #4567 created, 12.5 CBM, $18k margin")
   ↓
Operator reviews (dashboard) and provides feedback if needed
```

---

## 14. Trust Indicators & UI Components

### Trust Principles

1. **Transparency**: Every AI decision must be explainable
2. **Controllability**: Users can override, edit, or reject AI outputs
3. **Explainability**: Users understand *why* AI made a decision
4. **Auditability**: All actions logged and reviewable
5. **Safety**: PII protected, errors handled gracefully

### UI Component Library

#### 1. Confidence Badge

**Purpose**: Show AI's certainty level.

**Visual Design**:
- Tag with text: "High confidence (94%)"
- Color:
  - High (>85%): Green background, white text
  - Medium (70-85%): Orange background, white text
  - Low (<70%): Red background, white text (should rarely show to users)

**Interaction**:
- Hover: Tooltip explains "Based on 95% match with CW1 master data"
- Click: Opens confidence breakdown modal

**When to Use**: After every AI-generated output (booking validation, rate calculation, shipper match)

**Example**:
```
Shipper: Acme Corp (customer_id: 12345)  [High confidence (94%)]
                                          ↑ Green badge
```

---

#### 2. Source Citation

**Purpose**: Prove grounding (every claim backed by source).

**Visual Design**:
- Inline link/icon next to claim: "Source: CW1 Audit Log ↗"
- Small font, muted color (blue-gray)

**Interaction**:
- Click: Opens source document in side panel
- Shows: Document name, last updated timestamp, relevant excerpt highlighted

**When to Use**: When AI cites specific data (rate, rule, SOP)

**Example**:
```
Rate for CNSHA → NLRTM: $12.50/CBM
[Source: Rate Repository, updated 2025-11-08 ↗]
```

---

#### 3. Reasoning Trace

**Purpose**: Explain AI logic step-by-step.

**Visual Design**:
- Expandable section: "How I decided" (collapsed by default)
- Accordion UI with numbered steps

**Interaction**:
- Click to expand: Shows decision tree or reasoning chain

**When to Use**: For complex decisions (rate calculation, consol optimization)

**Example**:
```
Suggested Consol: 8 bookings, 12.5 CBM, $18k margin
[▼ How I decided]
  1. Grouped by destination: NLRTM (8 bookings)
  2. Grouped by ready date: 2025-11-15 (±1 day)
  3. Checked capacity: 12.5 CBM < 15 CBM limit ✓
  4. Calculated margin: $18k (15% avg) ✓
  5. Avoided DG mixing: No DG cargo ✓
```

---

#### 4. Approval Button

**Purpose**: Human-in-the-loop gate for high-risk actions.

**Visual Design**:
- Primary button: "Approve & Execute" (green)
- Secondary button: "Edit" (blue)
- Tertiary button: "Reject" (red outline)

**Interaction**:
- Click "Approve": Agent executes action immediately
- Click "Edit": Opens inline edit form (user modifies, then approves)
- Click "Reject": Agent cancels action, logs reason

**When to Use**: High-risk actions (booking >$50k, DG cargo, new customer)

**Example**:
```
┌──────────────────────────────────────────────┐
│ Booking #67890 Ready for Approval            │
│ Shipper: Acme Corp                           │
│ Route: CNSHA → NLRTM                         │
│ Value: $52,000                               │
│                                              │
│ [Approve & Execute]  [Edit]  [Reject]       │
└──────────────────────────────────────────────┘
```

---

#### 5. Override Controls

**Purpose**: Let human edit AI output before execution.

**Visual Design**:
- Inline edit fields (pencil icon)
- "Use My Version" button appears after edit

**Interaction**:
- Click pencil icon → Field becomes editable
- User modifies value
- Click "Use My Version" → Agent uses human's value
- System logs override (for learning)

**When to Use**: When AI output is close but not perfect (e.g., location code typo)

**Example**:
```
Origin: CNSHA ✏️  [Edit]
  ↓ (User edits)
Origin: CNSHG [Use My Version] [Cancel]
```

---

#### 6. Feedback Buttons

**Purpose**: Capture quality signal for learning.

**Visual Design**:
- 👍 👎 buttons (icon only, no text)
- Optional comment field (appears after click)

**Interaction**:
- Click 👍: Toast message "Thanks for feedback!"
- Click 👎: Dropdown asks "What went wrong?" (predefined options + "Other")
- Optional comment field for additional context

**When to Use**: After every AI response (chat, validation, recommendation)

**Example**:
```
Shipper match: Acme Corp (customer_id: 12345)
[👍]  [👎]  [💬 Comment]
```

**Feedback Options** (after 👎):
- Not accurate
- Not relevant
- I didn't understand the wording
- Missing information
- Other (please describe)

---

#### 7. Activity Log

**Purpose**: Audit trail of all AI actions.

**Visual Design**:
- Chronological list (most recent first)
- Each entry: Timestamp, Agent, Action, Status, User (if involved)

**Interaction**:
- Expandable: Click entry to see full context (inputs, outputs, reasoning)
- Filterable: By agent, date range, status (success/fail/pending)
- Searchable: Full-text search by booking ID, customer name

**When to Use**: For compliance, debugging, post-incident review

**Example**:
```
┌──────────────────────────────────────────────────────────────┐
│ Activity Log                                                 │
├──────────────────────────────────────────────────────────────┤
│ 2025-11-10 08:32:00 | Booking Validator | Validated BK-67890│
│   Status: Success | Confidence: 94% | Operator: N/A         │
│   [▼ View Details]                                           │
├──────────────────────────────────────────────────────────────┤
│ 2025-11-10 08:31:15 | Email Analyzer | Parsed email abc123  │
│   Status: Success | Confidence: 95% | Operator: N/A         │
├──────────────────────────────────────────────────────────────┤
│ 2025-11-10 08:20:45 | Rate Agent | Calculated rate BK-67889 │
│   Status: Success | Operator: J.Smith (overrode margin)     │
└──────────────────────────────────────────────────────────────┘
```

---

### Design Specifications

**Figma Component Anatomy** (Confidence Badge):
```
┌─────────────────────────────────┐
│ High confidence (94%)           │ ← 14px text, white
│                                 │
│ Background: Green (#00B050)     │
│ Border-radius: 4px              │
│ Padding: 4px 8px                │
│ Font: Inter Medium              │
└─────────────────────────────────┘

Hover state: Tooltip appears
┌───────────────────────────────────────────┐
│ Based on 95% match with CW1 master data  │
│ Last validated: 2025-11-10 08:32:00      │
└───────────────────────────────────────────┘
```

**React Component Example**:
```typescript
import React from 'react';

interface ConfidenceBadgeProps {
  confidence: number; // 0-1
  reasoning?: string;
}

export const ConfidenceBadge: React.FC<ConfidenceBadgeProps> = ({ 
  confidence, 
  reasoning 
}) => {
  const level = confidence > 0.85 ? 'high' : confidence > 0.70 ? 'medium' : 'low';
  const color = {
    high: 'bg-green-600',
    medium: 'bg-orange-500',
    low: 'bg-red-600'
  }[level];
  
  return (
    <span 
      className={`${color} text-white text-sm px-2 py-1 rounded`}
      title={reasoning}
    >
      {level.charAt(0).toUpperCase() + level.slice(1)} confidence ({Math.round(confidence * 100)}%)
    </span>
  );
};
```

---

## 15. Conversational AI Evaluation

### Evaluation Stages

#### 1. Offline Evaluation (Pre-Deployment)

**Purpose**: Test new agent/prompt on curated test set before production.

**Process**:
1. Curate test set (100+ samples with ground truth)
2. Run new agent on test set
3. Compare outputs to ground truth
4. Calculate metrics (accuracy, F1, Grounding@K)
5. Gate: Must achieve >85% accuracy to deploy

**Metrics**:
- **Accuracy**: % of outputs matching ground truth
- **Precision**: TP / (TP + FP)
- **Recall**: TP / (TP + FN)
- **F1 Score**: Harmonic mean of precision & recall
- **Grounding@K**: % of claims backed by sources (top K docs)

**Tools**:
- Test harness (automated test runner)
- Human labeling tool (for creating ground truth)
- A/B test framework (compare old vs new)

---

#### 2. Online Evaluation (Production)

**Purpose**: Monitor agent outputs in real-time, flag anomalies.

**Process**:
1. Evaluation Agent scores every output (LLM-as-Judge)
2. Track metrics in real-time (latency, error rate, thumbs up rate)
3. Alert if threshold breached (e.g., >10% error rate)
4. On-call engineer investigates and mitigates

**Metrics**:
- **Latency**: Avg response time (target: <3s)
- **Error Rate**: % of requests resulting in error (target: <1%)
- **Operator Feedback Score**: Avg thumbs up rate (target: >80%)
- **Escalation Rate**: % requiring human review (target: <25%)

**Alerting Thresholds**:
- 🟢 Green: All metrics within target
- 🟡 Yellow: 1 metric slightly degraded (e.g., latency 3-6s)
- 🔴 Red: Critical threshold breached (e.g., error rate >5%, latency >10s)

**Dashboard** (Real-Time):
```
Agent Health Dashboard
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
Email Analyzer       🟢 Healthy
  Latency: 2.1s      ✅ Target: <3s
  Error Rate: 0.3%   ✅ Target: <1%
  Feedback: 88% 👍    ✅ Target: >80%

Booking Validator    🟡 Degraded
  Latency: 4.5s      ⚠️ Target: <3s
  Error Rate: 0.8%   ✅ Target: <1%
  Feedback: 75% 👍    ⚠️ Target: >80%

Rate Agent           🟢 Healthy
  Latency: 1.8s      ✅ Target: <3s
  Error Rate: 0.1%   ✅ Target: <1%
  Feedback: 92% 👍    ✅ Target: >80%
```

---

#### 3. Human-in-the-Loop Evaluation (Periodic Audit)

**Purpose**: Human experts validate agent quality periodically.

**Process**:
1. Sample 100 agent outputs per week (stratified by agent, confidence level)
2. Human expert scores each output (1-5 scale) on 6 criteria
3. Calculate inter-rater agreement (if multiple raters)
4. Calculate BUS-11 score (Chatbot Usability Scale)
5. Review low-scoring outputs with team (monthly meeting)

**Metrics**:
- **UMUX-Lite**: 2-question survey (monthly)
  - Q1: "CargoX's functionality meets my needs" (1=Strongly Disagree, 5=Strongly Agree)
  - Q2: "CargoX is easy to use" (1=Strongly Disagree, 5=Strongly Agree)
  - Score: (Q1 + Q2 - 2) × 12.5 (converts to 0-100 scale)
  - Target: >75
- **BUS-11**: 11-question survey (quarterly)
  - Accessibility (2 questions)
  - Functional Interactive Conversation (7 questions)
  - Privacy (1 question)
  - Responsiveness (1 question)
  - Score: Avg of all questions × 20 (converts to 0-100 scale)
  - Target: >80 (Very Good)

**UMUX-Lite Survey** (embedded in app, shown once per month per user):
```
How much do you agree with the following?

1. CargoX's functionality meets my needs
   [1] [2] [3] [4] [5]
   Strongly Disagree      Strongly Agree

2. CargoX is easy to use
   [1] [2] [3] [4] [5]
   Strongly Disagree      Strongly Agree

[Submit]
```

**Calculation**:
```python
def calculate_umux_lite(q1_score, q2_score):
    # q1_score, q2_score: 1-5
    raw_score = q1_score + q2_score  # 2-10
    normalized = (raw_score - 2) * 12.5  # 0-100
    return normalized

# Example: User responds [4, 4]
score = calculate_umux_lite(4, 4)  # (4+4-2)*12.5 = 75
```

---

### Metrics Library

| Metric | Description | Target | Measurement | Owner |
|--------|-------------|--------|-------------|-------|
| **Accuracy** | % of outputs matching ground truth | >90% | Offline eval | Data Science |
| **Grounding@K** | % of claims backed by top K sources | >85% | Offline eval | Data Science |
| **Coverage@K** | % of relevant facts retrieved in top K | >80% | Offline eval | Data Science |
| **Diversity@K** | Non-redundant doc sources in top K | >75% | Offline eval | Data Science |
| **Latency** | Avg response time | <3s | Online monitoring | Engineering |
| **Error Rate** | % of requests resulting in error | <1% | Online monitoring | Engineering |
| **Operator Feedback** | Avg thumbs up rate | >80% | Online monitoring | Product |
| **Escalation Rate** | % requiring human review | <25% | Online monitoring | Product |
| **UMUX-Lite** | Perceived usability & usefulness | >75 | Monthly survey | UX |
| **BUS-11** | Conversational usability | >80 | Quarterly survey | UX |
| **Touchless Rate** | % auto-processed (no human touch) | 70% | Business metrics | Product |

---

### A/B Testing Framework

**Purpose**: Compare new agent/prompt against current before full rollout.

**Process**:
1. **Hypothesis**: "New prompt improves shipper matching accuracy by 5%"
2. **Setup**:
   - Control group: 50% traffic → Old prompt
   - Treatment group: 50% traffic → New prompt
   - Duration: 1 week (min 100 samples per group)
3. **Measurement**:
   - Primary metric: Shipper matching accuracy
   - Secondary metrics: Latency, escalation rate, operator feedback
4. **Analysis**:
   - Calculate improvement: Treatment vs Control
   - Statistical significance test (p-value < 0.05)
5. **Decision**:
   - If improvement >5% and p<0.05 → Deploy to 100%
   - If improvement <5% or p>0.05 → Rollback

**Example Results**:
```
A/B Test: Shipper Matching Prompt v2.1
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
Control (v2.0)     Treatment (v2.1)
Accuracy: 86%      Accuracy: 93%      ↗️ +7%
Latency: 2.1s      Latency: 2.3s      ↗️ +0.2s
Escalation: 22%    Escalation: 15%    ↘️ -7%

Verdict: ✅ Deploy v2.1 (improvement >5%, p=0.003)
```

---

## 16. Governance & Security

### AI Governance Policy Framework

| Policy Area | Policy | Approval Authority | Enforcement Mechanism |
|-------------|--------|-------------------|----------------------|
| **Data Privacy** | No PII in agent prompts or logs without encryption | Data Protection Officer | Pre-deployment PII scan; runtime PII detection & redaction |
| **Financial Risk** | Bookings >$50k require human approval | Finance Manager | Orchestrator blocks auto-execution; sends approval request |
| **Safety** | DG cargo requires DG specialist approval | DG Compliance Officer | DG Agent flags hazardous cargo → escalates to specialist |
| **Bias & Fairness** | No discrimination by customer size, region, or type | Ethics Committee | Quarterly audit of agent decisions; bias metrics dashboard |
| **Model Changes** | New model/prompt requires A/B test for 1 week + >85% accuracy | AI Product Owner | Evaluation Agent gates deployment; rollback if regression |
| **Incident Response** | Agent errors escalated within 1 hour; P0 incidents <15min | On-call Engineer | Automated alerting system; runbooks for common issues |
| **Audit & Compliance** | All agent actions logged for 7 years (regulatory requirement) | Compliance Officer | Immutable audit log; monthly compliance reports |

### Security Policies

**PII Handling**:
- **Detection**: Scan prompts and logs for PII (names, emails, phone numbers, credit cards)
- **Redaction**: Replace PII with placeholders (e.g., `[EMAIL_REDACTED]`)
- **Encryption**: Encrypt PII at rest and in transit (AES-256)
- **Access Control**: Only authorized roles can view PII (operator, compliance officer)
- **Retention**: Delete PII after 90 days (GDPR compliance)

**PII Detection Regex Examples**:
```python
import re

PII_PATTERNS = {
    "email": r'\b[A-Za-z0-9._%+-]+@[A-Za-z0-9.-]+\.[A-Z|a-z]{2,}\b',
    "phone": r'\b\d{3}[-.]?\d{3}[-.]?\d{4}\b',
    "credit_card": r'\b\d{4}[-\s]?\d{4}[-\s]?\d{4}[-\s]?\d{4}\b',
}

def redact_pii(text):
    for pii_type, pattern in PII_PATTERNS.items():
        text = re.sub(pattern, f'[{pii_type.upper()}_REDACTED]', text)
    return text
```

**Access Control** (Role-Based):

| Role | Permissions | PII Access |
|------|------------|-----------|
| **Operator** | View bookings, approve actions, provide feedback | Yes (shipper/consignee names, emails) |
| **Finance Manager** | Approve high-value bookings, view margin data | Yes (customer names, payment terms) |
| **DG Specialist** | Approve DG cargo, view material safety data sheets | Yes (shipper names, cargo details) |
| **Compliance Officer** | View audit logs, generate compliance reports | Yes (all PII for audit purposes) |
| **Data Scientist** | Retrain models, view anonymized feedback data | No (all PII redacted) |
| **On-Call Engineer** | Debug agent errors, view system logs | No (all PII redacted) |

**Incident Response Runbooks**:

**P0 Incident**: Agent down or critical error (>10% error rate)
1. Alert sent to on-call engineer (PagerDuty)
2. Engineer acknowledges within 15 minutes
3. Engineer investigates logs (observability dashboard)
4. If agent bug → Rollback to previous version
5. If external dependency issue (CW1, email) → Escalate to integration team
6. Post-incident review within 48 hours

**P1 Incident**: Agent degraded (latency >6s or escalation rate >50%)
1. Alert sent to on-call engineer (Slack)
2. Engineer acknowledges within 1 hour
3. Engineer investigates metrics (is it temporary spike or sustained?)
4. If sustained → Scale up resources or optimize prompt
5. If temporary → Monitor for another hour, then resolve

---

## 17. Observability & Operations

### Observability Architecture

```
┌─────────────────────────────────────────────────────────────┐
│                   Agent System                              │
│  (Email Analyzer, Booking Validator, Rate Agent, etc.)     │
└─────────────────────┬───────────────────────────────────────┘
                      │ Emits logs, metrics, traces
                      ↓
┌─────────────────────────────────────────────────────────────┐
│            Observability Infrastructure                     │
├─────────────────────────────────────────────────────────────┤
│ • Logging: Structured logs (JSON) → Log aggregation        │
│ • Metrics: Time-series data → Prometheus / Grafana         │
│ • Traces: Distributed tracing → OpenTelemetry / Jaeger     │
│ • Events: Audit log → Immutable event store                │
└─────────────────────┬───────────────────────────────────────┘
                      │ Queried by
                      ↓
┌─────────────────────────────────────────────────────────────┐
│              Dashboards & Alerting                          │
├─────────────────────────────────────────────────────────────┤
│ 1. Agent Health Dashboard (real-time metrics)               │
│ 2. Quality Trends Dashboard (accuracy, escalation over time)│
│ 3. User Feedback Dashboard (thumbs up/down, comments)      │
│ 4. Learning Progress Dashboard (improvement per agent)      │
│ 5. Cost & Efficiency Dashboard (cost per request, tokens)  │
│                                                             │
│ Alerting: Threshold breaches → PagerDuty / Slack           │
└─────────────────────────────────────────────────────────────┘
```

### Key Metrics & SLOs

| Metric Category | Metric | Green | Yellow | Red | Alert Action |
|-----------------|--------|-------|--------|-----|--------------|
| **Latency** | Avg response time | <3s | 3-6s | >6s | Scale up agents or optimize prompts |
| **Accuracy** | Validation accuracy | >90% | 85-90% | <85% | Trigger retraining or review rules |
| **Availability** | Agent uptime | >99% | 95-99% | <95% | Page on-call; restart agent |
| **Cost** | Cost per request | <$0.10 | $0.10-0.20 | >$0.20 | Optimize prompts (shorter context) or cache results |
| **Escalation Rate** | % escalated to human | <20% | 20-35% | >35% | Review escalation thresholds or agent logic |
| **User Satisfaction** | Thumbs up rate | >80% | 70-80% | <70% | UX improvement sprint; collect feedback |
| **Error Rate** | % requests with error | <1% | 1-3% | >3% | Investigate logs; fix bugs or external dependencies |

### Dashboard Examples

**1. Agent Health Dashboard** (Real-Time):

```
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
Agent Health Dashboard                      Last Updated: 08:45
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
Agent                Status    Latency   Error Rate   Feedback
───────────────────────────────────────────────────────────────
Email Analyzer       🟢 OK      2.1s      0.3%         88% 👍
Booking Validator    🟡 SLOW    4.5s      0.8%         75% 👍
Rate Agent           🟢 OK      1.8s      0.1%         92% 👍
Quotation Agent      🟢 OK      2.4s      0.5%         79% 👍
Consol Planner       🟢 OK      3.2s      0.2%         85% 👍
Invoice Validator    🟢 OK      2.0s      0.1%         94% 👍
Learning Agent       🟢 OK      N/A       0.0%         N/A
Evaluation Agent     🟢 OK      0.8s      0.0%         N/A
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
```

**2. Quality Trends Dashboard** (30-Day View):

```
Booking Validator - Quality Trends (Last 30 Days)
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
Accuracy         ↗️ 88% → 94% (+6%)
Escalation Rate  ↘️ 28% → 22% (-6%)
Touchless Rate   ↗️ 35% → 42% (+7%)
Operator UMUX    ↗️ 70 → 73 (+3)

[Line Chart: Accuracy over time]
94% ┤                                      ●
92% ┤                               ●
90% ┤                         ●
88% ┤  ●     ●
86% ┤
    ├────────────────────────────────────────
    Oct 1   Oct 8   Oct 15  Oct 22  Oct 29
```

**3. Cost & Efficiency Dashboard**:

```
Cost & Efficiency (October 2025)
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
Total Requests:          12,450
Total Cost:              $1,245 ($0.10 per request)
Avg Tokens per Request:  2,500 (prompt) + 500 (completion)
Cache Hit Rate:          65% (saves $800/month)

Cost Breakdown by Agent:
Email Analyzer     $300 (24%)
Booking Validator  $450 (36%)
Rate Agent         $200 (16%)
Quotation Agent    $150 (12%)
Other              $145 (12%)

[Pie Chart: Cost by Agent]
```

### Cost Management Strategies

| Strategy | Description | Savings |
|----------|-------------|---------|
| **Prompt Optimization** | Shorten prompts by removing redundant context | 20-30% |
| **Caching** | Cache frequent queries (e.g., rate lookups) for 1 hour | 40-50% |
| **Smaller Models** | Use smaller models (GPT-3.5 instead of GPT-4) for simple tasks | 80-90% |
| **Batch Processing** | Batch multiple requests into single API call | 10-20% |
| **Early Rejection** | Reject low-quality inputs before LLM call | 5-10% |

---

## 18. Adoption & Change Management

### Stakeholder Engagement

| Stakeholder | Role | Concerns | Engagement Strategy |
|------------|------|----------|---------------------|
| **CX Operators** | Primary users | Job security, usability, trust | Shadow mode first; training; feedback loops |
| **Finance Team** | Approve high-value bookings | Accuracy, compliance | Monthly reports; audit logs |
| **IT / Engineering** | Build & maintain agents | Technical complexity, scalability | Architecture reviews; monitoring dashboards |
| **Compliance / Legal** | Ensure regulatory compliance | Data privacy, auditability | Policy framework; quarterly audits |
| **Leadership** | Approve budget & strategy | ROI, risk | Business case; KPI dashboards |
| **Customers** | Receive quotes, confirmations | Service quality, responsiveness | Faster quotes; proactive updates |

### Training Materials

**Operator Training** (2-day workshop):
- **Day 1: Introduction**
  - What is CargoX? (vision, principles)
  - How agents work (agent personas, workflows)
  - Trust Maturity Model (shadow → confirm → autonomous)
  - Hands-on: Shadow mode walkthrough
- **Day 2: Hands-On**
  - Practice: Review exception queue, provide feedback
  - Practice: Approve bookings, override agent decisions
  - Q&A: Common scenarios, troubleshooting
  - Certification: Pass quiz (80% required)

**Training Assets**:
- **Videos** (5-10 min each):
  - "CargoX Overview" (vision, benefits)
  - "How to Review a Booking Exception"
  - "How to Provide Feedback to Agents"
  - "Understanding Confidence Scores"
- **Docs**:
  - User guide (step-by-step instructions)
  - FAQ (troubleshooting common issues)
  - Agent reference (what each agent does)
- **Sandbox**:
  - Test environment (operators can practice without real data)
  - Pre-loaded scenarios (DG cargo, new shipper, low margin)

### Pilot Strategy

**Phase 1: Shadow Mode** (Week 1-4)
- **Goal**: Build familiarity, no risk
- **Approach**: Agents suggest, humans always execute
- **Participants**: 10 operators (early adopters)
- **Success Criteria**: 50+ interactions, UMUX-Lite >65

**Phase 2: Confirm Mode** (Week 5-12)
- **Goal**: Reduce workload, build trust
- **Approach**: Agents execute after human approval
- **Participants**: 25 operators (expand pilot)
- **Success Criteria**: 30% touchless, UMUX-Lite >75

**Phase 3: Autonomous Mode** (Week 13-20)
- **Goal**: Scale to all operators, high confidence auto-executes
- **Approach**: Agents execute >90% confidence, humans monitor
- **Participants**: All operators (100+)
- **Success Criteria**: 50% touchless, accuracy >90%, UMUX-Lite >80

**Phase 4: Proactive Mode** (Week 21+)
- **Goal**: Agents initiate optimizations
- **Approach**: Agents suggest consols, alert on exceptions
- **Participants**: All operators + management
- **Success Criteria**: 70% touchless, BUS-11 >80, operator satisfaction >90%

### ROI Tracking

**Business Case**:
- **Problem**: Manual booking process takes 4 hours per booking, 88% accuracy
- **Solution**: AI agents automate 70% of bookings, 95% accuracy
- **Investment**: $500k (Year 1: development, training, pilot)
- **Savings**: $2M/year (1,500 hours/week saved × $25/hour × 52 weeks)
- **Payback Period**: 3 months
- **ROI**: 400% (Year 1)

**Metrics Dashboard** (Monthly Review):

| Metric | Baseline | Target (Year 1) | Current (Q3) | On Track? |
|--------|---------|----------------|--------------|-----------|
| **Touchless Rate** | 0% | 70% | 42% | ↗️ Yes |
| **Time to Quote** | 4 hours | 15 min | 28 min | ↗️ Yes |
| **Operator Hours Saved** | 0 | 1,500/week | 900/week | ↗️ Yes |
| **Cost Savings** | $0 | $2M/year | $1.2M annualized | ↗️ Yes |
| **Operator Satisfaction** | N/A | >80 UMUX | 73 | ⚠️ Behind |
| **Customer Satisfaction** | 3.2/5 | >4.0/5 | 3.8/5 | ↗️ Yes |

### Continuous Improvement

**Quarterly Reviews** (with stakeholders):
1. **Review Metrics**: KPIs, UMUX-Lite, BUS-11, cost savings
2. **Identify Gaps**: What's not working? Where are operators struggling?
3. **Prioritize Improvements**: High-impact, low-effort first
4. **Update Roadmap**: Next quarter's focus areas
5. **Celebrate Wins**: Recognize operators, teams, improvements

**Feedback Channels**:
- **In-App**: Thumbs up/down, comment field
- **Slack**: #cargox-feedback channel (async)
- **Office Hours**: Weekly 30-min Q&A with product team
- **Surveys**: Monthly UMUX-Lite, quarterly BUS-11
- **Interviews**: 1-on-1 with 5-10 operators per quarter

---

## Appendix: Change Log

### v1.1 (November 2025)
- ✨ Added Email/Attachment Intake Blueprint (§12)
- ✨ Added Multi-Agent Coordination Patterns (§2.3)
- ✨ Added Human-Agent Interaction Patterns (§13)
- ✨ Added Trust Indicators & UI Components (§14)
- ✨ Added Conversational AI Evaluation Framework (§15)
- ✨ Added Agent Persona Cards with RACI (§3)
- ✨ Added RAG Feedback Loop Operationalization (§7)
- ✨ Added Governance & Security Policies (§16)
- ✨ Added Observability & Operations (§17)
- ✨ Added Adoption & Change Management (§18)
- ✨ Expanded Capability Mapping with 13 use cases (§8)
- ✨ Added Trust Maturity Model (§5)
- ✨ Added Event Taxonomy with schemas (§2.3)
- ✨ Added Learning SLOs (§7)
- 🔧 Revised Timeline to 26-week phased rollout (§10)

### v1.0 (October 2025)
- Initial release
- Vision, principles, architecture, agent types
- RAG/retrieval concepts, UX framework
- Basic capability mapping, 6-week rollout

---

**End of Playbook v1.1**

---

**Document Metadata**:
- **Version**: 1.1
- **Date**: November 2025
- **Authors**: AI Architecture Team, Product, UX, Engineering
- **Status**: Production Ready
- **Next Review**: January 2026
- **Feedback**: Send to cargox-feedback@maersk.com
