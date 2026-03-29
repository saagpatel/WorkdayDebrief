# WorkdayDebrief

[![Rust](https://img.shields.io/badge/Rust-dea584?style=flat-square&logo=rust)](#) [![License](https://img.shields.io/badge/license-MIT-blue?style=flat-square)](#)

> End every workday with a clear narrative — generated locally from what you actually did.

WorkdayDebrief aggregates your daily activity from Jira, Google Calendar, and Toggl, then uses a local Ollama model to generate a coherent end-of-day summary. Review and edit the narrative, then deliver it via email, Slack, or file export. Everything stays local in SQLite — no cloud, no subscriptions.

## Features

- **Activity aggregation** — pulls from Jira tickets, Google Calendar events, and Toggl time entries
- **Local LLM narrative** — Ollama generates human-readable summaries from raw activity data
- **Review and edit** — full text editing before delivery, with tone and length controls
- **Flexible delivery** — send via email (lettre), post to Slack, or export to file
- **Summary history** — SQLite stores all past summaries for review and pattern analysis

## Quick Start

### Prerequisites
- macOS, Node.js, npm
- Rust toolchain (`rustup`)
- [Ollama](https://ollama.com/) running locally

### Installation
```bash
npm ci
```

### Usage
```bash
npm run tauri dev
```

## Tech Stack

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

## License

MIT
