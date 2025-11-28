Titan-Core & Titan-X Compliance Pack
Document 3 — Data Governance (Integrator Guidance & Shared Responsibilities)

(This is the companion doc to 02, focused specifically on integrators and real deployment obligations.)

Version: 1.0
Applies to: Titan-Core (API) & Titan-X (Platform Integrations)
Status: Approved for public + enterprise use

1. Purpose of this document

Document 02 described Titan’s internal governance model.

Document 03 describes what integrators must do when deploying Titan-Core or Titan-X, including:

their responsibilities under the EU AI Act

expectations around lawful data handling

their accountability for end-user impact

required governance steps

boundaries between Titan and the integrator

This document is intentionally short, direct, and written as compliance guidance.

2. Integrator Role & Responsibilities
2.1 Integrators are the AI “system provider”

When a company incorporates Titan-Core into any product that interacts with end users, they become the:

AI System Provider (EU AI Act terminology)

Data Controller (GDPR/UK GDPR terminology)

Owner of end-user impact, communication, rights, and risk

Titan is the technical component providing behavioural telemetry.

2.2 Integrator determines:

Integrators must determine and document:

lawful basis for collection (e.g., legitimate interests, contract, etc.)

the purpose of telemetry

how telemetry influences UX, adaptation, or automation

whether any model/classifier sits downstream

where and how telemetry is stored

retention periods

deletion workflows (if any)

end-user transparency mechanisms

data protection and privacy notices

any DPIAs or high-risk assessments (if applicable)

Titan cannot make these determinations on their behalf.

3. Integrator Data Obligations
3.1 Define and document telemetry fields

Integrators must:

document all custom telemetry fields

ensure fields do not contain identifiers or user content

ensure no special category data is transmitted

ensure no accidental PII enters free-form context fields

3.2 Maintain data minimisation

Integrators are responsible for:

removing identifiers before sending data

preventing excessive or nonessential telemetry

configuring their application to send only the required signals

3.3 Configure storage safely (if storing telemetry)

If integrators choose to store telemetry:

they must define retention periods

they must enforce access controls

they must encrypt data at rest

they must log access

they must implement deletion mechanisms

Titan does not store user telemetry by default.

4. End-User Impact & Transparency
4.1 When transparency is required

If telemetry contributes to user-facing decisions (UX adaptation, personalisation), integrators must:

include Titan telemetry in their privacy notice (simple description)

document how telemetry affects the user experience

provide end-user communication where required by law

For low-risk UX optimisation, transparency is typically straightforward.

4.2 When explicit consent is not required

Titan telemetry normally falls under:

legitimate interests (for UX improvement), or

performance of a contract (for interaction/training tools)

Consent is only needed if:

telemetry feeds into high-risk profiling,

or if required by integrator’s local law.

Titan does not require or enforce consent.

5. Accountability & Governance
5.1 Integrator risk assessments

Integrators must decide whether a DPIA is required based on their use case. Examples:

DPIA usually NOT required for:

standard UX optimisation

clickstream analysis

friction/engagement measurement

DPIA MAY BE required for:

workplace monitoring

credit, insurance, hiring, or other protected decisions

applications involving children where user-level outcomes are affected

psychological, educational, or health assessments

5.2 Integrators must perform:

governance checks before launch

documentation of intended use

internal sign-off

monitoring for potential misuse

periodic review of telemetry mapping

6. Integrator Security Requirements

Integrators must:

protect API keys

avoid client-side API calls

implement RBAC for stored telemetry

ensure network isolation if multi-tenant

audit logs for anomaly detection

ensure backups respect data retention periods

7. Integrator Incident Responsibilities

If integrators detect:

accidental transmission of personal data

API key exposure

suspected misuse of telemetry

unauthorised access to stored logs

…then they must follow their internal incident processes and notify Titan if relevant.

Titan will support investigations but cannot determine regulatory obligations for the integrator.

8. Prohibited Integrator Uses

Integrators must NOT:

use Titan to infer protected characteristics

treat telemetry as psychological profiling

rely on Titan telemetry alone for high-stakes decisions

send biometrics, content, names, messages, or identifiers

attempt to reverse-engineer or derive identity from session behaviour

9. Integrator Deployment Checklist

Before deploying, integrators should complete this checklist:

✔ Telemetry fields reviewed & safe
✔ No personal data sent
✔ Custom fields documented
✔ Purpose & lawful basis documented
✔ Privacy notice updated (if required)
✔ Retention periods defined
✔ API keys secured
✔ Access controls in place
✔ Monitoring established
✔ Internal sign-off completed
✔ Post-market monitoring enabled
10. Document Control

Version: 1.0

Status: Active

Next review: ≤ 12 months

Owner: Titan Project Maintainers
