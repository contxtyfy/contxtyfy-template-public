# Changelog

All notable changes to the Contxtyfy Railway template.
Updating: redeploy the Command Centre service in Railway — the template's
`stable` image tag always points at the latest release below.

## 0.2.0 — 2026-08-11

First published edition. Free-model resilience for zero-credit OpenRouter
deployments:

- Provider-capacity 502s ("at capacity", "request limit reached", bare
  "Provider returned error") retry as transient instead of failing the run.
- When every model in the chain fails transiently, the supervisor waits and
  re-walks the whole chain (CC_MODEL_CHAIN_ROUNDS × CC_MODEL_CHAIN_ROUND_DELAY_S).
- Per-attempt ceilings tunable: CC_FREE_ATTEMPT_LIMIT_S (default 1500) /
  CC_PAID_ATTEMPT_LIMIT_S (default 600) — free models get time to finish real work.
- Control-plane self-healing: orphaned parked runs are reaped after 24 h and
  POST /api/control-plane/unwedge clears a same-day wedge without shell access.
- Documented free-first model chain that runs on a $0 OpenRouter key.

## 0.1.0 — 2026-08-03

Initial release: GTD command centre + knowledge graph, six supervised agents,
first-boot setup wizard (accounts, model backend, Composio OAuth), meeting
prep + artifacts, job-applications pipeline, approval-gated external actions.
