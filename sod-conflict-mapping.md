# Segregation of Duties (SoD) Conflict Mapping — IGA and PAM Environments

This document provides a structured SoD conflict mapping framework for auditors assessing Identity Governance and Administration (IGA) and Privileged Access Management (PAM) environments during manual-to-automated migrations.

All scenarios are synthetic and based on common control design patterns observed across financial services and critical infrastructure environments. No content originates from a live client engagement.

---

## Framework Overview

SoD conflicts in automated IGA/PAM environments differ from traditional SoD in two ways:

1. **Administrative role conflicts** — where a user holds both operational and review privileges within the same platform (e.g., provisioning access and approving their own UAR).
2. **Query logic conflicts** — where the automated tool that produces the UAR population is configured or maintained by the same team being reviewed.

Both categories require explicit audit testing and documented compensating controls.

---

## SoD Conflict Matrix

| Conflict ID | Role A | Role B | Conflict Type | Risk | Inherent Rating | Compensating Control | Residual Rating |
|-------------|--------|--------|---------------|------|-----------------|----------------------|-----------------|
| SoD-01 | UAR Reviewer | Privileged Platform Admin | Administrative | Reviewer can approve their own privileged access during UAR | High | Independent secondary review by separate business line; evidence required | Medium |
| SoD-02 | Access Provisioner | Access Approver | Administrative | Same individual grants and approves access requests | High | Dual-team provisioning structure with documented RACM; walkthrough evidence required | Medium |
| SoD-03 | IGA Platform Config Admin | UAR Population Owner | Logic Conflict | Individual controlling query logic also defines who appears in the review population | High | IPE integrity validation by independent auditor; query output reconciled against authoritative HR/AD source | Medium |
| SoD-04 | Vault Administrator | Session Recording Reviewer | Administrative | Individual can access session recordings of their own privileged sessions | Medium | Automated log forwarding to SIEM; SIEM access restricted to separate security operations team | Low |
| SoD-05 | Change Approver | Change Implementer | Administrative | Individual approves and implements the same platform change | High | Peer review gate in change management workflow; system-enforced approval sequencing in ServiceNow/equivalent | Medium |
| SoD-06 | Third-Party MSP Operator | Internal UAR Reviewer | Administrative | External managed service provider holds privileged access not captured in UAR scope | High | Third-party users included in UAR population; confirmed via independent query against all privileged AD groups | Medium |
| SoD-07 | Password Rotation Config Admin | Account Owner | Logic Conflict | Individual responsible for rotation policy also owns accounts subject to that policy | Medium | Service account rotation configured as platform default; exceptions logged and approved | Low |
| SoD-08 | Access Deprovisioner | Leaver Notification Owner | Administrative | Individual processing leaver requests also receives HR termination notifications | Medium | HR system automated feed to IGA platform; manual override requires dual sign-off | Low |

---

## Audit Testing Guidance

### SoD-01 and SoD-02 — Administrative Role Conflicts

**What to obtain:**
- Full provisioned user list from the IGA/PAM platform
- UAR reviewer assignment log for the audit period
- RACM (Risk and Control Matrix) documenting the dual provisioning team structure

**What to test:**
- Cross-reference provisioned users against UAR reviewer list
- Confirm that no reviewer is assigned to approve their own access
- Where exceptions exist, confirm secondary review evidence

**Common finding:** Sole reviewer holds a privileged role within the platform being reviewed. Compensating control (secondary review) is verbal rather than documented. Raises a control design exception.

---

### SoD-03 and SoD-07 — Logic Conflicts (IPE Risk)

**What to obtain:**
- Automated query used to generate UAR population (e.g., Veza query output, CyberArk report config)
- Access rights of the individual who configured the query
- Independent AD or HR extract covering all privileged role categories

**What to test:**
- Confirm query logic covers all privileged categories defined in control design
- Reconcile query output against independent extract — any delta is an IPE exception
- Confirm query configuration access is restricted to a separate admin team

**Common finding:** Query configured by PAM admin who also holds a privileged role. No independent reconciliation of query output against AD performed during the period.

---

### SoD-06 — Third-Party / MSP Conflicts

**What to obtain:**
- Contract or statement of work defining MSP scope
- List of accounts provisioned to MSP operatives
- Confirmation of whether MSP accounts are included in UAR scope

**What to test:**
- Confirm MSP accounts appear in both provisioning population (C2 equivalent) and UAR population (C3 equivalent)
- Where MSP transitioned mid-period, confirm inclusion from transition date

**Common finding:** MSP accounts provisioned under a separate AD OU not captured by the standard UAR query. Results in a completeness gap in the UAR population.

---

## Escalation Criteria

Raise to senior management / client before issuing if:

- A sole reviewer is identified with no documented secondary review process
- Query logic is maintained by a team member whose own access appears in the output
- Third-party accounts are confirmed absent from the UAR population for the full period
- Compensating controls are verbal rather than evidenced in the workpaper trail

---

## Regulatory Alignment

| Regulation / Framework | Relevant Requirement |
|------------------------|----------------------|
| SOX / ITGC | SoD controls are key controls for access management; exceptions require management response and compensating evidence |
| DORA (Art. 9) | ICT systems access governed by least-privilege; third-party ICT providers subject to equivalent access controls |
| ISO 27001:2022 (A.5.3) | Segregation of duties shall be implemented to reduce opportunities for unauthorised or unintentional modification or misuse |
| NIST CSF (PR.AC-4) | Access permissions and authorisations managed incorporating least privilege and separation of duties |

---

*All scenarios in this document are synthetic. Data has been restructured and anonymised. Nothing in this document originates from a live client engagement or proprietary system.*

*Author: Layla Bhatti — Digital Audit & IT Risk | github.com/lbhatti-risk*
