# CLAUDE.md - AI Assistant Guide for AI-AIRLCL Repository

**Version**: 1.0 | **Date**: January 2026 | **Purpose**: Guide AI assistants working on the CargoX AI Agentic Initiative

**Read Time**: ~10 minutes

---

## 🎯 Repository Overview

### What This Repository Is

This is a **documentation-centric repository** for the **CargoX AI Agentic Initiative** at Maersk, focused on automating Air & LCL (Less than Container Load) freight operations using a multi-agent AI architecture. The repository contains strategic playbooks, architectural blueprints, feature mappings, and integration analyses for a 13-agent system designed to achieve touchless freight processing.

**Primary Purpose**: Single source of truth for CargoX architecture, agent design, and 2026 phased rollout strategy.

**Not a Code Repository**: This repo contains documentation and reference materials only. Implementation code lives in separate repositories.

### Key Success Metrics (2026 Target)
- **80% touchless rate** for Air & LCL bookings (up from 10% baseline)
- **90% booking accuracy** with automated validation
- **95% quote generation speed** improvement (minutes vs. hours)
- **400% ROI** with 3-month payback period
- **100+ operator adoption** across 3 global hubs

---

## 📁 Repository Structure

```
/home/user/AI-airlcl/
├── Core Documentation (Root Level - 9 markdown files)
│   ├── AI_Agentic_Playbook_v1.2.md              [LATEST] Production roadmap with Hubble v1.5 baseline
│   ├── AI_Agentic_Playbook_v1.1.md              Comprehensive blueprint (all 13 agents)
│   ├── AI_Agentic_Playbook_v1.1_Core.md         15-min executive brief
│   ├── AI_Agentic_Playbook_v1.1_Executive_Summary.md  Business case & ROI
│   ├── Feature_to_Agent_Mapping.md              98 features → 13 agents mapping
│   ├── CargoX_Agent_to_Orchestration_Hub_Mapping.md  Platform architecture alignment
│   ├── CargoX_Value_Map.md                      Deliverable-to-outcome framework
│   ├── Hubble_CargoX_Integration_Analysis.md    Gap analysis & migration strategy
│   └── # AI Agentic Playbook v1.md              Initial iteration (historical)
│
├── asset/                                        Supporting materials (17 files)
│   ├── PDFs (12)     Research, architecture specs, evaluation frameworks
│   ├── Excel (3)     Roadmaps, DILO notes, request tracking
│   ├── PowerPoint (1) Operational excellence documentation
│   └── Diagrams (2)   Architecture visualizations (SVG/PNG)
│
├── .git/             Version control metadata
└── CLAUDE.md         This file - AI assistant guide
```

**Total Size**: 34 MB (primarily asset PDFs)
**Total Documentation**: 5,874+ lines of markdown across 9 documents

---

## 📚 Document Hierarchy & Navigation

### Which Document to Read When

| Your Goal | Start Here | Why |
|-----------|-----------|-----|
| **Get latest production context** | `AI_Agentic_Playbook_v1.2.md` | Includes Hubble v1.5 baseline, gap analysis, 2026 roadmap |
| **Understand agent architecture** | `AI_Agentic_Playbook_v1.1.md` | Comprehensive 2,209-line blueprint with all 13 agents |
| **Quick 15-min overview** | `AI_Agentic_Playbook_v1.1_Core.md` | Executive summary with core concepts |
| **Business case & ROI** | `AI_Agentic_Playbook_v1.1_Executive_Summary.md` | Problem statement, benefits, metrics |
| **Implementation planning** | `Feature_to_Agent_Mapping.md` | 98 features mapped to agents with priorities |
| **Platform integration** | `CargoX_Agent_to_Orchestration_Hub_Mapping.md` | One Platform orchestration alignment |
| **AS-IS vs TO-BE analysis** | `Hubble_CargoX_Integration_Analysis.md` | Migration strategy, enhance-not-replace approach |
| **Success measurement** | `CargoX_Value_Map.md` | Deliverable-to-outcome tracking framework |

