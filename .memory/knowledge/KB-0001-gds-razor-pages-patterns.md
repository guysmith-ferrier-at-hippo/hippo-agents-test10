---
id: KB-0001
title: Implementing GDS Form Patterns in ASP.NET Core Razor Pages
component: frontend-ui
domain: gds-compliance
tags:
- gds
- razor-pages
- accessibility
- forms
- wcag
status: validated
created: '2026-11-16'
updated: '2026-11-16'
depends_on:
- ADR-0001
supported_by: []
---

# KB-0001: Implementing GDS Form Patterns in ASP.NET Core Razor Pages

## Summary
When building UK government digital services using ASP.NET Core Razor Pages, all citizen-facing UI components must conform to the GOV.UK Design System specifications.

## Key Points
1. **Error Summary and Field Association:**
   - Every validation failure must render in the `govuk-error-summary` box at the top of the page.
   - The error summary link href must match the input element `id` exactly (e.g., `#Applicant_DateOfBirth_Day`).
   - Inputs must include `aria-describedby` referencing both the field hint ID and error message ID.
2. **Form Group Validation Styling:**
   - Enclosing `div.govuk-form-group` must append the `govuk-form-group--error` CSS class when model validation fails.
   - Text inputs must receive the `govuk-input--error` class.
3. **Tag Helpers:**
   - Implement custom ASP.NET Core Tag Helpers for standard GDS components (`<govuk-input>`, `<govuk-radios>`, `<govuk-button>`, `<govuk-error-summary>`) to prevent markup errors and ensure consistent semantic HTML generation.

## Why It Matters
Automated accessibility linters and GDS service assessments strictly evaluate keyboard focus management and screen reader announcements on validation errors. Failing to correctly associate error messages with form fields causes non-compliance with WCAG 2.2 AA.

## Applicability
Applies to all public-facing Razor Pages and form components across the Digital Licensing and Case Management Service.