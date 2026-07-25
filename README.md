# Nova

> [!CAUTION]
> This repository is a living snapshot of software under ongoing development. The public source code is updated as the work evolves and matures.
>
> It may contain incomplete features, known limitations, bugs, or security vulnerabilities. Do not deploy this snapshot to production or use it with real user data, payments, credentials, or other sensitive information without an independent security review.

Nova is a local-first stock alert and trading workstation: read-only market scanning, HOD Momo alerts, optional IBKR paper execution, and an Electron or browser UI. It is designed for disciplined, operator-in-the-loop trading — not unattended auto-trading.

## Highlights

- **FastAPI backend** with modular routes, IBKR integration, and centralized execution (see [ADR 007](architecture/decisions/007-centralized-trading-execution.md))
- **React + Vite frontend** with workspace shell, Stock View, and account tooling
- **Security posture** documented under [`security/`](security/) with a findings registry and audit tooling
- **Agent OS** specialist prompts in [`.cursor/agents/`](.cursor/agents/) for structured AI-assisted development

## Documentation

| Document | Purpose |
|----------|---------|
| [AGENTS.md](AGENTS.md) | Project constitution, invariants, and agent routing |
| [architecture/README.md](architecture/README.md) | Target architecture and ADR index |
| [docs/](docs/) | Operator guides, paper shadow protocol, agent operations |
| [CHANGELOG.md](CHANGELOG.md) | Narrative of shipped changes |

### Architecture decisions (ADRs)

| ADR | Title |
|-----|-------|
| [001](architecture/decisions/001-modular-monolith.md) | Modular monolith |
| [002](architecture/decisions/002-hexagonal-ports-adapters.md) | Hexagonal ports/adapters |
| [003](architecture/decisions/003-functional-core-imperative-shell.md) | Functional core / imperative shell |
| [004](architecture/decisions/004-strangler-facades.md) | Strangler facades |
| [005](architecture/decisions/005-frontend-feature-slices.md) | Frontend feature slices |
| [006](architecture/decisions/006-css-itcss-cascade-layers.md) | CSS cascade layers |
| [007](architecture/decisions/007-centralized-trading-execution.md) | Centralized trading execution |
| [008](architecture/decisions/008-persistent-ibkr-scanner-rosters.md) | Persistent IBKR scanner rosters |

## Quick start (Windows)

### Browser (web UI)

1. Clone or copy this tree locally.
2. Copy `.env.example` → `.env` and set Alpaca read-only keys (`APCA_API_KEY_ID`, `APCA_API_SECRET_KEY`).
3. Double-click `Run Nova.bat`.

Expected endpoints:

- API: [http://127.0.0.1:8000](http://127.0.0.1:8000)
- Web UI: [http://localhost:5173](http://localhost:5173)

First-time: run `npm install` in `frontend/` if needed; ensure Python 3 is on PATH for the backend.

### Desktop (Electron)

```bat
cd frontend
npm install
npm run electron:dev
```

Windows installer: `npm run electron:pack` → `frontend/release/Nova-Setup-*.exe`.

Packaged app stores keys and cache under `%APPDATA%\Nova\`.

## Configuration

All secrets belong in `.env` (see `.env.example`). Optional modules include IBKR Gateway, Pinecone course memory, Cloudflare R2 archive, and Sentry. None are required for read-only scanning.

## Deploy (optional hosted web)

- Frontend: Vercel (project `nova`)
- Backend: Railway (see `.github/workflows/deploy.yml`)
- Desktop builds are local-only

## Public portfolio note

This tree is a sanitized export for portfolio review. Private agent memory, Obsidian vaults, graph exports, and internal scratch logs are omitted.

## Testing

From the **repository root** (required so `tools/` imports resolve):

```bash
pip install -r backend/requirements.txt
pytest backend/
cd frontend && npm ci && npm test
```

Agent contract validation (optional):

```bash
py -3 tools/agent_contract.py --ci
```

### Known test gaps in this public extract

A small number of tests depend on a live IBKR Gateway session or brokerage credentials that aren't available outside the original working environment, so they fail or are skipped when run from a fresh clone of this export rather than reflecting a regression. The overwhelming majority of the suite (unit tests, contract tests, and mocked-broker fixtures) runs and passes standalone.

## License

MIT — see [LICENSE](./LICENSE). This repository is a sanitized public extract from a private working monorepo, published for portfolio and demonstration purposes. Warrior Trading course materials referenced in docs are third-party content and not redistributed here.