### Version Hierarchy

```
v1.0 (Initial) → v1.1 (Comprehensive) → v1.1_Core + v1.1_Executive_Summary → v1.2 (Latest)
                      ↓                         ↓
                Feature Mapping          Integration Analysis
```

**Convention**: Always use **v1.2 as latest baseline**, reference v1.1 for detailed agent specifications.

---

## 🤖 The 13 CargoX Agents

### Agent Naming Convention

**Pattern**: `[Emoji] [Agent Name] [Variant]`

| Agent | Primary Function | Input | Output | Priority |
|-------|------------------|-------|--------|----------|
| 📧 **Email Analyzer** | Parse inbound customer emails | Raw email + attachments | Structured booking data | 🟢 High |
| ✅ **Booking Validator** | Validate booking parameters | Extracted booking fields | Validation report + confidence | 🟢 High |
| 💰 **Rate Agent** | Calculate freight pricing | Origin, destination, cargo details | Rate card with breakdown | 🟢 High |
| 📦 **Quotation Agent** | Generate customer quotes | Validated booking + rates | Professional quote document | 🟢 High |
| 🚚 **Consolidation Planner** | Optimize shipment grouping | Multiple bookings | Consol plan + cost savings | 🟠 Medium |
| 🧾 **Invoice Validator** | Audit billing accuracy | Invoice + booking reference | Discrepancy report | 🟠 Medium |
| 🎓 **Learning Agent** | Continuous improvement from feedback | Operator corrections | Model fine-tuning recommendations | 🟢 High |
| ⚖️ **Evaluation Agent** | Quality scoring (LLM-as-Judge) | Agent outputs + ground truth | Confidence scores, accuracy metrics | 🟢 High |
| 🔧 **Master Data Agent** | Enrich with reference data | Entity IDs (customer, location) | Full entity profiles | 🟠 Medium |
| 📞 **Exception Handler** | Manage edge cases | Low-confidence scenarios | Escalation routing + context | 🟠 Medium |
| 🗺️ **Route Planner** | Optimize routing decisions | Lanes, transit times, costs | Recommended routes | 🔴 Low |
| 💬 **Conversational Agent** | Natural language interface | User queries | Context-aware responses | 🔴 Low |
| 📊 **Dashboard Agent** | Insights & analytics | Operational data | KPI summaries, alerts | 🔴 Low |

### Agent Status Indicators

- ✅ **Implemented/Done**
- 🟢 **High Priority** (Q1-Q2 2026)
- 🟠 **Medium Priority** (Q3 2026)
- 🔴 **Low Priority** (Q4 2026)
- ❌ **Gap/Not Planned**

---

## 🏗️ Technology Stack

### AI/ML Layer

| Component | Technology | Usage |
|-----------|-----------|-------|
| **Agent Orchestration** | LangChain | Prompt management, workflow coordination |
| **Multi-Agent Graphs** | LangGraph (Q1 2026) | State machine-based agent collaboration |
| **RAG Pipeline** | Azure AI Search + OpenAI Embeddings | Freight Knowledge Base (500+ docs) |
| **Foundation Models** | OpenAI (primary), Claude (alternative) | Core reasoning, decision-making |
| **LLM-as-Judge** | Custom Evaluation Agent | Quality scoring, confidence assessment |
| **Document Intelligence** | Azure Document Intelligence | OCR for email attachments (PDF/Excel/Word) |

### Integration & Backend

| Component | Technology | Purpose |
|-----------|-----------|---------|
| **Order Management** | CargoWise One (CW1) | Primary operational system |
| **Event Bus** | Azure Service Bus / RabbitMQ | Async agent communication |
| **APIs** | REST + BFF pattern | Routing, Master Data, Order services |
| **Microservices** | Java (Routing), Python (Geo, Master Data) | Domain-specific services |
| **Email Integration** | Outlook/Gmail API + Email Trans adapter | Inbound processing |
| **Storage** | Azure Blob Storage | Document persistence |

### Frontend & Observability

