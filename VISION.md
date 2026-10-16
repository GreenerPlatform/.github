# GreenerPlatform — Vision

## Thesis

Operational reasoning is safer when every claim can point to evidence with known
provenance, scope, time, and collection status. GreenerPlatform builds that evidence
substrate for Kubernetes investigations and keeps model reasoning optional.

Determinism helps with reproducibility and auditability. It does not, by itself, prove
that a check is correct, complete, or causally relevant.

## Architecture

1. **Evidence collection** — `kubectl-sentinel` performs read-only Kubernetes API checks
   and emits structured observations, collection status, and evidence subjects.
2. **Rule-based correlation** — `incident-triage` ranks those observations against a
   normalized alert and records evidence gaps and candidate response steps.
3. **Interoperability** — `greenerplatform-mcp` exposes both tools through MCP without
   adding a model or changing their evidence contract.
4. **Reasoning and orchestration** — a host agent may request approved reads, challenge
   hypotheses, and explain the evidence. Human approval remains the default for mutation.

No layer turns an observation into a fact merely by formatting it as JSON. Claims remain
limited by collector quality, coverage, permissions, timing, and interpretation.

## Scope

GreenerPlatform owns:

- Kubernetes reliability evidence and provenance
- explicit collection failures and unavailable data
- rule-based correlation with explicit uncertainty
- fixtures that test detection, missed signals, and false reassurance

GreenerPlatform integrates with, but does not replace, metrics, logs, traces, deployment
history, security posture, or incident-management systems. Time-windowed sources belong
behind bounded read-only adapters with query provenance and cost limits.

The default operating boundary is read-only. Recommendations may gather more evidence or
propose remediation, but they are not automatically safe fixes.

## Current position

GreenerPlatform is an **evidence substrate and partial evaluation harness**, not a complete
autonomy harness. Offline fixture gates verify selected evidence-integrity contracts.
Broader live-cluster validation, held-out multi-source investigations, durable run state,
identity controls, and team-utility evidence remain roadmap work.

## Roadmap

- Complete collector-failure coverage and live-cluster validation.
- Add approved historical adapters for metrics, logs, traces, and change history.
- Evaluate graph coverage, false reassurance, latency, and query cost on held-out cases.
- Add durable checkpoints, budgets, and explicit terminal states for long investigations.
- Measure utility with SRE teams before expanding execution authority.
