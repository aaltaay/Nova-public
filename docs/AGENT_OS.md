# Agent OS (public export notes)

Nova is built and maintained with a fleet of specialized Cursor agents (`.cursor/agents/*.md`), each scoped to one domain (execution, tester, security, maintainer, etc.) and routed by a conductor (`daddy.md`). This document explains how that system works and what is intentionally **not** included in this public export.

## How the Agent OS works (in the private working repo)

- **Specialist prompts** — `.cursor/agents/*.md` define each agent's mission, guardrails, and workflow. These are included in this export unchanged (minus memory-file instructions, see below).
- **Living memory** — each agent normally maintains a session-local memory file (e.g. `tester-memory.md`) that accumulates a running snapshot, an improvement backlog, and pending facts learned across runs. Memory lets an agent pick up where it left off without re-deriving context every session.
- **Contracts and registry** — `.cursor/agent-system/contract.json` and `registry.json` define the fleet's routing rules and validation gates (`tools/agent_contract.py`).
- **Continuity rules** — `.cursor/rules/*-continuity.mdc` files enforce that agents check and update their memory/dashboards as part of their workflow.

## What's different in this export

Agent memory is **session-local and not shipped publicly** — it can contain internal run logs, environment-specific findings, and work-in-progress notes that aren't meaningful (or appropriate) outside the original working environment. Every agent spec in this repo has had its "read memory first" instruction replaced with a pointer to this document.

Everything else — the mission statements, guardrails, workflows, contracts, and routing logic — is unchanged and reflects how this project is actually run.
