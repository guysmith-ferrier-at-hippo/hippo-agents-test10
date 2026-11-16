---
id: ASSUME-0002
title: Cloud Hosting on Microsoft Azure UK South
component: infrastructure
domain: infrastructure
tags:
- azure
- hosting
- data-residency
- compliance
status: unresolved
created: '2026-11-16'
updated: '2026-11-16'
depends_on: []
supported_by: []
---

# ASSUME-0002: Cloud Hosting on Microsoft Azure UK South

## Assumption Description
We assume the service will deploy to Microsoft Azure UK South data centre regions to satisfy UK public sector data residency and compliance rules.

## Rationale
UK government data residency mandates require all citizen data, document evidence, and audit logs to remain within the United Kingdom. Azure UK South provides complete compliance certifications and managed services required for high availability.

## Context & Boundaries
- All application services, managed PostgreSQL databases, and document storage blobs reside in Azure UK South.
- Disaster recovery paired region is Azure UK West.

## Impact if Invalid
If AWS or Crown Hosting is mandated instead, infrastructure-as-code scripts (Terraform/Bicep) and CI/CD deployment pipelines must be re-authored.

## Verification Method
Review department cloud architecture guidelines and formalize hosting approval with the departmental technical design authority (TDA).