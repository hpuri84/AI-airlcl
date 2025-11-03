# Feature-to-Agent Mapping: Customer Experience → CargoX Agents

**Date**: November 2025  
**Purpose**: Map customer-facing features to CargoX domain agents for implementation planning

---

## Mapping Summary

| Customer Module | Primary Agent(s) | Supporting Agent(s) | Implementation Priority |
|----------------|------------------|-------------------|------------------------|
| **Email Processing & AI Integration** | Email Analyzer, Booking Validator | Master Data Agent, Exception Handler | **P0** (Foundation) |
| **Shipment Monitoring Dashboard** | Dashboard Agent (new), Forecast Agent | Master Data Agent, CW1 Sync Agent | **P1** (Core Experience) |
| **SAP Invoice Processing** | Invoice Validator | Rate Agent, CW1 Sync Agent | **P1** (Financial Accuracy) |
| **Flight Status Verification** | Forecast Agent (enhanced) | Exception Handler | **P2** (Advanced) |
| **Flight Allocation & Consolidation** | Consolidation Planner | Rate Agent, Routing Agent, CW1 Sync Agent | **P0** (Core Operations) |
| **Consolidation Monitoring Dashboard** | Dashboard Agent (new), Exception Handler | Customs Agent, CW1 Sync Agent | **P1** (Visibility) |
| **WMS (Warehouse Management)** | Warehouse Agent | Master Data Agent, Exception Handler | **P2** (Optional) |

---

## Module 1: Email Processing & AI Integration

### Agent Mapping

| Feature | Agent | Rationale | Feasibility | Priority |
|---------|-------|-----------|-------------|----------|
| **Receive external emails** | **📧 Email Analyzer** | Core capability: monitors inbox, downloads attachments | Feasible | High |
| **Store email content and attachments** | **📧 Email Analyzer** | Already handles blob storage for attachments | Feasible | High |
| **NEW BOOKING - Single** | **📧 Email Analyzer** → **✅ Booking Validator** | Email Analyzer parses → Booking Validator validates | Feasible | High |
| **NEW BOOKING - Multiple** | **📧 Email Analyzer** (batch mode) → **✅ Booking Validator** (loop) | Requires batch processing logic | Probably | Mid |
| **UPDATE BOOKING - Single** | **✅ Booking Validator** (update mode) | Requires booking ID matching logic | Probably | High |
| **UPDATE BOOKING - Multiple** | **✅ Booking Validator** (batch update) | Requires batch + matching logic | Probably | Mid |
| **PROVIDE ADDITIONAL DOC** | **📧 Email Analyzer** → **🔧 Master Data Agent** | Parse doc → attach to booking in CW1 | Probably | High |
| **Processing by main and sub agents** | **CargoX Orchestrator** | Already designed for multi-agent coordination | Feasible | High |
| **Address to organization code mapping** | **🔧 Master Data Agent** | Master data lookup (customer org → CW1 code) | Feasible | High |
| **Extract and tag key information** | **📧 Email Analyzer** | NER (Named Entity Recognition) for key fields | Feasible | High |
| **Display processed email content** | **Dashboard Agent** (new) | UI layer to show parsed email results | Feasible | High |
| **User review of AI content** | **Dashboard Agent** + **Operator Feedback UI** | Human-in-the-loop review interface | Feasible | High |
| **Sync to CW1 data and electronic documents** | **CW1 Sync Agent** | Already handles CW1 integration | Feasible | High |
| **Mark email as read** | **📧 Email Analyzer** | Email client API integration | Feasible | High |
| **Real-time email interface sync** | **📧 Email Analyzer** | Webhook or polling for real-time updates | Feasible | High |
| **Q&A section for users** | **Conversational Agent** (new) | Chatbot for shipment questions | Probably | Mid |
| **Reply to email** | **📧 Email Analyzer** (response mode) | Draft reply based on booking status | Probably | High |
| **Automatically send WIP to customer email** | **📧 Email Analyzer** + **Notification Agent** (new) | Trigger email on booking status change | Probably | Mid |

