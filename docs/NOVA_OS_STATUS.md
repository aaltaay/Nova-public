# Nova OS status (public summary)

Nova OS is the decision and archive engine behind the trading workstation UI. This public tree includes the implementation and architecture references; private Obsidian decision vaults and graph exports are not included.

## Engine scope (P0–P10)

Nova OS covers event-time replay, mode receipts, archive durability, and operator-facing judgment surfaces in the Stock View dock. Product-facing "what's next" lives in [ROADMAP_STATUS.md](./ROADMAP_STATUS.md).

## Authoritative references

| Topic | Location |
|-------|----------|
| Execution path | [ADR 007](../architecture/decisions/007-centralized-trading-execution.md) |
| Trading validation | [trading-execution-validation.md](./trading-execution-validation.md) |
| Paper shadow ops | [paper-shadow-protocol.md](./paper-shadow-protocol.md) |
| Security findings | [security/findings-registry.json](../security/findings-registry.json) |

## Public tree omissions

The following are intentionally excluded from this export:

- Private knowledge vault (`knowledge/obsidian/`)
- Agent runtime memory files (`.cursor/agent-memory/`)
- Graphify output (`graphify-out/`)
- Internal scratch logs (`PROBLEM_LOG.md`, `progress.md`, etc.)
