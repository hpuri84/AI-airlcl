# CargoX Domain Agent Mapping to AI Logistics Orchestration Hub

**Purpose**: Map the 13 CargoX domain agents from the AI Agentic Playbook v1.2 to the One Platform Orchestration Hub architecture.

**Version**: 1.0  
**Date**: January 2025

---

## Architecture Overview

```
AI Logistics Orchestration Hub (One Platform)
        ↓
┌───────────────────────────────────────────────────────────────────────┐
│                    ORCHESTRATION HUBS                                  │
├────────────┬──────────────┬──────────────┬──────────────┬─────────────┤
│ Customer   │ Shipment     │ Visibility   │ Integration  │ Operational │
│ Experience │ Orchestration│ Orchestration│ Orchestration│ Hub         │
│ (CX) Hub   │ Hub          │ Hub          │ Hub          │             │
└────────────┴──────────────┴──────────────┴──────────────┴─────────────┘
        ↓                                                         ↓
  [Domain Agents]                                      [Monitoring & Feedback]
        ↓
  [Model Selector] → [Foundation Model 1 / 2]
        ↓
  [RAG Pipeline: Ingestion → Chunking → Embeddings → Vector Store]
```

---

## 1. CUSTOMER EXPERIENCE (CX) ORCHESTRATION HUB

**Purpose**: Customer-facing interactions (email, chat, quotes, bookings, pricing)

### Agent Mapping

