# OWASP LLM & AI-Security Notes

Study and reference notes on securing applications built on Large Language Models (LLMs),
organised around the **OWASP Top 10 for LLM Applications** and complementary frameworks
(**MITRE ATLAS**, **NIST AI RMF**, **ISO/IEC 42001**). Written as a defensive learning
reference for SOC / AppSec / GRC work with AI systems.

> **Attribution:** The OWASP Top 10 for LLM Applications is a work of the OWASP Foundation,
> published under **Creative Commons Attribution-ShareAlike 4.0 (CC BY-SA 4.0)**. These notes
> summarise and link to it; the canonical, authoritative content is the OWASP project itself —
> see [`references.md`](references.md). This repo is **not** affiliated with or endorsed by OWASP.

## Contents
| File | Topic |
|---|---|
| [`owasp-llm-top10.md`](owasp-llm-top10.md) | The OWASP Top 10 for LLM Apps — risk-by-risk, with mitigations |
| [`key-concepts.md`](key-concepts.md) | Prompt injection, jailbreaks, data leakage, agent/tool risks |
| [`testing-and-mitre-atlas.md`](testing-and-mitre-atlas.md) | Evaluating LLM security; mapping to MITRE ATLAS |
| [`governance-iso42001-nist.md`](governance-iso42001-nist.md) | Governance view: ISO/IEC 42001 & NIST AI RMF |
| [`references.md`](references.md) | Sources, licences and further reading |

## Why this matters
LLM features introduce risks that traditional AppSec checklists miss: the model follows
**instructions found in data**, outputs are **non-deterministic**, and LLM "agents" can be
given **tools and permissions**. Defending them combines classic controls (authz, input/output
handling, least privilege) with AI-specific measures (prompt-injection defence, output
validation, model/supply-chain integrity, and monitoring).

## How to use these notes
- Start with [`owasp-llm-top10.md`](owasp-llm-top10.md) for the risk catalogue.
- Use [`key-concepts.md`](key-concepts.md) to understand the main attack classes.
- Use [`testing-and-mitre-atlas.md`](testing-and-mitre-atlas.md) when planning evaluation / red-teaming.
- Use [`governance-iso42001-nist.md`](governance-iso42001-nist.md) for the GRC / audit angle.

---
*Compiled by Osman Onur Uyar as a defensive learning reference. Framework content belongs to its
respective owners (OWASP, MITRE, NIST, ISO); see [`references.md`](references.md).*
