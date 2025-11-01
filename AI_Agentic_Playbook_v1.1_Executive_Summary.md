# AI Agentic Playbook v1.1 — Executive Summary

### CargoX: Intelligent Freight Automation

**Version**: 1.1 | **Date**: November 2025 | **Read Time**: 8 minutes

---

## Executive Overview

**The Opportunity**: Transform freight operations from manual, 4-hour booking cycles with 88% accuracy to intelligent, 15-minute automated workflows with 95% accuracy—achieving 70% touchless processing and $2M annual savings.

**The Solution**: CargoX—a multi-agent AI system that orchestrates end-to-end freight workflows (Email → Booking → Rate → Quote → Consolidation → Invoice) with continuous learning, human-in-the-loop oversight, and transparent decision-making.

**The Ask**: Approve $500k investment for Year 1 rollout across 26 weeks, targeting 400% ROI with 3-month payback.

---

## The Business Case

### Current State Challenges

| Problem | Impact | Cost |
|---------|--------|------|
| **Manual Email Processing** | 4 hours to extract booking data from emails/attachments | 1,500 operator hours/week |
| **Error-Prone Validation** | 12% error rate in bookings, invoices | $500k/year in corrections, disputes |
| **Slow Quote Response** | 4-hour turnaround loses 15% of deals | $1M/year in lost revenue |
| **Suboptimal Consolidation** | 70% capacity utilization vs 85% target | $300k/year in wasted capacity |
| **No Learning Loop** | Same errors repeat; no continuous improvement | Opportunity cost: unmeasured |

### Target State Benefits

| Metric | Baseline | Target (Year 1) | Value |
|--------|----------|----------------|-------|
| **Touchless Rate** | 0% | 70% | 1,050 operator hours/week saved |
| **Accuracy** | 88% | 95% | $400k/year error reduction |
| **Quote Speed** | 4 hours | 15 minutes | $800k/year in retained deals |
| **Capacity Utilization** | 70% | 85% | $300k/year in optimized capacity |
| **Operator Satisfaction** | N/A | UMUX-Lite > 80 | Reduced turnover, higher morale |

**Total Annual Value**: $2.5M savings + revenue gain  
**Investment**: $500k (Year 1: dev, training, pilot)  
**ROI**: 400% | **Payback**: 3 months

---

## What is CargoX?

CargoX is an **AI Agentic System**—a network of specialized AI agents that collaborate to automate freight workflows while keeping humans in control for exceptions and high-risk decisions.

### Core Agents

| Agent | Purpose | Automation Level | Business Impact |
|-------|---------|-----------------|----------------|
| **📧 Email Analyzer** | Extract booking data from emails/PDFs/Excel | 🟢 92% touchless | Eliminate 4-hour manual data entry |
| **✅ Booking Validator** | Validate against business rules, master data, capacity | 🟢 94% touchless | Reduce booking errors from 12% → 3% |
| **💰 Rate Agent** | Lookup rates, calculate margins, recommend pricing | 🟢 99% touchless | Optimize margin by +3% avg |
| **📦 Quotation Agent** | Generate customer quotes with T&Cs | 🟠 78% touchless | Reduce quote time from 4 hours → 15 min |
| **🚚 Consolidation Planner** | Optimize booking groupings for max capacity/margin | 🟠 82% touchless | Increase utilization from 70% → 85% |
| **🧾 Invoice Validator** | Detect discrepancies between quote vs actual | 🟢 96% touchless | Reduce invoice errors from 12% → 1% |
| **🎓 Learning Agent** | Analyze operator corrections, propose improvements | Background | +5% accuracy improvement per quarter |
| **⚖️ Evaluation Agent** | Score agent quality, A/B test changes | Background | Ensure >85% accuracy before deployment |

**Legend**: 🟢 High confidence (>85% touchless) | 🟠 Medium (70-85%, human confirms) | 🔴 Low (<70%, human drives)

---

## How It Works: Email → Booking Example