| Component | Technology | Purpose |
|-----------|-----------|---------|
| **Dashboard UI** | React (Vite) | Operator review interface |
| **Monitoring** | Azure Monitor + App Insights | Performance, telemetry |
| **Audit Logging** | 7-year retention | Compliance, regulatory traceability |

**Design Philosophy**: Language-agnostic, event-driven, microservices-based. LangChain/LangGraph as central orchestration layer.

---

## 📝 Documentation Conventions

### Document Structure Pattern

All playbooks follow this standard structure:

```markdown
# Document Title
### Subtitle/Context
**Version**: X.Y | **Date**: Month Year | **Status**: [Production/Draft/Review]
**Purpose**: [One sentence describing intent]

## Table of Contents
[Anchor links to major sections]

## Document Overview
- Purpose
- What's New (version changes)
- Intended Audience

## Vision & Principles
[Strategic context]

## Architecture
[Usually 3 layers: Presentation, Orchestration, Data/Services]

## Agent Persona Cards
[Emoji + Name + Function + Inputs/Outputs + Rationale]

## Trust & Learning Framework
[Confidence thresholds, approval gates, feedback loop]

## Success Metrics & KPIs
[Measurable outcomes]

## Rollout/Implementation Plan
[Phased timeline with deliverables]
```

**Convention**: Always include Version, Date, Purpose, Status, and Read Time in headers.

### Table Format

Use markdown tables with emoji-based status badges:

```markdown
| Feature/Agent | Description | Rationale | Priority | Status |
|---------------|-------------|-----------|----------|--------|
| Example Feature | What it does | Why it matters | 🟢 High | ✅ Done |
```

**Column Order**: Feature → Description → Function/Rationale → Priority/Feasibility → Status

### Architecture Diagrams

Use **ASCII box diagrams** in code blocks:

```
┌─────────────────────────────────────┐
│       Presentation Layer            │
│   (Dashboard UI, Email Interface)   │
└─────────────────┬───────────────────┘
                  ↓
┌─────────────────────────────────────┐
│      Orchestration Layer            │
│  (LangGraph, Event Bus, Agents)     │
└─────────────────┬───────────────────┘
                  ↓
┌─────────────────────────────────────┐
│     Data & Services Layer           │
│ (CW1, RAG, Master Data, Blob Store) │
└─────────────────────────────────────┘
```

**Convention**: Use `→` for horizontal flow, `↓` for vertical hierarchy.

### Agent Naming in Documentation

```
Pattern: [Emoji] [Descriptive Name] [(aka Alternative Name)]

Examples:
✅ Booking Validator (aka Order Validation Agent)
💰 Rate Agent (aka Pricing Agent)
🚚 Consolidation Planner (aka Consol Planner)
```

**Convention**: Emoji + clear domain association + aliases in parentheses if applicable.

---

## 🔄 Git Workflow & Branching

### Current Repository State

- **Active Branch**: `claude/add-claude-documentation-VlEJy` (feature branch for adding Claude documentation)
- **Remote**: `origin` at `http://local_proxy@127.0.0.1:22677/git/hpuri84/AI-airlcl`
- **Primary Committer**: harsh.puri@maersk.com (hpuri84)
- **Commit Frequency**: Steady iteration (~9 commits over 10 days)

### Branch Naming Convention

**Pattern**: `claude/[descriptive-name]-[session-id]`

**Example**: `claude/add-claude-documentation-VlEJy`

**CRITICAL**:
- Branch MUST start with `claude/`
- Branch MUST end with matching session ID
- Push will fail with 403 error if convention not followed

### Commit Message Style

**Pattern**: `[Action] [Component]: [Detailed description]`

**Examples**:
```
Add CargoX agent mapping to One Platform orchestration hub architecture
Add Feature_to_Agent_Mapping: 98 features mapped to 13 agents with 99% coverage
Add Hubble v1.5 integration analysis with gap analysis and phased roadmap
Add AI Agentic Playbook v1.2 with Hubble v1.5 integration
Update agent priority levels based on Q1 2026 roadmap feedback
```

