# WorkdayDebrief — Portfolio Disposition

**Status:** Release Frozen — Tauri 2 + Rust + React 19 desktop app
on `origin/main` that aggregates Jira + Toggl + Google Calendar +
Slack into a daily debrief, summarizes via local LLM, and delivers
via email / file / Slack. Joins the signing cluster as the 14th
member.

> Disposition uses strict `origin/main` verification.

---

## Verification posture

This repo has both `origin` (`saagpatel/WorkdayDebrief`) and
`legacy-origin` (`saagar210/WorkdayDebrief`) remotes. **Local clone's
`main` is tracking `origin/main` correctly** — no trap here, unlike
FreeLanceInvoice / PersonalKBDrafter / BattleGrid / PomGambler /
LegalDocsReview.

Specifically verified on `origin/main`:

- Tip: `1baceda` chore: add feature request issue template
- Substantive commits on `origin/main`:
  - `5e445f8` feat(dev): add lean dev mode and cleanup scripts
  - `82a2896` chore(deps): trim tokio features and remove stale ignore rules
- Tree on `origin/main` is a real Tauri 2 desktop app with rich
  aggregation surface:
  - `src-tauri/src/aggregation/{calendar,jira,toggl,mod}.rs`
  - `src-tauri/src/delivery/{email,file,slack,mod}.rs`
  - `src-tauri/src/llm/{mod,prompts}.rs`
  - `src-tauri/src/{commands,db,markdown,oauth,error,lib,main}.rs`
  - `src-tauri/migrations/001_initial.sql`
- Release scaffolding: none on `origin/main` (no `RELEASE-READINESS.md`,
  no `release-smoke.yml`)
- Default branch: `main`

---

## Legacy-origin orphan note

`legacy-origin/master` has no commits not on `origin/main`. Clean
state. Legacy bootstrap branches exist (`codex/bootstrap-tests-docs-v1`,
`codex/chore/bootstrap-codex-os`, etc.) but reflect frozen-account
bootstrap work and are not load-bearing.

---

## Current state in one paragraph

WorkdayDebrief is a Tauri 2 + React 19 desktop tool that pulls work
context from three sources — Jira tickets, Toggl time entries, and
Google Calendar events (via OAuth2) — and turns them into a daily
"workday debrief" with LLM-generated summaries. Delivery channels are
pluggable: email (via `lettre`), file output, and Slack webhook.
Storage is SQLite via `sqlx`. The aggregation layer is split per
source, the delivery layer is split per channel, and there's an
explicit `markdown.rs` for output formatting. Phased Tauri 2 +
TypeScript + Vite + Tailwind frontend.

For full detail see `README.md` on `origin/main`.

---

## Why "Release Frozen" instead of other dispositions

- **Active** — wrong. The product surface (3 source aggregators, 3
  delivery channels, LLM layer) looks complete; only signing is
  missing.
- **Cold Storage / Archived** — wrong. Recent commits and full
  src-tauri surface argue for live product.
- **Release Frozen** — correct. Joins the cluster.

This is the **14th signing cluster member**: DesktopPEt / ContentEngine
/ AIGCCore / Relay / FreeLanceInvoice / Nexus / DeepTank / OPscinema /
ShipKit / SignalFlow / PixelForge / DatabaseSchema / LegalDocsReview /
**WorkdayDebrief**.

---

## Unblock trigger (operator)

When ready to ship:

1. Wire Apple Developer ID + notarization credentials.
2. Decide LLM strategy for v1: bundle local model (Ollama?), require
   operator API keys (Claude / OpenAI), or both. WorkdayDebrief has
   `llm/prompts.rs` — the abstraction exists, the operator just needs
   to commit on a provider for the shipped product.
3. Decide OAuth2 + secrets posture for distribution. Three external
   integrations (Jira, Toggl, Google Calendar) plus Slack delivery
   means real credential management is needed — `src-tauri/src/oauth.rs`
   covers the Google flow but operator should confirm the others are
   distribution-ready before public release.
4. Cut v1.0.0 release tag.
5. Verify signed/notarized DMG opens cleanly with no Gatekeeper
   warnings.

Estimated operator time once credentials are in hand: ~4 hours
including OAuth registration cleanup and notarization round-trip.

---

## Portfolio operating system instructions

| Aspect | Posture |
|---|---|
| Portfolio status | `Release Frozen` |
| Review cadence | Suspend overdue counting |
| Resurface conditions | (a) Apple signing credentials wired, (b) operator picks LLM provider strategy, (c) operator confirms OAuth client IDs are distribution-ready for Jira/Toggl/Google, or (d) operator opens a v1.1 scope packet |
| Co-batch with | Signing cluster: DesktopPEt / ContentEngine / AIGCCore / Relay / FreeLanceInvoice / Nexus / DeepTank / OPscinema / ShipKit / SignalFlow / PixelForge / DatabaseSchema / LegalDocsReview / **WorkdayDebrief** — **now 14 repos** |
| Special concern | **External integration credentials.** Three OAuth integrations + one webhook means more credential plumbing than typical desktop apps before public distribution. |

---

## Why this row has an OAuth concern

Most signing-cluster repos have local-only state (file system, local
SQLite) and don't need OAuth client IDs registered for distribution.
WorkdayDebrief talks to three external services:

- **Jira** — API tokens or OAuth, per-instance
- **Toggl** — API token
- **Google Calendar** — OAuth2 with registered client ID/secret
- **Slack** — incoming webhook (or bot token)

If the operator's current `oauth.rs` uses development OAuth credentials
or hardcoded client IDs, those need to be rotated to production
credentials before a public distribution. This is a categorically
different concern from "the app builds and signs" and worth raising
explicitly.

---

## Reactivation procedure (for the next code session)

1. Verify `git branch -vv` shows `main` tracking `origin/main`.
   This repo's local tracking was correct as of this disposition.
2. Review the local stash (`r8-workdaydebrief-stash`) — contains
   modifications to `package.json`, `vite.config.ts`, `AGENTS.md`,
   plus untracked husky/, perf scripts, test files. Decide what
   belongs on `origin/main`.
3. Delete stale `codex/*` branches that pre-date the current
   `origin/main` tip.
4. Re-run `pnpm install && pnpm tauri build` to confirm the
   toolchain still works.
5. **Audit OAuth credentials for distribution-readiness before
   signing.**

---

## Last known reference

| Field | Value |
|---|---|
| `origin/main` tip | `1baceda` chore: add feature request issue template |
| Last substantive commit | `5e445f8` feat(dev): add lean dev mode and cleanup scripts |
| Default branch | `main` |
| Build system | Tauri 2 + Rust + React 19 + TypeScript + Vite + Tailwind + SQLite (sqlx) |
| External integrations | Jira + Toggl + Google Calendar (OAuth2) + Slack (webhook); email via lettre |
| Release scaffolding | **None on `origin/main`** |
| Build verification status | Untested in this pass — needs `pnpm tauri build` smoke |
| Blocker | Apple signing + LLM provider decision + OAuth distribution-readiness (operator-only) |
| Migration state | `legacy-origin` present but local tracking is correct; no orphans on legacy-origin/master |
| Distinguishing feature | **Three OAuth integrations + Slack webhook** — credential plumbing is part of the release-readiness scope, not just signing |
