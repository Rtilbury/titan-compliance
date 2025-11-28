Titan Compliance Pack
Document 7 — Limitations & Safety Profile

Version: 1.0
Applies to: Titan-Core & Titan-X
Status: Approved for public + enterprise use

1. Purpose of this Document

This document describes the inherent limitations of Titan-Core and Titan-X and clarifies what the system does not do.
This is mandatory under the EU AI Act for:

General-Purpose AI Components

Safety-aligned transparency

Risk mitigation and integrator guidance

It protects both Titan and integrators from unintended interpretation or misuse.

2. Fundamental System Limitations
2.1 Titan is not an AI model in v1

Titan-Core contains no machine-learning model.
It:

does not learn

does not adapt based on training

does not store or analyse historical data

does not classify or score individuals

Titan-Core provides deterministic behavioural metrics only.

2.2 Titan cannot predict outcomes

Titan does not:

predict user performance

infer user skill or ability

assess psychological states

estimate future behaviour

segment users

Outputs are strictly rolling averages of telemetry supplied by the integrator.

2.3 Titan cannot make automated decisions

Titan does not:

approve or reject anything

determine rights or access

trigger automated enforcement

generate assessments

make high-stakes decisions

All adaptation logic is performed by the integrator, not Titan.

3. Safety Profile Overview

Titan’s safety profile is based on being:

low-risk under EU AI Act

deterministic

stateless

non-profiling

privacy-minimising

fully transparent

Titan cannot create human harm by itself because it:

has no autonomy

has no learning capability

has no long-term memory

has no ability to evaluate people

4. What Titan Cannot Process

Titan must not be used for:

4.1 Personal data

It does not rely on or require:

names

emails

phone numbers

addresses

identifiers

messages

documents

user content

4.2 Sensitive data

Titan must not receive:

biometric data

health data

protected attributes

political or religious views

special category data (GDPR)

4.3 Children’s personal data

Titan can be used in child-facing apps ONLY if telemetry is non-personal and integrators meet their own legal duties.

5. Behavioural Signal Limitations

Titan receives numeric signals only.
These signals:

are integrator-defined

have no intrinsic meaning to Titan

do not describe user intent

cannot infer emotions

cannot infer identity

cannot determine ability or disability

cannot be used as proxies for protected characteristics

Titan simply computes averages from numbers supplied by integrators.

6. No Multimodal Processing

Titan v1 does not process:

audio

video

images

text

documents

biometric features

This dramatically reduces compliance burden and security exposure.

7. No Long-Term User Models

Titan:

does not build user profiles

does not track behaviour across multiple sessions (unless integrator designs that externally)

does not cluster or segment users

does not perform pattern recognition

All long-term analysis, if needed, is performed by the integrator.

8. No Automated Behavioural Interpretation

Titan cannot determine:

whether a user is frustrated

whether a user is confused

skill level of a learner

emotional state

cognitive ability

intent or motivation

Titan simply processes raw numbers and returns rolling values.

9. Integration Safety Limitations

Integrators must understand that Titan:

does not replace user research

does not replace accessibility tools

does not enforce safety in UI

does not ensure fairness in decision-based systems

does not validate integrator use cases

does not check for regulatory compliance in downstream systems

10. Appropriate Use vs. Misuse
10.1 Appropriate Use

Titan is appropriate for:

UX optimisation

behavioural telemetry

interaction improvement

workflow automation

product onboarding analysis

adaptive interfaces when controlled by integrators

10.2 Misuse / Prohibited Use

Titan must not be used for:

psychological profiling

educational grading

employment decisions

healthcare diagnosis

credit scoring

behavioural surveillance

monitoring students or workers

determining eligibility or benefits

11. Safety Boundaries and Warning Flags

Integrators should investigate if:

telemetry affects user rights

telemetry feeds into high-stakes logic

telemetry is combined with personal identifiers

children or vulnerable users are involved

any decision is automated based on Titan outputs

If yes → integrators must run a DPIA and/or regulatory review.

12. Residual Safety Risk

After applying limitations and boundaries:

Residual safety risk: VERY LOW

Titan cannot independently cause harm because it:

makes no decisions

cannot interpret people

cannot store personal data

processes numeric telemetry only

13. Document Control

Version: 1.0

Status: Active

Next Review: 12 months

Owner: Titan Project Maintainers
