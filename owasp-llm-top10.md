# OWASP Top 10 for LLM Applications — Notes

A risk-by-risk summary with practical mitigations. This is a **study summary**; the
authoritative list (including the current year's exact IDs and wording) is maintained by the
OWASP Foundation under **CC BY-SA 4.0** — always confirm against the official project
(see [`references.md`](references.md)).

> The OWASP GenAI/LLM project periodically renumbers and renames entries between editions.
> The categories below reflect the widely used list; check the official site for the edition
> that applies to you.

## LLM01 — Prompt Injection
Untrusted input manipulates the model's instructions.
- **Direct:** the user tells the model to ignore its rules.
- **Indirect:** malicious instructions hidden in content the model ingests (a web page,
  document, email, or tool output) hijack its behaviour.
- **Mitigations:** separate system/developer instructions from user/data content; treat all
  retrieved/tool content as untrusted; constrain and validate what the model can do; require
  human approval for sensitive actions; apply least privilege to any tools/agents.

## LLM02 — Sensitive Information Disclosure
The model reveals secrets, PII, proprietary data, or system-prompt content.
- **Mitigations:** data minimisation; don't put secrets in prompts; output filtering/redaction;
  strict access control on retrieval sources; scrub training/fine-tuning data.

## LLM03 — Supply Chain
Risks from third-party models, datasets, plugins, and libraries (poisoned/backdoored models,
vulnerable components, typosquatted packages).
- **Mitigations:** vet model/dataset provenance; verify signatures/hashes; SBOM; pin and scan
  dependencies; evaluate third-party plugins before trust.

## LLM04 — Data & Model Poisoning
Tampered training / fine-tuning / embedding data introduces backdoors or bias.
- **Mitigations:** source and validate data; integrity checks; anomaly detection; isolate and
  review fine-tuning pipelines; evaluate models for backdoors before release.

## LLM05 — Improper Output Handling
Downstream systems trust model output blindly → XSS, SQLi, SSRF, RCE, command injection.
- **Mitigations:** treat model output as **untrusted input**; encode/escape; parameterise
  queries; validate against a schema; never pass raw output to shells, eval, or SQL.

## LLM06 — Excessive Agency
An LLM agent has too much autonomy, permission, or functionality and takes harmful actions.
- **Mitigations:** least privilege for tools and APIs; minimise available functions; require
  human-in-the-loop for high-impact actions; scope and rate-limit; log every tool call.

## LLM07 — System Prompt Leakage
Treating the system prompt as a secret / security control; its exposure reveals sensitive logic.
- **Mitigations:** don't put secrets or sole authz logic in the prompt; enforce controls in
  the application layer; assume the prompt can be extracted.

## LLM08 — Vector & Embedding Weaknesses
Weaknesses in RAG / embeddings: injection via retrieved docs, cross-tenant leakage, poisoned
vector stores.
- **Mitigations:** access-control the vector DB per tenant/user; validate and sanitise ingested
  content; monitor retrieval; isolate indexes.

## LLM09 — Misinformation
Over-reliance on confident but wrong output ("hallucinations"), with real-world consequences.
- **Mitigations:** ground answers (RAG with citations); human review for high-stakes use;
  communicate uncertainty; verify facts; constrain scope.

## LLM10 — Unbounded Consumption
Resource abuse: cost/DoS from expensive queries, and model extraction/theft via mass querying.
- **Mitigations:** rate limiting and quotas; input/length limits; cost monitoring and alerts;
  detect scraping/extraction patterns.

---
### Cross-cutting defences
- **Zero-trust for model I/O:** untrusted in, untrusted out.
- **Least privilege** for every tool, data source, and agent.
- **Human-in-the-loop** for consequential actions.
- **Logging & monitoring** of prompts, outputs, and tool calls (feed your SIEM).
- **Evaluation / red-teaming** before and after release (see
  [`testing-and-mitre-atlas.md`](testing-and-mitre-atlas.md)).

*Summarised from the OWASP Top 10 for LLM Applications (CC BY-SA 4.0). Confirm IDs/wording
against the official project — see [`references.md`](references.md).*