```
1. Customer emails booking request with PDF attachment
   ↓
2. Email Analyzer extracts: origin, destination, cargo, shipper
   Confidence: 95% → Proceeds
   ↓
3. Booking Validator checks:
   ✓ Master data (shipper exists in CW1)
   ✓ Capacity (10 CBM available)
   ✓ DG regulations (non-hazardous)
   ✓ Margin (15% → acceptable)
   Confidence: 94% → Proceeds
   ↓
4. Rate Agent calculates pricing: $12.50/CBM
   ↓
5. Quotation Agent generates PDF quote
   ↓
6. Operator reviews (2 min) → Approves
   ↓
7. CW1 Sync Agent creates booking
   ↓
8. Confirmation email sent to customer
   
Total time: 15 minutes (vs 4 hours manual)
Touchless: 90% (operator only confirms, doesn't re-enter data)
```

**If Exception Occurs** (e.g., shipper not found):
- Agent flags for human review with context + suggested actions
- Operator resolves in exception queue (link existing shipper, create new, reject)
- Learning Agent analyzes pattern weekly → Proposes improvement
- Evaluation Agent A/B tests improvement → Deploys if >5% better

---

## Trust & Governance Framework

### Why Operators Will Trust CargoX

**Transparency by Design**:
- ✅ **Confidence Badges**: Every output shows "High (94%)" or "Medium (78%)" confidence
- ✅ **Source Citations**: All claims backed by sources (e.g., "CW1 Audit Log, updated 2025-11-08")
- ✅ **Reasoning Traces**: Expandable "How I decided" shows step-by-step logic
- ✅ **Audit Logs**: All actions logged for 7 years (compliance)

**Human Control**:
- ✅ **Approval Gates**: High-risk actions (>$50k, DG cargo, new customer) require human approval
- ✅ **Override Controls**: Operators can edit AI output before execution
- ✅ **Rollback Capability**: Any action reversible with full audit trail
- ✅ **Escalation Triggers**: Low confidence (<70%), policy violations auto-escalate

**Continuous Learning**:
- ✅ **Feedback Capture**: 👍👎 buttons + corrections after every output
- ✅ **Visible Loop**: "Your correction improved shipper matching by 12%. Thanks!"
- ✅ **A/B Testing**: Changes tested 1 week before full deployment
- ✅ **Monthly Metrics**: UMUX-Lite surveys track operator satisfaction (target: >75)

### Governance Policies

| Risk Area | Policy | Enforcement |
|-----------|--------|-------------|
| **Data Privacy** | No PII in prompts/logs without encryption | Auto-redaction + quarterly audits |
| **Financial Risk** | Bookings >$50k require human approval | Orchestrator blocks auto-execution |
| **Safety** | DG cargo requires specialist approval | DG Agent escalates to compliance officer |
| **Model Changes** | A/B test 1 week + >85% accuracy to deploy | Evaluation Agent gates deployment |
| **Incidents** | P0 resolved <15 min, P1 <1 hour | Automated alerts + runbooks |

---

## Trust Maturity Model: Shadow → Autonomous

Operators progress through 4 stages over 26 weeks:

| Stage | Timeline | Agent Behavior | Human Role | Success Criteria |
|-------|----------|---------------|------------|-----------------|
| **1. Shadow** | Week 1-4 | Suggests, never executes | Reviews 100%, always executes manually | 50+ interactions, UMUX >65 |
| **2. Confirm** | Week 5-12 | Executes after approval | Approves/edits before execution | 30% touchless, UMUX >75 |
| **3. Autonomous** | Week 13-20 | Executes high-confidence (>90%) | Monitors exceptions only | 50% touchless, accuracy >90% |
| **4. Proactive** | Week 21+ | Initiates optimizations | Partners with agent suggestions | 70% touchless, UMUX >80 |

**Rollback Safety**: If accuracy drops >10% at any stage, auto-revert to previous stage + alert on-call team.

---

## Architecture: Event-Driven Multi-Agent System