**Conventions**:
- **Action-first style**: Add, Update, Refactor, Fix, Remove
- **No colons after action** (use space instead)
- **Descriptive, not terse**: Explain what changed and why
- **Reference component/document**: Make it easy to understand scope

### Push Strategy

**Standard Push**:
```bash
git push -u origin <branch-name>
```

**With Retry Logic (Network Failures)**:
- Retry up to 4 times with exponential backoff: 2s, 4s, 8s, 16s
- Only retry on network errors, NOT on 403 (branch name issue)

**Fetch/Pull Strategy**:
```bash
git fetch origin <branch-name>
git pull origin <branch-name>
```
- Prefer fetching specific branches
- Apply same retry logic for network failures

### .gitignore Status

**Current**: No `.gitignore` file exists

**Why**: This is a documentation-only repository—all files are intended to be tracked.

**Recommendation**: Consider adding:
```
.DS_Store
*.swp
*.tmp
~*
```
to exclude OS-generated files and editor temp files.

---

## 🛠️ Development Workflow & Phased Rollout

### 2026 Implementation Timeline

| Phase | Timeline | Focus | Key Deliverables | Budget |
|-------|----------|-------|------------------|--------|
| **Phase 1: Trust & Observability** | Q1 2026 | Confidence scoring, operator feedback UI, Learning Agent v1, dashboards | Feedback UI, Learning Agent, observability stack | $0 baseline |
| **Phase 2: Knowledge Enhancement** | Q2 2026 | RAG Freight KB (500+ docs), Master Data Lookup, Document Intelligence | RAG system, Document Agent, 30+ user training | Variable |
| **Phase 3: Multi-Agent CargoX v2.0** | Q3-Q4 2026 | 13 domain agents, event orchestration, Dashboard + Conversational Agents | Production multi-tenant system, 100+ operator adoption | Full budget |

### Approval & Testing Pattern

- **Approval Gates**: By risk level
  - **Low risk**: Auto-approve (high-confidence, simple updates)
  - **Medium risk**: Operator confirm (1-click approval)
  - **High risk**: Manual review (complex bookings, high-value shipments)
- **Confidence Thresholds**: Block deployment if accuracy <85%
- **A/B Testing**: Before any agent changes roll to production
- **Feedback Loop**: Weekly batch learning from operator corrections

### Documentation Update Cadence

| Document Type | Update Trigger | Versioning |
|---------------|----------------|------------|
| **Playbook** | Major architecture changes | Increment major version (v1.0 → v1.1 → v1.2) |
| **Feature Mapping** | New features or priority shifts | Update inline (track in commit message) |
| **Integration Analysis** | System upgrades or gap discoveries | Update inline with date stamp |
| **Asset Library** | New research or design artifacts | Continuous accumulation |

---

## 🤝 How AI Assistants Should Contribute

### Before Making Changes

✅ **DO**:
1. **Read existing documentation first**: Use `AI_Agentic_Playbook_v1.2.md` as latest baseline
2. **Check feature mappings**: Ensure no conflicts with existing 13-agent model
3. **Verify business alignment**: All changes should tie to success metrics (touchless %, accuracy, quote speed)
4. **Maintain consistency**: Follow emoji badges, table formats, ASCII diagrams
5. **Include metadata**: Add Version, Date, Purpose, Status to all new sections

❌ **DON'T**:
1. **Don't guess or infer architecture**: Stick to documented patterns
2. **Don't skip version headers**: Every document must have metadata
3. **Don't break table formatting**: Maintain column alignment and emoji badges
4. **Don't introduce new agent names**: Use the 13 canonical agents unless explicitly adding new ones
5. **Don't commit without descriptive messages**: Follow commit message conventions

### Adding New Features

