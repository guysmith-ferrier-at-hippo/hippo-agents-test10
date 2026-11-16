---
id: ASSUME-0003
title: Statutory Ten Working Day Casework Decision SLA
component: case-workflow
domain: licensing-policy
tags:
- sla
- casework
- statutory-timeframe
- notifications
status: unresolved
created: '2026-11-16'
updated: '2026-11-16'
depends_on: []
supported_by: []
---

# ASSUME-0003: Statutory Ten Working Day Casework Decision SLA

## Assumption Description
We assume the target service level agreement (SLA) for statutory license determination is 10 working days from valid fee receipt and document verification.

## Rationale
Operational stakeholders require a target turnaround time to configure automated reminder notifications, escalation flags, and dashboard performance metrics for casework managers.

## Context & Boundaries
- Clock begins when application submission passes automated validation and payment clears.
- Clock pauses if caseworkers formally issue a "Request for Further Information" (RFI) to the applicant.

## Impact if Invalid
If regulatory statutory timeframes are different (e.g., 20 or 28 calendar days), timer calculations, escalation rules, and notification cadences must be adjusted in the workflow engine.

## Verification Method
Confirm statutory timeframes with regulatory policy owners and legal counsel during the alpha review.