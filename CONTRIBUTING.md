# Contributing

Everything here applies to [`docs/ai-starter-guide.md`](docs/ai-starter-guide.md) and any future document under `docs/`.

## How to make a change

1. Branch off `main` and edit the Markdown directly.
2. Open a PR describing what changed and, for anything policy-adjacent, who needs to approve it.

## Review bar

The guide's own *Change Process* section sets the bar. Classify your change before requesting review.

**Low-risk — normal review is enough:**

- Clarifying language
- Fixing typos
- Improving examples without changing policy meaning
- Adding links to already-approved resources
- Making navigation easier

**Higher-risk — must be reviewed by the relevant owner before merging:**

- New guidance about sensitive data
- New approved or unapproved tools
- New model, tenant, connector, MCP, plugin, hook, or agent guidance
- New role-specific advice for HR, legal, finance, security, compliance, or customer commitments
- Any change that could be read as permission to use real client, employee, regulated, or confidential data

If you are unsure which bucket your change falls into, treat it as higher-risk.

## Owners

The guide's *Ownership and Maintenance* section defines the ownership model — overall guide, security and privacy, legal/compliance/HR/finance, tooling and integrations, and role examples each have a named owner.

## Editing conventions

- **Keep navigation in sync.** Adding, renaming, or removing a section means updating the *Table of Contents*, the *Start Here: Pick Your Problem* tables, and any in-document anchor links that point at it. Anchors are GitHub-style slugs of the heading text.
- **Keep the back-links.** Each top-level section starts with `[Back to Start Here](#start-here-pick-your-problem)`.
- **Keep the front matter current.** The `Status`, `Audience`, and `Source check` lines at the top of the guide are part of the document's authority — update `Source check` when you verify links, model names, or product behavior.
- **Do not use real data.** Examples must not contain real client, employee, or regulated data, even sanitized-looking fragments.
- **Do not invent company specifics.** Where the guide defers to company policy or a named owner, keep the deferral. Do not fill it in with plausible-sounding guesses.

## Status labels

- **Draft** — useful but not approved as official guidance (current state)
- **Reviewed** — checked by relevant owners for the current rollout
- **Approved** — accepted as official internal guidance for a defined scope
- **Deprecated** — kept for history but no longer current

## Review cadence

Review the guide at least quarterly, and additionally:

- When a major Claude, Codex, or company AI tool changes
- When new models, surfaces, connectors, or permission modes roll out
- When company policy or client requirements change
- After a serious AI-related mistake, near miss, or support pattern
- After feedback from new users or non-technical readers

## Feedback

Open an issue or PR for:

- Confusing sections
- Missing examples
- Unsafe or outdated advice
- Links that no longer work
- Claude features that do not match the company tenant
- Workflows that deserve a skill, instruction file, hook, MCP integration, or plugin
