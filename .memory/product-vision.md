# 🧭 Product Vision Document

## 1. Product Overview

**Product Name:**  
Digital Licensing and Case Management Service

**Author / Owner:**  
Agile Delivery Team and Technical Leadership (`hippo-agents-test10`)

---

## 2. Vision Statement

Deliver an accessible, reliable, and secure digital service that lets UK citizens and businesses apply for and manage regulatory licenses online, while giving caseworkers clear tools to process submissions quickly and accurately.

---

## 3. Problem Statement

Current regulatory licensing procedures depend on paper forms, manual spreadsheets, and disconnected email communications.

- **Who experiences the problem?**
  - UK citizens and businesses who submit statutory license applications.
  - Regulatory caseworkers and compliance managers who review, approve, or reject applications.
- **What is the impact of the problem today?**
  - Applicants wait long periods without visibility into application status.
  - Caseworkers spend excessive time doing manual data entry and document checks.
  - High error rates increase rework and administrative costs.
- **Why does solving this matter?**
  - A modern digital service speeds up processing, lowers operational cost, improves regulatory compliance, and meets UK Government Digital Service (GDS) standards.

---

## 4. Target Users / Audiences

| Persona | Description | Key Needs / Goals |
|---|---|---|
| Citizen Applicant | Individual UK resident or sole trader applying for a statutory license. | Complete applications easily on mobile or desktop devices. Upload proof files. Track application progress. |
| Business Representative | Agent or employee who manages multiple licenses for a registered company. | Submit bulk or corporate applications. View team submissions. Pay fees securely online. |
| Regulatory Caseworker | Operational officer who checks application evidence and makes license determinations. | View prioritized work queues. Validate uploaded documents. Request additional details. Issue approvals or refusals. |
| Service Manager / Auditor | Compliance manager who oversees service performance and statutory compliance. | Access audit trails. Monitor turnaround times against statutory service levels. Export regulatory reports. |

---

## 5. Product Goals & Outcomes

| Goal | Metric / KPI | Desired Outcome |
|---|---|---|
| High Digital Adoption | Digital take-up rate >= 85% within 12 months | Majority of applicants submit applications through the digital channel. |
| Rapid Application Completion | Median submission time <= 15 minutes | Clear guidance and accessible form fields prevent user hesitation. |
| Fast Processing Turnaround | Casework determination completed within 10 working days for 90% of cases | Caseworkers process cases without administrative delays. |
| Accessible to All Users | Zero WCAG 2.2 Level AA accessibility violations | Fully accessible service usable with screen readers, speech input, and keyboards. |
| High Service Reliability | Service availability >= 99.9% during core hours | Stable platform with minimal downtime for public applicants. |

---

## 6. Key Features / Capabilities

- **GOV.UK One Login Integration:** Secure authentication and identity verification for citizens and business operators.
- **Guided Form Steps:** Step-by-step application questions following the GOV.UK Design System patterns.
- **Document Evidence Upload:** Secure upload, virus scanning, and storage for proof of identity and qualification documents.
- **Integrated Fee Payments:** Seamless payment processing via GOV.UK Pay integration.
- **Automated Notifications:** SMS and email updates sent to applicants via GOV.UK Notify at key workflow milestones.
- **Caseworker Operations Console:** Central dashboard with queue filtering, task allocation, evidence review, and decision recording.
- **Comprehensive Audit Trail:** Immutable event logs recording every application update, caseworker review, and determination.

---

## 7. Value Proposition

| For (user type) | Who want to (need) | Our product (solution) | Unlike (alternative) |
|---|---|---|---|
| UK Citizen and Business Applicants | Apply for and track statutory licenses easily without paper forms | A secure, responsive GOV.UK digital application service | Manual paper forms, postal submissions, and unverified email communications |
| Regulatory Caseworkers | Review applications and make determinations efficiently | An integrated case management console with automated queues and document viewers | Disconnected spreadsheets, shared network folders, and manual physical paper files |
| Regulatory Leadership | Ensure compliance with statutory timelines and government standards | An observable platform with real-time audit logging and analytics dashboards | Legacy siloed databases with incomplete metrics and slow manual reporting |