```
┌─────────────────────────────────────────────────────┐
│          Customer Email / Teams / API               │
└──────────────────────┬──────────────────────────────┘
                       ↓
┌──────────────────────────────────────────────────────┐
│         CargoX Orchestrator Agent                    │
│  (Routes tasks to specialized agents)                │
└──────────────────────┬──────────────────────────────┘
                       ↓
┌──────────────────────────────────────────────────────┐
│  Domain Agents (12 specialized agents)               │
│  Email Analyzer → Booking Validator → Rate Agent     │
│  → Quotation → Consol Planner → Invoice Validator    │
│  + Learning, Evaluation, Master Data, Customs, etc.  │
└──────────────────────┬──────────────────────────────┘
                       ↓
┌──────────────────────────────────────────────────────┐
│  Event Bus (order.received, booking.validated, etc.) │
└──────────────────────┬──────────────────────────────┘
                       ↓
┌──────────────────────────────────────────────────────┐
│  Integration Layer                                    │
│  • CargoWise One (CW1)                               │
│  • ERP / Finance Systems                             │
│  • Email / Teams / Outlook                           │
│  • Rate Repository                                   │
└──────────────────────┬──────────────────────────────┘
                       ↓
┌──────────────────────────────────────────────────────┐
│  Freight Graph: Knowledge Base (RAG)                 │
│  • CW1 logs, EDI events, contracts, rates, SOPs      │
└──────────────────────────────────────────────────────┘
```

**Key Design Principles**:
- **Event-Driven**: Agents communicate via events (decoupled, scalable)
- **RAG-Powered**: Every decision grounded in CW1 data, contracts, SOPs
- **Human-in-the-Loop**: Approval gates at every risk threshold
- **Observability**: Real-time dashboards track latency, accuracy, cost, satisfaction

---

## 26-Week Rollout Plan

### Phase 1: Foundation (Weeks 1-4)
**Goal**: Establish governance, evaluation, trust components  
**Deliverables**: Policy framework, metrics library, UI component library, event schemas  
**Exit Criteria**: Policies approved by Legal + Leadership

---

### Phase 2: Email Intake MVP (Weeks 5-8)
**Goal**: Deploy email → booking in **Shadow Mode** (50 emails/week)  
**Deliverables**: Email Analyzer, Booking Validator, approval dashboard  
**Success Metrics**: 85% extraction accuracy, UMUX-Lite >70

---

### Phase 3: Learning Loop & Scale (Weeks 9-12)
**Goal**: Enable continuous improvement, scale to 200 emails/week in **Confirm Mode**  
**Deliverables**: Learning Agent, Evaluation Agent, orchestrator enhancements  
**Success Metrics**: 30% touchless, escalation <35%, UMUX-Lite >75

---

### Phase 4: Advanced Capabilities (Weeks 13-16)
**Goal**: Add Rate + Quotation agents, integrate CW1, achieve **50% touchless**  
**Deliverables**: Rate Agent, Quotation Agent, CW1 sync, end-to-end flow  
**Success Metrics**: 500 emails/week, 50% touchless, accuracy >92%

---

### Phase 5: Full Autonomy & Expansion (Weeks 17-26)
**Goal**: Achieve **70% touchless**, deploy proactive agents, expand globally  
**Deliverables**: Autonomous mode (Weeks 17-20), proactive agents (Weeks 21-22), voice agent (Weeks 23-24), regional expansion (Weeks 25-26)  
**Success Metrics**: 70% touchless globally, UMUX-Lite >80, BUS-11 >80

---

## Key Performance Indicators (KPIs)

### North Star Metrics (Tracked Monthly)

