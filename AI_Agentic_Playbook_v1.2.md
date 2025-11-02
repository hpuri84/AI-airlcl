# AI Agentic Playbook v1.2

### Hubble → CargoX Evolution Roadmap

**Version**: 1.2  
**Date**: November 2025  
**Status**: Production-Aligned (Based on Live Hubble v1.5)

---

## Document Overview

**Purpose**: Provide a phased enhancement roadmap to evolve **Hubble v1.5** (currently live with 5 GCA LCL customers) into **CargoX v2.0** (advanced multi-agent system with trust framework, continuous learning, and 70% touchless automation).

**What's New in v1.2**:
- 🔄 **Hubble v1.5 AS-IS Architecture** integrated as baseline (§0)
- 🎯 **Gap Analysis**: What Hubble has vs what's needed (§0.2)
- 📈 **Phased Enhancement Strategy**: Q1-Q4 2026 roadmap (§10)
- ✅ **Current State Metrics**: 5 customers live, ~60% touchless (§0.3)
- 🚀 **Target State**: 70% touchless, 95% accuracy, 15+ customers, $2M savings (§9)

**Key Insight**: You're not starting from zero—Hubble v1.5 = **CargoX Phase 2-3 equivalent**. This playbook shows how to reach Phase 5 (Full Autonomy & Global Scale).

---

## Table of Contents

