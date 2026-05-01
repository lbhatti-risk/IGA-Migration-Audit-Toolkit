
# IGA Migration Audit Toolkit

This repository contains frameworks and risk-based audit programmes for managing the transition from manual User Access Reviews (UAR) to automated Identity Governance and Administration (IGA) and Privileged Access Management (PAM) platforms.

## Overview

As global organisations migrate from spreadsheet-based reviews to automated polling tools like **CyberArk** and **Veza**, the primary audit risk shifts from "human error in review" to the "integrity of the automated query." 

This toolkit provides structured methodology for auditors to validate technical query logic, ensure population completeness (IPE), and manage the unique risks associated with hybrid migration phases.

## Featured Artefacts

### [IGA Migration Risk Matrix](migration-risk-matrix.md)
A comprehensive matrix covering 11 critical risk points identified during manual-to-automated migrations. It categorises risks into:
* **IPE Integrity**: Validating that automated queries capture the full technical population.
* **Logic Completeness**: Identifying custom objects or roles that standard tool polling might miss.
* **Operational SLAs**: Monitoring fulfillment lead times and synchronisation between HR feeds and security vaults.
* **Segregation of Duties (SoD)**: Addressing administrative role conflicts within automated workflows.

## Regulatory Alignment

The methodologies in this toolkit are designed to align with:
* **DORA (Digital Operational Resilience Act)**: Specifically the ICT Third-Party Risk and Operational Resilience pillars.
* **SOX / ITGC**: Addressing Completeness and Accuracy (C&A) for automated reporting.
* **NIST AI RMF / EU AI Act**: Principles applied to automated identity decision-making.

## A Note on Confidentiality

All materials in this repository have been fully anonymised, restructured, and utilise synthetic data. No content originates from a live client engagement or proprietary internal system. These documents represent my personal methodologies and professional viewpoint on industry best practices.

---
**Return to main profile**: [github.com/lbhatti-risk](https://github.com/lbhatti-risk)  
**Connect on LinkedIn**: [linkedin.com/in/layla-b-3470a31b8](https://www.linkedin.com/in/layla-b-3470a31b8)