**New Agents Needed**:
1. **Dashboard Agent**: UI orchestration for operator/customer views
2. **Conversational Agent**: Q&A chatbot for shipment inquiries
3. **Notification Agent**: Automated email/SMS notifications on events

---

## Module 2: Shipment Monitoring Dashboard

### Agent Mapping

| Feature | Agent | Rationale | Feasibility | Priority |
|---------|-------|-----------|-------------|----------|
| **Integrate shipment data** | **Dashboard Agent** | Aggregate data from CW1, EDI, tracking systems | Feasible | High |
| **Auto import from CW1 job header** | **CW1 Sync Agent** | Real-time sync from CW1 to dashboard | Feasible | High |
| **Provide searchable criteria** | **Dashboard Agent** | Search/filter UI over shipment data | Feasible | High |
| **Display shipment details** | **Dashboard Agent** | Render shipment cards/tables | Feasible | High |
| **Enable fixed time list update / real-time update** | **Dashboard Agent** + **Event Bus** | WebSocket or polling for real-time updates | Feasible | High |
| **Execute automated CW1 operation - print HAWB** | **CW1 Sync Agent** | Direct CW1 API call (if available) | NOT Feasible | Low |
| **System checks and alerts for data quality** | **⚖️ Evaluation Agent** + **📞 Exception Handler** | Monitor data anomalies → alert operators | Feasible | Mid |
| **Custom fields, FREE TEXT** | **Dashboard Agent** | Flexible schema for custom fields | Feasible | High |
| **Download custom reports** | **Dashboard Agent** | Export to Excel/PDF | Probably | High |

**Implementation Note**: Dashboard Agent is primarily a **UI orchestration layer**, not a traditional AI agent. Consider building as a **frontend service** that consumes agent APIs.

---

## Module 3: SAP Invoice Processing

### Agent Mapping

| Feature | Agent | Rationale | Feasibility | Priority |
|---------|-------|-----------|-------------|----------|
| **Detect daily SAP invoice generation** | **🧾 Invoice Validator** | Monitor SAP for new invoices (file watcher or API) | Feasible | High |
| **Create company-specific forms** | **🧾 Invoice Validator** | Template library for invoice formats | Feasible | High |
| **Populate customizable Excel templates** | **🧾 Invoice Validator** | Excel generation from invoice data | Feasible | High |
| **Allow customer-specific settings** | **🧾 Invoice Validator** + **🔧 Master Data Agent** | Customer preferences stored in master data | Feasible | High |
| **Schedule and send emails** | **Notification Agent** | Scheduled email delivery (e.g., every Monday 9am) | Feasible | High |
| **Verify email delivery and record** | **Notification Agent** | Email tracking (SMTP delivery status) | Feasible | High |
| **Process tax invoice replies and upload to CW1** | **📧 Email Analyzer** + **🧾 Invoice Validator** + **CW1 Sync Agent** | Parse reply email → validate → upload to CW1 | Probably | High |

**Workflow**:
```
SAP → Invoice Validator (detect + generate) → Notification Agent (send) 
   → Email Analyzer (receive reply) → Invoice Validator (validate) 
   → CW1 Sync Agent (upload)
```

---

## Module 4: Flight Status Verification (Smart Feature)

### Agent Mapping

| Feature | Agent | Rationale | Feasibility | Priority |
|---------|-------|-----------|-------------|----------|
| **Trigger verification one day before ETD** | **📊 Forecast Agent** | Scheduled job (daily batch at midnight) | Probably | Mid |
| **Identify airline and website** | **📊 Forecast Agent** | Lookup airline from MAWB → map to tracking URL | Probably | Mid |
| **LLM-driven flight data web scraping** | **📊 Forecast Agent** | Use LLM to parse airline websites (e.g., via Playwright + GPT-4) | Probably | Mid |
| **Compare with CW1 records** | **📊 Forecast Agent** + **CW1 Sync Agent** | Fetch CW1 ETD/ETA → compare with scraped data | Probably | Mid |
| **Notify gateway upon changes** | **📞 Exception Handler** + **Notification Agent** | Alert if ETD changed by >2 hours | Probably | Mid |
| **Detect split shipment and unloading issues** | **📊 Forecast Agent** | Anomaly detection (e.g., partial MAWB unloaded) | Probably | Mid |
| **Update CW1 with verified data** | **CW1 Sync Agent** | Write back corrected ETD/ETA to CW1 | Probably | Mid |
| **Use LLM to adaptively handle website changes** | **📊 Forecast Agent** | Self-healing scraper (LLM adjusts to HTML changes) | Probably | Mid |