0. **[Hubble v1.5: Current State Baseline](#0-hubble-v15-current-state-baseline)** ⬅️ **NEW**
   - 0.1 [Hubble Architecture (AS-IS)](#01-hubble-architecture-as-is)
   - 0.2 [Gap Analysis vs CargoX Playbook](#02-gap-analysis-vs-cargox-playbook)
   - 0.3 [Current Metrics & Customer Rollout](#03-current-metrics--customer-rollout)

1. [Vision & Principles](#1-vision--principles)
2. [Architecture Overview](#2-architecture-overview)
   - 2.1 [CargoX Agent Stack (TO-BE)](#21-cargox-agent-stack-to-be)
   - 2.2 [Freight Graph Knowledge Layer](#22-freight-graph-knowledge-layer)
   - 2.3 [Multi-Agent Coordination Patterns](#23-multi-agent-coordination-patterns)
3. [Agent Persona Cards](#3-agent-persona-cards)
4. [Retrieval & RAG Pipeline](#4-retrieval--rag-pipeline)
5. [Trust Maturity Model](#5-trust-maturity-model)
6. [Human-Agent Collaboration](#6-human-agent-collaboration)
7. [RAG Feedback & Learning Loop](#7-rag-feedback--learning-loop)
8. [Capability Mapping](#8-capability-mapping)
9. [Success Metrics & KPIs](#9-success-metrics--kpis)
10. **[Hubble → CargoX v2.0 Rollout (2026)](#10-hubble--cargox-v20-rollout-2026)** ⬅️ **UPDATED**
11. [References](#11-references)
12. [Email/Attachment Intake Blueprint](#12-emailattachment-intake-blueprint)
13. [Human-Agent Interaction Patterns](#13-human-agent-interaction-patterns)
14. [Trust Indicators & UI Components](#14-trust-indicators--ui-components)
15. [Conversational AI Evaluation](#15-conversational-ai-evaluation)
16. [Governance & Security](#16-governance--security)
17. [Observability & Operations](#17-observability--operations)
18. [Adoption & Change Management](#18-adoption--change-management)

---

## 0. Hubble v1.5: Current State Baseline

### 0.1 Hubble Architecture (AS-IS)

**Current Production System** (Live since Aug 2025):

```
┌────────────────────────────────────────────────────────────┐
│                    Platform GUI                            │
│  (Web Interface for Operators)                             │
└──────────────────────┬─────────────────────────────────────┘
                       ↓
┌──────────────────────────────────────────────────────────┐
│  Platform API/BFF (Backend for Frontend)                  │
│  • Routing BFF → Master data BFF → Order BFF             │
└──────────────────────┬─────────────────────────────────────┘
                       ↓
        ┌──────────────┴──────────────┐
        ↓                              ↓
┌───────────────┐              ┌───────────────────┐
│ Routing SVC   │              │ Booking SVC       │
│ (Java)        │              │ (Order Core)      │
└───────┬───────┘              └────────┬──────────┘
        │                               │
        ↓                               ↓
┌────────────────────────────────────────────────────────────┐
│           Email Trans → Order Adapter (Connect MQ)          │
│  • Monitors inbox (polling or webhook)                     │
│  • Downloads attachments to blob storage                   │
│  • Publishes order.received event                          │
└──────────────────────┬─────────────────────────────────────┘
                       ↓
┌──────────────────────────────────────────────────────────┐
│       AI Hubble Agent (LangChain) 🤖                      │
│  • Single orchestrator agent                              │
│  • Parses email body + attachments (PDF, Excel, Word)    │
│  • OCR for scanned documents (AI Fine-tuning planned)    │
│  • Calls downstream microservices                         │
└──────────────────────┬─────────────────────────────────────┘
                       ↓
        ┌──────────────┼──────────────┬──────────────┐
        ↓              ↓              ↓              ↓
┌─────────────┐ ┌─────────────┐ ┌─────────────┐ ┌─────────────┐
│ Quote 2 Book│ │ Booking     │ │ Route       │ │ Master Data │
│ (Order Core)│ │ Amendment   │ │ Planner SVC │ │ MCP         │
│             │ │             │ │ (Java)      │ │ (Python)    │
└──────┬──────┘ └──────┬──────┘ └──────┬──────┘ └──────�┬──────┘
       │               │               │               │
       └───────────────┴───────────────┴───────────────┘
                       ↓
        ┌──────────────┼──────────────┐
        ↓              ↓              ↓
┌─────────────┐ ┌─────────────┐ ┌─────────────┐
│ Map Registry│ │ Route       │ │ Master Data │
│ (Master Data│ │ Planner MCP │ │ Svc         │
│  Service)   │ │ (GEO,Python)│ │             │
└──────┬──────┘ └──────┬──────┘ └─────────────┘
       │               │
       └───────────────┘
                       ↓
               ┌───────────────┐
               │  GEO Service  │
               └───────┬───────┘
                       ↓
┌──────────────────────────────────────────────────────────┐
│              CargoX → CW1 E-adapter SVC                   │
│  • Syncs validated bookings to CargoWise One              │
└──────────────────────────────────────────────────────────┘
```

**Key Components**:
- ✅ **Email Trans + Order Adapter**: Monitors inbox, downloads attachments, publishes events
- ✅ **AI Hubble Agent (LangChain)**: Single orchestrator for all AI logic
- ✅ **Microservices**: Route Planner, Master Data, GEO Service (Python + Java)
- ✅ **CW1 Integration**: CargoX → CW1 E-adapter for booking sync
- ✅ **Event-Driven**: Message Queue (MQ) for async processing

**Current Capabilities**:
1. **Email/Attachment Intake**: Parse booking requests from emails (PDF, Excel, Word)
2. **OCR**: Extract text from scanned documents
3. **Master Data Lookup**: Match shipper/consignee to CW1 master data
4. **Routing Lookup**: Suggest CFS station, pickup agent, receiving agent
5. **Booking Creation**: Sync to CW1 via CargoX adapter
6. **Semi-Automation**: Human confirms AI suggestions before execution

---

### 0.2 Gap Analysis vs CargoX Playbook

| Capability | Hubble v1.5 Status | CargoX v2.0 Target | Gap Priority | ETA |
|------------|-------------------|-------------------|--------------|-----|
| **Email Intake** | ✅ Email Trans → Order Adapter | ✅ Email Analyzer Agent | 🟢 Strong (80%+ aligned) | Live |
| **OCR / Doc Parsing** | ✅ AI Fine-tuning planned (Nov 2025) | ✅ Email Analyzer (PDF, Excel, Word) | 🟢 Strong | Q4 2025 |
| **Booking Validation** | ✅ Booking Amendment + Quote 2 Book | ✅ Booking Validator Agent | 🟡 Partial (60% aligned) | Q1 2026 |
| **Master Data Lookup** | ✅ Master Data MCP (Python) | ✅ Master Data Agent + Freight Graph | 🟡 Partial (50% aligned) | Q1 2026 |
| **Routing Lookup** | ✅ Route Planner MCP (GEO, Python) | ✅ Routing Agent | 🟢 Strong (70% aligned) | Live |
| **Rate Calculation** | ❓ Not explicitly shown | ✅ Rate Agent (lookup + margin) | 🔴 Missing | Q1 2026 |
| **Quotation Generation** | ❓ Not explicitly shown | ✅ Quotation Agent (PDF, multi-currency) | 🔴 Missing | Q1 2026 |
| **Consolidation Planning** | 🚧 Hackathon followup (Dec 2025) | ✅ Consol Planner Agent | 🟡 Partial (40% aligned) | Q4 2025-Q1 2026 |
| **Invoice Validation** | ❓ Not shown | ✅ Invoice Validator Agent | 🔴 Missing | Q2 2026 |
| **Learning Agent** | ❓ "AI booking new ways training" (Nov 2025) | ✅ Learning Agent (analyze corrections, weekly) | 🔴 **Critical** | **Q1 2026** |
| **Evaluation Agent** | ❓ Not shown | ✅ Evaluation Agent (LLM-as-Judge, A/B test) | 🔴 **Critical** | **Q1 2026** |
| **Confidence Scores** | ❓ Not visible in UI | ✅ High/Medium/Low badges on all outputs | 🔴 **Critical** | **Q1 2026** |
| **Operator Feedback UI** | ❓ Not shown | ✅ 👍👎 buttons, corrections, comments | 🔴 **Critical** | **Q1 2026** |
| **RAG / Freight Graph** | ❓ Route knowledge base (partial) | ✅ Unified KB (CW1, EDI, contracts, rates, SOPs) | 🔴 Missing | Q1-Q2 2026 |
| **Source Citations** | ❓ Not shown | ✅ Every claim cited (CW1, contracts, SOPs) | 🔴 Missing | Q1 2026 |
| **Observability Dashboard** | ❓ Not shown | ✅ Real-time KPIs (latency, accuracy, UMUX) | 🔴 **Critical** | **Q1 2026** |
| **Multi-Agent Orchestration** | 🟡 Single LangChain agent | ✅ Orchestrator + 8+ specialized agents | 🟡 Partial (30% aligned) | Q2 2026 |

**Legend**:
- 🟢 **Strong Alignment** (70-100% compatible, minor enhancements needed)
- 🟡 **Partial Alignment** (40-70% compatible, moderate work needed)
- 🔴 **Missing** (0-40% compatible, new component required)

**Critical Gaps Summary** (Must-Have for Trust & Scale):
1. ❌ **Learning Agent**: No systematic improvement from operator corrections
2. ❌ **Evaluation Agent**: No quality gate (LLM-as-Judge)
3. ❌ **Operator Feedback UI**: Can't capture corrections to improve agents
4. ❌ **Confidence Scores**: Operators don't know when to trust AI vs review
5. ❌ **Observability Dashboard**: Can't track accuracy, touchless rate, UMUX

---

### 0.3 Current Metrics & Customer Rollout

**Hubble v1.5 Performance** (As of Nov 2025):

| Metric | Current Value | Source | Gap to Target |
|--------|--------------|--------|---------------|
| **Customer Rollout** | 5 big customers live (Aug-Oct 2025) | Renner, DK Company, PUMA, Schneider, Vestas | Target: 15+ by Dec 2026 |
| **Touchless Rate** | ~60% (estimated) | "Semi-automation" implies human confirmation | Target: 70% |
| **Time Savings** | 3-5 mins per booking | Rollout plan states "save 3-5 mins" | Target: 15 mins (vs 4 hrs manual) |
| **Accuracy** | **Unknown** ⚠️ | Not tracked (Critical Gap!) | Target: 95% |
| **Operator Satisfaction** | **Unknown** ⚠️ | Not tracked (Critical Gap!) | Target: UMUX-Lite >80 |
| **Customer Satisfaction** | **Unknown** ⚠️ | Not tracked (Critical Gap!) | Target: CSAT >4.0/5 |

**Rollout Timeline** (Sep - Dec 2025):

| Milestone | Timeline | Status | Business Value |
|-----------|----------|--------|---------------|
| **GCA LCL SCM/SCP 5 Big Customers** | Aug 1 - Oct 31, 2025 | ✅ **Live** | Automated E2E AI booking journey; save 3 mins/booking |
| **GCA LCL Pure LCL Customers** | Nov 7, 2025 | 🚧 In Progress | Semi-automation AI booking; save >5 mins/booking |
| **AI Booking Training for Operators** | Nov 21, 2025 | 🚧 Planned | New ways of working training for GCA LCL |
| **Full SCM/SCP GCA LCL Rollout** | Nov 28, 2025 | 🚧 Planned | Automate all SCM/SCP customers in GCA LCL |
| **Pilot Another LCL Country** | Nov 14, 2025 | 🚧 Planned | Summarize LCL booking experience globally |
| **Pilot One Air Booking Country** | Nov 30, 2025 | 🚧 Planned | Summarize Air booking experience globally |
| **AI Master Data Auto Pickup** | Nov 15, 2025 | 🚧 Planned | Reduce risk of wrong master data pickup |
| **AI Routing Search (CFS Station)** | Nov 30, 2025 | 🚧 Planned | Reduce work X mins/shipment for routing team |
| **AI GCA LCL Consol Planning** | Est. Dec 31, 2025 | 🚧 Hackathon followup | Reduce work X mins/shipment for routing team |

**Tech Resource**: 3.5 FTEs within ALP Platform (Sep - Dec 2025)

**Technical Milestones Achieved**:
- ✅ Azure AI integration
- ✅ Dify integration
- 🚧 AI Fine-tuning capability in OCR (Nov 2025)
- 🚧 LangChain full migration (Nov 2025)
- 🚧 Prompt repo setup (Nov 2025)
- 🚧 Master data knowledge base and rule setup (Nov 2025)
- 🚧 Routing knowledge base setup (Nov 2025)
- 🚧 Self-building vector DB (Nov 2025)
- 🚧 Knowledge self-learning module design (Dec 2025)
- 🚧 LCL Capacity service readiness (Dec 2025)

**Key Strengths** (Already Operational):
1. ✅ **Production-Proven**: 5 big customers live, processing real bookings
2. ✅ **Event-Driven Architecture**: MQ for async, scalable processing
3. ✅ **LangChain Integration**: AI orchestration framework in place
4. ✅ **CW1 Integration**: CargoX adapter syncs to CargoWise One
5. ✅ **Microservices**: Route Planner, Master Data, GEO as separate services
6. ✅ **Customer-Centric Rollout**: Phased rollout with big customers (Renner, PUMA, etc.)

**Gaps to Address** (Q1-Q2 2026):
1. ❌ No trust framework (confidence scores, feedback UI, evaluation)
2. ❌ No learning loop (systematic improvement from corrections)
3. ❌ No observability (KPI tracking for accuracy, touchless rate, UMUX)
4. ❌ Limited RAG capabilities (no Freight Graph for grounding)
5. ❌ Single LangChain agent (no multi-agent specialization yet)

---

## 1. Vision & Principles

### Vision Statement

**From Semi-Automation to Full Intelligence**: Transform Hubble v1.5 (currently 60% touchless with semi-automation) into CargoX v2.0 (70% touchless with self-learning, proactive workflows) by adding trust framework, continuous learning, and specialized agents.

**Current Reality** (Hubble v1.5):
- ✅ Email intake automated
- ✅ Human confirms AI suggestions (semi-automation)
- ❌ No systematic learning from corrections
- ❌ Operators can't gauge AI confidence
- ❌ No quality gate before deployment

**Target Reality** (CargoX v2.0 by Dec 2026):
- ✅ Email intake automated + grounded in CW1/contracts
- ✅ High-confidence cases auto-execute (>90% confidence)
- ✅ Learning Agent improves weekly (+5% accuracy/quarter)
- ✅ Operators see confidence scores, provide feedback
- ✅ Evaluation Agent gates all deployments (>85% accuracy required)

### Core Principles

| Principle | Implementation Checklist | Hubble v1.5 Status | Enhancement Needed |
|-----------|-------------------------|-------------------|-------------------|
| **Transparency by Design** | ✅ Source citations for every AI claim<br>✅ Confidence scores (High/Medium/Low)<br>✅ Reasoning traces ("How I decided")<br>✅ Audit logs for all actions | ❌ None visible | **Q1 2026**: Add confidence scoring + source citations |
| **Human-in-the-Loop (HITL)** | ✅ Approval gates by risk level<br>✅ Override controls<br>✅ Escalation triggers | 🟡 Semi-automation (human confirms) | **Q1 2026**: Formalize approval workflows by risk level |
| **Continuous Learning** | ✅ Feedback capture (👍👎 + corrections)<br>✅ Learning Agent analyzes patterns weekly<br>✅ A/B testing before deployment<br>✅ Visible feedback loop | ❌ No Learning Agent | **Q1 2026**: Build Learning Agent + Feedback UI |
| **Trust through Explainability** | ✅ Confidence badges on all outputs<br>✅ Source badges<br>✅ Decision journal<br>✅ Rollback capability | ❌ None visible | **Q1 2026**: Add trust indicators to Hubble UI |
| **Governance & Safety** | ✅ PII detection and redaction<br>✅ Financial approval gates<br>✅ DG specialist approval<br>✅ Incident response runbooks<br>✅ Quarterly bias/fairness audits | ❓ Not documented | **Q1 2026**: Formalize governance policies |
| **Experience-Driven Adoption** | ✅ UMUX-Lite surveys (monthly)<br>✅ BUS-11 conversational usability (quarterly)<br>✅ Shadow → Confirm → Autonomous progression<br>✅ Training materials | 🟡 Training planned (Nov 2025) | **Q1 2026**: Add UMUX-Lite surveys + dashboards |

### Trust Maturity Model

**Current State** (Hubble v1.5): **Stage 2 - Confirm Mode**
- ✅ Agent proposes, human approves before execution
- ✅ 60% touchless rate achieved
- ❌ No formal trust indicators (confidence scores)
- ❌ No systematic learning from corrections

**Target Progression**:

```
✅ Stage 2: Confirm Mode (Current - Nov 2025)
- Agent executes after human approval
- Goal: Reduce operator workload by 30%
- Status: 60% touchless achieved ✓

→ Stage 3: Autonomous Mode (Q1-Q2 2026)
- Agent executes for high-confidence cases (>90%)
- Human monitors exceptions only
- Goal: 65% touchless rate
- Enhancement: Add confidence scoring + Learning Agent

→ Stage 4: Proactive Mode (Q3-Q4 2026)
- Agent initiates conversations ("Should we consolidate these 5 bookings?")
- Goal: 70% touchless rate, proactive optimization
- Enhancement: Add proactive agents + voice interface
- Success: UMUX-Lite > 80, BUS-11 > 80
```

---

## 2. Architecture Overview

### 2.1 CargoX Agent Stack (TO-BE)

**Evolution Path**: Hubble v1.5 (Single LangChain Agent) → CargoX v2.0 (Multi-Agent Specialization)

**Phase 1-2 (Q1 2026)**: **Enhance Existing LangChain Agent**
```
Email Trans → Order Adapter → LangChain Agent (Enhanced) 🤖
                                      ↓
                              [Confidence Scoring] ⬅️ NEW
                              [Feedback Capture] ⬅️ NEW
                              [RAG Retrieval] ⬅️ NEW
                                      ↓
                              → Booking SVC → CargoX → CW1
                                      ↓
                              [Learning Agent] (weekly batch) ⬅️ NEW
                              [Evaluation Agent] (real-time monitor) ⬅️ NEW
```

**Phase 3 (Q2 2026)**: **Migrate to Multi-Agent Architecture**
```
[Customer/Operator/Partner]
          ↓
  [CargoX Orchestrator Agent] ⬅️ NEW (replaces single LangChain agent)
          ↓
  ┌───────────────────────────────────────┐
  │  Domain Agents (Multi-Agent System)   │ ⬅️ NEW (specialized agents)
  ├───────────────────────────────────────┤
  │ 📧 Email Analyzer (from Hubble)       │ ⬅️ Extract from LangChain
  │ ✅ Booking Validator (from Hubble)    │ ⬅️ Extract from LangChain
  │ 💰 Rate Agent                         │ ⬅️ NEW
  │ 📦 Quotation Agent                    │ ⬅️ NEW
  │ 🚚 Consolidation Planner (Hubble)    │ ⬅️ From Hackathon project
  │ 📊 Forecast Agent                     │ ⬅️ NEW (optional)
  │ 🧾 Invoice Validator                  │ ⬅️ NEW
  │ 🎓 Learning Agent                     │ ⬅️ NEW (Q1 2026)
  │ ⚖️ Evaluation Agent (LLM-as-Judge)    │ ⬅️ NEW (Q1 2026)
  │ 🔧 Master Data Agent (from Hubble)   │ ⬅️ From Master Data MCP
  │ 🛃 Customs Agent                      │ ⬅️ NEW (optional)
  │ 📞 Exception Handler                  │ ⬅️ NEW
  └───────────────────────────────────────┘
          ↓
  [Event Bus: order.received, booking.validated, operator.feedback, etc.]
          ↓
  ┌───────────────────────────────────────┐
  │  Integration Layer                    │
  ├───────────────────────────────────────┤
  │ • CargoWise One (CW1) ✅ Already Live │
  │ • ERP / Finance Systems               │
  │ • EDI / API Partners                  │
  │ • Email / Teams / Outlook ✅ Live     │
  │ • Warehouse Management Systems        │
  └───────────────────────────────────────┘
          ↓
  [Freight Graph: Knowledge Base] ⬅️ NEW (Q1-Q2 2026)
  - CW1 logs (operational truth)
  - EDI events (real-time milestones)
  - Contracts (pricing, SLAs)
  - Rate Repository (procurement data) ⬅️ Build in Q1 2026
  - SOPs (policy, process)
  - Emails/Notes (human context)
```

**Migration Strategy**:
1. **Don't Disrupt Live Customers**: Phase 1-2 enhancements are non-breaking
2. **Prove Value First**: Add trust components (confidence, feedback, learning) before refactoring
3. **A/B Test Multi-Agent**: Run parallel for 2 weeks (50% traffic each) before 100% migration
4. **Rollback Plan**: If multi-agent performs worse, revert to enhanced LangChain agent

---

### 2.2 Freight Graph Knowledge Layer

**Current State (Hubble v1.5)**:
- 🟡 **Partial**: Route knowledge base (GEO Service, Route Planner MCP)
- 🟡 **Partial**: Master data lookup (Master Data MCP, Master Data Svc)
- ❌ **Missing**: CW1 booking history (no RAG retrieval)
- ❌ **Missing**: Customer contracts (pricing, T&Cs)
- ❌ **Missing**: Rate repository (supplier rates, margins)
- ❌ **Missing**: SOPs (DG handling, customs procedures)

**Target State (CargoX v2.0)**:

**Purpose**: Unified cognitive map of freight operations accessible via RAG (Retrieval-Augmented Generation).

**Data Sources**:

| Source | Content | Update Frequency | Access Pattern | Hubble v1.5 Status | Enhancement Timeline |
|--------|---------|------------------|----------------|-------------------|---------------------|
| **CW1 Logs** | Bookings, shipments, invoices, master data | Real-time (event-driven) | Semantic search + SQL | ❌ Not indexed | **Q1 2026** (Weeks 11-12) |
| **EDI Events** | Milestones (cargo ready, departed, arrived) | Real-time (event-driven) | Event query by HAWB/MAWB | ❌ Not indexed | Q2 2026 |
| **Customer Contracts** | Pricing, payment terms, SLAs, volume commitments | Weekly batch | Vector search by customer | ❌ Not indexed | **Q1 2026** (Weeks 13-14) |
| **Rate Repository** | Supplier rates, validity dates, margins | Daily batch | Vector + filter by lane | ❌ Not indexed | **Q1 2026** |
| **SOPs / Manuals** | DG handling, customs procedures, escalation rules | Monthly | Semantic search | ❌ Not indexed | Q2 2026 |
| **Emails / Notes** | Customer inquiries, operator decisions, exceptions | Real-time | Full-text + semantic | ✅ Partial (email parsing live) | Q1 2026 (enhance) |
| **Route Knowledge** | CFS stations, pickup agents, receiving agents | Weekly batch | Geo search by location | ✅ **Live** (Route Planner MCP) | Enhancement: Add RAG |
| **Master Data** | Shipper, consignee, locations | Real-time | Exact match + fuzzy | ✅ **Live** (Master Data MCP) | Enhancement: Add RAG |

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

**Implementation Priority** (Q1-Q2 2026):
1. **Week 11-12**: Index CW1 booking history (1 year of data)
2. **Week 13-14**: Index customer contracts (pricing, T&Cs)
3. **Q2 2026**: Enhance Route + Master Data with RAG (currently exact match only)
4. **Q2 2026**: Index EDI events, SOPs (nice-to-have)

---

### 2.3 Multi-Agent Coordination Patterns

**Current State (Hubble v1.5)**:
- ✅ **Event-Driven**: MQ (message queue) for async processing
- 🟡 **Single Orchestrator**: LangChain agent coordinates all logic
- ❌ **Limited Specialization**: All AI logic in one agent

**Target State (CargoX v2.0)**:

**Purpose**: Define how agents collaborate to complete complex workflows.

#### Pattern Catalog

| Pattern | Description | Example Workflow | Handoff Trigger | Compensation Strategy | Hubble v1.5 Status |
|---------|-------------|------------------|-----------------|----------------------|-------------------|
| **Sequential Delegation** | Agent A completes → triggers Agent B | Email Analyzer → Booking Validator → Rate Agent | `booking.validated` event | Undo in reverse order | 🟡 Partial (MQ in place, agents not specialized) |
| **Parallel Consultation** | Orchestrator queries multiple agents simultaneously, aggregates results | Orchestrator asks (Quotation + Capacity + Routing) → selects best | User query "find best route" | N/A (read-only) | ❌ Not implemented |
| **Hierarchical Escalation** | Agent tries → fails → escalates to senior agent or human | Booking Validator (confidence < 70%) → Exception Handler → Human Operator | Confidence threshold breach | Human decision logged as ground truth | 🟡 Partial (human confirms all, no confidence threshold) |
| **Collaborative Refinement** | Agents iterate together until consensus or threshold met | Rate Agent proposes margin → Invoice Validator checks → Rate Agent adjusts | Validation fails | Iteration limit (max 3 rounds) | ❌ Not implemented |
| **Human-in-the-Loop Gate** | Agent proposes → human reviews → agent executes only after approval | Consol Planner suggests grouping → Operator approves → CW1 Sync Agent books | High-risk action (DG cargo, >$50k, new customer) | Human approval required; no auto-execution | ✅ **Live** (semi-automation) |
| **Compensating Transaction** | Agent A executes → Agent B detects error → Agent C reverses | Booking Agent creates CW1 record → Validator detects duplicate → Cleanup Agent deletes | Error detected in audit | Idempotent operations; audit log retained | ❓ Unknown (audit log not visible) |

**Implementation Timeline**:
- **Q1 2026**: Formalize HITL gates with confidence thresholds (currently all human-confirmed)
- **Q2 2026**: Implement Sequential Delegation + Hierarchical Escalation (multi-agent)
- **Q3 2026**: Implement Parallel Consultation + Collaborative Refinement (advanced)

#### Event Taxonomy for Freight Operations

**Core Events** (trigger agent activation):

| Event | Trigger Condition | Agent(s) Activated | Downstream Events | Payload Schema | Hubble v1.5 Status |
|-------|------------------|-------------------|-------------------|----------------|-------------------|
| `order.received` | Email attachment parsed | Email Analyzer → Booking Validator | `booking.validated` or `booking.exception` | `{email_id, attachments[], parsed_fields{}}` | ✅ **Live** (Email Trans publishes) |
| `booking.validated` | All mandatory fields present, rules passed | Rate Agent → Capacity Agent | `rate.calculated`, `capacity.checked` | `{booking_id, confidence, validation_result{}}` | 🟡 Partial (Quote 2 Book, no confidence) |
| `booking.exception` | Missing data, rule violation, low confidence | Exception Handler → Human Escalation | `operator.notified` | `{booking_id, exception_type, missing_fields[], reason}` | ❌ Not formalized (human confirms all) |
| `rate.calculated` | Rate lookup complete | Quotation Agent | `quotation.generated` | `{booking_id, rate_details{}, margin, validity}` | ❌ Not implemented |
| `consol.created` | Planner finalizes consolidation | Invoice Generator → CW1 Sync Agent | `invoice.drafted`, `cw1.updated` | `{consol_id, booking_ids[], total_cbm, departure_date}` | 🚧 Hackathon project (Dec 2025) |
| `operator.feedback` | Human corrects agent output | Learning Agent → RAG Retraining | `model.retrained`, `prompt.updated` | `{agent_id, feedback_type, correction{}, operator_id, timestamp}` | ❌ **Critical Gap** (Q1 2026) |
| `agent.error` | Agent throws exception | Exception Handler → On-Call Engineer | `incident.created`, `alert.sent` | `{agent_id, error_message, stack_trace, context{}}` | ❓ Unknown (incident response not documented) |

**Event Flow Example** (Email to Booking):

```
1. Email arrives → `order.received` ✅ Live
   ↓
2. Email Analyzer extracts fields → `email.parsed` ✅ Live (LangChain agent)
   ↓
3. Booking Validator checks fields ✅ Live (Quote 2 Book)
   ├─ All valid → `booking.validated` ✅ Live
   └─ Missing data → `booking.exception` ❌ Not formalized → Operator notified
   ↓
4. Rate Agent calculates margin → `rate.calculated` ❌ Not implemented
   ↓
5. Quotation Agent generates quote → `quotation.generated` ❌ Not implemented
   ↓
6. Operator approves → `booking.confirmed` ✅ Live (semi-automation)
   ↓
7. CW1 Sync Agent creates booking → `cw1.booking_created` ✅ Live (CargoX adapter)
   ↓
8. Confirmation email sent → `customer.notified` ❓ Unknown
```

---

## 3. Agent Persona Cards

*(Agent persona cards from v1.1 remain unchanged, but with Hubble alignment notes)*

### 🤖 Email Analyzer Agent

**Hubble v1.5 Status**: ✅ **Live** (LangChain agent + Order Adapter)

**Current Implementation**:
- ✅ Email Trans monitors inbox (polling or webhook)
- ✅ Order Adapter (Connect MQ) downloads attachments to blob storage
- ✅ LangChain agent parses email body + attachments (PDF, Excel, Word)
- ✅ OCR for scanned documents (AI Fine-tuning planned Nov 2025)
- ✅ Publishes `order.received` event to MQ

**Enhancement Needed** (Q1 2026):
- ❌ **Confidence Scoring**: Add confidence % to extraction (High/Medium/Low)
- ❌ **Source Citations**: Tag which fields extracted from which attachment page
- ❌ **Reasoning Trace**: Explain extraction decisions (e.g., "Shipper from email body line 3")

**Implementation**:
```python
# Current: LangChain agent extracts fields
def extract_booking_data(email_text, attachments):
    result = langchain_agent.run(email_text, attachments)
    return result  # No confidence score

# Enhanced (Q1 2026): Add confidence scoring
def extract_booking_data_enhanced(email_text, attachments):
    result = langchain_agent.run(email_text, attachments)
    
    # Calculate confidence based on:
    # - Field completeness (all required fields present?)
    # - OCR quality (if scanned document)
    # - Ambiguity (multiple possible values?)
    confidence = calculate_confidence(result)
    
    return {
        "booking_data": result,
        "confidence": confidence,  # 0.0 - 1.0
        "confidence_level": get_level(confidence),  # "High" / "Medium" / "Low"
        "reasoning": explain_confidence(result),
        "sources": tag_sources(result, attachments)  # Which field from which page
    }
```

---

### ✅ Booking Validator Agent

**Hubble v1.5 Status**: 🟡 **Partial** (Quote 2 Book + Booking Amendment, no confidence scoring)

**Current Implementation**:
- ✅ Quote 2 Book validates booking requests
- ✅ Booking Amendment handles updates
- ✅ Master Data MCP cross-checks shipper/consignee against CW1
- ✅ Route Planner MCP suggests CFS station, pickup agent
- ❓ Unknown: Capacity check, DG regulation check, margin check

**Enhancement Needed** (Q1 2026):
- ❌ **Confidence Scoring**: Add validation confidence (High/Medium/Low)
- ❌ **Escalation Rules**: Formalize when to escalate (confidence < 70%, DG cargo, etc.)
- ❌ **Feedback Loop**: Capture operator corrections for Learning Agent

**Decision Logic** (TO-BE):
1. **Mandatory Field Check**
   - Origin, destination, cargo details, ready date
   - If missing → `booking.exception`

2. **Master Data Validation** ✅ Live (Master Data MCP)
   - Cross-check shipper/consignee against CW1
   - If not found → Trigger Master Data Agent (create new or link existing)

3. **DG Regulation Check** ❓ Unknown if implemented
   - If hazardous cargo detected → Validate against DG database
   - If Class 1-9 → Require DG specialist approval

4. **Capacity Check** ❓ Unknown if implemented
   - Calculate CBM, check against available capacity
   - If overbooked → Suggest alternate dates

5. **Margin Check** ❓ Unknown if implemented
   - If margin < 5% → Flag for review
   - If margin < 0% → Reject

6. **Confidence Scoring** ❌ Not implemented (Q1 2026)
   - High (>90%): All checks pass, master data match perfect
   - Medium (70-90%): Minor issues (e.g., location alias)
   - Low (<70%): Missing critical data or multiple issues

**Escalation Rules** (TO-BE, Q1 2026):
- Confidence < 70% → Exception Handler → Operator review
- DG cargo → DG Compliance Officer approval required
- New shipper (not in CW1) → Master Data Agent → Operator confirms
- Margin < 0% → Rate Agent recalculates → Operator approves pricing

---

### 💰 Rate Agent

**Hubble v1.5 Status**: ❌ **Missing** (Manual rate lookup still required)

**Enhancement Priority**: **High** (Q1 2026, Weeks 17-18)

**Implementation Plan**:
1. **Week 17**: Build Rate Repository (index supplier rates, customer contracts)
2. **Week 18**: Extract rate lookup logic from LangChain agent → Dedicated Rate Agent
3. **Week 18**: Integrate with Booking Validator (sequential delegation pattern)

**Decision Logic** (TO-BE):
1. **Rate Lookup**
   - Query Rate Repository by lane (origin → destination)
   - Filter by validity date
   - Select best rate (lowest cost or preferred supplier)

2. **Margin Calculation**
   - Sell Rate = Buy Rate + Margin %
   - Apply customer-specific discounts (from contract)

3. **Dynamic Pricing** (optional, Q2 2026)
   - Adjust margin based on:
     - Capacity utilization (high demand → +5%)
     - Customer tier (VIP → -2%)
     - Market trends (spot rate vs contract rate)

---

### 📦 Quotation Agent

**Hubble v1.5 Status**: ❌ **Missing** (Manual quote generation still required)

**Enhancement Priority**: **High** (Q1 2026, Weeks 19-20)

**Implementation Plan**:
1. **Week 19**: Build quotation template library (PDF generation, multi-currency)
2. **Week 20**: Integrate with Rate Agent (sequential delegation pattern)
3. **Week 20**: Add email draft functionality (send quote to customer)

---

### 🚚 Consolidation Planner Agent

**Hubble v1.5 Status**: 🚧 **In Progress** (Hackathon project followup, Dec 2025)

**Current Plan** (From Rollout Plan):
- **Features**: LCL container load plan beta, LCL capacity integration, LCL routing engine integration, LCL scheduling integration, LCL AI Consol planning
- **Business Value**: Reduce work at least X mins per shipment for GCA LCL routing team
- **Timeline**: Est. Dec 31, 2025
- **Technical Milestones**: Knowledge self-learning module design, LCL Capacity service readiness

**Enhancement Needed** (Q1 2026):
- ✅ Integrate Hackathon output into CargoX multi-agent architecture
- ❌ Add confidence scoring + reasoning trace for consol recommendations
- ❌ Add operator feedback loop (accept/reject/modify consol suggestions)

---

### 🎓 Learning Agent

**Hubble v1.5 Status**: ❌ **Critical Gap** (Q1 2026, Weeks 9-10)

**Purpose**: Analyze operator corrections, identify patterns, and propose improvements to other agents.

**Why Critical**: Without Learning Agent, Hubble can't improve systematically from operator corrections. Same errors will repeat.

**Implementation Plan** (Q1 2026):
1. **Week 3-4**: Build Operator Feedback UI (👍👎 buttons + correction form)
2. **Week 9-10**: Build Learning Agent (aggregate corrections weekly → propose improvements)
3. **Week 10**: Integrate with Evaluation Agent (A/B test proposed improvements)

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

**Learning SLOs**:
- **Feedback Response Time**: < 7 days from correction to model update (target)
- **Accuracy Improvement Rate**: +5% per quarter (target)
- **Feedback Adoption Rate**: > 70% of operator corrections incorporated (target)

---

### ⚖️ Evaluation Agent (LLM-as-Judge)

**Hubble v1.5 Status**: ❌ **Critical Gap** (Q1 2026, Weeks 7-8 offline, Weeks 15-16 production)

**Purpose**: Continuously assess quality of agent outputs before and after deployment.

**Why Critical**: Without Evaluation Agent, no quality gate before deploying prompt changes. Risk of regression when Learning Agent proposes improvements.

**Implementation Plan** (Q1 2026):
1. **Week 7-8**: Build Evaluation Agent (offline mode for A/B testing)
2. **Week 15-16**: Deploy Evaluation Agent (production mode, score 100% of outputs)
3. **Week 16**: Integrate with Learning Agent (gate deployments, alert on regression)

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

---

*(Remaining agent persona cards: Master Data Agent, Invoice Validator, Exception Handler, etc. follow similar pattern - documenting Hubble v1.5 status + enhancement plan)*

---

## 4-8. [Sections 4-8 remain largely unchanged from v1.1]

*(Retrieval & RAG Pipeline, Trust Maturity Model, Human-Agent Collaboration, RAG Feedback & Learning Loop, Capability Mapping - content from v1.1 with Hubble alignment notes where relevant)*

---

## 9. Success Metrics & KPIs

### North Star Metrics

| Metric | Hubble v1.5 Baseline (Nov 2025) | CargoX v2.0 Target (Dec 2026) | Gap to Close | Trend |
|--------|--------------------------------|-------------------------------|--------------|-------|
| **Touchless Rate** | ~60% (estimated) | 70% | +10% | ↗️ Q1-Q4 2026 |
| **Booking Accuracy** | Unknown (not tracked) ⚠️ | 95% | Establish baseline + improve | ↗️ Start tracking Q1 2026 |
| **Time to Quote** | 3-5 mins per booking | 15 minutes (vs 4 hours manual) | 3x improvement | ↗️ Q1-Q2 2026 (add Rate + Quotation agents) |
| **Invoice Error Rate** | Unknown (not tracked) ⚠️ | 3% | Establish baseline + improve | ↗️ Start tracking Q1 2026 |
| **Operator Satisfaction (UMUX-Lite)** | Unknown (not tracked) ⚠️ | 80 | Establish baseline + improve | ↗️ Start tracking Q1 2026 |
| **Conversational Usability (BUS-11)** | Unknown (not tracked) ⚠️ | 80 (Very Good) | Establish baseline + improve | ↗️ Start tracking Q2 2026 |
| **Customer Rollout** | 5 big customers (Aug-Oct 2025) ✅ | 15+ customers globally | 3x growth | ↗️ Q1-Q4 2026 |
| **Cost Savings (annualized)** | $0 (baseline) | $2M/year | Measure from Jan 2026 | ↗️ Track monthly |

**Action Items** (Immediate):
1. **Establish Baseline Metrics** (Week 1-2, Dec 2025)
   - Survey 10 operators from 5 big customers: Current touchless rate? Accuracy? Satisfaction?
   - Manual tracking if automated dashboards not ready yet
   - Set baseline for Q1 2026 target-setting

2. **Build Observability Dashboard** (Weeks 5-6, Q1 2026)
   - Track 7 North Star metrics in real-time
   - Accessible to all stakeholders (operators, leadership, on-call engineers)
   - Alerts if any metric degrades >10%

---

### Agent-Level KPIs (Tracked Monthly)

| Agent | Key Metric | Hubble v1.5 Baseline | Target (Dec 2026) | Current Status | Action if Below Target |
|-------|-----------|---------------------|------------------|---------------|----------------------|
| Email Analyzer | Extraction accuracy | Unknown (not tracked) | >90% | **Establish baseline Q1 2026** | Review OCR fine-tuning (planned Nov 2025) |
| Booking Validator | Validation accuracy | Unknown (not tracked) | >92% | **Establish baseline Q1 2026** | Review business rules, master data quality |
| Booking Validator | Touchless rate | ~60% (estimated) | >65% (Q2 2026) → >70% (Q4 2026) | **Track from Q1 2026** | ⚠️ Review escalation rules; add confidence scoring |
| Rate Agent | Rate accuracy | N/A (not implemented) | >98% | **Build in Q1 2026** | Validate Rate Repository completeness |
| Quotation Agent | Quote acceptance rate | N/A (not implemented) | >65% | **Build in Q1 2026** | Analyze rejected quotes; adjust pricing |
| Consol Planner | Utilization rate | Unknown (Hackathon project) | >85% | **Integrate Q1 2026** | Review grouping algorithm from Hackathon |
| Invoice Validator | Error detection rate | N/A (not implemented) | >95% | **Build in Q2 2026** | Compare quote vs actual systematically |
| Learning Agent | Feedback adoption rate | N/A (not implemented) | >70% | **Build in Q1 2026** | Prioritize high-impact corrections first |
| Evaluation Agent | Human agreement rate | N/A (not implemented) | >90% | **Build in Q1 2026** | Calibrate LLM-as-Judge with human expert scoring |

---

## 10. Hubble → CargoX v2.0 Rollout (2026)

**Overview**: This section replaces the generic 26-week rollout from v1.1 with a **Hubble-specific phased enhancement plan** aligned with live production constraints.

**Key Principles**:
1. **Don't Disrupt Live Customers**: 5 big customers already live, more rolling out Nov-Dec 2025
2. **Enhance, Not Replace**: Add trust framework around existing LangChain agent first (Q1 2026)
3. **Migrate Gradually**: Move to multi-agent architecture only after trust components validated (Q2 2026)
4. **Measure Everything**: Establish baselines Q1, track monthly, adjust quarterly

---

### Phase 1: Trust & Observability Foundations (Dec 2025 - Feb 2026)

**Goal**: Add trust indicators, feedback loops, and observability **without disrupting live rollout**.

**Constraints**:
- ✅ 5 big customers live (Renner, DK, PUMA, Schneider, Vestas)
- 🚧 More customers rolling out (Nov 28 - Dec 31, 2025 per Hubble roadmap)
- ⚠️ Must be **non-breaking** enhancements (no refactor yet)

| Week | Focus | Deliverables | Owner | Risk | Success Criteria |
|------|-------|--------------|-------|------|-----------------|
| **Week 1-2 (Dec 2025)** | Confidence Scoring | Add confidence % to LangChain agent outputs (High >85%, Medium 70-85%, Low <70%) | AI Team | Low (non-breaking) | 100% of Hubble outputs show confidence scores in logs |
| **Week 3-4 (Jan 2026)** | Operator Feedback UI | Add 👍👎 buttons + correction form in Hubble Platform GUI | Frontend Team | Low | Operators can provide feedback; target: 50+ corrections/week |
| **Week 5-6 (Jan 2026)** | Observability Dashboard v0.1 | Build KPI dashboard: touchless rate, accuracy, latency, operator feedback | Data Engineering | Medium | Dashboard tracks 5 core KPIs; accessible to all stakeholders |
| **Week 7-8 (Feb 2026)** | Evaluation Agent (Offline) | Build LLM-as-Judge for A/B testing (not production yet) | AI Team | Low | Offline eval suite ready; 100+ test cases with ground truth |

**Budget**: $50k (leverage existing 3.5 FTEs, no new hires)

**Success Criteria**:
- ✅ 100% of Hubble outputs show confidence scores (visible in UI or logs)
- ✅ Operators can provide feedback (target: 50+ corrections/week from 5 customer sites)
- ✅ Dashboard tracks 5 core KPIs (touchless, accuracy, latency, escalation, UMUX)
- ✅ No regression in customer rollout (continue onboarding new customers per Hubble roadmap)

**Rollback Plan**:
- If confidence scoring causes latency issues → Make async (calculate post-response)
- If feedback UI confuses operators → Simplify to 👍👎 only (no comment field initially)
- If dashboard build delayed → Use manual tracking (Google Sheets) temporarily

---

### Phase 2: Learning Loop & RAG Foundation (Mar - Apr 2026)

**Goal**: Enable continuous improvement via Learning Agent + build Freight Graph knowledge base.

| Week | Focus | Deliverables | Owner | Risk | Success Criteria |
|------|-------|--------------|-------|------|-----------------|
| **Week 9-10 (Mar 2026)** | Learning Agent | Aggregate operator corrections weekly → Propose prompt improvements | AI Team | Medium | Learning Agent deployed; 1st prompt improvement in production (target: +5% accuracy) |
| **Week 11-12 (Mar 2026)** | Freight Graph (CW1 Logs) | Index CW1 booking/shipment logs for RAG retrieval | Data Engineering | High (CW1 integration) | RAG retrieval operational for CW1 (Grounding@K > 80%) |
| **Week 13-14 (Apr 2026)** | Freight Graph (Contracts) | Index customer contracts (pricing, T&Cs) | Domain Expert + AI | Medium | RAG retrieval operational for contracts |
| **Week 15-16 (Apr 2026)** | Evaluation Agent (Production) | Deploy LLM-as-Judge to score 100% of outputs in real-time | AI Team | Medium | Evaluation Agent scores all outputs; alerts if accuracy drops >10% |

**Budget**: $75k (may need 1 temporary data engineer for CW1 integration)

**Success Criteria**:
- ✅ Learning Agent deployed; 1st prompt improvement in production (target: +5% accuracy)
- ✅ RAG retrieval operational for CW1 + contracts (Grounding@K > 80%)
- ✅ Evaluation Agent scores all outputs; alerts if accuracy drops >10%
- ✅ Touchless rate improves to 65% (up from 60%)

**Rollback Plan**:
- If Learning Agent proposes bad improvements → Evaluation Agent blocks deployment
- If CW1 indexing causes performance issues → Batch index nightly (not real-time)
- If Evaluation Agent latency >1s → Make async (score post-response)

---

### Phase 3: Multi-Agent Specialization (May - Jul 2026)

**Goal**: Decompose monolithic LangChain agent into specialized domain agents.

**Risk**: **High** (major refactor, extensive testing required)

| Week | Focus | Deliverables | Owner | Risk | Success Criteria |
|------|-------|--------------|-------|------|-----------------|
| **Week 17-18 (May 2026)** | Rate Agent (Standalone) | Extract rate lookup logic from LangChain agent → Dedicated Rate Agent | AI Team | High (refactor risk) | Rate Agent operational; accuracy >98%, latency <2s |
| **Week 19-20 (May 2026)** | Quotation Agent (Standalone) | Build Quotation Agent (generate PDF, multi-currency) | AI Team | Medium | Quotation Agent operational; generation time <1 min |
| **Week 21-22 (Jun 2026)** | Agent Orchestrator v2.0 | Build orchestrator to route tasks: Email Analyzer → Booking Validator → Rate → Quotation | Backend Team | High | Orchestrator operational; 3-agent workflow live |
| **Week 23-24 (Jun 2026)** | Invoice Validator Agent | Build Invoice Validator (detect quote vs actual discrepancies) | AI Team | Medium | Invoice Validator operational; error detection >95% |
| **Week 25-26 (Jul 2026)** | A/B Test Multi-Agent vs Monolith | Run parallel for 2 weeks: Old LangChain vs New Multi-Agent | Full Team | High | Multi-agent matches or exceeds LangChain (accuracy, latency, touchless) |

**Budget**: $150k (may need 1 temporary backend engineer for orchestrator)

**Success Criteria**:
- ✅ Multi-agent system operational; 50% traffic routed to new architecture
- ✅ Accuracy maintained or improved (>95%)
- ✅ Latency < 3s (same as current)
- ✅ **If successful → 100% migration; if not → rollback to enhanced LangChain**

**Decision Gate** (Week 26):
- **Go/No-Go**: Multi-agent vs LangChain A/B test results
  - **Go** (100% migration): Multi-agent accuracy ≥ LangChain AND latency ≤ LangChain AND touchless ≥ LangChain
  - **No-Go** (rollback): Any metric worse by >5% → Revert to enhanced LangChain agent, continue improving

**Rollback Plan**:
- If multi-agent performs worse → Revert to enhanced LangChain agent
- If orchestrator has bugs → Fallback to direct LangChain calls (bypass orchestrator)
- If specific agent fails → Fallback to LangChain for that capability only (hybrid mode)

---

### Phase 4: Advanced Capabilities & Scale (Aug - Dec 2026)

**Goal**: Deploy proactive agents, voice interface, and expand globally.

| Focus | Deliverables | Timeline | Success Criteria |
|-------|--------------|----------|-----------------|
| **Consol Planner Agent** | Integrate Hackathon output into multi-agent system | Aug - Sep 2026 | Consol Planner operational; utilization rate >85% |
| **Proactive Agents** | Agents initiate suggestions ("Should we consolidate these 5 bookings?") | Sep - Oct 2026 | 65% touchless → 67% touchless; proactive suggestions accepted >50% |
| **Voice Agent (Warehouse)** | Hands-free booking updates via mobile app | Oct - Nov 2026 | Voice task completion rate > 85%; warehouse pilot live |
| **Regional Expansion** | Deploy to 3 additional Air/LCL countries (beyond GCA LCL) | Nov - Dec 2026 | 15+ customers globally (3x from 5); 70% touchless achieved |

**Budget**: $175k (may need regional deployment support)

**Success Criteria**:
- ✅ 70% touchless rate globally (up from 60%)
- ✅ 95% accuracy (up from unmeasured baseline)
- ✅ 15+ customers globally (up from 5)
- ✅ Operator satisfaction: UMUX-Lite > 80, BUS-11 > 80
- ✅ Cost savings: $2M/year annualized

---

### Hubble Roadmap Integration (Nov-Dec 2025)

**Current Hubble Plan** (Already Approved):

| Milestone | Timeline | Status | Integration with CargoX Playbook |
|-----------|----------|--------|----------------------------------|
| **Full SCM/SCP GCA LCL Rollout** | Nov 28, 2025 | 🚧 Planned | ✅ Complete as planned; sets baseline for Q1 2026 enhancements |
| **Pilot Another LCL Country** | Nov 14, 2025 | 🚧 Planned | ✅ Complete as planned; learn from pilot for regional expansion (Q4 2026) |
| **Pilot One Air Booking Country** | Nov 30, 2025 | 🚧 Planned | ✅ Complete as planned; Air agent patterns inform multi-agent design (Q2 2026) |
| **AI Master Data Auto Pickup** | Nov 15, 2025 | 🚧 Planned | ✅ Complete as planned; integrate with Master Data Agent (Q2 2026) |
| **AI Routing Search (CFS Station)** | Nov 30, 2025 | 🚧 Planned | ✅ Complete as planned; enhance with RAG (Q1-Q2 2026) |
| **AI GCA LCL Consol Planning** | Dec 31, 2025 | 🚧 Hackathon followup | ✅ Complete as planned; integrate with Consol Planner Agent (Q3 2026) |

**Recommendation**: **Do NOT delay or modify Hubble v1.5 roadmap**. Complete all Nov-Dec milestones as planned. Use Q1 2026 to add trust components around proven Hubble architecture.

---

### Timeline Summary (2026 Roadmap)

| Quarter | Focus | Key Deliverables | Budget | FTEs |
|---------|-------|-----------------|--------|------|
| **Q1 2026** | Trust + Learning | Confidence scores, Feedback UI, Learning Agent, Evaluation Agent, RAG (CW1 + contracts), Observability dashboard | $125k | 3.5 (existing) + 0.5 temp (CW1 integration) |
| **Q2 2026** | Multi-Agent | Rate Agent, Quotation Agent, Invoice Validator, Orchestrator v2.0, A/B test | $150k | 3.5 + 1.0 temp (backend orchestrator) |
| **Q3 2026** | Advanced | Consol Planner integration, Proactive agents | $75k | 3.5 |
| **Q4 2026** | Scale | Voice agent, Regional expansion | $100k | 3.5 + 0.5 temp (regional deployment) |
| **Total** | - | - | **$450k** | **Avg 4.25 FTEs** |

**Contingency**: $50k buffer → **Total Year 1 Investment: $500k** (aligned with playbook business case)

---

## 11-18. [Sections 11-18 remain largely unchanged from v1.1]

*(References, Email/Attachment Intake Blueprint, Human-Agent Interaction Patterns, Trust Indicators & UI Components, Conversational AI Evaluation, Governance & Security, Observability & Operations, Adoption & Change Management - content from v1.1 with Hubble alignment notes where relevant)*

---

## Appendix: Change Log

### v1.2 (November 2025) - **Hubble Integration Release**
- 🔄 **NEW §0**: Hubble v1.5 AS-IS Architecture, Gap Analysis, Current Metrics
- 🎯 **UPDATED §1**: Vision statement revised to "From Semi-Automation to Full Intelligence"
- 🎯 **UPDATED §2**: Architecture shows Hubble AS-IS → CargoX TO-BE evolution path
- 🎯 **UPDATED §3**: Agent persona cards annotated with Hubble v1.5 status + enhancement plans
- 📈 **UPDATED §9**: KPIs show Hubble v1.5 baseline (60% touchless, 5 customers) → CargoX v2.0 target (70%, 15+)
- 🚀 **COMPLETELY REWRITTEN §10**: Hubble-specific 2026 rollout plan (4 phases, Q1-Q4)
- ✅ **Integration Notes**: Throughout document, Hubble v1.5 status noted with alignment indicators (🟢🟡🔴)

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

**End of Playbook v1.2**

---

**Document Metadata**:
- **Version**: 1.2
- **Date**: November 2025
- **Authors**: AI Architecture Team, Product, UX, Engineering
- **Status**: Production-Aligned (Based on Live Hubble v1.5)
- **Next Review**: January 2026 (after Phase 1 complete)
- **Feedback**: Send to cargox-feedback@maersk.com
- **Companion Documents**:
  - `Hubble_CargoX_Integration_Analysis.md` (detailed gap analysis)
  - `AI_Agentic_Playbook_v1.1_Executive_Summary.md` (8-min exec read)
