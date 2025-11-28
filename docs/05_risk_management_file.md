Titan Compliance Pack
Document 5 — Risk Management File (RMF)

Version: 1.0
Applies to: Titan-Core (API) and Titan-X (Platform Integrations)
Status: Approved for public + enterprise use

1. Purpose of this document

This Risk Management File documents:

risks associated with Titan-Core & Titan-X

controls and mitigations

responsibilities between Titan and integrators

post-market monitoring

testing strategy

change management

long-term safety governance

It ensures Titan meets modern AI regulatory expectations while maintaining its privacy-first, low-risk posture.

2. System Risk Classification

Under the EU AI Act:

✔ Titan-Core (low-resolution behavioural telemetry API):

Classified as "low risk"
→ No user-level inference, no profiling, no decisioning, no automated harm potential.

✔ Titan-X (developer-facing toolkit for adaptation logic):

May become “limited risk” depending on integrator use cases.
→ Titan-X’s job is to provide signals, not decisions.

❌ Titan products do not qualify as:

high-risk educational AI

biometric categorisation

emotion recognition

behavioural profiling

automated decision systems

children-targeting adaptive systems

social scoring

worker monitoring

Titan’s design deliberately avoids all these categories.

3. Risk Breakdown Structure (RBS)
3.1 Categories

Risks are grouped into:

Data Risks

Privacy Risks

Security Risks

Model/Logic Risks

Operational Risks

Integrator Misuse Risks

Compliance Risks

3.2 Top-level Risk Summary

Titan’s total inherent risk: low
Titan’s total residual risk after controls: very low

4. Detailed Risk Register
4.1 Data & Privacy Risks
Risk	Likelihood	Impact	Controls	Residual
Storing raw behavioural telemetry accidentally	Very Low	Medium	Titan stores no telemetry by design	Very Low
Personal data included in payloads	Medium	Medium	Validation rejects personal fields; schema restricts input	Low
Re-identification via session_id	Very Low	Low	Titan requires pseudonymous session IDs	Very Low
Developer misuse of data	Medium	High	Clear integrator responsibilities + docs	Medium
4.2 Security Risks
Risk	Likelihood	Impact	Controls
API endpoint abuse	Low	Medium	Rate limiting (optional), input validation, logging
Injection attacks	Low	High	Strict JSON schema + safe parsing
Compromise of integrator systems	Medium	High	Titan stores no data → indirect exposure only
4.3 Model / Logic Risks

Titan has no ML model in v1.
Risks relate to behavioural scoring logic only.

Risk	Likelihood	Impact	Controls
Incorrect score calculation	Low	Low	Unit tests + deterministic formulas
Bias	Very Low	Low	No personal attributes processed
Misinterpretation of signals	Medium	Medium	Clear developer guidance + examples
4.4 Operational Risks
Risk	Likelihood	Impact	Controls
Service downtime	Low	Medium	Logging + health checks + horizontal scaling
Version mismatch	Medium	Low	Semantic versioning + changelogs
Breaking changes	Low	Medium	Backwards-compatible contracts
4.5 Integrator Misuse Risks

This is the biggest category and the one regulators care about.

Risk	Likelihood	Impact	Controls
Using Titan to profile individuals	Medium	High	Documentation prohibits profiling; Titan stores no data
Using Titan for decisions affecting rights	Medium	High	Requires integrator DPIA; Titan provides signals only
Combining Titan signals with personal identifiers	Medium	Medium	Strong warnings + compliance docs
Using Titan in high-risk domains without governance	Low	Medium	Titan classification guidance
5. Risk Treatment Strategy
Titan responsibility

reduces inherent risk through architecture

ensures no personal data processing

ensures no behavioural records

provides transparent documentation

validates payload structures

enforces compliance boundaries

Integrator responsibility

ensure lawful use

maintain their own DPIA (if required)

prevent misuse of telemetry

implement user-facing transparency

store data responsibly if they persist it

This clear split protects Titan and maintains your USP.

6. Testing Strategy

Titan uses:

✔ Unit tests (coverage for: core calculations, validation, routing)
✔ Integration tests (Postman collection + CI pipeline)
✔ Manual behavioural simulations
✔ Static code analysis (security)
✔ Semantic contract tests
✔ Version regression tests (for next releases)
7. Post-Market Monitoring

Regulator required. Titan does:

monitor error patterns

track integrator misuse indicators

issue version advisories

investigate anomalies

update documentation annually

run internal safety reviews

Integrators must notify Titan of:

incidents

adverse effects

misuse

security breaches

incorrect behavioural use

any user rights impact

8. Change Management Plan

All changes:

are logged in CHANGELOG.md

follow semantic versioning

receive risk re-evaluation

maintain backwards compatibility

must not increase risk category without executive approval

Major changes require:

updated version of this RMF

updated technical documentation

updated transparency notices

9. Residual Risk Conclusion

After all mitigations:

Residual risk: VERY LOW

Titan is safe for:

enterprise integrations

government procurement

education (if integrator meets duties)

healthcare toolchains (non-clinical)

public sector tools

commercial SaaS

Web2, Web3, and hybrid environments

Titan cannot cause harm by itself — and never makes user-facing decisions.

10. Document Control

Version: 1.0

Status: Active

Owner: Titan Project Maintainers

Next Review: 12 months
