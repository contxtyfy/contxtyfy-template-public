# Changelog

All notable changes to the Contxtyfy Railway template.
Updating: redeploy the Command Centre service in Railway — the template's
`stable` image tag always points at the latest release below.

## 0.3.0 — 2026-08-17

**Fixes a bug that could throw away work your agents had already done.** If any
third-party tool call returned HTTP 403 — an expired accounting or storage
connection was enough — the run was classified as an authentication failure and
stopped, even though it had finished its work and written its files. The stage
then exited non-zero and took the following stage down with it. In the reference
deployment this discarded five consecutive days of completed cycles while every
cycle wrote its summary normally, and the knowledge graph stopped advancing.
Upgrade if you run scheduled cycles.

- A failed tool result no longer counts as a failure of the run. The scan now
  matches the Composio result envelope rather than the word "Error:", so real
  provider failures are still caught and retried.
- A run that exits cleanly and produces the output it promised is a success,
  whatever its transcript contains.
- A run that produced real output is no longer recorded as failed. Its own log
  does not count as output.
- A successful run no longer carries a failure class.
- Failure decisions now log the line that caused them, so a wrong one can be
  traced without reading the whole transcript.

**Xero is removed.** The `/webhooks/xero` receiver, the `XERO_WEBHOOKS_KEY`
setting and the setup-wizard field are gone, and Xero is no longer requested as
a Composio toolkit. `POST /webhooks/composio` is now the only inbound receiver.
If you set `XERO_WEBHOOKS_KEY`, it is ignored — no other action is needed.

Slack alerting is unchanged.

## 0.2.1 — 2026-08-11

- Composio provisioning no longer fails outright when a toolkit's auth config
  cannot be auto-created (e.g. Xero, which needs custom OAuth credentials).
  The toolkit is dropped with a warning and re-joins automatically on the next
  provision after you add an auth config in the Composio dashboard.

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
