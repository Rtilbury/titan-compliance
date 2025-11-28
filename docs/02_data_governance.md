Titan-Core & Titan-X Compliance Pack
Document 2 — Data Governance

Version: 1.0
Applies to: Titan-Core (API) & Titan-X (Platform Integrations)
Status: Approved for public + enterprise use

1. Purpose & Scope
1.1 Purpose of this document

This document explains how data is handled, protected, and governed when using Titan-Core and Titan-X. It supports:

EU AI Act General-Purpose AI (GPAI) obligations

Data protection and privacy assessments (e.g. GDPR, UK GDPR)

Vendor due diligence and security questionnaires

Internal governance and risk management for integrators

It is not legal advice. Integrators remain responsible for their own legal compliance.

1.2 Systems in scope

This document covers:

Titan-Core – the behavioural telemetry API

Titan-X – the broader platform that consumes Titan-Core signals

It focuses on:

what Titan is designed to process,

what Titan is explicitly not designed to process, and

how responsibilities are shared between Titan and integrators.

1.3 Relationship to other documents

Read this document alongside:

01_system_overview.md – high-level architecture & purpose

04_logging_and_traceability.md – detailed logging model

06_cybersecurity_and_robustness.md – security controls

08_post_market_support.md – incidents & ongoing support

2. Data Categories & Telemetry Model
2.1 Core principle: behavioural telemetry, not identity

Titan is designed around a behavioural telemetry model.
By default, Titan operates on numeric signals and technical context, not on identity, personal, or content data.

2.2 Typical data categories processed by Titan-Core

Required:

session_id – a pseudonymous identifier chosen by the integrator

Behavioural metrics (numeric), for example:

friction score

hesitation duration

pace score

Optional:

user_id – a pseudonymous identifier (recommended, not required)

Context object (free-form JSON), for example:

page / view name (e.g. "pricing_page")

UI element identifiers (e.g. "cta_button")

non-personal technical details

2.3 Data categories that Titan is not designed to process

Titan is not intended to receive:

names, emails, phone numbers, addresses

government identifiers (e.g. NI numbers, social security numbers)

biometric data (face, voice, gait, fingerprints, etc.)

health information or medical records

financial account numbers or payment details

special category data as defined by GDPR (e.g. political views, religion, sexual orientation)

These categories should be excluded or pseudonymised by integrators before any data is sent to Titan.

2.4 Custom telemetry fields

Integrators may define additional numeric telemetry fields (for example, a custom “scroll_depth” score). These:

must be documented internally by the integrator,

must not encode direct personal identifiers,

remain fully under the integrator’s control and responsibility.

3. Data Lifecycle
3.1 Ingestion

Data enters Titan-Core via authenticated API calls to:

/v1/start

/v1/event

/v1/end

Titan validates basic structure and types, then processes the signals to maintain rolling metrics for the relevant session.

3.2 Processing

Processing includes:

tracking per-session counters and averages

computing friction/hesitation/pace metrics

generating deterministic session summaries

providing helper responses from Support / Marketing modules

No model is trained on customer telemetry in v1.
No long-term profiles of individuals are created by Titan.

3.3 Storage & retention (default model)

Titan v1 is designed to operate in a stateless, request–response pattern:

Rolling metrics are held in memory for the lifetime of the session

Once a session is ended, any in-memory state can be discarded

Titan-Core does not require persistent storage of customer data

Integrators may choose to log or store telemetry data in their own infrastructure for analytics or audit purposes. That storage is entirely under the integrator’s control.

3.4 Deletion

Because Titan does not require persistent storage by default, standard operation does not require deletion workflows within Titan itself.

If a deployment introduces storage (for example, for extended analytics), the integrator must:

define retention periods,

implement deletion and anonymisation procedures,

ensure data subject rights can be respected (where applicable).

3.5 Aggregation & anonymisation

Where integrators aggregate telemetry (e.g. across thousands of sessions):

Aggregation should be performed on pseudonymised or anonymous datasets

Reports and dashboards should not expose identifiable user-level raw data

Aggregation can significantly reduce privacy risk and compliance burden

4. Roles & Responsibilities
4.1 Titan as a technical provider

Titan-Core and Titan-X act as technical components that process telemetry under the instructions of the integrator.

