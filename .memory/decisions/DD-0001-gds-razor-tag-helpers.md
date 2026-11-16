---
id: DD-0001
title: Adopt GovUk.Frontend.AspNetCore for UI Component Rendering
component: frontend-ui
domain: ui-design
tags:
- gds
- design-system
- tag-helpers
- razor-pages
status: accepted
created: '2026-11-16'
updated: '2026-11-16'
depends_on:
- ADR-0001
supported_by: []
---

# DD-0001: Adopt GovUk.Frontend.AspNetCore for UI Component Rendering

## Context
Citizen-facing digital services in the UK public sector must strictly follow the GOV.UK Design System HTML markup, CSS styling, and JavaScript behaviors. We need a reliable mechanism to render GDS components in ASP.NET Core without manually copying HTML fragments into every Razor view.

## Options Considered
1. **Manual HTML copying:** Razor templates hand-craft GDS HTML markup from scratch. High risk of missing accessibility tags and difficult to maintain when GOV.UK Frontend updates.
2. **Client-side React with GOV.UK React:** SPA client interacting with ASP.NET Core API. Adds heavy client runtime bundle, complicates server-side progressive enhancement, and reduces page load speed.
3. **GovUk.Frontend.AspNetCore Library:** Mature, open-source ASP.NET Core Tag Helper package wrapping the official GOV.UK Frontend npm package.

## Evaluation
- **Accessibility:** GovUk.Frontend.AspNetCore automatically generates required ARIA attributes, error linking, and heading hierarchy.
- **Maintainability:** Updates to the upstream GOV.UK design tokens are incorporated via package updates.
- **Performance:** Server-side rendered HTML delivers optimal initial page load times and zero-JS accessibility.

## Decision
We adopt `GovUk.Frontend.AspNetCore` for all public citizen-facing views, backed by the official `govuk-frontend` asset pipeline.

## Consequences
- Developers write declarative Razor Tag Helpers (`<govuk-input>`, `<govuk-radios>`, `<govuk-button>`) that automatically emit compliant GDS markup.
- All public pages guarantee zero-javascript base accessibility and full progressive enhancement.