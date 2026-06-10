

<!-- comm-contract:start -->

## Communication Contract

- Inherit global Codex communication and reporting rules from `/Users/d/.codex/AGENTS.override.md` and `/Users/d/.codex/policies/communication/BigPictureReportingV1.md`.
- Repo-specific instructions below add project constraints only; do not restate global voice or status-reporting rules here.
<!-- comm-contract:end -->

## Inherited Operating Rules

- Inherit global git, review/fix, testing, docs, UI, security, skill-use, and reporting gates from `/Users/d/.codex/AGENTS.md` and active session instructions.
- Use `.codex/verify.commands` and `.codex/scripts/run_verify_commands.sh` as this repo-local verification authority when present.
- API/command surface changes must update generated contract artifacts and request/response examples.

<!-- portfolio-context:start -->
# Portfolio Context

## What This Project Is

WorkdayDebrief is a local-first Tauri desktop app that aggregates daily work activity from Jira, Google Calendar, and Toggl, then uses a local Ollama model to draft an end-of-day narrative for review and delivery.

## Current State

The repo is active IT workflow tooling. Existing local changes are PR-template metadata, so context recovery should stay documentation-only.

## Stack

| Layer | Technology |
|-------|------------|
| Language | Rust + TypeScript |
| Desktop runtime | Tauri 2 |
| Frontend | React 19, Vite, Tailwind CSS |
| AI inference | Ollama (local) |
| Storage | SQLite (sqlx) |
| Auth | OAuth2 (Google) |
| Email | lettre |
| HTTP | reqwest |

## How To Run

```bash
npm run tauri dev
```

## Known Risks

- Calendar, Jira, Toggl, Slack, and email integrations can expose sensitive work data; keep secrets and OAuth tokens out of source.
- Local Ollama summarization is part of the privacy contract.
- Generated summaries should remain review/edit-before-send, not auto-send.
- Keep PR-template drift separate from integration or delivery behavior.

## Next Recommended Move

Resolve PR-template drift separately, then verify activity imports, local narrative generation, review/edit flow, delivery targets, and history persistence before shipping changes.

<!-- portfolio-context:end -->