**Checklist**:
1. **Update Feature_to_Agent_Mapping.md**: Add feature with agent assignment, priority, status
2. **Update AI_Agentic_Playbook_v1.2.md**: Reflect in architecture or roadmap
3. **Check CargoX_Agent_to_Orchestration_Hub_Mapping.md**: Ensure orchestration hub alignment
4. **Verify no gaps**: Cross-reference with Hubble_CargoX_Integration_Analysis.md
5. **Add asset references**: Link research PDFs or spreadsheets that justify the feature
6. **Commit with detailed message**: Explain what, why, and where it fits in the roadmap

### Proposing Architecture Changes

**Decision Framework**:
- **v1.2.1 (Patch)**: Minor clarifications, typo fixes, metadata updates
- **v1.3 (Minor)**: New agent added, phase timeline adjusted, orchestration hub changes
- **v2.0 (Major)**: Fundamental architecture shift, different tech stack, new business model

**Required Updates**:
1. Update playbook with version bump
2. Update all affected mappings (feature, orchestration, integration)
3. Add "What's New" section explaining changes
4. Include business justification (KPI impact, cost analysis)
5. Update asset library with supporting research

### Reviewing Pull Requests (If Applicable)

**Focus Areas**:
1. **Consistency**: Does it follow naming conventions and table formats?
2. **Completeness**: Are all related documents updated?
3. **Accuracy**: Does it align with the 13-agent model and Hubble v1.5 baseline?
4. **Traceability**: Are asset references included? Is there a business case?
5. **Clarity**: Is the commit message descriptive enough for future reference?

---

## 🔍 Common Tasks & How to Do Them

### Task 1: Understanding the Current Architecture

**Steps**:
1. Read `AI_Agentic_Playbook_v1.1_Core.md` (15-min quick overview)
2. Deep dive into `AI_Agentic_Playbook_v1.2.md` (Hubble v1.5 baseline + 2026 roadmap)
3. Review `Feature_to_Agent_Mapping.md` (98 features → 13 agents)
4. Check `CargoX_Agent_to_Orchestration_Hub_Mapping.md` (platform integration)

**Key Sections to Focus On**:
- Architecture (3 layers: Presentation, Orchestration, Data/Services)
- Agent Persona Cards (13 agents with inputs/outputs)
- Trust Framework (confidence thresholds, approval gates)
- Success Metrics (touchless rate, accuracy, quote speed)

### Task 2: Finding Which Agent Handles a Feature

**Steps**:
1. Open `Feature_to_Agent_Mapping.md`
2. Use Ctrl+F to search for feature name (e.g., "quote generation")
3. Check **Agent Assignment** column
4. Note **Priority** (🟢 🟠 🔴) and **Status** (✅ ❌)
5. Cross-reference with `AI_Agentic_Playbook_v1.1.md` for agent details

**Example**:
```
Feature: Automated Quote Generation
Agent: 📦 Quotation Agent
Input: Validated booking + rate card
Output: Professional quote document (PDF)
Priority: 🟢 High
Status: ✅ Implemented in v1.2
```

### Task 3: Adding a New Document

**Steps**:
1. **Choose naming convention**: `[Name]_[Version]_[Audience].md` (if versioned) or `[Descriptive_Name].md`
2. **Include metadata header**:
   ```markdown
   # Document Title
   **Version**: 1.0 | **Date**: January 2026 | **Purpose**: [One sentence]
   **Read Time**: ~X minutes
   ```
3. **Follow standard structure**: Overview → ToC → Content → Appendices
4. **Use emoji badges**: ✅ 🟢 🟠 🔴 ❌ for status indicators
5. **Add ASCII diagrams**: If architecture is involved
6. **Commit with descriptive message**: `Add [Document Name]: [Brief description]`

### Task 4: Updating Agent Priorities

**Steps**:
1. Open `Feature_to_Agent_Mapping.md`
2. Locate agent rows (e.g., 📦 Quotation Agent)
3. Update **Priority** column: Change 🟠 Medium → 🟢 High
4. Update **Status** if applicable: ❌ Gap → ✅ Done
5. Open `AI_Agentic_Playbook_v1.2.md`
6. Update Phase timeline if priority shift affects roadmap
7. Commit: `Update agent priorities: [Reason for change]`