| **CargoX Agent** | **Function** | **One Platform Module** | **Priority** | **Effort** |
|------------------|--------------|-------------------------|--------------|------------|
| **📧 Email Analyzer** | Parse customer emails, extract booking details, download attachments | Email Processing & AI Integration (Hubble) | **P0** | Low (already live) |
| **🔄 Order Transformation Agent** | Convert parsed email → structured booking JSON | Email Processing & AI Integration | **P0** | Low (already live) |
| **✅ Order Validation Agent** | Validate booking fields (mandatory fields, business rules) | Email Processing & AI Integration | **P0** | Low (already live) |
| **💰 Quotation Agent** | Generate rate quotes based on lane, cargo type, volume | Pricing Agent (CX Hub) | **P1** | Medium |
| **📦 Pricing Agent** | Real-time pricing lookup from rate repository + margin calculation | Pricing Agent (CX Hub) | **P1** | Medium |
| **🗺️ Route Planner Agent** | Suggest optimal routing (CFS station, carrier, transit time) | Route Planner Agent (CX Hub) | **P0** | Low (already live) |
| **💬 Conversational Agent** | Q&A chatbot for shipment inquiries (\"Where is my cargo?\") | Q&A Section (CX Hub) | **P2** | Medium |

**Technology Stack**:
- **Frontend**: React (Vite) dashboard for operator review
- **Backend**: LangChain → LangGraph for multi-agent orchestration
- **RAG**: Azure AI Search + OpenAI embeddings for customer contract lookup
- **Integrations**: Outlook/Gmail API (email intake), CargoWise One (booking submission)

**Key Workflows**:
1. **Email-to-Booking**:
   ```
   Email arrives → Email Analyzer (parse) → Order Transformation (structure) 
      → Order Validation (check rules) → Quotation Agent (price) 
      → Operator Approval (HITL) → CW1 Sync
   ```

2. **Conversational Q&A**:
   ```
   Customer asks \"Where is HAWB 12345?\" → Conversational Agent 
      → RAG lookup (CW1 logs + EDI events) → Response with milestones
   ```

---

## 2. SHIPMENT ORCHESTRATION HUB

**Purpose**: Planning and execution of consolidations, routing, capacity optimization

### Agent Mapping

| **CargoX Agent** | **Function** | **One Platform Module** | **Priority** | **Effort** |
|------------------|--------------|-------------------------|--------------|------------|
| **🚚 Consolidation Planner** | Optimize consolidation plan (bin-packing, margin maximization) | Flight Allocation & Consolidation (GCA Air) | **P0** | Medium (Hackathon project) |
| **📊 Forecast Agent** | Predict capacity needs, flight delays, demand surges | Flight Status Verification (Smart Feature) | **P2** | High |
| **🗺️ Route Planner Agent** | Route optimization (already mapped to CX Hub above) | Flight Allocation & Consolidation | **P0** | Low (already live) |

**Technology Stack**:
- **Optimization**: Python (PuLP, OR-Tools) for bin-packing + margin maximization
- **RAG**: Retrieve block space agreements, ULD assignments from contracts
- **Integrations**: TMS (transport management system), CargoWise One (CONSOL creation)

**Key Workflows**:
1. **Consolidation Planning**:
   ```
   Daily ULD assignments received → Consolidation Planner (optimize) 
      → Operator Review (HITL) → TMS creates CONSOL → CW1 Sync 
      → Warehouse receives loading plan
   ```

2. **Flight Status Monitoring**:
   ```
   Daily batch (midnight) → Forecast Agent (scrape airline websites or API) 
      → Compare with CW1 ETD/ETA → Exception Handler (if >2h delta) 
      → Notify gateway → Update CW1
   ```

---

## 3. VISIBILITY ORCHESTRATION HUB

**Purpose**: Real-time tracking, dashboards, demand estimation, alerts

### Agent Mapping

| **CargoX Agent** | **Function** | **One Platform Module** | **Priority** | **Effort** |
|------------------|--------------|-------------------------|--------------|------------|
| **📊 Order Visibility Agent** | Track order status (email received → booking created → confirmed) | Shipment Monitoring Dashboard | **P1** | Low |
| **🚢 Shipment Visibility Agent** | Track shipment milestones (warehouse arrival → loading → flight departure → arrival) | Shipment Monitoring Dashboard + Consolidation Monitoring | **P1** | Medium |
| **📈 Demand Estimation Agent** | Forecast weekly booking volume, capacity requirements | Demand Estimation (Visibility Hub) | **P2** | High |
| **📊 Dashboard Agent** | UI orchestration for operator/customer dashboards | Shipment Monitoring Dashboard + Consolidation Monitoring | **P0** | Medium |

**Technology Stack**:
- **Frontend**: React (Vite) with real-time WebSocket updates
- **Backend**: Event-driven (Azure Event Grid or Kafka) for milestone tracking
- **RAG**: Query CW1 logs, EDI events, warehouse scans for real-time status
- **Integrations**: CargoWise One, WMS, TMS, airline tracking APIs

**Key Workflows**:
1. **Real-Time Shipment Tracking**:
   ```
   Warehouse scan event → Shipment Visibility Agent (update status) 
      → Dashboard Agent (push update to UI) → Customer/Operator sees milestone
   ```

2. **Demand Forecasting**:
   ```
   Weekly batch → Demand Estimation Agent (analyze CW1 booking history) 
      → Predict next week volume → Alert ops team if capacity shortage
   ```

---

## 4. INTEGRATION ORCHESTRATION HUB

**Purpose**: System integrations (CargoWise One, SAP, WMS, customs, master data)

### Agent Mapping

| **CargoX Agent** | **Function** | **One Platform Module** | **Priority** | **Effort** |
|------------------|--------------|-------------------------|--------------|------------|
| **💼 Financial Integration Agent** | SAP invoice processing, AR/AP posting | SAP Invoice Processing | **P1** | Medium |
| **🏭 Warehouse Integration Agent** | WMS integration (receive cargo, measure, track picking/loading) | WMS (Warehouse Management) | **P1** | Medium |
| **🔧 Master Data Integration Agent** | Customer/consignee/shipper lookup and validation | Address-to-Org Code Mapping (already live) | **P0** | Low (already live) |
| **💰 Rates Integration Agent** | Rate repository lookup, margin calculation | Flight Allocation & Consolidation (FRT cost calculation) | **P1** | Medium |
| **🛃 Customs Agent** | Customs clearance tracking, document validation | Consolidation Monitoring (customs clearance status) | **P2** | High |

**Technology Stack**:
- **SAP Integration**: REST API or BAPI for invoice extraction
- **WMS Integration**: REST API or EDI (DESADV, IFTSTA) for warehouse events
- **Master Data**: Direct DB lookup (Master Data MCP already live)
- **Integrations**: CargoWise One, SAP, WMS, customs portals

**Key Workflows**:
1. **SAP Invoice Automation**:
   ```
   Daily SAP invoice generated → Financial Integration Agent (detect + parse) 
      → Populate customer-specific Excel → Notification Agent (email) 
      → Customer replies → Email Analyzer (parse reply) 
      → Financial Integration Agent (validate) → CW1 Sync (upload)
   ```

2. **Warehouse Cargo Receipt**:
   ```
   Cargo arrives → Warehouse Integration Agent (create WMS record) 
      → Measure dimensions/weight → Compare with pre-alert 
      → Evaluation Agent (flag discrepancies) → CW1 Sync (update)
   ```

---

## 5. OPERATIONAL HUB

**Purpose**: Operator feedback, learning, evaluation, exception handling

### Agent Mapping

| **CargoX Agent** | **Function** | **One Platform Module** | **Priority** | **Effort** |
|------------------|--------------|-------------------------|--------------|------------|
| **👥 Feedback Collection Agent** | Capture operator corrections (👍👎, edits, manual overrides) | Operator Feedback UI (One Platform) | **P0** | Low |
| **🎓 Learning Agent** | Analyze feedback patterns weekly, retrain prompts/models | AI Monitoring Hub (Learning Loop) | **P0** | Medium |
| **⚖️ Evaluation Agent** | LLM-as-Judge for output quality, grounding checks | AI Monitoring Hub (Quality Gate) | **P0** | Medium |
| **📞 Exception Handler Agent** | Escalate low-confidence cases, anomalies, errors to human operators | Exception Handling (across all hubs) | **P0** | Medium |
| **🔔 Notification Agent** | Send alerts (email, SMS, Teams) for exceptions, milestones | Automated Notifications (across all hubs) | **P1** | Low |

**Technology Stack**:
- **Feedback UI**: React component embedded in all operator screens
- **Learning Agent**: Python (pandas, scikit-learn) for pattern analysis + GPT-4 for prompt rewriting
- **Evaluation Agent**: GPT-4-as-Judge for quality scoring (accuracy, grounding, completeness)
- **Alerting**: Azure Logic Apps or Functions for email/SMS/Teams notifications

**Key Workflows**:
1. **Operator Feedback Loop**:
   ```
   Operator corrects booking → Feedback Collection Agent (capture correction) 
      → Learning Agent (weekly batch analysis) → Identify error pattern 
      → Retrain prompt → A/B test → Deploy if >5% improvement
   ```

2. **Quality Gate Before Deployment**:
   ```
   New prompt candidate → Evaluation Agent (test on 100 bookings) 
      → Score accuracy, grounding, completeness 
      → If >85% pass → Deploy to production 
      → If <85% → Reject + alert product team
   ```

3. **Exception Escalation**:
   ```
   Booking Validator (confidence <70%) → Exception Handler 
      → Notify operator via Teams + Dashboard alert 
      → Operator reviews → Provides feedback → Learning Agent learns
   ```

---

## 6. AI MONITORING HUB

**Purpose**: Model selection, observability, A/B testing, governance

### Agent Mapping

| **CargoX Component** | **Function** | **One Platform Module** | **Priority** | **Effort** |
|----------------------|--------------|-------------------------|--------------|------------|
| **🤖 Model Selector** | Route query to Foundation Model 1 (GPT-4) or Model 2 (Claude, Gemini) | Model Selector (AI Monitoring Hub) | **P1** | Low |
| **📊 Observability Dashboard** | Track agent KPIs (accuracy, latency, cost, touchless rate) | Azure Monitor + App Insights | **P0** | Low (already live) |
| **🔬 A/B Testing Engine** | Split traffic between prompt versions, compare performance | Learning Agent + Evaluation Agent | **P1** | Medium |
| **🛡️ Governance Agent** | PII detection, DG specialist approval gates, bias audits | Governance Framework (playbook) | **P2** | High |

**Technology Stack**:
- **Model Selector**: LangChain `ChatModelSwitch` or custom router
- **Observability**: Azure Application Insights (telemetry), custom dashboards (Grafana or Power BI)
- **A/B Testing**: Custom Python service (traffic split) + statistical significance testing (t-test)

**Key Workflows**:
1. **Model Selection**:
   ```
   Query arrives → Model Selector (route based on query type) 
      ├─ Simple query → GPT-3.5-Turbo (cost-optimized)
      ├─ Complex reasoning → GPT-4o (accuracy-optimized)
      └─ Sensitive data → On-prem LLaMA (security-optimized)
   ```

2. **A/B Testing**:
   ```
   New prompt candidate → A/B Testing Engine (50% traffic to new, 50% to old) 
      → Evaluation Agent (score both) → After 2 weeks → Statistical test 
      → If new wins → Deploy 100% → If old wins → Reject new
   ```

---

## 7. RAG PIPELINE

**Purpose**: Unified knowledge layer for all agents (Freight Graph)

### RAG Components

| **Component** | **Function** | **Technology** | **Priority** | **Effort** |
|---------------|--------------|----------------|--------------|------------|
| **📥 Ingestion** | Load documents (CW1 logs, contracts, SOPs, emails) | Azure Data Factory, Logic Apps | **P0** | Medium |
| **✂️ Chunking** | Split documents into 500-token chunks with overlap | LangChain `RecursiveCharacterTextSplitter` | **P0** | Low |
| **🧠 Embeddings** | Generate embeddings (Azure OpenAI `text-embedding-ada-002`) | Azure OpenAI Embeddings API | **P0** | Low |
| **🗄️ Vector Store** | Index embeddings for semantic search | Azure AI Search (hybrid: vector + keyword) | **P0** | Medium |
| **🔍 Retrieval** | Hybrid search (semantic + BM25) → Rerank → Top 5 results | Azure AI Search + Cohere Rerank | **P0** | Medium |

**RAG Data Sources** (Freight Graph):

| **Source** | **Content** | **Update Frequency** | **Q1 2026 Priority** |
|------------|-------------|----------------------|----------------------|
| **CW1 Logs** | Booking history (1 year) | Real-time (event-driven) | **✅ Week 11-12** |
| **Customer Contracts** | Pricing, T&Cs, SLAs | Weekly batch | **✅ Week 13-14** |
| **Rate Repository** | Supplier rates, validity dates | Daily batch | **✅ Q1 2026** |
| **Route Knowledge** | CFS stations, pickup agents | Weekly batch | ✅ Already live (Route Planner MCP) |
| **Master Data** | Shipper, consignee, locations | Real-time | ✅ Already live (Master Data MCP) |
| **EDI Events** | Milestones (departed, arrived) | Real-time | 🚧 Q2 2026 |
| **SOPs / Manuals** | DG handling, customs procedures | Monthly | 🚧 Q2 2026 |

**Key Workflows**:
1. **RAG Retrieval for Quotation Agent**:
   ```
   Customer requests quote → Quotation Agent (query \"rate for Shanghai-LA, 10 CBM\") 
      → RAG Pipeline (semantic search in Rate Repository + Customer Contracts) 
      → Top 5 results (rate cards, customer-specific discounts) 
      → Quotation Agent (calculate final price with margin) → Return quote
   ```

2. **RAG Retrieval for Conversational Agent**:
   ```
   Customer asks \"What documents do I need for DG cargo?\" 
      → Conversational Agent → RAG Pipeline (search SOPs + Manuals) 
      → Top 5 results (DG handling SOP, MSDS requirements) 
      → Conversational Agent (synthesize answer with source citations)
   ```

---

## Implementation Roadmap

### **Phase 1: Trust Foundation (Q1 2026)**
**Goal**: Enhance Hubble v1.5 with trust framework (no multi-agent migration yet)

| **Week** | **Deliverable** | **Agents/Components** | **Success Criteria** |
|----------|----------------|-----------------------|---------------------|
| **1-2** | Confidence scoring engine | All CX Hub agents (Email Analyzer, Order Validation) | 90% of bookings have confidence score |
| **3-4** | Operator feedback UI | Feedback Collection Agent | 80% of operators submit ≥1 feedback/week |
| **5-6** | Learning Agent v1.0 | Learning Agent | Accuracy improves 10% month-over-month |
| **7-8** | Evaluation Agent v1.0 | Evaluation Agent (LLM-as-Judge) | >85% output quality score |
| **9-10** | Enhanced observability | Azure Monitor dashboards | KPI dashboards live for ops team |
| **11-12** | RAG: CW1 Logs indexing | RAG Pipeline (Ingestion, Chunking, Embeddings, Vector Store) | 1 year of CW1 bookings indexed |
| **13-14** | RAG: Customer Contracts | RAG Pipeline | 100+ customer contracts indexed |

**No multi-agent migration in Phase 1** — all enhancements within existing LangChain agent.

---

### **Phase 2: Knowledge Enhancement (Q2 2026)**
**Goal**: Expand RAG coverage, add new domain agents

| **Week** | **Deliverable** | **Agents/Components** | **Success Criteria** |
|----------|----------------|-----------------------|---------------------|
| **15-18** | Master Data Lookup Agent v1.0 | Master Data Integration Agent (enhance with RAG) | 95% master data lookup accuracy |
| **19-22** | Rate & Quote Agent v1.0 | Quotation Agent + Pricing Agent + Rates Integration Agent | 80% automated quote generation |
| **23-26** | Dashboard Agent v1.0 | Dashboard Agent (Shipment Monitoring + Consolidation Monitoring) | 100+ operators using dashboards daily |

**Begin multi-agent migration planning** — LangChain agent → LangGraph orchestrator with specialized agents.

---

### **Phase 3: Multi-Agent CargoX v2.0 (Q3-Q4 2026)**
**Goal**: Full multi-agent platform with 13 domain agents

| **Quarter** | **Deliverable** | **Agents/Components** | **Success Criteria** |
|-------------|----------------|-----------------------|---------------------|
| **Q3 2026** | Multi-agent orchestrator | CargoX Orchestrator (LangGraph) | Event-driven coordination live |
| **Q3 2026** | Domain agent migration | Email Analyzer, Order Validation, Quotation, Rate, Consolidation Planner | 5 core agents migrated |
| **Q4 2026** | Advanced agents | Forecast Agent, Notification Agent, Conversational Agent, Warehouse Agent, Customs Agent | 13 agents in production |
| **Q4 2026** | Production rollout | 100+ operators, 500+ daily intakes, 5 trade lanes | 70% touchless rate, NPS +10 |

---

## Technology Stack Summary

| **Component** | **Technology** | **One Platform Integration** |
|---------------|----------------|------------------------------|
| **Frontend** | React (Vite) | ALP Portal (Chassis UI) |
| **Orchestration** | LangChain → LangGraph | One Platform multi-agent layer |
| **Email Intake** | Outlook/Gmail API | Hubble Email Trans |
| **AI Models** | Azure OpenAI (GPT-4, GPT-3.5-Turbo), Claude, Gemini | Model Selector (AI Monitoring Hub) |
| **RAG** | Azure AI Search + OpenAI Embeddings | Freight Graph Knowledge Layer |
| **Event Bus** | Azure Event Grid or Kafka | Event-driven microservices backbone |
| **Observability** | Azure Monitor + App Insights | AI Monitoring Hub dashboards |
| **Integration** | CargoWise One, SAP, WMS, TMS | Integration Orchestration Hub |
| **Optimization** | Python (PuLP, OR-Tools) | Consolidation Planner (bin-packing) |
| **Data Storage** | Azure SQL, Cosmos DB, Blob Storage | Unified data layer |

---

## Agent-to-Hub Quick Reference

| **CargoX Agent** | **Orchestration Hub** | **Priority** | **Phase** |
|------------------|-----------------------|--------------|-----------|
| Email Analyzer | **CX Hub** | P0 | ✅ Live (Hubble) |
| Order Transformation | **CX Hub** | P0 | ✅ Live (Hubble) |
| Order Validation | **CX Hub** | P0 | ✅ Live (Hubble) |
| Quotation Agent | **CX Hub** | P1 | Q2 2026 |
| Pricing Agent | **CX Hub** | P1 | Q2 2026 |
| Route Planner | **CX Hub** | P0 | ✅ Live (Hubble) |
| Conversational Agent | **CX Hub** | P2 | Q4 2026 |
| Consolidation Planner | **Shipment Hub** | P0 | Q3 2026 (Hackathon) |
| Forecast Agent | **Shipment Hub** | P2 | Q4 2026 |
| Order Visibility | **Visibility Hub** | P1 | Q2 2026 |
| Shipment Visibility | **Visibility Hub** | P1 | Q2 2026 |
| Demand Estimation | **Visibility Hub** | P2 | Q4 2026 |
| Dashboard Agent | **Visibility Hub** | P0 | Q2 2026 |
| Financial Integration | **Integration Hub** | P1 | Q3 2026 |
| Warehouse Integration | **Integration Hub** | P1 | Q3 2026 |
| Master Data Integration | **Integration Hub** | P0 | ✅ Live (Hubble) |
| Rates Integration | **Integration Hub** | P1 | Q2 2026 |
| Customs Agent | **Integration Hub** | P2 | Q4 2026 |
| Feedback Collection | **Operational Hub** | P0 | Q1 2026 |
| Learning Agent | **Operational Hub** (AI Monitoring Hub) | P0 | Q1 2026 |
| Evaluation Agent | **Operational Hub** (AI Monitoring Hub) | P0 | Q1 2026 |
| Exception Handler | **Operational Hub** | P0 | Q1 2026 |
| Notification Agent | **Operational Hub** | P1 | Q2 2026 |

---

## Success Metrics by Hub

### **CX Hub**
- **Adoption**: 100+ operators using AI-assisted booking workflow
- **Process**: 50% automatic booking conversion rate (email → CW1 without manual edits)
- **Performance**: 30% increase in bookings per operator per day
- **Outcome**: CSLS score +5 points, NPS +10

### **Shipment Hub**
- **Adoption**: 30+ consolidations planned by AI weekly
- **Process**: Consolidation planning time reduced from 2 hours to 30 minutes
- **Performance**: 10% margin improvement via optimal bin-packing
- **Outcome**: $500K annual savings from freight cost optimization

### **Visibility Hub**
- **Adoption**: 500+ shipments tracked real-time daily
- **Process**: Milestone updates within 5 minutes of event (warehouse scan, flight departure)
- **Performance**: 90% proactive communication (pre-alerts sent before customer asks)
- **Outcome**: Customer complaints reduced 40%

### **Integration Hub**
- **Adoption**: 100% SAP invoices processed automatically
- **Process**: Invoice generation → email → reply upload within 24 hours (vs 3 days manual)
- **Performance**: 95% invoice accuracy (no manual corrections)
- **Outcome**: Finance team capacity freed 20%

### **Operational Hub**
- **Adoption**: 80% of operators submit feedback weekly
- **Process**: Learning Agent retrains prompts monthly, accuracy improves 5% per quarter
- **Performance**: 90% of agent outputs pass quality gate (>85% accuracy)
- **Outcome**: AI maturity level progresses from Level 2 (Confirm Mode) to Level 4 (Proactive Mode)

---

**Document Version**: 1.0  
**Last Updated**: 2025-01-10  
**Owner**: AI Product Manager, CargoX Initiative  
**Next Review**: Q1 2026 Phase Gate