In most deployments:

Titan is a tool or component within the integrator’s architecture

The integrator defines the lawful basis, scope, and use of the telemetry

The integrator is responsible for any classification under GDPR or similar laws

4.2 Integrator as controller / system provider

The integrator typically acts as:

the data controller (GDPR language) or organisational equivalent, and

the AI system provider for any final product that incorporates Titan

The integrator is responsible for:

defining and documenting the intended use

ensuring collection is lawful, fair, and transparent

configuring Titan so it receives only appropriate telemetry

providing user-facing notices (where applicable)

ensuring downstream decisions comply with law and policy

4.3 Shared responsibilities

Both Titan and integrators share responsibility for:

implementing appropriate technical and organisational measures

maintaining safe defaults and clear documentation

responding appropriately in case of suspected misuse or incidents

5. Lawful Basis & Transparency (Integrator Responsibility)
5.1 Lawful basis for processing

Titan does not define or enforce a lawful basis.
The integrator must determine and document the relevant basis, for example:

legitimate interests

performance of a contract

consent (where appropriate)

The choice depends on the integrator’s use case, jurisdiction, and user base.

5.2 Transparency to end users

Where applicable, the integrator should ensure that privacy notices and user-facing documentation explain:

what behavioural telemetry is collected

why it is collected (e.g. to improve usability, reduce friction, detect bugs)

how it is processed and for how long

whether any automated actions are taken using these metrics

5.3 Data protection impact assessments (DPIA)

If an integrator uses Titan within a context where DPIAs are required (e.g. large-scale monitoring, or high-risk sectors), they should:

document Titan as a component in the DPIA

clearly state that Titan processes behavioural telemetry, not direct identifiers

reference this Data Governance document as supporting material

6. Data Minimisation & Privacy by Design
6.1 Default minimisation

Titan is designed so that:

it does not require personal data,

it does not require content or message bodies,

it can operate fully on pseudonymous session IDs and numeric telemetry.

This supports strong data minimisation by default.

6.2 Recommended patterns

Integrators are strongly encouraged to:

use pseudonymous user identifiers (e.g. random UUIDs)

avoid sending any fields that directly identify an individual

avoid embedding personal data in “context” fields

strip referrers, URLs, or free-text that might inadvertently contain PII

6.3 Disallowed patterns

Integrators should not:

send raw user names, emails, phone numbers, addresses

send free-text fields containing user messages or documents

use Titan telemetry to infer special category data

If in doubt, the safe position is: do not send the field.

6.4 Configuration boundaries

Titan intentionally exposes a limited surface area for configuration in v1. This reduces the risk of misconfiguration that could lead to unwanted data exposure.

7. Storage, Retention & Backups
7.1 Titan default storage posture

The Titan-Core v1 design assumes:

processing in memory

no persistent telemetry storage by default

no re-use of telemetry data for training or profiling

Any change to this model in future major versions will be:

clearly documented,

versioned, and

accompanied by updated compliance documentation.

7.2 Integrator storage responsibilities

If integrators choose to store Titan telemetry (for example in a data warehouse or logging system), they are responsible for:

defining and enforcing retention schedules

ensuring backups respect the same schedules

implementing deletion/anonymisation processes

encrypting data at rest and in transit

7.3 Retention guidelines (non-binding)

As a general principle:

telemetry that is only needed for real-time adaptation should be kept briefly

telemetry used for aggregated analytics should be anonymised as early as possible

Exact retention periods depend on the integrator’s purpose, legal requirements, and internal policies.

8. Access Control & Security (High-Level)

Detailed technical controls are documented in 06_cybersecurity_and_robustness.md. This section summarises governance-level expectations.

8.1 Access to Titan APIs

Integrators should:

protect API keys and credentials

limit access to backend services that legitimately need to call Titan

avoid exposing keys in client-side code

8.2 Internal access at integrator side

Telemetry stored by integrators should:

be accessible on a need-to-know basis only

sit behind role-based access controls (RBAC)

be logged and monitored for unusual access patterns

8.3 Multi-tenant deployments

Where integrators operate multi-tenant systems (e.g. SaaS platforms), they must ensure:

telemetry associated with one tenant is isolated from others