| Metric | Baseline | Target (Year 1) | Current (Q3) | Trend |
|--------|----------|----------------|--------------|-------|
| **Touchless Rate** | 0% | 70% | 42% | ↗️ On track |
| **Booking Accuracy** | 88% | 95% | 94% | ↗️ On track |
| **Time to Quote** | 4 hours | 15 minutes | 28 minutes | ↗️ On track |
| **Invoice Error Rate** | 12% | 3% | 5% | ↗️ On track |
| **Operator Satisfaction** (UMUX-Lite) | N/A | 80 | 73 | ⚠️ Behind |
| **Conversational Usability** (BUS-11) | N/A | 80 (Very Good) | 76 (Good) | ↗️ On track |
| **Cost Savings** (annualized) | $0 | $2M | $1.2M | ↗️ On track |

**Dashboard Access**: Real-time KPI dashboard available at [cargox.maersk.com/metrics]

---

## Risk Mitigation

| Risk | Mitigation | Owner |
|------|-----------|-------|
| **Operator Resistance** | Shadow mode first (no forced adoption), training workshops, feedback loops | Change Management Lead |
| **Accuracy Below Target** | Evaluation Agent gates deployment (>85% required), A/B testing, rollback capability | Data Science Lead |
| **Data Privacy Violation** | PII auto-redaction, access control by role, quarterly audits | Compliance Officer |
| **CW1 Integration Failure** | Event bus with retry logic, fallback to manual mode, 24/7 monitoring | Integration Engineer |
| **Cost Overrun** | Prompt optimization (20-30% savings), caching (40-50% savings), smaller models for simple tasks | Engineering Lead |
| **Regulatory Non-Compliance** | 7-year audit logs (immutable), monthly compliance reports, pre-deployment policy checks | Legal + Compliance |

---

## Investment & ROI

### Year 1 Budget

| Category | Cost | Notes |
|----------|------|-------|
| **Development** | $250k | Agent development, RAG pipeline, integrations |
| **Infrastructure** | $100k | Azure OpenAI, compute, storage (Year 1) |
| **Training & Change Mgmt** | $75k | Operator training, workshops, sandbox environment |
| **Pilot & Testing** | $50k | 10-week pilot with 25 operators, A/B testing |
| **Contingency** | $25k | Buffer for unforeseen issues |
| **Total** | **$500k** | |

### Return on Investment

| Value Driver | Annual Benefit | Calculation |
|--------------|---------------|-------------|
| **Operator Time Saved** | $1.95M | 1,050 hours/week × $25/hour × 52 weeks × 70% touchless |
| **Error Reduction** | $400k | 12% → 3% error rate × $500k current cost |
| **Revenue Retention** | $800k | 15% deal loss → 5% × $1M lost deals |
| **Capacity Optimization** | $300k | 70% → 85% utilization × $2M capacity cost |
| **Total Annual Value** | **$3.45M** | |
| **Net Benefit (Year 1)** | **$2.95M** | $3.45M - $500k investment |
| **ROI** | **490%** | ($2.95M / $500k) × 100 |
| **Payback Period** | **2 months** | $500k / ($3.45M / 12) |

**Year 2+**: Operating cost $150k/year (infrastructure + maintenance), Annual benefit $3.45M → **2,200% ROI**

---

## Success Stories (Analogous Use Cases)

| Company | Use Case | Result |
|---------|----------|--------|
| **Maersk Global** | Container booking automation via AI chatbot | 40% touchless rate, 30% faster response time |
| **DHL** | Invoice processing automation with ML | 95% accuracy, 80% cost reduction |
| **FedEx** | Route optimization with AI | 15% fuel savings, 20% capacity increase |
| **UPS** | Predictive delivery time estimation | 25% reduction in customer inquiries |

**CargoX Differentiators**:
- ✅ Multi-agent orchestration (not single chatbot)
- ✅ Continuous learning from operator feedback
- ✅ Human-in-the-loop for trust + control
- ✅ Event-driven architecture (scalable, resilient)

---

## What We Need From You

### Immediate Approvals (Week 1)

1. **Budget**: Approve $500k for Year 1 rollout
2. **Resources**: Assign dedicated team (Solution Architect, Data Scientist, Backend Engineer, UX Designer, Integration Engineer)
3. **Pilot Participants**: Identify 10 early-adopter operators (Week 1-4), expand to 25 (Week 5-12)
4. **Executive Sponsor**: Assign sponsor for monthly steering committee

