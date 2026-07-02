## GreenerPlatform

**Deterministic first, AI for reasoning.** Open-source SRE and platform tools for
Kubernetes — the deterministic *evidence layer* an AI or agent can reason over, instead
of another LLM guessing at your cluster.

As AI moves into operations, the moat isn't a smarter model — it's evidence the model is
**bounded by**: reproducible, auditable, CI-safe. We call it **AIReliability**.

### What we build
- **[kubectl-sentinel](https://github.com/GreenerPlatform/kubectl-sentinel)** — a point-in-time cluster health snapshot with severity rules. Tells you **why**, not just what. Structured JSON, exit codes, runs at 3am in CI with no internet.
- **[incident-triage](https://github.com/GreenerPlatform/incident-triage)** — alert × snapshot → causation chain + prioritized fix plan. Deterministic Python, stdlib only.
- **AI skills & agents** — a reasoning layer on top of the JSON that adds causation and next actions, always grounded in observed facts.

### The rule of the stack
Each layer may reason, but only the bottom layer establishes fact. The deterministic
tools stay dependency-light and testable; the AI is optional and bounded by the evidence.
We deliberately stay *out* of what the observability stack already owns (metrics, logs,
traces) and out of security posture — we are the reliability evidence those systems act on.

**→ Start with [kubectl-sentinel](https://github.com/GreenerPlatform/kubectl-sentinel)** · read the full [VISION](VISION.md).