---

## 8. Constraints / Assumptions

### Assumptions
- [ASSUME-0001: Use GOV.UK One Login for Citizen Identity Authentication](assumptions/ASSUME-0001-govuk-one-login.md) - Citizen authentication will use the central GOV.UK One Login service via OpenID Connect.
- [ASSUME-0002: Cloud Hosting on Microsoft Azure UK South](assumptions/ASSUME-0002-azure-uk-south-hosting.md) - All cloud infrastructure, managed relational databases, and file stores will reside in Azure UK South for UK data residency compliance.
- [ASSUME-0003: Statutory Ten Working Day Casework Decision SLA](assumptions/ASSUME-0003-statutory-casework-sla.md) - Service workflow targets a 10 working day determination turnaround from valid submission to decision.

### Constraints
- **Regulatory Compliance:** Must comply with UK statutory licensing regulations and GDPR / Data Protection Act 2018.
- **Accessibility Standard:** Must satisfy public sector accessibility regulations (WCAG 2.2 Level AA conformance).
- **Service Standard:** Must satisfy the 14 points of the UK Government Digital Service (GDS) Standard for public beta assessment.
- **Data Residency:** All personal data, evidence uploads, and database backups must remain within United Kingdom borders.

---

## 9. Success Metrics

- **Primary metric(s):**
  - End-to-end digital completion rate >= 85%.
  - Statutory determination SLA compliance >= 90% within 10 working days.
- **Secondary metric(s):**
  - First-time pass rate for document validation >= 80%.
  - Customer satisfaction score (CSAT) >= 80%.
  - Payment processing success rate >= 98%.
- **Qualitative indicators:**
  - Positive feedback from public user research sessions.
  - Reduced caseworker stress and fewer manual handovers reported in operational retrospectives.

---

## 10. Stakeholders

| Role | Name / Team | Interest / Contribution |
|---|---|---|
| Senior Responsible Owner (SRO) | Departmental Licensing Director | Overall business accountability, regulatory compliance, and budget approval. |
| Service Owner | Digital Delivery Lead | Product direction, backlog prioritization, and GDS Service Standard compliance. |
| Technical Lead & Architect | Software Engineering Team | Technical architecture, code quality, infrastructure automation, and security posture. |
| Casework Operations Lead | Licensing Operations Team | Operational requirements, caseworker workflow design, and operational acceptance. |
| Information Security / DPO | Information Assurance Team | Data protection compliance, threat assessment, and privacy impact approval. |

---

## 11. Risks & Open Questions

- **Risk: Identity Verification Delays:** Applicants without standard UK identity documents may fail automatic One Login verification.
  - *Mitigation:* Implement alternative offline verification path with manual caseworker document review.
- **Risk: Peak Load Submission Spikes:** Renewal deadlines could generate temporary traffic spikes.
  - *Mitigation:* Use scalable cloud application containers and asynchronous queue workers.
- **Open Question:** Will statutory inspection partners require direct API access to case determination records during Phase 1?
  - *Validation Path:* Validate partner requirements during Beta discovery interviews.

---

## 12. References

- [UK Government Service Standard](https://www.gov.uk/service-manual/service-standard)
- [GOV.UK Design System](https://design-system.service.gov.uk/)
- [WCAG 2.2 Accessibility Guidelines](https://www.w3.org/TR/WCAG22/)
- [GOV.UK One Login Technical Guidance](https://docs.sign-in.service.gov.uk/)
- [GOV.UK Notify Documentation](https://www.notifications.service.gov.uk/)
- [GOV.UK Pay Documentation](https://www.payments.service.gov.uk/)