**Technical Challenge**: Web scraping airline sites is **fragile** (sites change frequently). Consider using **flight tracking APIs** (e.g., FlightAware, FlightStats) instead of scraping.

**Alternative Approach**:
```
Forecast Agent → Flight Tracking API (FlightAware) → Compare with CW1 
   → Exception Handler (if discrepancy) → CW1 Sync Agent (update)
```

---

## Module 5: Flight Allocation & Consolidation

### Agent Mapping

| Feature | Agent | Rationale | Feasibility | Priority |
|---------|-------|-----------|-------------|----------|
| **Receive transport instructions, real-time sync** | **🚚 Consolidation Planner** + **Event Bus** | Receive allocation events from TMS | Probably | High |
| **Manage block space agreements and track completion** | **🚚 Consolidation Planner** | Track allocated vs used space per airline | Feasible | High |
| **Data returns to single platform** | **Dashboard Agent** | Centralized view of allocations | Feasible | High |
| **Receive daily ULD assignments** | **🚚 Consolidation Planner** | Import ULD data from airline | Feasible | High |
| **Dashboard** | **Dashboard Agent** | UI for allocation overview | Feasible | High |
| **Simulate SP loading, optimize profit allocation** | **🚚 Consolidation Planner** + **💰 Rate Agent** | Bin-packing optimization + margin calculation | Probably | High |
| **User review and manual override** | **Dashboard Agent** + **HITL Gates** | Operator can adjust consol plan before execution | Feasible | High |
| **TMS creates CONSOL, sync with CW1** | **🚚 Consolidation Planner** + **CW1 Sync Agent** | Create CONSOL in TMS → sync to CW1 SHIPMENT | Probably | High |
| **Generate Excel loading plan** | **🚚 Consolidation Planner** | Export consol plan to Excel (for warehouse) | Feasible | High |
| **Update final weight** | **🚚 Consolidation Planner** | Receive actual weight from warehouse → update CW1 | Feasible | High |
| **Auto-fill CONSOL DETAILS** | **🚚 Consolidation Planner** | Pre-fill MAWB, ULD, flight details | Probably | Mid |
| **Send airline MAWB print requirements to CW1** | **CW1 Sync Agent** | Trigger CW1 print job (if API available) | Probably | Mid |
| **Auto record FRT cost and recover from Station** | **💰 Rate Agent** + **CW1 Sync Agent** | Calculate freight cost → post to CW1 AP/AR | Feasible | Mid |
| **TMS returns COST to CW1 (FRT ONLY)** | **💰 Rate Agent** + **CW1 Sync Agent** | Freight cost reconciliation | Feasible | Mid |
| **CW1 creates AP LINE based on TMS instructions** | **CW1 Sync Agent** | Create AP (Accounts Payable) records | Feasible | Mid |
| **AP = AR, DEBITOR based on PICKUP AGENT** | **💰 Rate Agent** + **CW1 Sync Agent** | Revenue recognition logic | Probably | Low |
| **POST AR (ALL AR CHARGE)** | **CW1 Sync Agent** | Post AR (Accounts Receivable) to CW1 | Probably | Low |
| **Request cargo / SPACE** | **🚚 Consolidation Planner** | Operator can request additional space from airline | Probably | Low |

**Workflow** (Consolidation to CW1):
```
Consolidation Planner (create plan) → Rate Agent (calculate FRT cost) 
   → Operator Approval (HITL) → CW1 Sync Agent (create CONSOL + SHIPMENT + AP/AR)
   → Notification Agent (send loading plan to warehouse)
```