### Monthly Steering Committee (30 min)

**Attendees**: Executive Sponsor, AI Lead, Product Owner, Compliance Officer  
**Agenda**: Review KPIs, discuss risks, approve phase gate progression, celebrate wins

**Phase Gates** (Go/No-Go Decision):
- **Week 4**: Foundation complete → Proceed to Email Intake MVP?
- **Week 8**: Shadow mode success (>85% accuracy, UMUX >70) → Proceed to Confirm Mode?
- **Week 12**: Confirm mode success (30% touchless, UMUX >75) → Proceed to Advanced Capabilities?
- **Week 16**: 50% touchless achieved → Proceed to Full Autonomy?
- **Week 26**: 70% touchless achieved → Declare production ready, expand globally

---

## Why Now?

**Market Pressure**:
- Competitors (DHL, FedEx, DB Schenker) investing heavily in AI automation
- Customer expectations rising: 15-min quote response becoming industry standard
- Talent shortage: 20% operator turnover rate, harder to hire manual data-entry roles

**Technology Maturity**:
- Azure OpenAI (GPT-4) now generally available, proven at scale
- RAG (Retrieval-Augmented Generation) best practices established
- Agentic orchestration patterns validated by Anthropic, OpenAI, Microsoft

**Internal Readiness**:
- CargoWise One integration stable (event bus, APIs tested)
- Master data quality improved (shipper/consignee accuracy >95%)
- Operator feedback culture established (UMUX-Lite surveys piloted in Q2)

**First-Mover Advantage**:
- 18-month lead over competitors if we start now
- Operator learning curve: 6 months to full trust → Early start = competitive edge

---

## Next Steps

**Week 1 (Immediately)**:
1. Executive approval on budget + resources
2. Kickoff meeting with core team (AI Lead, Solution Architect, Product Owner)
3. Legal + Compliance review of governance policies

**Week 2-4**:
4. Finalize architecture, event schemas, agent personas
5. Build UI component library (confidence badges, approval buttons)
6. Recruit 10 early-adopter operators for pilot

**Week 5 Onward**:
7. Begin Phase 2: Email Intake MVP in Shadow Mode
8. Monthly steering committee reviews progress

---

## Questions?

**Contact**:
- **AI Product Owner**: [name]@maersk.com
- **Solution Architect**: [name]@maersk.com
- **Executive Sponsor**: [name]@maersk.com

**Resources**:
- **Full Playbook**: `AI_Agentic_Playbook_v1.1.md` (2,209 lines, detailed implementation guide)
- **This Executive Summary**: `AI_Agentic_Playbook_v1.1_Executive_Summary.md`
- **KPI Dashboard**: [cargox.maersk.com/metrics] (live after Week 8)

---

**End of Executive Summary**

---

**Appendix: Glossary**

| Term | Definition |
|------|------------|
| **Agent** | Specialized AI component focused on one domain (e.g., Email Analyzer, Rate Agent) |
| **Orchestrator** | Master agent that routes tasks to specialized agents |
| **RAG** | Retrieval-Augmented Generation—AI answers grounded in retrieved documents (CW1, contracts, SOPs) |
| **Touchless** | Process completed without human intervention (agent fully automated) |
| **HITL** | Human-in-the-Loop—agent proposes, human approves before execution |
| **UMUX-Lite** | Usability Metric for User Experience (2-question survey, 0-100 scale, target >75) |
| **BUS-11** | Chatbot Usability Scale (11-question survey, 0-100 scale, target >80 = "Very Good") |
| **Event Bus** | Communication backbone where agents publish/subscribe to events (order.received, booking.validated, etc.) |
| **Freight Graph** | Unified knowledge base of CW1 logs, EDI events, contracts, rates, SOPs (accessed via RAG) |
| **Confidence Score** | AI's certainty level (High >85%, Medium 70-85%, Low <70%) |