### Task 5: Adding Research Assets

**Steps**:
1. Save file to `/home/user/AI-airlcl/asset/`
2. Use descriptive naming: `[Topic]_[Source]_[Date].[ext]`
   - Example: `RAG_Best_Practices_LangChain_2026.pdf`
3. Reference in relevant markdown document:
   ```markdown
   See [RAG Best Practices](asset/RAG_Best_Practices_LangChain_2026.pdf) for implementation details.
   ```
4. Commit: `Add asset: [File name] for [Purpose]`

### Task 6: Understanding Migration Strategy

**Steps**:
1. Open `Hubble_CargoX_Integration_Analysis.md`
2. Read **AS-IS Baseline (Hubble v1.5)** section
3. Compare with **TO-BE Target (CargoX)** section
4. Review **Gap Analysis** table (✅ existing, ❌ missing)
5. Check **Enhancement Strategy** (enhance-not-replace approach)
6. Note **Migration Risks** and **Mitigation Plans**

**Key Insight**: CargoX **enhances Hubble**, not replaces it. Focus on incremental value-add.

---

## 📊 Success Metrics & KPIs

### Primary KPIs (Tracked in CargoX_Value_Map.md)

| Metric | Baseline (AS-IS) | Target (TO-BE) | Measurement Method |
|--------|------------------|----------------|-------------------|
| **Touchless Processing Rate** | 10% | 80% | (Auto-approved bookings / Total bookings) × 100 |
| **Booking Accuracy** | 75% | 90% | (Error-free bookings / Total bookings) × 100 |
| **Quote Generation Speed** | 4-6 hours | <15 minutes | Avg. time from inquiry to quote delivery |
| **Operator Efficiency** | 30 bookings/day | 100+ bookings/day | Avg. bookings processed per operator |
| **Customer Satisfaction (NPS)** | 45 | 70+ | Net Promoter Score surveys |
| **Cost per Booking** | $15 | $5 | Fully loaded cost (labor + overhead) |

### Agent-Specific Metrics

Tracked via **⚖️ Evaluation Agent** (LLM-as-Judge):

- **Confidence Score**: Agent's self-assessment (0-100%)
- **Accuracy**: Human validation rate (operator confirms AI output)
- **Latency**: Time to process (email to booking draft)
- **Throughput**: Requests processed per hour
- **Error Rate**: % of outputs requiring operator correction

**Threshold for Production Deployment**: ≥85% accuracy, ≥90% confidence on validation set.

---

## 🔒 Security & Compliance

### Data Handling

- **PII Protection**: Anonymize customer data in logs (GDPR/CCPA compliance)
- **Audit Logging**: 7-year retention for all AI decisions (regulatory requirement)
- **Access Control**: Role-based permissions (operator, supervisor, admin)
- **Encryption**: TLS in transit, AES-256 at rest (Azure Blob, CW1)

### AI Safety & Trust

- **Human-in-the-Loop**: Operators approve high-risk decisions
- **Confidence Thresholds**: Auto-reject outputs below 85% confidence
- **Explainability**: All agent decisions include reasoning trace
- **Bias Monitoring**: Monthly audits for fairness across customer segments
- **Model Versioning**: Track model lineage (which version produced which output)

### Regulatory Compliance

- **Freight Regulations**: IATA (air), IMO (ocean), customs compliance
- **Data Residency**: Region-specific storage (EU data in EU datacenters)
- **Audit Trail**: Immutable logs of all booking modifications
- **SLA Commitments**: 99.9% uptime for quote generation

---

## 🆘 Troubleshooting & FAQs

### FAQ 1: Which document is the "source of truth"?

**Answer**: `AI_Agentic_Playbook_v1.2.md` is the **latest production baseline** (includes Hubble v1.5 integration). Use this unless you need comprehensive agent specs, then refer to v1.1.

### FAQ 2: How do I know which agent handles a feature?

**Answer**: Check `Feature_to_Agent_Mapping.md`. Search for the feature name (Ctrl+F), and the **Agent Assignment** column shows which of the 13 agents owns it.

