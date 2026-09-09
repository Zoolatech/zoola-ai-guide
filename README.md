# zoola-ai-guide

Internal AI enablement documentation. This repo holds the source of truth for our AI usage guidance and publishes it automatically to Google Cloud Storage.

## Contents

| Path | What it is |
| --- | --- |
| [`docs/ai-starter-guide.md`](docs/ai-starter-guide.md) | **AI Effectiveness Guide for Claude Code** — the main document (~3.2k lines). Practical guidance on using AI as a durable work partner, for both technical and non-technical roles. |
| [`CONTRIBUTING.md`](CONTRIBUTING.md) | How to change the guide: review bar, editing conventions, status labels, review cadence. |
| `.github/workflows/main.yml` | Publishing pipeline: syncs `docs/` to GCS on every push to `main`. |

## The guide

`docs/ai-starter-guide.md` is written to be read non-linearly. It opens with a **Start Here: Pick Your Problem** table — find the problem closest to yours and jump to that section. A full Table of Contents follows it.

What it covers:

| Area | Sections |
| --- | --- |
| **Getting started** | One-Page Quick Start · What This Guide Is Not · Should I Use AI For This Task? |
| **Foundations** | Generative AI Refresher · Mental Model · Glossary · FAQ |
| **Safety and policy** | Do Not Blindly Trust AI · Security, Privacy, and Data Use · Company-Specific Rules · Work, Client, and Personal Boundaries · Ethics and Human Accountability · Minimum Responsible AI Checklist · When To Stop Using AI · Escalation Rules |
| **Prompting** | Core Prompting Pattern · Practical Prompting Techniques · Definition of Done · Context Is Fuel · Token Usage and Reasonable Use |
| **Claude Code mechanisms** | The Effectiveness Ladder · Daily Use vs Advanced Claude Code · Claude Modes, Surfaces, and Versions · Project Instructions (`CLAUDE.md`) · Choosing the Right Mechanism · Skills · Hooks · MCP · Plugins · Subagents and Parallel Work · Permissions and Safety |
| **External resources** | External Tools and Open-Source Resources · Approved External Resource Policy |
| **Rollout and review** | Measuring AI Quality · Ownership and Maintenance · Role-Based Guidance · Experience-Based Learning Paths · Common Anti-Patterns · Prompt Examples · Review Standards By Output Type · Review Checklist for AI Output |
| **Learning** | Claude Courses · Official Docs |

Most of it transfers to Codex, OpenCode, Cursor, and other agentic tools — the concepts hold, but file paths, commands, and configuration differ, so check each tool's own docs before porting a pattern.

### Status and authority

The guide is currently marked **draft**. It is practical enablement material, not policy. Per its own *What This Guide Is Not* section, when rules conflict, follow the stricter one in this order:

1. Client or customer requirements
2. Company policy
3. Legal, privacy, security, compliance, HR, or finance guidance
4. Tool or vendor terms
5. This guide

The **Company-Specific Rules** section (approved tools, tenants, data classes, approval owners) still contains `To be added` placeholders. Until those are filled in and approved, the guide grants no permission to use a specific tool, model, connector, or data class.

## Publishing

Pushing to `main` with changes under `docs/**` (or a manual `workflow_dispatch`) triggers `.github/workflows/main.yml`, which:

1. Authenticates to GCP via Workload Identity Federation (no long-lived keys; the service account comes from the `GCP_GHA_SA` secret).
2. Runs `gcloud storage rsync docs/ gs://gcp-eun-it-gcs-docs/ --recursive --delete-unmatched-destination-objects`.
3. Publishes a message to the `gcp-eun-it-sync` Pub/Sub topic to trigger an immediate downstream sync.

Notes:

- The sync is **mirroring** — files removed from `docs/` are deleted from the bucket.
- Only `docs/` is published. This README and other root files stay in the repo.
- Project: `it-monitoring-245619` · Region: `europe-north1`.

## Contributing

See [CONTRIBUTING.md](CONTRIBUTING.md) for the change process, review bar, editing conventions, status labels, and review cadence.
