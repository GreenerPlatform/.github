# GreenerPlatform — Vision

## The thesis: deterministic first, AI for reasoning

As AI moves into operations, the differentiator is not another model that *guesses* at
cluster state — it is a **deterministic evidence layer the AI is bounded by**.
GreenerPlatform builds that layer for reliability: **AIReliability**.

## Why this is defensible

The observability ecosystem (Prometheus/Grafana, the cloud vendors) owns metrics, logs,
traces, and alerting. Most "AI SRE" products bolt an LLM onto those systems and let it
narrate — which hallucinates commands, isn't reproducible, and can't run in CI.
GreenerPlatform sits in the gap they leave open:

- **Reproducible** — same cluster state in, same findings out. No model in the collection hot path.
- **Auditable** — every finding is a fact with a severity rule and a concrete next command; nothing invented.
- **Cheap & CI-friendly** — deterministic CLIs run in a pipeline; the LLM is optional and only reasons *over* the evidence.
- **Bounded AI** — reasoning layers consume structured JSON, so causation is grounded in observed facts.

## Architecture — three layers

1. **Deterministic layer (the core).** Dependency-light CLIs that collect and correlate
   cluster state and emit structured JSON.
   - `kubectl-sentinel` — a point-in-time cluster **snapshot** with severity rules.
   - `incident-triage` — alert × snapshot → **causation chain + prioritized fix plan + confidence**.
2. **Reasoning layer (skills).** Natural-language framing and causal reasoning on top of the JSON.
3. **Orchestration layer (agents).** Goal-driven automation — always human/agent-in-the-loop, never silent auto-remediation.

**The rule of the stack:** each layer up may reason, but only the bottom layer establishes fact.

## Scope discipline — the litmus test

For any proposed capability:

> "Would an on-call SRE run this `kubectl` during an incident, **and** is it deterministic
> from a single snapshot?"

- **Yes → in scope.**
- **Needs a time window, a metrics backend, or a security judgment → out of scope.**

### Explicitly out of scope (by design)
- Time-series, trends, alerting → Prometheus / Grafana / Thanos. Sentinel is a *snapshot*, not a monitor.
- Log aggregation → Loki. Tracing → Tempo / Jaeger.
- Security & compliance posture (CIS, RBAC audit, CVEs) → a dedicated tool's lane, not sentinel's.
- Cost, APM, synthetic checks, auto-remediation by default.

Staying out of these is what keeps the tools focused and lightweight — they are the
reliability *evidence* those systems and an AI act on.

## Roadmap themes
- Broaden the deterministic snapshot with high-signal, single-`kubectl` checks (workload rollouts, disruption budgets, quotas, scheduled jobs, DNS, certificate expiry).
- Sharpen triage with **change correlation** ("what changed right before the alert").
- Keep the CLIs dependency-light and CI-safe; keep the AI optional and evidence-bounded.
