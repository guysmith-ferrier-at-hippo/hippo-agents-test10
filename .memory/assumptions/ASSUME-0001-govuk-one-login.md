---
id: ASSUME-0001
title: Use GOV.UK One Login for Citizen Identity Authentication
component: licensing-portal
domain: identity-and-access
tags:
- authentication
- govuk-one-login
- identity
- gds
status: unresolved
created: '2026-11-16'
updated: '2026-11-16'
depends_on: []
supported_by: []
---

# ASSUME-0001: Use GOV.UK One Login for Citizen Identity Authentication

## Assumption Description
We assume the service will integrate with GOV.UK One Login as the standard identity verification and authentication provider for UK citizens.

## Rationale
GOV.UK One Login is the mandated authentication platform across UK central government departments for citizen-facing digital services. Using One Login provides consistent identity verification, prevents duplicate citizen records, and adheres to GDS standards.

## Context & Boundaries
- Citizen users authenticate through GOV.UK One Login OpenID Connect (OIDC).
- Internal caseworkers use corporate Microsoft Entra ID (Azure AD), not One Login.

## Impact if Invalid
If GOV.UK One Login integration is delayed or not approved for the initial Beta rollout, the project must implement a temporary OIDC bridge or email-based magic link authentication, adding delivery effort and migration overhead.

## Verification Method
Validate onboarding and integration access in the GOV.UK One Login integration environment with the government onboarding team before the private Beta release.