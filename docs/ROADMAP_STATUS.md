# Nova roadmap status (public summary)

This is a high-level product roadmap index for the public portfolio tree. Detailed phase ledgers and private planning notes are not included in this export.

## Current focus areas

| Area | Status | Notes |
|------|--------|-------|
| Architecture maintenance | Ongoing | See [architecture/README.md](../architecture/README.md) and ADRs |
| Paper shadow protocol | Active | See [paper-shadow-protocol.md](./paper-shadow-protocol.md) |
| IBKR execution path | Shipped | Centralized via ADR 007 |
| HOD Momo parity | Ongoing | Scanner + alert engine hardening |
| Agent OS | Reference | Specialist prompts in `.cursor/agents/` |

## Safety gates (non-negotiable)

- `auto_live` is **NO-GO** unless explicitly unlocked in a separate approved phase.
- Broker mutations go through the centralized execution service (ADR 007).
- Secrets live in `.env` only — never in source or commits.

## Where to read more

- Constitution: [AGENTS.md](../AGENTS.md)
- Architecture decisions: [architecture/decisions/](../architecture/decisions/)
- Task history (sanitized): [knowledge/task-log/](../knowledge/task-log/)