### FAQ 3: What if I find outdated information?

**Answer**:
1. Verify against `AI_Agentic_Playbook_v1.2.md` (latest)
2. Check commit history: `git log --oneline --all -- [file_path]`
3. If confirmed outdated, update the document and commit with clear message
4. Consider if this requires a version bump (patch vs. minor vs. major)

### FAQ 4: Can I add a new agent?

**Answer**: Only if **strongly justified** with business case:
1. Explain why existing 13 agents can't handle the use case
2. Document inputs, outputs, accuracy requirements
3. Update `Feature_to_Agent_Mapping.md` and `AI_Agentic_Playbook_v1.2.md`
4. Add to `CargoX_Agent_to_Orchestration_Hub_Mapping.md`
5. Update phase timeline (which quarter for implementation?)
6. Get approval from repository owner (harsh.puri@maersk.com)

### FAQ 5: Why are some features marked ❌ (gap)?

**Answer**: These are **out of scope for 2026**. Reasons:
- Low business impact (not on critical path to 80% touchless rate)
- High complexity relative to value
- Dependency on external systems not yet available
- Budget constraints

If you believe a gap should be filled, provide ROI justification in `CargoX_Value_Map.md`.

### FAQ 6: How do I handle merge conflicts?

**Answer**:
1. This is a documentation repo—conflicts are usually easy to resolve
2. **Prefer latest version** (v1.2 over v1.1) if conflict is between playbook versions
3. **Preserve metadata**: Don't overwrite Version, Date, Purpose headers
4. **Merge table rows**: If two commits add different features, keep both rows
5. **Ask for clarification**: If conflict is substantive (different architectures), escalate to repository owner

### FAQ 7: What if I need to reference external code repos?

**Answer**: This repo is documentation-only. For code references:
1. **Use hyperlinks**: `[Routing Service](https://github.com/maersk/routing-service)`
2. **Add to asset library**: Save architecture diagrams or API specs to `/asset/`
3. **Document integration points**: Update `CargoX_Agent_to_Orchestration_Hub_Mapping.md`
4. **Don't copy code**: Link to source repos, don't duplicate code here

### FAQ 8: How do I know if a change needs a new version?

**Versioning Guide**:
- **No version change**: Typo fixes, formatting, clarifications
- **Patch (v1.2 → v1.2.1)**: Metadata updates, minor additions to existing sections
- **Minor (v1.2 → v1.3)**: New agent, phase timeline shift, orchestration hub changes
- **Major (v1.2 → v2.0)**: Architecture overhaul, different tech stack, new business model

When in doubt, **patch version is safe**.

---

## 🎓 Key Concepts for AI Assistants

### RAG (Retrieval-Augmented Generation)

**What It Is**: Combines LLM reasoning with document retrieval from a Freight Knowledge Base (500+ docs: tariffs, regulations, SOPs).

**How CargoX Uses It**:
- **📧 Email Analyzer**: Retrieves templates for common booking patterns
- **💰 Rate Agent**: Fetches tariff rules and surcharge logic
- **✅ Booking Validator**: Looks up regulatory requirements (IATA, customs)

**Tech Stack**: Azure AI Search (vector store) + OpenAI Embeddings (text-embedding-ada-002)

### LLM-as-Judge

**What It Is**: Using an LLM (⚖️ Evaluation Agent) to score other agents' outputs instead of human evaluation.

**How CargoX Uses It**:
- **Confidence Scoring**: 0-100% assessment of output quality
- **Accuracy Validation**: Compare against ground truth (historical bookings)
- **Feedback Loop**: Flag low-confidence outputs for operator review

**Benefits**: Scalable, consistent, faster than human review (but human-in-loop for high-risk).

### Touchless Processing

**What It Is**: End-to-end booking automation without operator intervention.

**CargoX Flow**:
```
Customer Email → 📧 Email Analyzer → ✅ Booking Validator → 💰 Rate Agent
→ 📦 Quotation Agent → Auto-Send Quote → ✅ Touchless (if confidence ≥90%)
```

