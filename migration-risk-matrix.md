# IGA Migration Risk Matrix: Manual-to-Automated Controls

This matrix outlines 11 critical risks identified during the transition from manual User Access Reviews (UAR) to automated Identity Governance and Administration (IGA) platform polling. 

## Framework Overview
As organisations migrate to tools like CyberArk and Veza, the primary audit risk shifts from "human error in review" to "integrity of the automated query." This framework focuses on the validation of automated logic and the remediation of legacy process gaps.

| Risk ID | Control Category | Risk Description | Recommended Mitigation / Audit Step |
|:--- |:--- |:--- |:--- |
| **01** | Account Hygiene | Privileged service accounts not subject to mandatory 24-hr rotation policies. | Enforce CPM onboarding and validate rotation status via automated exception reporting. |
| **02** | Population Integrity | Legacy manual reports used for baseline reviews fail to capture all user tiers (e.g., Ops Lvl 2). | Reconcile manual source data against IGA tool output to identify "fallen through" populations. |
| **03** | Governance | Safe/Container naming conventions are not followed, leading to discovery gaps. | Implement automated naming validation at the point of container creation. |
| **04** | Control Design | Control wording remains aligned with legacy manual processes rather than automated workflows. | Update control narratives to reflect technical polling logic and automated remediation steps. |
| **05** | IPE Integrity | Automated query logic (e.g., SQL/JSON) has not been validated against the full technical environment. | Perform full Completeness and Accuracy (IPE) validation on all queries used for reporting. |
| **06** | Query Logic | Specific "Custom Roles" or objects are excluded from the tool's standard polling logic. | Conduct a line-by-line code review of tool-specific queries to ensure all custom objects are captured. |
| **07** | Fulfillment SLA | Service requests for privileged access exceed the defined internal SLA (e.g., 3-day target). | Establish real-time dashboards to monitor fulfillment lead times and escalate overdue requests. |
| **08** | Segregation of Duties | Administrative role conflicts allow users (e.g., Safe Owners) to bypass approval workflows. | Enforce strict SoD policies within the IGA tool to prevent users from approving their own access. |
| **09** | Offboarding Sync | HR system feeds (e.g., Oracle HCM) have a high latency, leading to delayed access removal. | Optimise API/feed frequency to ensure near real-time synchronisation between HRIS and IGA systems. |
| **10** | Process Visibility | New containers or Safes are created without assigned ownership, creating a monitoring gap. | Implement mandatory ownership fields and automated alerts for any "orphan" containers identified. |
| **11** | Exception Management | Accounts whitelisted from standard rotation or security policies are not periodically reviewed. | Define a formal, quarterly review process specifically for all control exceptions and whitelists. |

---
*Disclaimer: This matrix is for methodology demonstration only and utilises synthetic audit findings. It does not represent any specific client environment.*