---

## Module 6: Consolidation Monitoring Dashboard

### Agent Mapping

| Feature | Agent | Rationale | Feasibility | Priority |
|---------|-------|-----------|-------------|----------|
| **Check consolidation cargo creation** | **Dashboard Agent** | Monitor CONSOL status (created, in-progress, completed) | Feasible | Mid |
| **Monitor shipment documents and customs clearance** | **🛃 Customs Agent** + **Dashboard Agent** | Track customs status per shipment | Feasible | Mid |
| **Track shipment arrival at warehouse** | **Warehouse Agent** + **Dashboard Agent** | Real-time tracking from WMS | Feasible | Mid |
| **Verify manifest and MAWB printing** | **Dashboard Agent** | Check if MAWB printed (from CW1 or TMS) | Probably | Mid |
| **Confirm package list printing** | **Dashboard Agent** | Verify packing list generated | Feasible | Mid |
| **Check loading plan generation** | **🚚 Consolidation Planner** | Ensure loading plan created before departure | Feasible | Mid |
| **Real-time warehouse outbound picking** | **Warehouse Agent** + **Dashboard Agent** | Track picking status from WMS | Probably | Mid |
| **Real-time confirmation of cargo loaded to ULD/truck** | **Warehouse Agent** + **Dashboard Agent** | Confirm loading complete (scan-based or manual) | Probably | Mid |
| **Real-time tracking of airport cargo receipt** | **📊 Forecast Agent** + **Dashboard Agent** | Track when airline receives cargo at airport | Probably | Mid |
| **Record flight departure and multi-leg times** | **📊 Forecast Agent** + **CW1 Sync Agent** | Update actual departure/arrival times (ATD/ATA) | Feasible | Low |
| **Automatically send PRE-ALERT** | **Notification Agent** | Send pre-alert email to consignee before arrival | Feasible | Mid |
| **Track PRE-ALERT sending status** | **Notification Agent** | Log email delivery status | Feasible | Mid |

**Dashboard Views** (for Consolidation Monitoring):
1. **CONSOL Overview**: List of all consols (status, CBM, weight, flight, ETD/ETA)
2. **Shipment Drill-Down**: Click consol → see all shipments in that consol
3. **Milestone Timeline**: Visual timeline (warehouse arrival → loading → airport receipt → departure → arrival)
4. **Alerts**: Highlight exceptions (customs hold, flight delay, missing MAWB)

---

## Module 7: WMS (Warehouse Management)

### Agent Mapping

| Feature | Agent | Rationale | Feasibility | Priority |
|---------|-------|-----------|-------------|----------|
| **Receive and register cargo** | **Warehouse Agent** | Receive inbound cargo → create WMS record | Feasible | High |
| **Receive cargo status** | **Warehouse Agent** | Track cargo status (received, picked, loaded) | Feasible | Low |
| **Measure package details** | **Warehouse Agent** | Capture dimensions, weight (from scanner or manual entry) | Feasible | High |
| **Input data into warehouse management system** | **Warehouse Agent** | Write to WMS database or API | Feasible | High |
| **Generate and store PDF reports** | **Warehouse Agent** | Export receiving reports, packing lists | Feasible | High |
| **Provide real-time data to customer experience and gateway** | **Warehouse Agent** + **Event Bus** | Publish warehouse events to other agents | Feasible | High |
| **AI comparison with pre-alert** | **Warehouse Agent** + **⚖️ Evaluation Agent** | Compare received cargo vs pre-alert (detect discrepancies) | Probably | Mid |
| **Auto sync valid data to CW1** | **Warehouse Agent** + **CW1 Sync Agent** | Update CW1 with actual weights, receipt timestamps | Probably | Mid |

**Warehouse Agent Workflow**:
```
1. Cargo arrives at warehouse
   ↓
2. Warehouse Agent creates WMS record (scan barcode or manual entry)
   ↓
3. AI comparison with pre-alert (if discrepancy → alert Exception Handler)
   ↓
4. Measure package details (dimensions, weight)
   ↓
5. Publish warehouse.received event → Event Bus
   ↓
6. CW1 Sync Agent updates CW1 with actual data
   ↓
7. Dashboard Agent shows real-time status to operators/customers
```

