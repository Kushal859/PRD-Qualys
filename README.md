# Qualys ETM Identity — NHI Risk Quantification & Attack-Path Prioritization

**Independent Portfolio PRD | Author: Kushal Zambare | June 2026**

> ⚠️ **Disclaimer:** This is an independent, unsolicited portfolio PRD written by Kushal Zambare based solely on public Qualys ETM Identity materials (ROCon Houston, October 2025, and publicly available Qualys product documentation). It is **not affiliated with, endorsed by, or produced for Qualys, Inc.** All sizing numbers and financial projections are illustrative assumptions — not internal Qualys data.

---

## What This PRD Covers

This 25-page product requirements document proposes the **Non-Human Identity (NHI) Risk Quantification & Attack-Path Prioritization** module for Qualys ETM Identity.

### The Problem
Enterprises have largely solved human identity risk. The new perimeter is **non-human** — service accounts, machine identities, API keys, and agentic AI agents that outnumber humans 50:1, operate at machine speed, have no clear owner, rotate slowly, and rarely have MFA protection.

Security teams face a flat export of 40,000 unmanaged NHIs with:
- ❌ No unified inventory across AD, Entra ID, Okta, IGA, and PAM
- ❌ No ownership attribution — orphaned accounts accumulate for years
- ❌ No prioritisation — everything looks equally dangerous
- ❌ No closed loop — no proof that remediation actually worked

### The Solution
ETM Identity as a **risk quantification overlay** — consuming signals from existing IAM, IGA, PAM, and ITDR tools to produce a unified Identity TruRisk score and closed-loop remediation workflow.

---

## PRD Scope — 4 Pillars

| Pillar | Description |
|--------|-------------|
| **1. Unified NHI Discovery & Inventory** | Connectors to AD, Entra ID, Okta, IGA/PAM; deduplication engine; ≥95% coverage target |
| **2. Confidence-Based Ownership Attribution** | 4-signal model (creating account, ticket history, naming convention, recent users); 1-click confirm/reassign |
| **3. Identity TruRisk Scoring** | Exposure × Exploitability × Blast Radius on the 1–2000 ETM scale; re-scores on any state change |
| **4. Attack-Path Graph + ROC→ITSM Closed Loop** | Chokepoint identification; ITSM ticket with blast-radius note; TruConfirm re-validation |

---

## Document Contents

```
PRD-Qualys/
├── Qualys-ETM-Identity-PRD-Final.pdf     ← Main PRD (25 pages)
```

### What's inside the PRD

- **Problem Definition** — The unmanaged NHI frontier
- **Goals & Business–Product Outcome Mapping**
- **Success Metrics** — North star + L1/L2/L3/Failure metrics
- **User Segmentation** — 5 personas (ROC Analyst, IAM Admin, CISO, App Owner, Compliance Officer)
- **Size & Impact Analysis** — $11.25M incremental ARR Year 1 (illustrative)
- **Problem Validation** — Research from Verizon DBIR 2024, IBM Cost of Breach 2024, CyberArk 2024
- **Competitor Research** — SailPoint, Saviynt, CrowdStrike, Silverfort, Microsoft
- **User Persona & Journey Map** — ROC Analyst "Anjali"
- **Pain Points & Unmet Needs** — Ranked by severity and frequency
- **Descoped Items** — With explicit reasoning
- **Solution Prioritization** — RICE scoring across 4 approaches
- **User Stories** — 6 features with full Given/When/Then acceptance criteria
- **Risk & Mitigation** — 8 risk/mitigation pairs
- **Data & Logic Changes** — Algorithm changes
- **Schema Changes** — 24 new `nhi_` prefixed fields across 5 categories
- **Data Instrumentation** — 10 events with full variable lists
- **System Design** — Architecture overview + 6 edge-case scenario tests
- **Launch Readiness** — 8-milestone checklist (Completed / In Progress / Not Started)
- **Future Iterations** — 8 user stories for v2–v3

---

## Key Concepts

**Identity TruRisk Formula:**
```
Identity TruRisk Score = Exposure × Exploitability × Blast Radius
```
- **Exposure** — Missing MFA, stale credentials (>90 days), excessive privilege, dormant-but-enabled
- **Exploitability** — Active threat-intel targeting, known exploit techniques (Kerberoasting, Pass-the-Hash), active campaigns
- **Blast Radius** — Hop count to Tier-0 assets × asset criticality × privileged group membership

**North Star Metric:** ↓ Aggregate NHI Identity TruRisk Score (QoQ)

**The Closed Loop:** ROC Analyst → Worklist → ITSM Ticket → App Owner → Remediation → TruConfirm Re-validation → Score Update

---

## Competitive Positioning

| Capability | SailPoint | CrowdStrike | Silverfort | Qualys ETM Identity |
|------------|-----------|-------------|------------|---------------------|
| NHI Discovery | — | — | ✓ | ✓ |
| Unified Vuln + Asset + Identity Score | — | — | — | **✓ ONLY** |
| Confidence-Based Ownership Attribution | — | — | — | **✓ ONLY** |
| Closed-Loop ROC → ITSM → Revalidate | — | — | — | **✓ ONLY** |

---

## Schema Highlights

24 new fields introduced, all prefixed `nhi_` for namespace consistency:

**Risk & Scoring:** `nhi_identity_trurisk_score DECIMAL(6,2)`, `nhi_is_chokepoint BOOLEAN DEFAULT FALSE`

**Ownership:** `nhi_owner_confidence_pct DECIMAL(4,1)`, `nhi_owner_confirmed_by VARCHAR(255)`

**Remediation:** `nhi_trueconfirm_status ENUM DEFAULT 'not_triggered'`

**Compliance:** `nhi_compliance_tags VARCHAR(300)` — values: `NIS2 | NERC_CIP | IEC_62443 | SOC2 | PCI_DSS`

---

## About the Author

**Kushal Zambare** — IIoT Solutions Engineer at Covacsis Technologies (Infinite Uptime), Mumbai.

- 3+ years deploying edge gateways across 12+ manufacturing sites
- Protocols: Modbus RTU/TCP, OPC-UA, MQTT
- PLCs: Siemens S7-1200/1500, Allen-Bradley CompactLogix, Delta
- Certifications: SAFe POPM 6.0, SAFe SSM 6.0
- Targeting: Product Manager — Identity & Cybersecurity

**LinkedIn:** [linkedin.com/in/kushalzambare-pm](https://linkedin.com/in/kushalzambare-pm)

---

*This PRD is written for portfolio purposes only. Based exclusively on public materials. Not affiliated with Qualys, Inc.*
