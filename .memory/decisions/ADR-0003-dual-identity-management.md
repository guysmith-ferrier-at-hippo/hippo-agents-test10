---
id: ADR-0003
title: Dual Identity Management via GOV.UK One Login and Microsoft Entra ID
component: authentication
domain: security
tags:
- identity
- authentication
- govuk-one-login
- entra-id
- oidc
status: accepted
created: '2026-11-16'
updated: '2026-11-16'
depends_on:
- ADR-0001
supported_by: []
---

# ADR-0003: Dual Identity Management via GOV.UK One Login and Microsoft Entra ID

## Context
The Digital Licensing and Case Management Service serves two distinct user populations with fundamentally different identity requirements:
1. **Public Citizens & Business Applicants:** Members of the public requiring secure, trusted, and government-standard single sign-on without managing bespoke passwords.
2. **Internal Caseworkers & Administrators:** Civil servants and operational staff requiring role-based access control, departmental device compliance, and integration with organizational directory infrastructure.

## Decision
We will implement dual authentication strategies:
- **GOV.UK One Login:** The sole identity and authentication provider for public applicants, integrated via OpenID Connect (OIDC).
- **Microsoft Entra ID (formerly Azure AD):** The identity provider for internal caseworkers and administrators, enforcing Multi-Factor Authentication (MFA) and Conditional Access policies.

## Consequences

### Positive
- Citizens use a familiar, centralized UK government identity service with verified credentials.
- Staff access is governed by departmental access policies, joiner-mover-leaver processes, and organizational MFA.
- Completely segregates citizen identity data from internal staff authentication stores.

### Negative
- Requires maintaining two separate OIDC authentication handlers and configuration profiles within the ASP.NET Core application pipeline.

## Options Considered
1. **Bespoke Identity Store (ASP.NET Identity):** Rejected due to security burden, credential management overhead, and non-compliance with the GOV.UK One Login mandate.
2. **Single Identity Provider (Entra External ID / B2C):** Rejected because central UK government digital standards require GOV.UK One Login for citizen services.
3. **Dual Identity (GOV.UK One Login + Microsoft Entra ID):** Selected as it follows government architectural guidelines for citizen and staff isolation.