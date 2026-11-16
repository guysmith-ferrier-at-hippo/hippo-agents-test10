# Digital Licensing and Case Management Service — Test Strategy

## Overview

This test strategy defines the verification requirements, testing levels, and automated quality gates for the Digital Licensing and Case Management Service. The system supports public citizen licensing applications and internal caseworker workflow operations. The strategy guarantees high reliability, regulatory compliance, performance, and accessibility conformance.

## Test Environments & Access

- **Environments:**
  - **Local Development:** Local developer workstations using Docker containers for PostgreSQL and Azure Storage Azurite emulator.
  - **CI / Build Pipeline:** Ephemeral Linux runners executing unit, integration, and security tests on pull requests.
  - **Staging / Test Environment:** Azure App Service environment mirroring production for E2E, performance, and accessibility tests.
  - **Production:** Monitored production environment with health checks and synthetic probes.
- **Access Needs:**
  - GOV.UK One Login test credentials and integration sandbox keys (see [ASSUME-0001](assumptions/ASSUME-0001-govuk-one-login.md)).
  - GOV.UK Pay test API keys and sandbox payment cards.
  - GOV.UK Notify test API keys and simulated phone numbers.
  - Azure Key Vault access for test secret distribution (see [ASSUME-0002](assumptions/ASSUME-0002-azure-uk-south-hosting.md)).
- **Data Management:**
  - Database fixtures are created and reset per test run using isolated schemas and Respawn.
  - Test evidence files are created dynamically in temporary storage and deleted during test cleanup.
  - Production data is never copied into non-production environments.
- **CI/CD Integration:**
  - GitHub Actions runs unit tests, integration tests, and static security scans on every pull request.
  - Pull requests require passing tests, code analysis approvals, and zero high-severity vulnerabilities before merge.
  - Continuous deployment to Staging triggers automated E2E, accessibility, and smoke test suites.

## Testing Approach

| Level | Scope / Objective | Tools / Frameworks | Success Criteria | Responsibilities |
|---|---|---|---|---|
| **Unit** | Verify domain logic, business rules, entities, and calculation algorithms in isolation. | xUnit, FluentAssertions, Moq | 85% branch coverage on Domain and Application core layers; 100% pass rate. | Software Engineers |
| **Component (Web)** | Verify Razor Page models, Tag Helpers, and GDS UI markup generation. | xUnit, Bunit, AngleSharp | All GDS Tag Helpers render valid semantic HTML attributes and error states. | Software Engineers |
| **Contract** | Verify contract compatibility with GOV.UK Pay and GOV.UK Notify external API endpoints. | Pact.NET | Consumer contracts validated against provider mocks; zero breaking changes. | Software Engineers, QA |
| **Integration (Mocked)** | Verify API endpoints, MediatR handlers, and database interactions with external services mocked. | Microsoft.AspNetCore.Mvc.Testing, WireMock.NET, Testcontainers | All controller routes and validation filters pass; all external dependencies mocked. | Software Engineers, QA |
| **Integration (API / Events)** | Verify database persistence, outbox event publishing, and background worker queues with real PostgreSQL. | xUnit, Testcontainers (PostgreSQL), Respawn | Database state updates correctly; outbox messages process within 2 seconds. | Software Engineers, QA |
| **Acceptance (Functional)** | Verify business requirements, form steps, and caseworker decision flows against user stories. | SpecFlow / Reqnroll, Playwright | All feature acceptance criteria pass; Gherkin scenarios pass in CI. | QA, Software Engineers |
| **End-to-End (E2E)** | Verify complete user journeys from citizen submission and payment to caseworker determination. | Playwright (.NET) | All critical journeys pass on Chromium, Firefox, and WebKit without flakes. | QA, Software Engineers |
| **Performance (API)** | Verify API throughput, response times, and concurrency under expected peak workloads. | k6 | 95th percentile response time < 250ms at 500 RPS; zero HTTP 5xx errors. | QA, DevOps, Software Engineers |
| **Performance (Web)** | Verify web page load performance, bundle sizes, and Core Web Vitals on citizen forms. | Lighthouse CI, Playwright Tracing | Largest Contentful Paint (LCP) < 2.0s; Total Blocking Time (TBT) < 150ms. | Software Engineers, QA |
| **Security** | Static application security testing (SAST), software composition analysis (SCA), container scans. | SonarQube, Snyk, GitHub Dependabot | Zero critical or high severity vulnerabilities in code or dependencies. | Security Lead, Software Engineers |
| **Accessibility** | Verify accessibility standards across all citizen and caseworker pages. | axe-core, Playwright axe, NVDA, VoiceOver | 100% compliance with WCAG 2.2 Level AA; zero automated axe errors. | QA, Accessibility Specialist, Devs |

## Risk & Mitigation

| Risk | Mitigation |
|---|---|
| E2E test flakiness (async UI and state) | Use explicit state-based assertions (`Expect(locator).ToBeVisibleAsync()`), never use hardcoded delays (`Thread.Sleep`). |
| External API downtime (GOV.UK Pay / Notify / One Login) | Use WireMock.NET and contract tests in CI pipelines; restrict live sandbox tests to scheduled nightly runs. |
| Test data contamination | Use separate test database instances via Docker Testcontainers; isolate test cases using isolated GUIDs and schema resets. |
| Race conditions in asynchronous event processing | Poll event outbox status with bounded timeout conditions using PollingConsumer assertions. |
| Browser version drift | Pin Playwright browser versions in container images and CI workflow configuration. |

## Reviewed by

| Name | Role | Approved | Date |
|---|---|---|---|
| Technical Lead | Tech Lead | [x] | 2026-11-16 |
| Quality Assurance Lead | Test Lead | [x] | 2026-11-16 |
| Product Manager | Product Manager | [x] | 2026-11-16 |
