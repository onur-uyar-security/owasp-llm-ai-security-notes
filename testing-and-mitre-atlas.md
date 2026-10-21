# Testing, Evaluation & MITRE ATLAS

How to evaluate the security of an LLM application and where industry frameworks fit.

## MITRE ATLAS
**ATLAS** (Adversarial Threat Landscape for Artificial-Intelligence Systems) is MITRE's
ATT&CK-style knowledge base of **tactics and techniques against ML/AI systems**, built from
real-world and research attacks. Use it to:
- Speak a common language for AI threats (reconnaissance, initial access, ML attack staging,
  model evasion/poisoning, exfiltration, impact).
- Map your LLM risks to known adversary techniques.
- Drive **threat modelling** and **red-team** scenarios for AI systems.

> ATLAS complements OWASP: OWASP LLM Top 10 catalogues **application risks**; ATLAS catalogues
> **adversary techniques**. They map onto each other (e.g. prompt injection ↔ ATLAS techniques
> for LLM prompt manipulation).

## Evaluation / red-teaming approach
1. **Threat model** the app: data flows, trust boundaries, tools/permissions, who can supply text.
2. **Define abuse cases** from OWASP LLM Top 10 + ATLAS (injection, leakage, excessive agency, …).
3. **Test systematically:**
   - Direct & **indirect** prompt injection (via RAG docs, tool output, uploaded files).
   - Jailbreak / policy-evasion attempts.
   - Sensitive-data and system-prompt extraction.
   - Insecure output handling (does output reach HTML/SQL/shell unescaped?).
   - Excessive agency (can the agent be steered into harmful tool calls?).
   - Resource abuse / model-extraction patterns.
4. **Automate regression:** keep a suite of adversarial prompts and expected safe behaviours;
   re-run on every model/prompt/tool change (non-determinism means run **multiple times**).
5. **Review results** with severity and remediation; track like any other vuln.

## Tools & resources (verify current versions)
- **MITRE ATLAS** + ATLAS navigator / case studies.
- **OWASP GenAI / LLM project** resources and guides.
- LLM red-teaming / eval frameworks (e.g. garak, PyRIT, promptfoo, Giskard) — evaluate fit and
  licence before use.
- Classic AppSec tooling still applies to the surrounding app (SAST/DAST, dependency scanning).

## What "good" looks like
- Documented threat model and abuse cases.
- Repeatable adversarial test suite run on every change.
- Clear trust boundaries and least-privilege tools.
- Output treated as untrusted; sensitive actions gated by humans.
- Monitoring/logging wired into the SOC.

See [`governance-iso42001-nist.md`](governance-iso42001-nist.md) for the governance wrap-around
and [`references.md`](references.md) for sources.
