---
id: ADR-0001
title: Adopt Modular Monolith Architecture
component: core-architecture
domain: architecture-pattern
tags:
- architecture
- modular-monolith
- dotnet
- domain-boundaries
status: accepted
created: '2026-11-16'
updated: '2026-11-16'
depends_on: []
supported_by: []
---

# ADR-0001: Adopt Modular Monolith Architecture

## Context
The Digital Licensing and Case Management Service requires rapid delivery, strict transaction boundaries between applications and payments, and unified operational oversight. The system has two primary web user experiences: a citizen-facing portal and a caseworker operations console, backed by core business logic and relational storage.

Microservices add operational complexity, distributed transaction hurdles, network latency, and deployment overhead that are not warranted at current transaction volumes. A monolithic architecture without clear module boundaries risks tight coupling, poor maintainability, and regression hazards.

## Decision
We will build the system as a **Modular Monolith** using ASP.NET Core (.NET 9 / C#). 
- Boundaries between domain modules (Applications, Casework, Payments, Notifications, Audit) are strictly enforced through internal module interfaces and separate project boundaries.
- Cross-module communication uses explicit in-process mediator commands/queries or domain events.
- Database access is partitioned by module schema within a single shared PostgreSQL database instance.

## Consequences

### Positive
- Single deployable unit simplifies CI/CD pipelines, local development, and monitoring.
- Strong compile-time interface enforcement prevents hidden dependencies between domains.
- Local transactions ensure consistency across application submission and payment tracking without distributed transaction coordinators.
- Simplifies evolution: modules can be separated into distinct microservices later if scaling demands require it.

### Negative
- All modules deploy together, requiring coordinated release verification.
- Shared database instance requires discipline to avoid cross-schema joins at the database layer.

## Options Considered
1. **Microservices Architecture:** Rejected due to excessive operational complexity, distributed data consistency challenges, and infrastructure costs for an initial Alpha/Beta service.
2. **Traditional Monolith (Unstructured):** Rejected due to risk of tight coupling and erosion of architectural boundaries over time.
3. **Modular Monolith:** Selected for simplicity, boundary isolation, and evolutionary flexibility.