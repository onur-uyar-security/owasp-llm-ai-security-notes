# Governance: ISO/IEC 42001 & NIST AI RMF

The GRC / audit view of AI security — how organisational governance frames the technical
controls in the rest of these notes. (See also the companion **`grc-toolkit`** repo for
ISO 27001 / 42001 / NIS2 templates — link it to your own repo URL once published.)

## ISO/IEC 42001:2023 — AI Management System (AIMS)
The first management-system standard for **artificial intelligence**, structured like ISO 27001
(Plan-Do-Check-Act, Annex of controls). It helps an organisation **govern** the development and
use of AI responsibly.
- **Scope & context:** define where AI is used and the obligations that apply.
- **Leadership & policy:** an AI policy, roles, and accountability.
- **Planning:** AI risk assessment and treatment, including impact on individuals/society.
- **Support & operation:** competence, data management, lifecycle controls, third-party AI.
- **Performance & improvement:** monitoring, audit, management review, corrective action.
- **Link to security:** AIMS sits alongside an ISMS (ISO 27001). Security risks of LLM apps
  (this repo) become **risks managed** within the AIMS, with controls and evidence.

## NIST AI Risk Management Framework (AI RMF 1.0)
A voluntary framework organised around four functions:
- **Govern** — culture, policies, roles, accountability for AI risk (cuts across the others).
- **Map** — context and risks of the AI system.
- **Measure** — analyse, assess, and track risks (including security and robustness).
- **Manage** — prioritise and act on risks; monitor over time.
Plus the **Generative AI Profile**, which adds GenAI-specific risk guidance.

## How it ties together
| Layer | Question it answers | Artifacts |
|---|---|---|
| **Governance** (ISO 42001 / NIST AI RMF) | Are we managing AI risk responsibly and provably? | AI policy, risk register, roles, audits |
| **Application risk** (OWASP LLM Top 10) | What can go wrong in this LLM app? | Threat model, abuse cases, controls |
| **Adversary techniques** (MITRE ATLAS) | How would an attacker do it? | Red-team scenarios, detections |
| **Operations** (SOC) | Will we see and respond to it? | Logging, SIEM detections, IR playbooks |

## Regulatory context (awareness)
- **EU AI Act** introduces risk-tiered obligations for AI systems; ISO 42001 / NIST AI RMF help
  demonstrate due diligence. Confirm current obligations and timelines for your jurisdiction and
  use case.
- Data-protection law (e.g. **GDPR**) still applies to personal data processed by AI features.

> Governance frameworks don't replace the technical controls — they make them **required,
> documented, and auditable**. The OWASP/ATLAS work in this repo provides the evidence that
> AI-specific risks are identified and treated.

See [`references.md`](references.md) for authoritative sources.
