## Definition of Done: Tests + Docs (Blocking)

- Any production code change must include meaningful test updates in the same PR.
- Meaningful tests must include at least:
  - one primary behavior assertion
  - two non-happy-path assertions (edge, boundary, invalid input, or failure mode)
- Trivial assertions are forbidden (`expect(true).toBe(true)`, snapshot-only without semantic assertions, render-only smoke tests without behavior checks).
- Mock only external boundaries (network, clock, randomness, third-party SDKs). Do not mock the unit under test.
- UI changes must cover state matrix: loading, empty, error, success, disabled, focus-visible.
- API/command surface changes must update generated contract artifacts and request/response examples.
- Architecture-impacting changes must include an ADR in `/docs/adr/`.
- Required checks are blocking when `fail` or `not-run`: lint, typecheck, tests, coverage, diff coverage, docs check.
- Reviewer -> fixer -> reviewer loop is required before merge.

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