any dashboards or exports are scoped to the correct tenant

9. Cross-Border Data Transfers
9.1 General position

Because Titan focuses on non-personal behavioural telemetry, many cross-border transfer restrictions are reduced or eliminated. However:

integrators are responsible for determining whether their telemetry qualifies as personal data under local law, and

for implementing appropriate safeguards (e.g. SCCs, IDTA, or equivalent) where required.

9.2 Deployment regions

Integrators should document:

where their Titan integration is deployed (e.g. EU, UK, US regions)

where any stored copies of telemetry are located

This helps support local residency, sovereignty, or sector-specific requirements.

10. Data Subject Rights (If Applicable)
10.1 Applicability

In many Titan deployments, no personal data is processed, and data subject rights (access, rectification, erasure, etc.) may not directly apply.

Where integrators choose to store identifiable telemetry (against our default recommendation), they must:

ensure data can be located per data subject (e.g. by pseudonymous ID),

provide access/erasure/portability mechanisms where legally required, and

ensure these mechanisms extend to any Titan-related telemetry they store.

10.2 Titan’s role

Titan itself does not maintain long-term records linked to individuals and therefore does not provide direct interfaces for data subject requests. Any rights must be exercised via the integrator.

11. Third-Party Processors & Sub-Processors
11.1 Titan’s upstream dependencies

Where Titan relies on infrastructure or service providers (for example, hosting providers), these are:

treated as sub-processors at the infrastructure level, and

managed via contracts, security controls, and standard practices described in 06_cybersecurity_and_robustness.md.

11.2 Integrator third parties

If integrators forward Titan telemetry to other services (for storage, analytics, or visualisation), those services:

become third-party processors within the integrator’s environment, and

must be assessed, contracted, and governed by the integrator.

12. Children & Sensitive Contexts
12.1 Use with children or vulnerable groups

Titan is not specifically designed for children, but may be used in applications whose end users include children or vulnerable groups.

In such cases, integrators should:

avoid sending any identifiers or content relating to children

restrict telemetry to technical behavioural signals (e.g. click timing, UI flows)

ensure that any resulting system complies with child protection, safeguarding, and local educational or healthcare regulations as applicable

12.2 Sensitive sectors

Where Titan is deployed in sensitive domains (e.g. health, education, employment, credit, public services), the integrator should:

treat Titan as a technical component in a broader high-stakes system

ensure that all high-risk or safety-critical assessments are performed by the integrator’s own models or logic, not by Titan

document Titan clearly in their system risk register and DPIAs

13. Data Incidents & Breach Handling
13.1 Incident categories

Data incidents relevant to Titan telemetry may include:

unauthorised access to stored telemetry within the integrator’s system

misconfiguration leading to personal data being sent to Titan

unexpected exposure of API keys or credentials

13.2 Integrator responsibilities

Integrators are responsible for:

detecting and triaging incidents within their environment

determining whether the data involved is personal data

assessing legal reporting obligations (e.g. to regulators or affected users)

notifying Titan where relevant

13.3 Titan responsibilities

Titan will:

cooperate with integrators investigating suspected telemetry misuse or data incidents relating to Titan systems,

provide logs and technical details where appropriate and lawful,

update documentation and controls if systemic issues are identified.

Full incident management processes are described in 08_post_market_support.md.

14. Governance & Review
14.1 Data governance oversight

Titan maintains a governance framework that includes:

designated ownership for documentation and compliance pack

review of changes to telemetry models and endpoints

assessment of impact on data governance and privacy

14.2 Review cadence

This Data Governance document will be:

reviewed at least annually, and

updated when material changes occur to Titan-Core, Titan-X, or relevant regulation.

14.3 Integrator governance expectations

Integrators are expected to:

maintain their own internal data governance processes

treat Titan as a component in their overall data architecture

periodically review their use of Titan telemetry for alignment with law and policy

15. Document Control
15.1 Version history

v1.0 – Initial public release of Titan Data Governance document.

15.2 Change log

Changes to this document will be recorded in CHANGELOG.md at the repository root.

15.3 Ownership

This document is owned by the Titan project maintainers and forms part of the official Titan Compliance Pack.

15.4 Status

Status: Active

Next review: Within 12 months of last update, or sooner if required by material changes.