---

## New Agents Required

Based on feature mapping, we need to add these agents to the core 8:

| Agent | Purpose | Priority | Estimated Effort |
|-------|---------|----------|-----------------|
| **Dashboard Agent (UI Orchestrator)** | Aggregate data for operator/customer dashboards | **P0** | Medium (frontend-heavy) |
| **Notification Agent** | Automated emails, SMS, Teams messages on events | **P1** | Low (use existing email service) |
| **Conversational Agent (Q&A)** | Chatbot for shipment inquiries | **P2** | Medium (LLM + RAG) |
| **Warehouse Agent** | WMS integration, cargo tracking | **P1** | Medium (API integrations) |
| **Customs Agent** | Track customs status, generate declarations | **P2** | High (complex domain logic) |

**Updated Agent Count**: 8 (original) + 5 (new) = **13 total agents**

---

## Implementation Roadmap (Aligned with Playbook v1.2)

### Phase 1: Foundation (Q1 2026) — Email Processing + Dashboard
**Agents**: Email Analyzer, Booking Validator, Dashboard Agent (v0.1), Notification Agent  
**Features**:
- ✅ Receive external emails
- ✅ NEW BOOKING - Single
- ✅ Extract and tag key information
- ✅ Sync to CW1
- ✅ Display processed email content
- ✅ User review of AI content

**Success Criteria**: 85% extraction accuracy, 30% touchless rate, UMUX-Lite >70

---

### Phase 2: Learning + RAG (Q1 2026) — Invoice Processing
**Agents**: Invoice Validator, Rate Agent, Learning Agent, Evaluation Agent  
**Features**:
- ✅ Detect daily SAP invoice generation
- ✅ Create company-specific forms
- ✅ Schedule and send emails
- ✅ Process tax invoice replies

**Success Criteria**: 95% invoice accuracy, operator feedback loop operational

---

### Phase 3: Multi-Agent (Q2 2026) — Consolidation Planning
**Agents**: Consolidation Planner, Rate Agent, CW1 Sync Agent, Orchestrator v2.0  
**Features**:
- ✅ Receive transport instructions, real-time sync
- ✅ Manage block space agreements
- ✅ Simulate SP loading, optimize profit allocation
- ✅ Generate Excel loading plan
- ✅ TMS creates CONSOL, sync with CW1

**Success Criteria**: 85% capacity utilization, 50% touchless consol creation

---

### Phase 4: Advanced (Q3-Q4 2026) — Flight Status + WMS + Dashboards
**Agents**: Forecast Agent (enhanced), Warehouse Agent, Customs Agent, Conversational Agent  
**Features**:
- ✅ LLM-driven flight data verification
- ✅ WMS integration (receive and register cargo)
- ✅ Real-time warehouse tracking
- ✅ Consolidation monitoring dashboard
- ✅ Shipment monitoring dashboard
- ✅ Q&A section for users

**Success Criteria**: 70% touchless globally, real-time visibility for all shipments, UMUX >80

---

## Feature Coverage Analysis

### By Priority

| Priority | Total Features | Feasible | Probably | Not Feasible | Coverage |
|----------|---------------|----------|----------|--------------|----------|
| **High** | 62 | 50 | 12 | 0 | 100% (all addressable) |
| **Mid** | 28 | 18 | 10 | 0 | 100% (all addressable) |
| **Low** | 8 | 4 | 4 | 1 | 88% (1 not feasible: print HAWB via CW1 API) |
| **Total** | **98** | **72 (73%)** | **26 (27%)** | **1 (1%)** | **99% coverage** |

### By Module