**Operator Involvement**: Only when confidence <90% or high-risk scenarios (e.g., hazmat, high-value).

### Confidence Thresholds

**Risk-Based Approval**:
- **≥90% confidence**: Auto-approve (touchless)
- **75-89% confidence**: Operator confirm (1-click)
- **<75% confidence**: Manual review (operator edits booking)

**Threshold Tuning**: Adjusted quarterly based on accuracy metrics and operator feedback.

### Learning Loop

**How CargoX Improves Over Time**:
1. **Operator Corrections**: Every manual edit is logged
2. **🎓 Learning Agent**: Analyzes patterns in corrections weekly
3. **Model Fine-Tuning**: Updates agent prompts or trains custom models
4. **A/B Testing**: Deploys improvements to 10% of traffic first
5. **Full Rollout**: If accuracy improves, promote to 100%

**Goal**: Continuous 1-2% monthly improvement in touchless rate.

---

## 📞 Contact & Escalation

### Repository Owner

**Name**: Harsh Puri
**Email**: harsh.puri@maersk.com
**GitHub**: hpuri84
**Role**: Technical Lead, CargoX AI Agentic Initiative

### When to Escalate

- **Architecture Changes**: New agents, fundamental design shifts
- **Scope Questions**: Is feature X in scope for 2026?
- **Conflict Resolution**: Merge conflicts with substantive disagreement
- **Access Issues**: Git push failures, permission errors
- **Business Alignment**: Does this change align with success metrics?

### Self-Service Resources

Before escalating, check:
1. `AI_Agentic_Playbook_v1.2.md` (latest baseline)
2. `Hubble_CargoX_Integration_Analysis.md` (AS-IS vs TO-BE)
3. `CargoX_Value_Map.md` (deliverable-to-outcome tracking)
4. Git commit history: `git log --oneline --all`
5. This `CLAUDE.md` file (you're here!)

---

## 🚀 Quick Start Checklist for New AI Assistants

- [ ] Read `AI_Agentic_Playbook_v1.1_Core.md` (15 minutes) for high-level overview
- [ ] Review `AI_Agentic_Playbook_v1.2.md` (latest production baseline)
- [ ] Skim `Feature_to_Agent_Mapping.md` to understand 13-agent model
- [ ] Check `CargoX_Agent_to_Orchestration_Hub_Mapping.md` for platform integration
- [ ] Review this `CLAUDE.md` file (you just did!)
- [ ] Verify current branch: `git branch` (should be `claude/add-claude-documentation-VlEJy` or similar)
- [ ] Check commit style: `git log --oneline -5` to see recent commit messages
- [ ] Understand emoji conventions: ✅ 🟢 🟠 🔴 ❌ for status/priority
- [ ] Bookmark key metrics: 80% touchless rate, 90% accuracy, 95% quote speed improvement
- [ ] Remember: **Documentation repo only**—no runtime code here

---

## 📝 Document Metadata

**Repository**: AI-airlcl
**Owner**: hpuri84 (harsh.puri@maersk.com)
**Size**: 34 MB (5,874+ lines of markdown + 17 asset files)
**Type**: Documentation-Centric (No runtime code)
**Purpose**: Strategic AI Agentic Initiative for Maersk Air & LCL freight automation
**Last Updated**: January 11, 2026
**CLAUDE.md Version**: 1.0

---

## 🔄 Changelog for CLAUDE.md

### Version 1.0 (January 11, 2026)
- Initial creation of CLAUDE.md
- Documented repository structure, 13-agent model, technology stack
- Added git workflow conventions (branch naming, commit style, push strategy)
- Included documentation conventions (tables, diagrams, emoji badges)
- Provided 2026 phased rollout timeline
- Added troubleshooting FAQs and quick start checklist
- Established metadata standards and versioning guide

---

**End of CLAUDE.md**

For questions or suggestions about this guide, contact harsh.puri@maersk.com or update this document following the conventions outlined above.
