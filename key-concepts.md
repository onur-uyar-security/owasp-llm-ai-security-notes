# Key Concepts in LLM Security

Deeper notes on the main attack classes behind the OWASP LLM Top 10.

## Prompt injection
The model cannot reliably tell **instructions** from **data** — both arrive as text. If an
attacker controls any text the model reads, they can try to steer it.

- **Direct prompt injection:** the user types adversarial instructions
  ("ignore previous instructions and …").
- **Indirect prompt injection:** the payload is planted in content the app feeds to the model —
  a web page, PDF, email, calendar invite, image with embedded text, or a tool's response. The
  user never sees it; the model acts on it. This is the dangerous one for **agents** and **RAG**.

**Defensive posture**
- Keep a clear trust boundary: system/developer instructions are trusted; user input and all
  retrieved/tool data are **not**.
- Don't let retrieved content silently expand the model's permissions.
- Constrain outputs (allow-lists, schemas) and require confirmation for sensitive actions.
- Consider a second check (classifier/guardrail) on inputs and outputs — but treat it as
  defence-in-depth, not a guarantee.

## Jailbreaks
Techniques that get a model to bypass its safety/usage policies (role-play framing, obfuscation,
encoding, "do-anything" personas, many-step priming). Related to prompt injection but aimed at
**policy evasion** rather than hijacking an app's logic.
- **Mitigations:** layered safety (model + application policy), output monitoring, abuse
  detection, and not relying on the model alone to enforce security-critical rules.

## Sensitive data leakage
- **Via output:** model repeats secrets/PII from its context, training data, or system prompt.
- **Via retrieval:** RAG pulls documents the current user shouldn't see (missing per-user authz).
- **Mitigations:** data minimisation, per-user access control on sources, output redaction, and
  never placing secrets in prompts.

## Insecure output handling
Model output is **untrusted input** to whatever consumes it. Rendering it as HTML → XSS;
concatenating into SQL → SQLi; passing to a shell/`eval` → RCE; using it as a URL → SSRF.
- **Mitigations:** encode/escape on output, parameterise queries, validate against a schema,
  and never execute model text directly.

## Agents, tools & excessive agency
LLM "agents" plan and call tools/APIs. Risk scales with **permissions × autonomy × tool count**.
- Grant each tool the **least privilege** it needs.
- Reduce the number of available/high-impact functions.
- Put a **human in the loop** for actions with real-world effect (send money, delete data, email
  externally).
- Rate-limit and **log every tool call** for detection and forensics.

## Supply chain & poisoning
Models, datasets, embeddings, and plugins are dependencies.
- **Poisoning:** tampered training/fine-tune/embedding data plants backdoors or bias.
- **Supply chain:** backdoored models, vulnerable libraries, malicious plugins, typosquatting.
- **Mitigations:** provenance and integrity verification, SBOM, dependency scanning, plugin
  vetting, and evaluation for backdoors before trust.

## SOC / monitoring angle
Treat an LLM feature like any other internet-facing app **plus** AI-specific signals:
- Log prompts, outputs, tool calls, and retrieval sources (mind privacy/PII).
- Alert on anomalies: injection patterns, mass querying (extraction/DoS), repeated policy
  refusals, unexpected tool usage, cost spikes.
- Feed these into your SIEM and correlate with identity and network telemetry.

See [`testing-and-mitre-atlas.md`](testing-and-mitre-atlas.md) for evaluation, and
[`references.md`](references.md) for sources.