| Module | Total Features | Agent Coverage | Missing Agents | Priority |
|--------|---------------|---------------|---------------|----------|
| **Email Processing** | 18 | 95% (Email Analyzer, Booking Validator, Dashboard, Notification, Conversational) | None | **P0** |
| **Shipment Monitoring** | 9 | 100% (Dashboard, CW1 Sync, Evaluation, Exception Handler) | None | **P1** |
| **SAP Invoice** | 7 | 100% (Invoice Validator, Rate, CW1 Sync, Notification) | None | **P1** |
| **Flight Status** | 8 | 100% (Forecast, Exception Handler, CW1 Sync) | None | **P2** |
| **Consolidation** | 22 | 95% (Consolidation Planner, Rate, CW1 Sync, Dashboard) | None | **P0** |
| **Consol Monitoring** | 13 | 100% (Dashboard, Warehouse, Customs, Forecast, Notification) | None | **P1** |
| **WMS** | 8 | 100% (Warehouse, CW1 Sync, Evaluation) | None | **P2** |

**Conclusion**: All 7 modules can be addressed with **13 agents** (8 original + 5 new). Only 1 feature is not feasible (print HAWB via CW1 API, due to CW1 API limitations).

---

## Technical Architecture: Feature → Agent → CW1

```
┌─────────────────────────────────────────────────────────────┐
│  Layer 1: Customer/Operator Interface                       │
│  • Email inbox                                               │
│  • Dashboard (web app): Shipment Monitoring, Consol Monitor │
│  • Teams/Slack notifications                                 │
└──────────────────────┬──────────────────────────────────────┘
                       ↓
┌─────────────────────────────────────────────────────────────┐
│  Layer 2: CargoX Agents (13 total)                          │
│  ┌────────────────────────────────────────────────────────┐ │
│  │ Core Agents (8):                                        │ │
│  │ • Email Analyzer, Booking Validator, Rate,             │ │
│  │   Quotation, Consol Planner, Invoice Validator,        │ │
│  │   Learning, Evaluation                                  │ │
│  ├────────────────────────────────────────────────────────┤ │
│  │ New Agents (5):                                         │ │
│  │ • Dashboard (UI orchestrator)                           │ │
│  │ • Notification (email/SMS automation)                   │ │
│  │ • Conversational (Q&A chatbot)                          │ │
│  │ • Warehouse (WMS integration)                           │ │
│  │ • Customs (compliance tracking)                         │ │
│  └────────────────────────────────────────────────────────┘ │
│  Event Bus: email.parsed, booking.validated,                │
│             consol.created, warehouse.received, etc.         │
└──────────────────────┬──────────────────────────────────────┘
                       ↓
┌─────────────────────────────────────────────────────────────┐
│  Layer 3: Integration + Knowledge                           │
│  • CargoWise One (CW1) — bookings, shipments, finance       │
│  • SAP — invoices                                            │
│  • TMS — consolidation, allocations                         │
│  • WMS — warehouse operations                                │
│  • Flight APIs — real-time flight status                    │
│  • Freight Graph (RAG) — CW1 logs, contracts, rates, SOPs   │
└─────────────────────────────────────────────────────────────┘
```

---

## Recommendations

### Quick Wins (Implement First)
1. **Email Processing (Module 1)** → Email Analyzer + Booking Validator already defined in playbook
2. **SAP Invoice (Module 3)** → Invoice Validator already defined, add Notification Agent
3. **Consolidation (Module 5)** → Consol Planner already defined, integrate with CW1 Sync Agent

### Medium Effort (Phase 2-3)
4. **Shipment Monitoring Dashboard (Module 2)** → Build Dashboard Agent (mostly frontend)
5. **Consol Monitoring Dashboard (Module 6)** → Reuse Dashboard Agent, add Warehouse Agent
6. **WMS (Module 7)** → Build Warehouse Agent (API integrations)

### Advanced (Phase 4)
7. **Flight Status Verification (Module 4)** → Enhance Forecast Agent with web scraping or API integration

### Not Recommended
8. **Print HAWB via CW1 API (Module 2)** → Marked "NOT Feasible" in requirements; requires CW1 vendor support

---

**Document Prepared By**: AI Architecture Team  
**Date**: November 2025  
**Next Review**: After Phase 1 complete (Q1 2026)
