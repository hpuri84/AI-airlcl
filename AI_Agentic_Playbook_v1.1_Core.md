# AI Agentic Playbook v1.1 — Core Edition

### CargoX: Intelligent Freight Automation

**Version**: 1.1 Core | **Date**: November 2025 | **Read Time**: 15 minutes  
**Full Version**: See `AI_Agentic_Playbook_v1.1.md` (40-min read, 2,209 lines)

---

## Quick Navigation

**Need a specific answer?**
- **"What is CargoX?"** → [§1 Vision](#1-vision-one-sentence)
- **"How does it work?"** → [§2 Architecture](#2-architecture-3-layers)
- **"Which agents do what?"** → [§3 Agent Portfolio](#3-agent-portfolio-8-core-agents)
- **"How do we build trust?"** → [§4 Trust Framework](#4-trust-framework-4-stages)
- **"What's the learning loop?"** → [§5 Continuous Learning](#5-continuous-learning-3-steps)
- **"What's the ROI?"** → [§6 Success Metrics](#6-success-metrics--roi)
- **"What's the timeline?"** → [§7 Rollout Plan](#7-rollout-plan-26-weeks)
- **"What could go wrong?"** → [§8 Risk Mitigation](#8-risk-mitigation)

---

## 1. Vision (One Sentence)

**CargoX transforms freight operations from manual 4-hour booking cycles (88% accuracy) to intelligent 15-minute automated workflows (95% accuracy) via multi-agent AI with continuous learning.**

### Core Principles (Implementation Checklist)

| Principle | Key Controls |
|-----------|--------------|
| **Transparency** | ✅ Confidence scores (High/Medium/Low) on every output<br>✅ Source citations for every claim<br>✅ "How I decided" reasoning traces |
| **Human-in-the-Loop** | ✅ Approval gates by risk: Low = auto, Medium = confirm, High = review<br>✅ Override controls (edit AI output before execution)<br>✅ Escalation triggers (confidence <70%, DG cargo, >$50k) |
| **Continuous Learning** | ✅ 👍👎 feedback + corrections captured<br>✅ Learning Agent analyzes weekly → proposes improvements<br>✅ A/B testing before deployment<br>✅ Visible loop ("Your correction improved shipper matching by 12%") |
| **Governance** | ✅ PII detection & redaction<br>✅ Financial gates (>$50k = human approval)<br>✅ DG specialist approval for hazardous cargo<br>✅ 7-year audit logs (regulatory compliance) |

---

## 2. Architecture (3 Layers)

```
┌─────────────────────────────────────────────────────────┐
│  Layer 1: User Interfaces                               │
│  • Email, Web App, Teams/Slack, Mobile, Voice, API     │
└───────────────────────┬─────────────────────────────────┘
                        ↓
┌─────────────────────────────────────────────────────────┐
│  Layer 2: CargoX Orchestrator + Domain Agents          │
│  ┌───────────────────────────────────────────────────┐ │
│  │ 📧 Email Analyzer  → ✅ Booking Validator         │ │
│  │ 💰 Rate Agent      → 📦 Quotation Agent           │ │
│  │ 🚚 Consol Planner  → 🧾 Invoice Validator         │ │
│  │ 🎓 Learning Agent  → ⚖️ Evaluation Agent          │ │
│  │ 🔧 Master Data     → 📞 Exception Handler         │ │
│  └───────────────────────────────────────────────────┘ │
│  Event Bus: order.received, booking.validated, etc.    │
└───────────────────────┬─────────────────────────────────┘
                        ↓
┌─────────────────────────────────────────────────────────┐
│  Layer 3: Integration + Knowledge                       │
│  • CargoWise One (CW1) — operational system             │
│  • Freight Graph (RAG) — CW1 logs, contracts, rates,   │
│    SOPs, master data (grounded knowledge base)          │
└─────────────────────────────────────────────────────────┘
```

**Key Design Decisions**:
1. **Event-Driven**: Agents communicate via events (decoupled, scalable)
2. **RAG-Powered**: Every decision grounded in CW1 data, contracts, SOPs (no hallucinations)
3. **Human-in-the-Loop**: Approval gates at every risk threshold (Low/Medium/High)
4. **Specialized Agents**: 8+ domain experts vs 1 monolithic AI (debuggable, evolvable)

---

## 3. Agent Portfolio (8 Core Agents)

### Operational Agents (Customer-Facing)

| Agent | Input | Output | Automation Level | Business Impact |
|-------|-------|--------|-----------------|----------------|
| **📧 Email Analyzer** | Email + attachments (PDF, Excel, Word) | Structured booking data (origin, dest, cargo, shipper) | 🟢 92% touchless | Eliminate 4-hour manual data entry |
| **✅ Booking Validator** | Parsed booking data | Validation result (pass/fail + confidence) | 🟢 94% touchless | Reduce errors from 12% → 3% |
| **💰 Rate Agent** | Origin, destination, CBM, weight | Rate quote (buy rate, sell rate, margin) | 🟢 99% touchless | Optimize margin +3% avg |
| **📦 Quotation Agent** | Validated booking + rate | PDF quote + email draft | 🟠 78% touchless | Reduce quote time 4 hours → 15 min |
| **🚚 Consol Planner** | All validated bookings | Consol plan (grouped bookings, optimized CBM) | 🟠 82% touchless | Increase utilization 70% → 85% |
| **🧾 Invoice Validator** | Quote vs actual shipment | Discrepancy report | 🟢 96% touchless | Reduce invoice errors 12% → 1% |

### Infrastructure Agents (Behind-the-Scenes)

| Agent | Purpose | Runs When | Output |
|-------|---------|-----------|--------|
| **🎓 Learning Agent** | Analyze operator corrections → propose improvements | Weekly batch | Improvement proposals (+5% accuracy/quarter target) |
| **⚖️ Evaluation Agent** | Score agent quality (LLM-as-Judge) | Real-time + pre-deployment | Quality scores (block if <85% accuracy) |

**Legend**: 🟢 High confidence (>85% touchless) | 🟠 Medium (70-85%, human confirms)

---

## 4. Trust Framework (4 Stages)

Operators progress through stages as trust builds:

### Stage 1: Shadow Mode (Week 1-4)
**Agent Behavior**: Suggests, never executes  
**Human Role**: Reviews 100%, always executes manually  
**Goal**: Learn patterns, build familiarity  
**Success**: 50+ interactions, UMUX-Lite >65

### Stage 2: Confirm Mode (Week 5-12)
**Agent Behavior**: Executes after human approval  
**Human Role**: Approves/edits before execution  
**Goal**: Reduce operator workload by 30%  
**Success**: Approval rate >80%, touchless >30%, UMUX-Lite >75

### Stage 3: Autonomous Mode (Week 13-20)
**Agent Behavior**: Executes for high-confidence cases (>90%)  
**Human Role**: Monitors exceptions only  
**Goal**: 50% touchless rate  
**Success**: Accuracy >90%, escalation <25%

### Stage 4: Proactive Mode (Week 21+)
**Agent Behavior**: Initiates conversations ("Should we consolidate these 5 bookings?")  
**Human Role**: Partners with agent on optimization  
**Goal**: 70% touchless rate, proactive optimization  
**Success**: UMUX-Lite >80, BUS-11 >80

**Rollback Safety**: If accuracy drops >10% at any stage → Auto-revert to previous stage + alert on-call team

---

## 5. Continuous Learning (3 Steps)

### Step 1: Feedback Capture (Real-Time)

**Scenario**: Booking Validator returns incorrect shipper match.

**Operator Action**:
1. Click "Incorrect match" next to suggested shipper
2. Select correct shipper from dropdown
3. Add comment: "Use full legal name, not trade name"
4. Submit feedback

**System**: Logs feedback with context (query, retrieved docs, agent's answer, correct answer)

---

### Step 2: Pattern Recognition (Weekly Batch)

**Learning Agent** (runs weekly):
1. Aggregate all corrections for each agent
2. Identify patterns: "50% of shipper mismatches due to trade name vs legal name"
3. Generate improvement hypothesis: "Always search by legal name first, then trade name"
4. Create updated prompt/retrieval strategy
5. Flag for Evaluation Agent A/B test

---

### Step 3: Validation & Deployment (1-2 Weeks)

**Evaluation Agent**:
1. Run A/B test:
   - Control: Current prompt (100 test cases)
   - Treatment: New prompt (100 test cases)
2. Measure improvement:
   - Grounding@K: +8% (92% → 100%)
   - Operator approval rate: +12% (78% → 90%)
3. **Decision**: If improvement >5% AND statistically significant (p<0.05) → Deploy to production
4. Monitor for 2 weeks → If regression detected → Rollback

**Visible Feedback Loop** (Operator sees):
- Immediate: "Thanks for your feedback! We're analyzing patterns to improve."
- 1 week later: "Your correction helped improve shipper matching by 12%. Keep it coming!"

---

## 6. Success Metrics & ROI

### North Star Metrics (Year 1 Targets)

| Metric | Baseline (Pre-AI) | Target (Year 1) | Current (Q3) | Trend |
|--------|------------------|----------------|--------------|-------|
| **Touchless Rate** | 0% | 70% | 42% | ↗️ On track |
| **Booking Accuracy** | 88% (manual) | 95% | 94% | ↗️ On track |
| **Time to Quote** | 4 hours | 15 minutes | 28 minutes | ↗️ On track |
| **Invoice Error Rate** | 12% | 3% | 5% | ↗️ On track |
| **Operator Satisfaction** (UMUX-Lite) | N/A | 80 | 73 | ⚠️ Behind |
| **Cost Savings** (annualized) | $0 | $2M | $1.2M | ↗️ On track |

### ROI Calculation

| Value Driver | Annual Benefit | Calculation |
|--------------|---------------|-------------|
| **Operator Time Saved** | $1.95M | 1,050 hours/week × $25/hour × 52 weeks × 70% touchless |
| **Error Reduction** | $400k | 12% → 3% error rate × $500k current cost |
| **Revenue Retention** | $800k | 15% deal loss → 5% × $1M lost deals |
| **Capacity Optimization** | $300k | 70% → 85% utilization × $2M capacity cost |
| **Total Annual Value** | **$3.45M** | |
| **Investment (Year 1)** | **$500k** | Development, infrastructure, training, pilot |
| **Net Benefit** | **$2.95M** | $3.45M - $500k |
| **ROI** | **490%** | ($2.95M / $500k) × 100 |
| **Payback Period** | **2 months** | $500k / ($3.45M / 12) |

**Year 2+**: Operating cost $150k/year, Annual benefit $3.45M → **2,200% ROI**

---

## 7. Rollout Plan (26 Weeks)

### Phase 1: Foundation (Weeks 1-4) — $0 Budget
**Deliverables**: Policy framework, metrics library (UMUX-Lite, BUS-11, accuracy), UI component library (confidence badges, approval buttons), event schemas  
**Exit Criteria**: Policies approved by Legal + Leadership

### Phase 2: Email Intake MVP (Weeks 5-8) — $50k
**Deliverables**: Email Analyzer agent, Booking Validator agent, approval dashboard, exception queue  
**Success Metrics**: 85% extraction accuracy, UMUX-Lite >70  
**Rollback**: If accuracy <70% → Disable auto-validation, revert to manual

### Phase 3: Learning Loop & Scale (Weeks 9-12) — $75k
**Deliverables**: Learning Agent, Evaluation Agent, orchestrator enhancements, scale to 200 emails/week  
**Success Metrics**: 30% touchless, escalation <35%, UMUX-Lite >75

### Phase 4: Advanced Capabilities (Weeks 13-16) — $150k
**Deliverables**: Rate Agent, Quotation Agent, CW1 sync, end-to-end flow (email → booking → quote)  
**Success Metrics**: 500 emails/week, 50% touchless, accuracy >92%

### Phase 5: Full Autonomy & Expansion (Weeks 17-26) — $225k
**Deliverables**: Autonomous mode (>90% confidence auto-execute), proactive agents, voice agent, regional expansion  
**Success Metrics**: 70% touchless globally, UMUX-Lite >80, BUS-11 >80

**Total Year 1 Budget**: $500k

**Phase Gates** (Go/No-Go Decision):
- **Week 4**: Foundation complete → Proceed to Email Intake MVP?
- **Week 8**: Shadow mode success (>85% accuracy, UMUX >70) → Proceed to Confirm Mode?
- **Week 12**: Confirm mode success (30% touchless, UMUX >75) → Proceed to Advanced Capabilities?
- **Week 16**: 50% touchless achieved → Proceed to Full Autonomy?
- **Week 26**: 70% touchless achieved → Declare production ready, expand globally

---

## 8. Risk Mitigation

| Risk | Impact | Mitigation | Owner |
|------|--------|------------|-------|
| **Operator Resistance** | Medium | Shadow mode first (no forced adoption), training workshops, feedback loops | Change Mgmt Lead |
| **Accuracy Below Target** | High | Evaluation Agent gates deployment (>85% required), A/B testing, rollback capability | Data Science Lead |
| **Data Privacy Violation** | High | PII auto-redaction, access control by role, quarterly audits | Compliance Officer |
| **CW1 Integration Failure** | High | Event bus with retry logic, fallback to manual mode, 24/7 monitoring | Integration Engineer |
| **Cost Overrun (Azure OpenAI)** | Medium | Prompt optimization (20-30% savings), caching (40-50% savings), smaller models for simple tasks | Engineering Lead |
| **Regulatory Non-Compliance** | High | 7-year audit logs (immutable), monthly compliance reports, pre-deployment policy checks | Legal + Compliance |

---

## Key Takeaways (TL;DR)

### What is CargoX?
Multi-agent AI system that automates freight workflows (email → booking → quote → consol → invoice) with continuous learning and human oversight.

### Why Multi-Agent?
**Specialized agents** (Email Analyzer, Rate Agent, etc.) are debuggable, evolvable, and scalable vs single monolithic AI.

### How to Build Trust?
**4-stage progression** (Shadow → Confirm → Autonomous → Proactive) + **transparency** (confidence scores, source citations, reasoning traces).

### How to Improve?
**Learning loop**: Operator corrections → Learning Agent identifies patterns → Evaluation Agent A/B tests → Deploy if >5% improvement.

### What's the ROI?
**$500k investment → $3.45M annual value → 490% ROI, 2-month payback**.

### What's the Timeline?
**26 weeks (6 months) to full autonomy**: Foundation (4 weeks) → Email MVP (4 weeks) → Learning Loop (4 weeks) → Advanced (4 weeks) → Autonomy (10 weeks).

### What Could Go Wrong?
**Top 3 risks**: Accuracy below target (mitigate: Evaluation Agent gates), operator resistance (mitigate: Shadow mode first), CW1 integration failure (mitigate: fallback to manual).

---

## Next Steps

### Week 1 (Immediately)
1. **Executive approval** on budget ($500k) + resources (4-5 FTEs)
2. **Kickoff meeting** with core team (AI Lead, Solution Architect, Product Owner)
3. **Legal + Compliance review** of governance policies

### Week 2-4
4. Finalize architecture, event schemas, agent personas
5. Build UI component library (confidence badges, approval buttons)
6. Recruit 10 early-adopter operators for pilot

### Week 5 Onward
7. Begin Phase 2: Email Intake MVP in Shadow Mode
8. Monthly steering committee reviews progress

---

## Document Family

| Document | Purpose | Read Time | Best For |
|----------|---------|-----------|----------|
| **This (Core v1.1)** | Quick reference, architecture overview | 15 min | Tech leads, architects, product managers |
| **Full v1.1** | Detailed implementation guide (2,209 lines) | 40 min | Builders, data scientists, engineers |
| **Executive Summary** | Business case, ROI, decision points | 8 min | Executives, budget approvers, steering committee |
| **v1.2 (Hubble)** | Production roadmap for Hubble v1.5 → CargoX v2.0 | 30 min | GCA LCL team, 2026 planning |
| **Integration Analysis** | Hubble gap analysis, technical enhancements | 20 min | Architects comparing AS-IS vs TO-BE |

---

**Document Metadata**:
- **Version**: 1.1 Core
- **Date**: November 2025
- **Authors**: AI Architecture Team
- **Status**: Reference Playbook (Technology-Agnostic)
- **Full Version**: `AI_Agentic_Playbook_v1.1.md` (2,209 lines)
- **Feedback**: cargox-feedback@maersk.com
