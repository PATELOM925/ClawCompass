# OpenClaw Hackathon (TTW26)

## Event
- **Hackathon**: OpenClaw Hackathon (Toronto Tech Week)
- **Format**: Hackathon
- **Constraint**: Must use OpenClaw host's frameworks/tools to build the solution

## Team
| Name | Role |
|--------|--------|
| Om Patel | AI/ML Lead, Full-Stack |
| Awais | Data Engineering, Backend |
| Abhinav | Backend / Systems |

## Project
Selected idea: **ClawCompass**, a paid capability broker for autonomous agents.

ClawCompass lets a requesting agent describe its task and safe context, then analyzes which skill, MCP, hook, plugin, rule, or sub-agent is needed. It recommends and sequences the right capability, redacts sensitive context, buys low-risk capabilities through x402 on behalf of the requester, sells listed capabilities as the marketplace broker, executes after verified payment, and records reputation.

The primary demo capability is **ClawUp SetupPilot**, focused on the lived onboarding pain around ClawUp, Telegram pairing, ERC-8004, x402, wallet readiness, and submission proof.

## Planning Scaffold
- Project instructions: [`AGENTS.md`](AGENTS.md)
- Durable context: [`memory.md`](memory.md)
- Work graph: [`docs/codex/work/WORK-GRAPH.md`](docs/codex/work/WORK-GRAPH.md)
- Idea intake: [`docs/hackathon/IDEA-INTAKE.md`](docs/hackathon/IDEA-INTAKE.md)
- Build runbook: [`docs/hackathon/BUILD-RUNBOOK.md`](docs/hackathon/BUILD-RUNBOOK.md)
- Demo and submission guide: [`docs/hackathon/DEMO-SUBMISSION.md`](docs/hackathon/DEMO-SUBMISSION.md)
- ClawCompass hub: [`docs/hackathon/clawcompass/README.md`](docs/hackathon/clawcompass/README.md)
- Custom ClawUp skill specs: [`docs/clawup-skills/`](docs/clawup-skills/)

## Local Backend

```bash
npm install
npm run dev
```

The API listens on `http://localhost:3000` by default. Useful demo endpoints:

- `GET /health`
- `GET /api/help`
- `POST /api/ask`
- `GET /api/marketplace`
- `GET /api/tool/pitchhawk`
- `GET /api/tool/setuppilot`
- `POST /api/buy`
- `POST /api/use/pitchhawk`
- `POST /api/use/setuppilot`
- `POST /api/approve/:transactionId`
- `POST /api/execute/pitchhawk`
- `POST /api/execute/setuppilot`
- `POST /api/register-tool`
- `POST /api/command`
- `GET /api/security`
- `GET /api/transactions`
- `GET /api/reputation/setuppilot`
- `GET /api/proof`
- `GET /api/payment/:transactionId/status`
- `POST /api/reputation/:id/write-onchain`

Local development can use `ENABLE_MOCK_X402=true` to unlock `/api/demo-settle/:transactionId`.
Keep it disabled for final demo evidence. Real paid execution uses the `goatx402-sdk-server`
adapter when merchant credentials and a payer wallet are available in untracked `.env`.

## Web App

```bash
npm run dev:web
```

The browser app runs through Vite, defaults to `http://localhost:5173`, and calls the API at
`http://localhost:3000`. Set `VITE_API_BASE_URL` if the API runs somewhere else.

Routes:
- `/buy`: buyer-agent workflow for context analysis, tool recommendation, x402 purchase intent, mock settlement, and execution.
- `/sell`: seller marketplace for listed paid capabilities and pending provider submissions.
- `/`: broker workflow for task intake, x402 payment, execution, transactions, and reputation.

Validation:

```bash
npm run validate
npm run build:web
npm audit --audit-level=moderate
```

Real ClawUp, wallet, x402 merchant, and ERC-8004 actions remain external gated steps. Put real credentials only in untracked `.env`, never in repo docs.
Sanitized public details extracted from the ClawUp environment document are tracked in
[`docs/hackathon/clawcompass/EXTERNAL-PROOF-INTAKE.md`](docs/hackathon/clawcompass/EXTERNAL-PROOF-INTAKE.md).

## Telegram Runtime

The official submission channel is still ClawUp-paired Telegram. The local server also includes an optional Telegram bridge that routes messages into the same `/api/command` handler:

```bash
TELEGRAM_BOT_ENABLED=true TELEGRAM_BOT_TOKEN=<rotated-token> npm run dev
```

Use only a rotated runtime token from an untracked environment. The bridge is disabled by default and should not be used as proof of ClawUp pairing.

## Brief And Plan

- Source-of-truth brief: `/Users/shreyapatel/Projects/zzz project docs/GOAT Hack/CODEX_IMPLEMENTATION_BRIEF_CLAWCOMPASS.md`
- Saved implementation plan: [`docs/hackathon/clawcompass/CODEX_IMPLEMENTATION_PLAN_CLAWCOMPASS.md`](docs/hackathon/clawcompass/CODEX_IMPLEMENTATION_PLAN_CLAWCOMPASS.md)
- Source snapshot: [`docs/hackathon/clawcompass/SOURCE-OF-TRUTH.md`](docs/hackathon/clawcompass/SOURCE-OF-TRUTH.md)
- External proof intake: [`docs/hackathon/clawcompass/EXTERNAL-PROOF-INTAKE.md`](docs/hackathon/clawcompass/EXTERNAL-PROOF-INTAKE.md)
- Judge demo deck: [`docs/presentations/clawcompass_judge_full_demo_stage.pptx`](docs/presentations/clawcompass_judge_full_demo_stage.pptx)
- Graphical demo deck copy: [`docs/presentations/clawcompass_stage_graphical_demo.pptx`](docs/presentations/clawcompass_stage_graphical_demo.pptx)
- Transaction QA recording: [`docs/demo-recordings/clawcompass-transactions-qa-2026-05-26.webm`](docs/demo-recordings/clawcompass-transactions-qa-2026-05-26.webm)

## Action Items
- [ ] Review OpenClaw's required frameworks and documentation
- [x] Identify compatible project ideas within host constraints
- [ ] Finalize roles per team member
- [ ] Build and demo

## Tools
- OpenClaw host framework(s) (primary constraint)
- Claude Code Pro
- Cursor Pro
- Python / FastAPI
- Lovable (UI)

## Status
- [ ] Confirm attendance
- [x] Finalize project idea using the idea intake workflow
- [x] Build local MVP
- [x] Add full web app for broker workflow, proof, security, transactions, and reputation
- [ ] Complete external ClawUp, x402, wallet, and ERC-8004 proof
- [ ] Demo

## Next Steps
1. Verify the ClawUp agent and Telegram pairing after explicit user action
2. Rotate or securely load exposed wallet/x402/Telegram credentials outside tracked files
3. Confirm wallet funds, run real x402, register ERC-8004, then rehearse and submit with public proof visible
