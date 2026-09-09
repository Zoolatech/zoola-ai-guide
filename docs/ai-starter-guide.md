# AI Effectiveness Guide for Claude Code

Status: draft
Audience: everyone who uses or may use AI at work, across technical and non-technical roles
Source check: 2026-06-25

This guide is a starting point for using AI as a **durable work partner**, not just a better autocomplete box.

It focuses on Claude Code because it can do more than answer questions. Claude Code can read context, edit files, run tools, remember project instructions, use reusable workflows, and connect to external systems. That extra power is useful only when people understand which mechanism to use and when.

Most concepts in this guide also transfer to Codex, OpenCode, Cursor, and other agentic AI tools. The names, file paths, commands, and configuration details will differ, so use each tool's official documentation before applying a Claude Code pattern elsewhere.

This is **not** a replacement for official documentation. It explains the concepts in plain language, gives examples, and links to official docs when you need exact commands or reference details.

## Start Here: Pick Your Problem

Different readers will come here with different problems. Use this section as the front door.

> **How to use this guide:** Start with the problem that sounds closest to yours. You do not need to read the document linearly.

### Learn The Basics

| If this is your problem | Start with | Why |
| --- | --- | --- |
| "I want the shortest safe way to start." | [One-Page Quick Start](#one-page-quick-start), [Minimum Responsible AI Checklist](#minimum-responsible-ai-checklist) | Start with the basic workflow before choosing advanced Claude Code features. |
| "I already use AI, but I want a plain refresher on what Generative AI actually is." | [Generative AI Refresher](#generative-ai-refresher), [Mental Model](#mental-model), [Glossary](#glossary) | Start with the basic concept before moving into agentic tools, permissions, and reusable workflows. |
| "I do not know what Claude Code is good for." | [Mental Model](#mental-model), [Role-Based Guidance](#role-based-guidance), [Prompt Examples](#prompt-examples) | Start with what the tool is, what it is not, and concrete use cases. |
| "I do not understand the difference between Claude, Claude Code, Claude Cowork, modes, and models." | [Claude Modes, Surfaces, and Versions](#claude-modes-surfaces-and-versions), [Glossary](#glossary) | Many mistakes come from mixing product surfaces, permission modes, output styles, and model choices. |
| "I do not understand common AI terms." | [Glossary](#glossary), [Mental Model](#mental-model) | Shared language makes later sections easier to use. |
| "I am not sure whether I should use AI for this task at all." | [Should I Use AI For This Task?](#should-i-use-ai-for-this-task), [Security, Privacy, and Data Use](#security-privacy-and-data-use) | Some tasks are good AI candidates; some need approval, sanitization, or no AI. |
| "I am not sure whether this guide is policy, documentation, or advice." | [What This Guide Is Not](#what-this-guide-is-not), [Security, Privacy, and Data Use](#security-privacy-and-data-use) | Know the boundary between practical guidance, official policy, and product documentation. |
| "I need the company-specific rules before I use AI for work." | [Company-Specific Rules](#company-specific-rules), [Security, Privacy, and Data Use](#security-privacy-and-data-use) | General AI advice is not enough; company tool, tenant, data, and approval rules decide what is allowed. |
| "I need guidance for my role." | [Role-Based Guidance](#role-based-guidance), [Experience-Based Learning Paths](#experience-based-learning-paths) | Different roles share core habits but have different risks and workflows. |
| "I am new and need a learning path." | [Experience-Based Learning Paths](#experience-based-learning-paths), [Prompt Examples](#prompt-examples), [Review Checklist for AI Output](#review-checklist-for-ai-output) | Start with prompts and review before advanced features. |
| "I prefer guided training instead of reading the whole guide." | [Claude Courses](#claude-courses), [One-Page Quick Start](#one-page-quick-start) | Use a course for structured practice, then come back to this guide for policy, review, and workflow choices. |

### Improve Day-To-Day Output

| If this is your problem | Start with | Why |
| --- | --- | --- |
| "I ask several prompts but still do not get the answer I need." | [Core Prompting Pattern](#core-prompting-pattern), [Definition of Done](#definition-of-done), [Context Is Fuel](#context-is-fuel) | The request probably lacks role, context, constraints, output format, or verification. |
| "I know the basic prompt pattern, but I want better techniques." | [Practical Prompting Techniques](#practical-prompting-techniques), [Core Prompting Pattern](#core-prompting-pattern), [Common Anti-Patterns](#common-anti-patterns) | Use planning, examples, rubrics, critique loops, and source grounding for harder everyday tasks. |
| "I need to turn messy notes into a useful output." | [Core Prompting Pattern](#core-prompting-pattern), [Definition of Done](#definition-of-done), [Prompt Examples](#prompt-examples) | The output needs audience, format, and completeness criteria. |
| "I need help writing, rewriting, or summarizing something." | [Core Prompting Pattern](#core-prompting-pattern), [Role-Based Guidance](#role-based-guidance), [Review Checklist for AI Output](#review-checklist-for-ai-output) | Most writing tasks improve when audience, tone, and source constraints are explicit. |
| "I need help understanding a codebase or document set." | [Context Is Fuel](#context-is-fuel), [Core Prompting Pattern](#core-prompting-pattern), [Do Not Blindly Trust AI](#do-not-blindly-trust-ai) | Exploration should start with scoped context and end with verifiable claims. |
| "The session is too long and the AI lost the plot." | [Token Usage and Reasonable Use](#token-usage-and-reasonable-use), [Context Is Fuel](#context-is-fuel), [Measuring AI Quality](#measuring-ai-quality) | Long threads need summarization, pruning, or a restart with focused context. |
| "AI sessions are getting expensive, slow, or noisy." | [Token Usage and Reasonable Use](#token-usage-and-reasonable-use), [Context Is Fuel](#context-is-fuel), [Measuring AI Quality](#measuring-ai-quality) | Better context control usually improves quality and reduces waste. |
| "I want hands-on practice improving everyday Claude output." | [Claude Courses](#claude-courses), [Core Prompting Pattern](#core-prompting-pattern), [Review Checklist for AI Output](#review-checklist-for-ai-output) | Courses help build muscle memory; the guide helps keep the work scoped, reviewed, and safe. |

### Make Work Reusable

| If this is your problem | Start with | Why |
| --- | --- | --- |
| "I keep repeating the same setup prompt every session." | [Project Instructions](#project-instructions), [Skills](#skills) | Stable context should move out of the prompt and into reusable instructions or workflows. |
| "My team has rules the AI keeps forgetting." | [Project Instructions](#project-instructions), [Hooks](#hooks), [Role-Based Guidance](#role-based-guidance) | Team expectations should be stored where tools can consistently load or enforce them. |
| "I do not know whether to use a prompt, CLAUDE.md, skill, hook, MCP, or plugin." | [Choosing the Right Mechanism](#choosing-the-right-mechanism) | Different concepts solve different persistence, workflow, automation, and integration problems. |
| "I am not sure whether an advanced Claude Code feature is worth it." | [Daily Use vs Advanced Claude Code](#daily-use-vs-advanced-claude-code), [The Effectiveness Ladder](#the-effectiveness-ladder), [Choosing the Right Mechanism](#choosing-the-right-mechanism) | Start with daily habits, then add advanced mechanisms only when they solve a real repeated problem. |
| "I repeat the same multi-step workflow often." | [Skills](#skills) | A skill turns repeated prompt boilerplate into a reusable workflow. |
| "I want to reuse a workflow across my team." | [Skills](#skills), [Plugins](#plugins), [External Tools and Open-Source Resources](#external-tools-and-open-source-resources) | Team reuse needs packaging, review, and ownership. |
| "I want to learn reusable Claude mechanisms step by step." | [Claude Courses](#claude-courses), [Choosing the Right Mechanism](#choosing-the-right-mechanism), [Skills](#skills) | Use courses for guided setup, then use the guide to decide what belongs in prompts, instructions, skills, hooks, MCP, plugins, or subagents. |

### Use Tools And Automation

| If this is your problem | Start with | Why |
| --- | --- | --- |
| "I want Claude Code to edit files or run commands." | [Permissions and Safety](#permissions-and-safety), [Definition of Done](#definition-of-done), [Review Checklist for AI Output](#review-checklist-for-ai-output) | Agentic work needs boundaries, approvals, and review. |
| "I want examples or open-source resources to start from." | [External Tools and Open-Source Resources](#external-tools-and-open-source-resources), [Where To Find Skills](#where-to-find-skills), [Where To Find Plugins](#where-to-find-plugins), [Where To Find Subagents](#where-to-find-subagents) | Start from existing resources, then adapt them to company and customer policy. |
| "The AI needs current data from another tool." | [MCP](#mcp), [Plugins](#plugins) | External context should come from approved integrations, not copy-paste when avoidable. |
| "I want checks to happen automatically." | [Hooks](#hooks), [Permissions and Safety](#permissions-and-safety) | Mechanical checks belong in automation, not in every prompt. |
| "I am not sure whether an external tool or GitHub repo is safe to use." | [Approved External Resource Policy](#approved-external-resource-policy), [External Tools and Open-Source Resources](#external-tools-and-open-source-resources), [Security, Privacy, and Data Use](#security-privacy-and-data-use) | Open source still needs approval, license review, and data-flow review. |
| "I want guided Claude Code training for tools, MCP, hooks, or subagents." | [Claude Courses](#claude-courses), [Permissions and Safety](#permissions-and-safety), [MCP](#mcp) | Learn the feature mechanics in a course, then check permissions, data boundaries, and review standards here. |

### Stay Safe And Accountable

| If this is your problem | Start with | Why |
| --- | --- | --- |
| "The AI gives plausible answers, but I do not fully trust them." | [Do Not Blindly Trust AI](#do-not-blindly-trust-ai), [Review Checklist for AI Output](#review-checklist-for-ai-output), [Measuring AI Quality](#measuring-ai-quality) | You need to separate generation from validation. |
| "I am not sure whether I can paste this data into AI." | [Company-Specific Rules](#company-specific-rules), [Security, Privacy, and Data Use](#security-privacy-and-data-use) | AI use must follow company, client, legal, and privacy boundaries. |
| "I use a client-provided model or personal AI account and want to know the boundary." | [Work, Client, and Personal Boundaries](#work-client-and-personal-boundaries) | Tool ownership and data ownership matter as much as the model quality. |
| "I need to know whether an AI use case is fair or appropriate." | [Ethics and Human Accountability](#ethics-and-human-accountability) | AI can assist decisions, but people own consequences and sensitive judgments. |
| "I am worried about hallucinations, privacy, cost, ownership, review, or job impact." | [FAQ](#faq), [Do Not Blindly Trust AI](#do-not-blindly-trust-ai), [Security, Privacy, and Data Use](#security-privacy-and-data-use) | Common fears usually need clear boundaries, review habits, and escalation paths. |
| "I need a quick checklist before using or sharing AI output." | [Minimum Responsible AI Checklist](#minimum-responsible-ai-checklist), [Review Checklist for AI Output](#review-checklist-for-ai-output) | A small checklist catches most preventable mistakes. |
| "AI keeps failing and I do not know when to stop." | [When To Stop Using AI](#when-to-stop-using-ai), [Measuring AI Quality](#measuring-ai-quality) | Repeated prompting is not always the right next step. |
| "I do not know when to involve a human owner." | [Escalation Rules](#escalation-rules), [When To Stop Using AI](#when-to-stop-using-ai) | Some situations require review, approval, or expert judgment before the work continues. |
| "I need to review a specific type of AI output." | [Review Standards By Output Type](#review-standards-by-output-type), [Review Checklist for AI Output](#review-checklist-for-ai-output) | Meeting notes, client emails, code, research, and HR/legal/security work fail in different ways. |

### Measure And Roll Out

| If this is your problem | Start with | Why |
| --- | --- | --- |
| "I want to know if this approach actually improved the result." | [Measuring AI Quality](#measuring-ai-quality) | Compare outputs with a small rubric, not only with intuition. |
| "I manage a team and need a rollout path." | [Role-Based Guidance](#role-based-guidance), [Experience-Based Learning Paths](#experience-based-learning-paths), [Measuring AI Quality](#measuring-ai-quality) | Adoption should be staged by need, experience level, and evidence. |
| "I need to know who owns this guidance and how it stays current." | [Ownership and Maintenance](#ownership-and-maintenance), [Measuring AI Quality](#measuring-ai-quality) | AI guidance gets stale unless ownership, review cadence, and approval paths are explicit. |
| "I need training resources for a team rollout." | [Claude Courses](#claude-courses), [Experience-Based Learning Paths](#experience-based-learning-paths), [Measuring AI Quality](#measuring-ai-quality) | Courses provide shared practice material; the guide provides rollout, review, and measurement framing. |

## Table of Contents

- [One-Page Quick Start](#one-page-quick-start)
- [What This Guide Is Not](#what-this-guide-is-not)
- [Should I Use AI For This Task?](#should-i-use-ai-for-this-task)
- [Generative AI Refresher](#generative-ai-refresher)
- [Mental Model](#mental-model)
- [Glossary](#glossary)
- [FAQ](#faq)
- [Do Not Blindly Trust AI](#do-not-blindly-trust-ai)
- [Security, Privacy, and Data Use](#security-privacy-and-data-use)
- [Company-Specific Rules](#company-specific-rules)
- [Work, Client, and Personal Boundaries](#work-client-and-personal-boundaries)
- [Ethics and Human Accountability](#ethics-and-human-accountability)
- [Minimum Responsible AI Checklist](#minimum-responsible-ai-checklist)
- [When To Stop Using AI](#when-to-stop-using-ai)
- [Escalation Rules](#escalation-rules)
- [Core Prompting Pattern](#core-prompting-pattern)
- [Practical Prompting Techniques](#practical-prompting-techniques)
- [Definition of Done](#definition-of-done)
- [Context Is Fuel](#context-is-fuel)
- [Token Usage and Reasonable Use](#token-usage-and-reasonable-use)
- [The Effectiveness Ladder](#the-effectiveness-ladder)
- [Daily Use vs Advanced Claude Code](#daily-use-vs-advanced-claude-code)
- [Claude Modes, Surfaces, and Versions](#claude-modes-surfaces-and-versions)
- [Project Instructions](#project-instructions)
- [Choosing the Right Mechanism](#choosing-the-right-mechanism)
- [Skills](#skills)
- [Hooks](#hooks)
- [MCP](#mcp)
- [Plugins](#plugins)
- [Subagents and Parallel Work](#subagents-and-parallel-work)
- [Permissions and Safety](#permissions-and-safety)
- [External Tools and Open-Source Resources](#external-tools-and-open-source-resources)
- [Approved External Resource Policy](#approved-external-resource-policy)
- [Measuring AI Quality](#measuring-ai-quality)
- [Ownership and Maintenance](#ownership-and-maintenance)
- [Role-Based Guidance](#role-based-guidance)
- [Experience-Based Learning Paths](#experience-based-learning-paths)
- [Common Anti-Patterns](#common-anti-patterns)
- [Prompt Examples](#prompt-examples)
- [Review Standards By Output Type](#review-standards-by-output-type)
- [Review Checklist for AI Output](#review-checklist-for-ai-output)
- [Claude Courses](#claude-courses)
- [Official Docs](#official-docs)

## One-Page Quick Start

[Back to Start Here](#start-here-pick-your-problem)

> **If you read only one section, use this workflow.**

### 1. Decide If AI Belongs In The Task

**Use AI** for drafting, summarizing, comparing, explaining, organizing, reviewing, generating options, and producing a first pass.

**Do not use AI** when the data, tenant, policy, review owner, or business risk is unclear.

Read next: [Should I Use AI For This Task?](#should-i-use-ai-for-this-task)

### 2. Protect Data Before Prompting

Before you paste or connect anything:

- Use only approved tools, tenants, models, accounts, and integrations.
- Remove secrets, credentials, private keys, and unnecessary personal or client data.
- Check whether client, legal, privacy, or security rules apply.
- Stop and ask when the data classification is unclear.

Read next: [Security, Privacy, and Data Use](#security-privacy-and-data-use) and [Company-Specific Rules](#company-specific-rules)

### 3. Prompt With Five Parts

Use this structure:

```text
Act as: [role or perspective]
Task: [what you need done]
Context: [source material, audience, constraints, background]
Definition of done: [what a good answer must include or avoid]
Output format: [bullets, table, email draft, checklist, code diff, etc.]
```

Example:

```text
Act as a careful operations partner.
Task: turn these meeting notes into action items.
Context: audience is the project team; do not invent owners or deadlines.
Definition of done: separate confirmed actions from open questions.
Output format: Markdown table with action, owner, deadline, source note, and uncertainty.
```

Read next: [Core Prompting Pattern](#core-prompting-pattern) and [Definition of Done](#definition-of-done)

### 4. Ask For Assumptions And Risks

Add one line to important prompts:

```text
Before finalizing, list assumptions, missing context, risks, and anything I should verify.
```

This makes the output **easier to review** and reduces hidden overconfidence.

Read next: [Do Not Blindly Trust AI](#do-not-blindly-trust-ai)

### 5. Review Before You Use The Output

Before **sending, shipping, or relying** on AI output:

- Verify facts, numbers, links, names, dates, and quotes.
- Check whether the answer follows the requested audience, tone, and format.
- Confirm no sensitive data was exposed.
- Confirm a human owns the final decision.
- Run tests or source checks when the output affects code, customers, money, people, policy, or security.

Read next: [Review Checklist for AI Output](#review-checklist-for-ai-output)

### 6. Move Repeated Work Out Of The Prompt

If you repeat the same setup often:

- Put stable repo or team context in [Project Instructions](#project-instructions).
- Turn repeatable workflows into [Skills](#skills).
- Use [Hooks](#hooks) for mechanical checks.
- Use [MCP](#mcp) for approved access to external systems.
- Use [Plugins](#plugins) when reusable capability needs packaging and distribution.

Anti-patterns:

- Starting with advanced features before basic prompting and review work
- Pasting sensitive data before checking the tenant and policy
- Asking AI to make the final decision for high-risk work
- Reusing output without verifying it

## What This Guide Is Not

[Back to Start Here](#start-here-pick-your-problem)

This guide is practical enablement material. It helps coworkers understand how to use AI and Claude Code-style tools more effectively, but it does not replace official sources of authority.

This guide is **not**:

- A replacement for company security, privacy, legal, compliance, HR, finance, or client-data policy
- A list of approved tools, models, tenants, accounts, connectors, plugins, or external repositories
- A guarantee that a specific Claude feature is enabled in your company tenant
- A substitute for Anthropic, OpenAI, cloud-provider, or vendor documentation
- A substitute for required human review, expert judgment, or approval
- A promise that AI output is correct, safe, unbiased, or ready to send

Use this guide to choose a good workflow. Use official policy and designated owners to decide what is allowed.

When there is a conflict, follow the stricter rule:

1. Client or customer requirements
2. Company policy
3. Legal, privacy, security, compliance, HR, or finance guidance
4. Tool or vendor terms
5. This guide

If the guide says "you can," read that as **"you can when the approved tool, tenant, policy, data class, and review owner allow it."**

Anti-patterns:

- Treating practical examples as approval to use real customer, employee, or regulated data
- Assuming a public Claude feature is enabled or approved internally
- Using this guide to bypass a required reviewer
- Treating official docs as company policy

## Should I Use AI For This Task?

[Back to Start Here](#start-here-pick-your-problem)

> **Use AI when it helps you move faster without hiding risk.**

**Short decision tree:**

1. Does the task involve secrets, credentials, private employee data, regulated data, or client confidential data?
   - Yes: use only an approved company or client environment for that data class. If no approved environment exists, do not use AI for that data.
   - No: continue.
2. Would a wrong answer cause legal, financial, security, employment, customer, or reputational harm?
   - Yes: AI can help draft, structure, or check, but a qualified human must own the decision and review the output.
   - No: continue.
3. Do you have enough context to judge the output?
   - Yes: use AI and verify the result.
   - No: first gather sources, examples, constraints, and acceptance criteria.
4. Is the task mostly about drafting, summarizing, comparing, brainstorming, explaining, organizing, reviewing, or producing a first pass?
   - Yes: AI is usually a good fit.
   - No: continue.
5. Is the task simple, faster manually, or already automated by a reliable system?
   - Yes: skip AI.
   - No: try AI with a clear definition of done and review the result.
6. Will you repeat this task often?
   - Yes: consider [Project Instructions](#project-instructions), [Skills](#skills), [Hooks](#hooks), [MCP](#mcp), or [Plugins](#plugins).
   - No: a normal prompt is enough.

Good AI candidates:

- First drafts
- Summaries of approved material
- Code or document exploration
- Reformatting and restructuring
- Review against a checklist
- Generating options before a human chooses
- Explaining unfamiliar concepts

Poor AI candidates:

- Entering secrets into an unapproved tool
- Making final people, legal, compliance, medical, security, or financial decisions
- Replacing required expert review
- Guessing facts without sources
- Copying client or company data into a personal account
- Solving a task where you cannot judge whether the output is correct

Anti-patterns:

- Using AI because it feels modern, not because it improves the task
- Asking AI to decide when the human decision owner is unclear
- Pasting sensitive data first and thinking about policy later
- Treating speed as the only success metric

## Generative AI Refresher

[Back to Start Here](#start-here-pick-your-problem)

Most coworkers do not need a deep technical explanation of Generative AI. They do need a shared mental model that is accurate enough to use it responsibly.

**Generative AI creates new output from patterns in data and the context you provide.** It can write text, summarize documents, draft code, transform notes, classify information, generate ideas, and reason through a task. It does this by predicting useful next steps or next words from the prompt, the conversation, connected tools, and any files or sources it can access.

That makes it very useful for knowledge work, but it also explains many failure modes:

- It can sound confident when it is wrong.
- It may fill gaps when context is missing.
- It may follow the shape of your request even when the request is flawed.
- It does not automatically know company policy, customer promises, or private context.
- It does not own the consequences of the work.

**Generative AI is not the same as search.** Search finds existing pages or records. Generative AI creates an answer. If you need current facts, exact policy, prices, laws, customer commitments, or source-backed claims, the AI needs approved sources or tools and the human still needs to verify the result.

**Generative AI is not the same as automation.** Traditional automation follows fixed rules. Generative AI is more flexible, which makes it useful for messy inputs and ambiguous work, but also less predictable. For repeated high-stakes actions, prefer deterministic systems, approved workflows, or human review.

**Generative AI is not the same as judgment.** It can help compare options, list tradeoffs, critique a draft, or surface missing assumptions. The accountable person or team still decides.

The practical takeaway:

- Use AI to produce a draft, structure, analysis, review, plan, or set of options.
- Give it the context a competent coworker would need.
- Tell it what constraints matter.
- Ask it to show assumptions, risks, and unknowns.
- Verify the parts that matter before using the output.

Everyday examples:

| Task | Good use of GenAI | Human responsibility |
| --- | --- | --- |
| Meeting notes | Turn notes into decisions, owners, open questions, and risks. | Confirm decisions and owners against the source. |
| Policy explanation | Rewrite approved policy in plain language. | Make sure meaning did not change and required reviewers approve. |
| Research synthesis | Group approved source material into themes. | Check sources, evidence, dates, and missing perspectives. |
| Code work | Explore files, propose a change, implement, and run tests. | Review diff, risks, and test results. |
| Customer communication | Draft a clearer response. | Verify facts, tone, commitments, and approval needs. |

Anti-patterns:

- Asking AI for "the answer" when you actually need a sourced decision
- Treating a fluent summary as evidence that the source was understood correctly
- Using AI output without knowing what data or sources it used
- Asking AI to make final decisions about people, money, law, compliance, security, or customer commitments

## Mental Model

[Back to Start Here](#start-here-pick-your-problem)

**Generative AI is a prediction and reasoning system** that works from instructions, context, tools, and feedback.

It is **not** a database, policy owner, legal authority, manager, reviewer of record, or replacement for human accountability.

Claude Code sits on that foundation, but it is not only a chat window.

Claude Code is an agentic work environment. It can inspect files, use tools, edit files, run commands, follow project instructions, and iterate toward a result. That makes it closer to a junior teammate with tools than to a search box.

**A simple chatbot gives you an answer.**

**An agent can gather context, make changes, run tools, and verify work.**

That means your job changes. You are not only asking questions. You are setting up a **working agreement**:

- What are we trying to achieve?
- What context matters?
- What constraints must not be violated?
- What should be checked before calling the work done?
- What should the AI ask before doing?
- What can it do without asking?

### What AI Is Good At

AI is good at:

- Turning messy input into structure
- Drafting and rewriting
- Explaining unfamiliar material
- Finding patterns across text or code
- Generating options
- Applying a checklist consistently
- Exploring a codebase faster than a human can manually click around
- Producing a first pass that a human can review

### What AI Is Not Good At By Default

AI is not automatically good at:

- Knowing hidden company context
- Knowing whether a statement is allowed by policy
- Understanding unstated priorities
- Verifying facts without sources or tools
- Reading your mind about audience, tone, or risk tolerance
- Owning consequences
- Knowing what "done" means unless you define it

Most disappointing AI output comes from one of these gaps:

- Missing context
- Vague task
- No definition of done
- No examples of good output
- No permission boundary
- No verification step

### The Right Expectation

> **Expect AI to accelerate work, not remove judgment.**

For low-risk work, AI can often produce a usable answer directly.

For important work, treat AI output as a draft, proposal, or implementation candidate that needs review.

For regulated, sensitive, financial, legal, security, or employment-impacting work, use AI as an assistant and keep human ownership explicit.

Anti-patterns:

- Treating AI as a source of truth instead of a working assistant
- Assuming a confident answer is a verified answer
- Asking AI to own decisions that humans must own
- Giving broad tool access before defining boundaries

This is why **"prompting" is only level one**.

## Glossary

[Back to Start Here](#start-here-pick-your-problem)

| Term | Plain-language meaning | Why it matters |
| --- | --- | --- |
| Prompt | The instruction or request you give to AI. | A vague prompt produces vague work. A good prompt gives role, task, context, constraints, and definition of done. |
| Model | The underlying AI system that reads your input and generates output. | Different models have different strengths, costs, speed, context limits, and risk profiles. |
| Token | A small chunk of text the model reads or writes. | Tokens affect cost, speed, and how much context can fit in one session. |
| Context | The background information the AI can use right now. | AI usually performs better when it has the right files, examples, goals, constraints, and source material. |
| Agent | AI that can take steps toward a goal, often by using tools. | Claude Code is agentic: it can inspect files, edit, run commands, and iterate instead of only answering. |
| Tool | A capability the AI can call, such as reading files, searching docs, running tests, or querying a system. | Tools let AI work with real context, but they also require permissions, review, and policy boundaries. |
| Surface | The place where you use Claude, such as Chat, Claude Code CLI, Claude Code Desktop, Claude Code on the web, or Cowork. | Different surfaces can have different tools, permissions, data boundaries, and workflows. |
| Permission mode | A Claude Code setting that controls when Claude can read, edit, run commands, or needs approval. | Permission modes are one of the main safety controls for agentic work. |
| Output style | A Claude Code setting that changes how Claude communicates and collaborates. | Output style can change tone and workflow guidance, but it does not change permissions. |
| MCP | Model Context Protocol: a standard way to connect AI tools to external systems and data sources. | MCP can reduce copy-paste and give AI approved access to current data, but each integration needs governance. |
| Skill | A reusable package of instructions, examples, and workflow knowledge for a specific task. | Skills reduce repeated prompt setup and help teams standardize good workflows. |
| Hook | Automation that runs at a specific moment in the AI workflow, such as before a tool call or after a file edit. | Hooks are useful for repeatable checks, policy reminders, and guardrails. |
| Plugin | An installable bundle that can package capabilities such as skills, hooks, MCP servers, commands, or related resources. | Plugins help distribute reusable capability, but they need ownership, review, and lifecycle management. |
| Tenant | A separated account, workspace, or environment with its own users, data, access rules, and governance. | Company, client, and personal tenants must not be mixed casually because data ownership and policy differ. |

Anti-patterns:

- Using technical terms without checking that everyone means the same thing
- Saying "the AI knows" when you mean "the current model may infer from provided context"
- Treating tools, skills, hooks, MCP, and plugins as interchangeable
- Ignoring tenant boundaries because two tools have similar names

## FAQ

[Back to Start Here](#start-here-pick-your-problem)

### What if AI hallucinates?

Assume AI can be wrong **even when it sounds confident**. Ask for assumptions, sources, and uncertainty. Verify factual claims against approved sources, tests, documents, or subject-matter experts.

### Can I paste private, client, or employee data into Claude Code?

Only if the tool, tenant, data type, and customer or company policy allow it. When unsure, stop and ask the relevant security, privacy, legal, or client owner. Redaction is useful, but it is not a replacement for policy.

### Will AI replace my job?

The useful framing is ownership, not replacement. AI can draft, summarize, explore, and automate parts of work. Humans still own judgment, context, relationships, accountability, and final decisions.

### Is AI expensive?

It can be. Cost comes from model usage, tokens, repeated attempts, tool calls, and human review time. Focused prompts, clean context, reusable skills, and short evaluation rubrics usually reduce waste.

### Who owns AI output?

Treat AI output as work product that needs the same ownership, review, policy checks, confidentiality handling, and quality standards as human-created work. Do not assume output is safe to publish, ship, or send to a client just because AI produced it.

### Do I still need review?

Yes. Review expectations depend on risk. Low-risk drafts may need a quick human pass. Customer-facing, code, financial, legal, security, HR, or policy-sensitive work needs stronger review and traceable sources or tests.

### Can I use a personal AI account for work?

Do not put company, client, employee, or confidential work data into a personal account unless policy explicitly allows it. Personal accounts usually have different ownership, retention, access, and audit rules.

### Can I use open-source skills, plugins, MCP servers, or agents from GitHub?

Only after the relevant approval. External tools can introduce license risk, data leakage, malicious code, unsupported dependencies, and customer policy violations. Start from them if useful, but review and adapt them before use.

### Should I disclose that AI helped?

Follow company, client, legal, and team expectations. When AI materially shaped a customer-facing, high-impact, or reviewed deliverable, transparency is usually safer than pretending it was fully manual.

Anti-patterns:

- Trusting confident wording instead of evidence
- Hiding AI use to avoid review
- Treating AI cost as only a tooling cost and ignoring rework
- Assuming ownership, privacy, and disclosure rules are the same in every tenant

## Do Not Blindly Trust AI

[Back to Start Here](#start-here-pick-your-problem)

AI can be **useful and wrong at the same time**. It can write clearly, sound confident, cite irrelevant sources, miss edge cases, or make assumptions you did not intend.

Blind trust is risky because AI output often **looks finished before it is verified**.

> **Rule:** the more important the outcome, the more explicit the verification.

For low-risk work, quick human review may be enough.

For important work, ask for assumptions, sources, tests, edge cases, and alternatives.

For high-risk work, require human review by the right owner before the output is used.

**Good validation prompts:**

```text
List the assumptions in your answer.
Separate facts from recommendations.
Flag anything that needs a source or human review.
```

```text
Critique your own answer.
Find the strongest reasons it might be wrong.
Return the top risks and how to verify them.
```

```text
Do not change the answer yet.
Create a verification checklist for this output.
Include tests, sources, edge cases, and reviewer questions.
```

Anti-patterns:

- Accepting AI output because it sounds confident
- Asking "are you sure?" instead of asking for evidence or verification
- Using AI-generated citations without opening them
- Letting AI be the only reviewer of sensitive decisions
- Shipping code or policy text without diff, test, or source review

## Security, Privacy, and Data Use

[Back to Start Here](#start-here-pick-your-problem)

> **The most important AI safety rule:** do not put data into an AI tool unless that tool, account, model, tenant, and use case are approved for that data.

**Treat AI input like sending data to another system.** The exact risk depends on the product, enterprise settings, retention policy, model provider, tenant, connector, and contract.

**Never paste these into AI unless an approved company process explicitly allows it:**

- Passwords
- API keys
- Private keys
- Access tokens
- Session cookies
- `.env` files
- Customer secrets
- Production credentials
- Unredacted security findings
- Sensitive personal data
- Confidential client data outside the approved client environment

> **If a secret is accidentally shared with AI, do not just delete the message.** Treat it as exposed: rotate or revoke the secret, notify the right internal owner, and follow the incident process.

**Use safer alternatives:**

- Redact names, emails, account IDs, tokens, and exact customer identifiers
- Use synthetic examples
- Share schemas instead of live data
- Share excerpts instead of full documents
- Use approved enterprise tools and connectors
- Ask the AI to work from a sanitized reproduction

Anti-patterns:

- Pasting secrets and planning to delete them later
- Sharing full customer documents when excerpts would work
- Moving client data into a non-client AI environment
- Using public AI tools for confidential work because they are convenient
- Assuming enterprise access automatically approves every data class

Useful prompt:

```text
Before answering, identify any sensitive data in this input.
If the task can be done with redacted or synthetic data, tell me what to remove.
Do not repeat secrets or personal data in your output.
```

For high-risk work, include the boundary in the prompt:

```text
This task may involve sensitive customer context.
Do not infer facts that are not present.
Do not include personal data in the final output.
Flag anything that needs legal, security, or privacy review.
```

Open-source security tools that may be useful in approved workflows:

- Gitleaks secret scanning: https://github.com/gitleaks/gitleaks
- TruffleHog secret scanning: https://github.com/trufflesecurity/trufflehog
- Semgrep static analysis: https://github.com/semgrep/semgrep
- OpenSSF Scorecard supply-chain checks: https://github.com/ossf/scorecard

**These tools can help detect risks, but they do not replace security review.** They must be approved for the environment and configured so scan inputs and outputs do not expose sensitive data.

## Company-Specific Rules

[Back to Start Here](#start-here-pick-your-problem)

This section is the place for company-specific AI rules. Until these details are filled in and approved, treat the guide as general guidance, not as permission to use a specific tool, tenant, model, connector, plugin, or data class.

> **Company rule of thumb:** use only approved AI tools, in approved accounts or tenants, for approved data classes, with the required human review.

### Approved AI Tools And Surfaces

Fill in the current company-approved options.

| Tool or surface | Approved for | Not approved for | Owner | Notes |
| --- | --- | --- | --- | --- |
| Company Claude tenant | To be added | To be added | To be added | To be added |
| Claude Code | To be added | To be added | To be added | To be added |
| Claude Cowork | To be added | To be added | To be added | To be added |
| Codex or other coding agents | To be added | To be added | To be added | To be added |
| Internal AI gateway or platform | To be added | To be added | To be added | To be added |
| Personal AI accounts | To be added | To be added | To be added | To be added |
| Client-provided AI environments | To be added | To be added | To be added | To be added |

Minimum rule:

- If a tool is not listed as approved for the specific data and use case, do not use it for that work.
- If a client provides a tool, use it only for that client's authorized purpose and data.
- If a tool is approved for one team, project, or data class, do not assume it is approved for all others.

### Data Classification Rules

Fill in the company's data classifications and examples.

| Data type | Example | Can it be used in approved AI tools? | Required handling | Required reviewer |
| --- | --- | --- | --- | --- |
| Public information | To be added | To be added | To be added | To be added |
| Internal business information | To be added | To be added | To be added | To be added |
| Confidential company information | To be added | To be added | To be added | To be added |
| Client confidential information | To be added | To be added | To be added | To be added |
| Employee or candidate personal data | To be added | To be added | To be added | To be added |
| Financial, legal, security, or regulated data | To be added | To be added | To be added | To be added |
| Secrets, credentials, keys, or tokens | To be added | To be added | To be added | To be added |

Default rules until the table is filled:

- Do not paste secrets, credentials, tokens, private keys, or `.env` files into AI.
- Do not put client confidential data into a non-client-approved environment.
- Do not put employee, candidate, compensation, legal, security, regulated, or financial decision data into AI unless policy explicitly allows it.
- Use sanitized, redacted, or synthetic examples when the real data is not required.
- When data classification is unclear, stop and ask the appropriate owner before prompting.

### Approved Models, Tenants, And Accounts

Fill in the model and tenant rules that apply to the company rollout.

| Item | Approved options | Restrictions | Owner |
| --- | --- | --- | --- |
| Company tenant or workspace | To be added | To be added | To be added |
| Client tenant or workspace | To be added | To be added | To be added |
| Model families or aliases | To be added | To be added | To be added |
| API access | To be added | To be added | To be added |
| Browser, desktop, IDE, or CLI surfaces | To be added | To be added | To be added |
| Connectors or integrations | To be added | To be added | To be added |
| Logging, retention, or monitoring settings | To be added | To be added | To be added |

Questions this table should answer:

- Which tenant should employees use for normal company work?
- Which tenant should be used for client work, if any?
- Which tools are allowed to access local files, repositories, browsers, tickets, docs, or cloud systems?
- Which models are allowed for which work?
- Which accounts are prohibited for company or client data?
- What logging, retention, or monitoring settings matter to users?

### Approval And Escalation Owners

Fill in the owners coworkers should contact before using AI in unclear or sensitive situations.

| Situation | Ask before using AI | Required reviewer before output is used |
| --- | --- | --- |
| Client confidential data | To be added | To be added |
| Employee, candidate, HR, or compensation data | To be added | To be added |
| Legal, compliance, or contract language | To be added | To be added |
| Security findings, vulnerability data, or credentials | To be added | To be added |
| Financial analysis or external reporting | To be added | To be added |
| Customer-facing commitments | To be added | To be added |
| New connector, MCP server, plugin, hook, or automation | To be added | To be added |
| External open-source resource | To be added | To be added |

### Required Disclosures And Review

Fill in when coworkers must disclose AI assistance or request review.

At minimum, define rules for:

- Client-facing materials
- External publication
- Legal, HR, finance, compliance, privacy, or security-sensitive work
- Code changes and pull requests
- Research or factual claims
- Decisions affecting people, money, customer commitments, or risk acceptance
- Outputs generated from confidential or regulated data

Suggested baseline:

- Disclose AI assistance when required by company, client, legal, or publication rules.
- Do not hide AI use to avoid review.
- Keep a human owner for every final decision.
- For high-risk work, keep enough source context, prompt context, and review notes to explain how the output was produced and checked.

### If You Are Unsure

Use this escalation prompt with a human owner, not with AI as the final authority:

```text
I want to use AI for this task:
[task]

The data involved is:
[data type, source, client/company ownership, and sensitivity]

The tool or tenant I plan to use is:
[tool, account, tenant, model, connector, or integration]

The output will be used for:
[audience, decision, customer impact, or internal workflow]

What is allowed, what must be removed or sanitized, and who must review the output?
```

Anti-patterns:

- Treating a general guide as approval for a specific data class
- Assuming a tool is approved because another team uses it
- Moving data between company, client, and personal tenants for convenience
- Asking AI whether a use case is allowed instead of checking policy
- Using redaction as a substitute for required approval

## Work, Client, and Personal Boundaries

[Back to Start Here](#start-here-pick-your-problem)

> **Keep tool context and data ownership aligned.**

Anti-patterns:

- Using a personal AI account for company work
- Using a company AI account for private side projects with confidential outside data
- Using a client-provided model for unrelated company work
- Using a client-provided model for personal work
- Moving client data into a non-client tenant
- Moving company data into a client tenant
- Reusing prompts, files, logs, or outputs across tenants without approval

**Client-provided AI environments should be treated as client environments.** Use them only for the client-authorized purpose, with client-authorized data, under the client's rules.

**Company AI environments should be used for company-authorized work**, with company-approved data and tools.

**Personal AI tools should not receive company or client confidential data unless policy explicitly allows it.** In most cases, personal tools are appropriate only for public information, generic learning, or fully sanitized examples.

When in doubt, ask:

- Who owns this data?
- Which tenant or account am I using?
- Is this tool approved for this data class?
- Could this output leak client, employee, security, or company-confidential information?
- Would I be comfortable explaining this data flow to security, legal, or the client?

## Ethics and Human Accountability

[Back to Start Here](#start-here-pick-your-problem)

> **AI can assist work, but humans remain accountable for decisions.**

Use extra caution when AI output affects:

- Hiring
- Performance reviews
- Compensation
- Promotions
- Disciplinary decisions
- Legal positions
- Security risk acceptance
- Financial decisions
- Customer commitments
- Accessibility or inclusion

Practical rules:

- Do not let AI be the only reviewer for consequential decisions
- Do not present AI-generated claims as verified facts without checking
- Do not ask AI to rank or judge people unless the use case is explicitly approved
- Do not use AI to bypass policy, access controls, licensing, or client boundaries
- Do not hide AI involvement when disclosure is required
- Do not use AI output that you cannot explain or defend

Anti-patterns:

- Asking AI to rank, judge, or profile people without an approved process
- Using AI to create a policy position without accountable review
- Presenting AI output as objective when it is a recommendation
- Using AI to avoid a difficult human decision
- Hiding AI use where disclosure is required

Good use:

```text
Review this policy draft for clarity and possible ambiguity.
Do not make legal claims.
Flag anything that needs legal or HR review.
```

Bad use:

```text
Rank these employees from strongest to weakest based on these private notes.
```

**For sensitive decisions, AI should help organize information, identify questions, and draft review materials.** It should not replace the accountable decision process.

## Minimum Responsible AI Checklist

[Back to Start Here](#start-here-pick-your-problem)

> **Use this checklist for any AI-assisted work.** For low-risk work, this takes less than a minute. For high-risk work, it tells you where to slow down.

### Before Using AI

- The task is appropriate for AI support.
- The tool, tenant, model, and account are approved for this work.
- The data classification is known.
- Secrets, credentials, private keys, and unnecessary sensitive data are removed.
- Client, legal, privacy, security, and contractual rules are respected.
- A human owner is clear.
- The definition of done is clear enough to review the output.

### While Working

- The prompt includes task, context, constraints, output format, and definition of done.
- The AI is asked to state assumptions, uncertainties, and missing context when relevant.
- Long sessions are summarized or restarted before they drift.
- The AI is not given broader tool access than the task requires.
- External tools, skills, plugins, MCP servers, and agents are used only when approved.

### Before Sharing Or Shipping Output

- Facts, numbers, names, dates, links, and quotes are verified.
- The output is checked against the requested audience, tone, and format.
- Sensitive data did not leak into the prompt, logs, generated files, screenshots, or output.
- High-risk work has the required human review.
- Code, configuration, or automation changes have appropriate tests or checks.
- AI use is disclosed when policy, client expectations, or the work context require it.
- The final owner accepts responsibility for the result.

### Before Installing Or Reusing External AI Resources

- The source is trusted enough for review.
- License and usage terms are acceptable.
- Data access is understood.
- Runtime behavior is understood.
- Maintenance owner is clear.
- Customer or company policy allows the resource.

Anti-patterns:

- Treating a checklist as approval
- Checking privacy only after the prompt is sent
- Letting the AI decide whether review is needed
- Installing an external tool because it is popular without reviewing access, code, and policy impact

## When To Stop Using AI

[Back to Start Here](#start-here-pick-your-problem)

> **Sometimes the best AI move is to stop, switch approach, or ask a person.**

**Stop using AI for the current attempt when:**

- You are unsure whether the data is allowed in the tool or tenant.
- The task needs a final legal, HR, security, compliance, medical, financial, or customer-impacting decision.
- Nobody owns review or final accountability.
- You cannot verify whether the answer is correct.
- The AI invents sources, names, policy, requirements, or facts.
- The AI keeps missing the same requirement after two or three focused attempts.
- The session has become long, contradictory, or hard to summarize.
- The AI asks for broad permissions or tool access without a clear reason.
- The task is faster, safer, or clearer to do manually.
- The output affects people and needs empathy, context, or judgment the AI does not have.

**What to do instead:**

- Ask the right human owner or subject-matter expert.
- Gather source material and restart with tighter context.
- Split the task into smaller parts.
- Use an approved system of record instead of a model guess.
- Switch from generation to review mode.
- Do the task manually and use AI only to check structure, clarity, or completeness.
- Document why AI was not appropriate if the case may repeat.

Anti-patterns:

- Continuing to prompt because you already spent time on the session
- Asking the AI to validate its own unsupported claim
- Giving more data or broader permissions to compensate for a vague task
- Treating a confident answer as a reason to skip expert review

## Escalation Rules

[Back to Start Here](#start-here-pick-your-problem)

**Escalation** means involving a human owner, reviewer, manager, security contact, privacy contact, legal contact, client owner, or subject-matter expert before continuing.

*This section is intentionally generic for now.* Replace the owner labels with company-specific teams, Slack channels, ticket queues, or approval paths after internal policy alignment.

### Escalate Before Using AI

Escalate before prompting or connecting tools when:

- You do not know the data classification.
- The task includes employee, candidate, customer, patient, financial, legal, security, or client-confidential information.
- You are not sure whether the selected tool, tenant, account, model, connector, MCP server, skill, hook, plugin, or agent is approved.
- The work uses a client-provided model, client tenant, personal account, or external tool outside the normal company environment.
- The task may violate a contract, policy, license, regulation, or customer expectation.
- The task would require access you do not normally have.

### Escalate While Working

Escalate during the session when:

- AI output conflicts with policy, source material, or expert guidance.
- AI invents sources, policy, numbers, legal language, requirements, or commitments.
- Claude asks for broader permissions than the task appears to require.
- You need to install or run an unreviewed external tool.
- The task expands from low-risk drafting into a decision, recommendation, or customer-facing deliverable.
- The session reveals sensitive data was included by mistake.
- The AI repeatedly fails after two or three focused attempts and the source of truth is unclear.

### Escalate Before Sharing, Shipping, Or Deciding

Escalate before using the output when it affects:

- Hiring, firing, promotion, compensation, performance review, or employee relations.
- Legal position, contract wording, privacy terms, compliance, or audit evidence.
- Security posture, vulnerability handling, access control, secrets, or incident response.
- Customer commitments, pricing, refunds, SLAs, roadmap promises, or public statements.
- Financial reporting, forecasting, budgeting, procurement, or investor-facing material.
- Medical, safety, regulated, or high-impact personal decisions.
- Production code, infrastructure, permissions, data migrations, or irreversible operations.

### What To Bring When You Escalate

Bring enough context that the reviewer can decide quickly:

- The task goal.
- The AI tool, tenant, account, model, and surface used.
- The data type and source.
- The prompt or summary of the prompt.
- The AI output or proposed action.
- The risk you see.
- The decision you need from the reviewer.
- Any deadline or business impact.

Good escalation note:

```text
I want to use Claude Code to summarize client-provided interview notes.
Data may include employee names and performance feedback.
The output would be used in an internal project staffing discussion.
I have not pasted the data yet.
Can this data be used in our company Claude tenant, and who needs to review the final summary?
```

Anti-patterns:

- Escalating only after sending sensitive data
- Asking AI whether escalation is required instead of checking policy
- Hiding AI use because review may slow the work down
- Treating manager approval as a substitute for security, privacy, legal, or client approval when those owners are required
- Continuing with a personal or external account because the approved tenant is inconvenient

## Core Prompting Pattern

[Back to Start Here](#start-here-pick-your-problem)

> **Use this template when the task matters.**

```text
Role:
Act as a [role] helping with [kind of work].

Context:
Here is the relevant background, files, data, audience, or decision history.

Task:
Do [specific outcome].

Constraints:
Follow these rules. Avoid these things. Ask before doing these actions.

Definition of done:
The work is done when [measurable result].

Verification:
Check the result by [test, review, command, source, rubric, stakeholder need].

Output format:
Return [bullets, table, patch, summary, decision memo, checklist].
```

**For small tasks, shorten it:**

```text
Summarize this meeting for a busy manager.
Focus on decisions, owners, deadlines, and unresolved questions.
Do not include personal opinions.
Return a table plus a 5-bullet executive summary.
```

**For engineering tasks:**

```text
Act as a senior engineer in this repo.
Find how authentication is handled, then propose the smallest safe change to add SSO.
Do not edit files yet.
Definition of done: I understand the affected files, risks, migration steps, and tests.
```

**For implementation:**

```text
Implement the agreed SSO change.
Keep the change minimal and consistent with existing patterns.
Run the relevant tests and fix failures caused by the change.
Definition of done: tests pass, no unrelated files changed, and the final answer lists changed files and remaining risks.
```

Anti-patterns:

- Asking for "something better" without audience or goal
- Combining many unrelated tasks into one prompt
- Omitting constraints and then rejecting reasonable output
- Asking "are you sure?" instead of asking for assumptions, tests, or sources
- Requesting a long answer when a decision table or checklist would be better

Official docs:

- Claude Code best practices: https://code.claude.com/docs/en/best-practices
- Claude Code prompt library: https://code.claude.com/docs/en/prompt-library

Courses:

- Claude 101: https://anthropic.skilljar.com/claude-101
- Building with the Claude API: https://anthropic.skilljar.com/claude-with-the-anthropic-api

Open-source starting points:

- Anthropic Claude cookbooks: https://github.com/anthropics/claude-cookbooks
- Anthropic prompt engineering tutorial: https://github.com/anthropics/prompt-eng-interactive-tutorial

**Use external prompt libraries as examples only.** Company or customer data, prompts, and outputs must stay within approved tools and approved data boundaries.

## Practical Prompting Techniques

[Back to Start Here](#start-here-pick-your-problem)

The core prompt pattern is enough for many tasks. Use these techniques when the task is important, ambiguous, repeated, or hard to review.

### Ask Before Answering

Use this when missing context would materially change the answer.

```text
Before answering, ask up to 5 clarifying questions if any missing information would change your recommendation.
If you can proceed with assumptions, list those assumptions first.
```

Good for:

- Policy drafts
- Customer communications
- Strategy work
- Ambiguous tickets
- Work where the audience or risk level is unclear

Anti-pattern: asking for clarifying questions on tiny tasks where a reasonable assumption is enough.

### Plan First

Use this when the work has multiple steps or could cause damage if started too quickly.

```text
Do not produce the final answer yet.
First propose a short plan, risks, assumptions, and what you need to verify.
Wait for my approval before executing the plan.
```

Good for:

- Code changes
- Data analysis
- Sensitive document edits
- Multi-step research
- Workflow automation

Anti-pattern: using plan-first prompting as a way to avoid giving clear goals.

### Give Examples

Use examples when style, format, or judgment matters.

```text
Here is an example of a good output:
[example]

Now produce the same kind of output for this new input:
[input]
```

Examples help with:

- Tone
- Table structure
- Level of detail
- Naming conventions
- Review comments
- Customer response style

Keep examples clean. Do not include private, client, employee, or regulated data unless the approved environment and policy allow it.

### Use Negative Constraints

Tell the AI what **not** to do when the default behavior is likely to drift.

```text
Do not invent dates, owners, customer commitments, legal interpretations, or policy exceptions.
If the source does not say it, mark it as unknown.
```

Useful negative constraints:

- Do not change the meaning.
- Do not add claims that are not in the source.
- Do not use marketing language.
- Do not make legal, financial, or HR recommendations.
- Do not edit files outside this folder.
- Do not install new dependencies without asking.

Anti-pattern: writing so many "do not" rules that the actual task becomes unclear.

### Ground The Answer In Sources

Use source-grounded prompting when factual accuracy matters.

```text
Use only the provided source material.
Separate facts from interpretations.
For each important claim, include the source section, link, file, or quote that supports it.
If the source does not answer something, say so.
```

Good for:

- Research briefs
- Client summaries
- Legal or policy-adjacent drafts
- Incident writeups
- Codebase explanations

Anti-pattern: asking for citations after the answer is written. Ask for source grounding before the model starts.

### Use Rubrics

Use a rubric when quality needs to be compared, not just admired.

```text
Score this draft from 1 to 5 on clarity, correctness, completeness, audience fit, and risk.
For each score, explain the reason and suggest the smallest improvement.
```

Rubrics are useful for:

- Comparing prompt versions
- Reviewing drafts
- Evaluating generated summaries
- Measuring whether a skill or workflow improved output
- Training a team on what "good" means

Anti-pattern: using vague rubric labels such as "quality" without defining what quality means for the task.

### Critique And Revise

Use this when the first draft is close but not good enough.

```text
Critique the draft against the goal, audience, constraints, and definition of done.
List the top 5 issues.
Then revise the draft to fix those issues without changing the intended meaning.
```

For higher-risk work, separate the steps:

```text
First critique only.
Do not rewrite yet.
Wait for me to choose which issues to fix.
```

Anti-pattern: asking the AI to approve its own high-risk output. A critique loop helps, but it does not replace a human reviewer.

### Debug Bad Output

When output is bad, do not only say "try again." Diagnose the prompt.

```text
The output missed the mark.
Analyze why: missing context, unclear task, wrong audience, weak constraints, bad output format, or missing definition of done.
Suggest a better prompt before retrying.
```

Common fixes:

- Add audience and decision context.
- Add source material or examples.
- Define what must be included and excluded.
- Ask for assumptions and unknowns.
- Change the output format.
- Split one giant request into smaller steps.

### Chain Techniques Without Making A Giant Prompt

For important work, a good sequence is often better than one huge prompt:

1. Ask what context is needed.
2. Provide source material.
3. Ask for a plan.
4. Approve or adjust the plan.
5. Ask for the draft or implementation.
6. Ask for critique against a rubric.
7. Verify the parts that matter.

Anti-patterns:

- Turning every prompt into a long ritual
- Using advanced prompting to compensate for missing source material
- Asking for chain-of-thought instead of asking for assumptions, evidence, risks, and checks
- Reusing a powerful prompt without adapting it to the data boundary and audience

## Definition of Done

[Back to Start Here](#start-here-pick-your-problem)

> **A definition of done is the difference between "please help" and "finish the job."**

**Weak:**

```text
Improve this document.
```

**Better:**

```text
Improve this document for non-technical employees.
Keep it under 900 words.
Remove jargon.
Preserve all policy requirements.
Definition of done: a new draft plus a 5-bullet summary of what changed.
```

For code, a definition of done often includes:

- Build passes
- Tests pass
- Lint passes
- Behavior is documented
- No unrelated changes
- Migration path is clear
- Security or privacy risks are called out

For business work, it often includes:

- Intended audience is clear
- Decisions are separated from discussion
- Owners and dates are explicit
- Assumptions are listed
- Risks are visible
- Output is in the right format

Anti-patterns:

- Treating "looks good" as done
- Defining done only after the AI returns an answer
- Omitting who will review or use the result
- Asking for implementation without saying how to verify it

## Context Is Fuel

[Back to Start Here](#start-here-pick-your-problem)

> **AI quality depends heavily on context quality.**

Useful context includes:

- The actual file, diff, ticket, meeting transcript, policy, spreadsheet, or design brief
- Who the output is for
- What decision will be made from the output
- What has already been tried
- What is out of scope
- What "good" looks like

Anti-patterns:

- "Make this better" with no audience
- "Fix the bug" with no reproduction steps
- "Summarize this" without saying what the summary will be used for
- "Write a strategy" without constraints, timeline, or tradeoffs
- Pasting huge context without saying what matters
- Reusing stale context from an old thread

**Good context pattern:**

```text
I need to send this to directors who have 3 minutes.
They care about risk, timeline, and cost.
Summarize only what changed since last week.
Flag anything that requires a decision.
```

## Token Usage and Reasonable Use

[Back to Start Here](#start-here-pick-your-problem)

**Tokens are the text the model reads and writes.** Large prompts, long files, repeated context, long conversations, logs, generated code, and tool outputs all consume tokens.

Token usage matters because it affects **cost, speed, context quality, and reliability**. More tokens are not automatically better. A huge context window can still bury the important facts.

> **Reasonable AI use** means giving enough context to solve the task, but not dumping everything "just in case."

Model choice also affects cost and speed. Claude model families exist because different tasks need different tradeoffs:

- Haiku-style models are built for fast, lower-cost work such as classification, simple extraction, short summaries, and first-pass drafts.
- Sonnet-style models are the balanced default for most daily work: capable enough for many reasoning, writing, coding, and analysis tasks without always paying for the top tier.
- Opus-style models are for harder reasoning, complex debugging, architecture, high-ambiguity reviews, and work where quality is worth extra latency and cost.
- Fable-style models, when available, are for the most demanding long-horizon agentic work.
- Mythos or preview models may be limited-access or specialized. Do not assume your tenant has them.

As of the 2026-06-25 source check, Anthropic's public API pricing shows current relative costs this way: Haiku 4.5 is $1 input / $5 output per million tokens, Sonnet 4.6 is $3 input / $15 output per million tokens, Opus 4.8 is $5 input / $25 output per million tokens, and Fable 5 is $10 input / $50 output per million tokens. These prices can change, and company plans may use subscription limits, enterprise terms, gateways, or cloud-provider pricing instead of direct API pricing.

**Good token habits:**

- Start with the smallest useful context
- Prefer relevant excerpts over full documents
- Summarize long background before asking for a decision
- Do the task manually when it is faster, safer, and does not benefit from AI
- Ask the AI what context it needs before pasting large files
- Use project instructions for stable context instead of repeating it
- Use skills for repeated workflows instead of long setup prompts
- Start a new thread when the old thread has drifted
- Ask for concise outputs when you only need a decision or checklist

**When working with code:**

- Point to relevant files or symptoms first
- Let the agent inspect the repo instead of pasting large trees manually
- Avoid pasting full logs when the last error block is enough
- Ask for a plan before a large implementation
- Use focused subagents or separate threads for independent work

Useful prompt:

```text
Before I paste more context, tell me the minimum information you need.
List files, logs, examples, or decisions that would materially change your answer.
```

Useful prompt for long threads:

```text
Summarize the current state, decisions made, open questions, and exact next step.
Keep only context needed to continue.
```

**Usage and observability tools may read local session logs, prompts, file paths, tool calls, or model outputs.** Approve them before using them with company or customer work.

Anti-patterns:

- Pasting entire documents when one section is relevant
- Keeping one endless thread for unrelated work
- Asking for long explanations when a checklist is enough
- Repeating the same setup prompt instead of using instructions or skills
- Letting tool output flood the conversation without summarizing what matters

## The Effectiveness Ladder

Use this ladder to decide **what to learn next**.

| Level | Capability | What changes |
| --- | --- | --- |
| 1 | Better prompts | You get clearer, more useful answers. |
| 2 | Better context | The AI stops guessing and starts working from real inputs. |
| 3 | Project instructions | The AI follows team norms without you repeating them. |
| 4 | Skills | Repeated workflows become reusable commands or capabilities. |
| 5 | MCP and plugins | The AI can use approved tools and shared systems. |
| 6 | Hooks and automation | Routine checks and guardrails run automatically. |
| 7 | Parallel agents | Large work is split across independent agents or sessions. |

**Most people should get comfortable with levels 1 to 3 first.**

**Most teams should standardize levels 3 to 5.**

**Advanced users and platform teams should own levels 5 to 7.**

Anti-patterns:

- Jumping to plugins or hooks before prompts and context are clear
- Treating advanced setup as proof of maturity
- Rolling out tools without measuring whether work improved
- Giving every user every advanced capability by default

## Daily Use vs Advanced Claude Code

[Back to Start Here](#start-here-pick-your-problem)

Claude Code can be used at several levels. The goal is not to make every coworker use every mechanism. The goal is to pick the lightest mechanism that improves the work without adding unnecessary risk or maintenance.

### Daily Use

Most people should start here.

Daily use includes:

- Asking better prompts
- Giving useful context
- Asking for assumptions, risks, and unknowns
- Asking for source-grounded answers when facts matter
- Using definitions of done
- Reviewing output before sending, shipping, or relying on it
- Using approved Claude surfaces for approved data
- Letting Claude Code inspect files or propose plans with appropriate permissions

Daily use is enough when:

- The task is one-off
- The output is easy for a human to review
- No external system access is needed
- The workflow is not repeated often
- A normal prompt plus review gives a good result

### Shared Team Practice

Use this level when a pattern is repeated by several people.

Shared team practice includes:

- Project instructions
- Shared definitions of done
- Reusable prompt examples
- Skills for repeated workflows
- Approved review checklists
- Basic measurement of output quality

Move to this level when:

- People keep pasting the same setup prompt
- Team standards are easy to forget
- Output quality varies too much by user
- Reviewers keep catching the same AI mistakes

### Advanced Claude Code Mechanisms

Hooks, MCP, plugins, subagents, broad tool access, and external open-source resources are advanced mechanisms. They can be valuable, but they change the risk profile because they may run code, connect to systems, expand access, distribute behavior to a team, or create parallel work that must be reconciled.

Use advanced mechanisms when:

- The manual workflow is understood
- The task is repeated enough to justify setup
- The data boundary and permission model are approved
- Someone owns maintenance
- Review and rollback are possible
- The benefit is measurable

Avoid advanced mechanisms when:

- The basic prompt is still vague
- The data classification is unclear
- The tool or integration is not approved
- Nobody owns updates
- The workflow changes every time
- The mechanism makes the work harder to inspect

Practical progression:

1. Do the work once with a clear prompt.
2. Improve context and definition of done.
3. Add a repeatable checklist or example.
4. Move stable rules into project instructions.
5. Turn repeated procedures into skills.
6. Add hooks only for mechanical checks.
7. Add MCP only for approved external context or actions.
8. Package with plugins only when distribution and versioning are needed.
9. Use subagents only when work can be split cleanly.

Anti-patterns:

- Treating advanced Claude Code setup as a badge of maturity
- Adding MCP when copy-paste from approved source material is enough
- Installing plugins before reading what they contain
- Automating a workflow nobody can explain manually
- Letting subagents create conflicting work without a merge owner

## Claude Modes, Surfaces, and Versions

[Back to Start Here](#start-here-pick-your-problem)

People use "Claude" to mean several different things:

- A model family, such as Haiku, Sonnet, Opus, Fable, or another model your tenant allows.
- A chat product, such as Claude in the web, mobile, or desktop Chat tab.
- An agentic coding product, Claude Code.
- A desktop agentic work surface, Claude Cowork.
- A deployment path, such as Claude Console, Amazon Bedrock, Google Vertex AI, Microsoft Foundry, or an internal gateway.
- A mode or setting inside Claude Code.

> **Do not treat these as interchangeable.** The same prompt can have different risk, cost, context, and permission behavior depending on where it runs.

### The Main Claude Surfaces

| Surface | Plain-language description | Best for | Be careful with |
| --- | --- | --- | --- |
| Claude Chat | The general chat experience in the web, mobile app, or desktop Chat tab. | Writing, summarizing, explaining, brainstorming, reviewing pasted or attached material. | It is still subject to company and client data rules. It is not the right surface for direct repo edits or command execution. |
| Claude Code CLI | The terminal version of Claude Code. | Technical users who want direct control, clear command visibility, repo work, scripts, tests, and local tools. | It can read files, edit files, and run commands depending on permissions. |
| Claude Code in an IDE | Claude Code inside VS Code, Cursor, JetBrains IDEs, or similar supported editors. | Engineers who want inline diffs, selected-file context, plan review, and editor-native workflow. | IDE context can make it easy to include more code than intended. |
| Claude Code Desktop Code tab | A graphical Claude Code surface for software development. | Visual diff review, multiple sessions, app previews, local or cloud sessions, side chats, and lower CLI friction. | Desktop convenience does not remove the need for review, permissions, and data controls. |
| Claude Code on the web | Browser-based Claude Code. | Long-running tasks, cloud sessions, work on repos that are not local, and parallel tasks. | Cloud sessions may have different access, data, and environment boundaries than local work. |
| Claude Cowork | The Claude Desktop Cowork tab for Dispatch and longer agentic work. | Longer non-code or mixed business workflows where a person wants an agentic assistant without using a coding terminal. | Availability, connectors, file access, and governance depend on your company tenant. Treat it as more powerful than normal chat. |
| Claude API or Console | Developer platform for building applications and integrations on Claude models. | Product integrations, internal tools, automation, and controlled application workflows. | This is an engineering and platform surface, not a replacement for everyday governed end-user tools. |

Rule of thumb:

- Use Claude Chat for conversation, drafting, summarization, and analysis.
- Use Claude Cowork for approved longer agentic business work that is not mainly software development.
- Use Claude Code when the task involves a repository, file edits, command execution, tests, pull requests, or developer tooling.
- Use Claude API or Console when you are building a product or integration around Claude.

Official docs: Claude Code overview: https://code.claude.com/docs/en/overview, Claude Code Desktop: https://code.claude.com/docs/en/desktop

### Claude Code Permission Modes

**Permission modes control autonomy.** They are not the same as model choice or output style.

| Mode | What it means | When to use it | Avoid when |
| --- | --- | --- | --- |
| Ask permissions / `default` | Claude asks before editing files or running commands. | New users, unfamiliar repos, high-review work, sensitive work, or when you want to learn what Claude is doing. | You need high-speed iteration on low-risk, well-scoped changes. |
| Auto accept edits / `acceptEdits` | Claude can accept file edits and common filesystem commands, but still asks for other terminal commands. | Low-to-medium risk coding tasks where you trust the scope and will review the diff. | The repo, data, or task boundaries are unclear. |
| Plan mode / `plan` | Claude can inspect and explore, then propose a plan without editing source files. | Complex changes, architecture work, unfamiliar codebases, security-sensitive changes, and tasks where you want approval before execution. | You already know the exact small change and just need it implemented. |
| Auto / `auto` | Claude executes actions with background safety checks that verify alignment with your request. | Approved environments, well-scoped tasks, experienced users, and work where fewer permission prompts are worth the risk tradeoff. | Sensitive data, unclear instructions, broad tool access, or high-impact tasks. |
| Do not ask / `dontAsk` | Claude auto-denies tools unless they were pre-approved. | Locked-down CLI sessions, read-mostly work, demos, or environments where you want strong default denial. | You expect the agent to discover and execute many actions independently. |
| Bypass permissions / `bypassPermissions` | Claude skips most permission prompts. | Only in isolated sandboxes, containers, or VMs where damage is limited and disposable. | Normal company work, client repos, personal machines, production environments, or unclear tasks. |

**Practical pattern:**

1. Start complex work in Plan mode.
2. Review the plan and risks.
3. Switch to Ask permissions or Auto accept edits for execution.
4. Use Auto only when the task and environment are approved and scoped.
5. Reserve Bypass permissions for disposable sandboxes.

Example prompt:

```text
Use plan mode first.
Inspect the relevant files and propose a plan.
Do not edit files yet.
Include risks, test strategy, and questions before execution.
```

Official docs: permissions and modes: https://code.claude.com/docs/en/permissions

### Other Settings People Mistake For Modes

| Setting | What it changes | What it does not change |
| --- | --- | --- |
| Output style | How Claude communicates. Built-in examples include Default, Proactive, Explanatory, and Learning. | It does not grant permissions or make unsafe actions safe. |
| Model choice | Which model or alias Claude uses, such as Haiku, Sonnet, Opus, or a tenant-approved model. | It does not change company policy or data boundaries. |
| Effort level or deep reasoning | How much thinking Claude spends on a task. | It does not guarantee correctness or remove review. |
| Fast mode | Response speed and cost tradeoff for supported Opus configurations. | It is not a different model and not a permission mode. |
| Transcript view mode | How much session detail you see, such as Normal, Verbose, or Summary in Desktop. | It does not change what Claude can access or do. |

**Use output styles** when you want a different collaboration style:

- Default: normal software-engineering behavior.
- Proactive: more action-oriented, but still subject to permissions.
- Explanatory: better for learning why Claude chose an approach.
- Learning: better for training because Claude asks you to complete small pieces.

**Use model choice** when the task changes:

- Haiku-style models: simple, fast, low-cost work when available.
- Sonnet-style models: default daily work.
- Opus-style models: complex reasoning, hard debugging, architecture, and high-ambiguity work.
- Fable-style models, if available in your tenant: hardest and longest-running tasks that need sustained investigation.
- Special aliases can change over time, so check the model picker or official docs instead of hardcoding assumptions.

Official docs: model configuration: https://code.claude.com/docs/en/model-config, output styles: https://code.claude.com/docs/en/output-styles, fast mode: https://code.claude.com/docs/en/fast-mode

### Common Confusions

- Plan mode is not the same as "ask Claude to write a plan." Plan mode changes what tools Claude can use.
- Proactive output style is not the same as Auto permission mode. One changes tone and behavior guidance; the other changes tool approvals.
- Claude Cowork is not just Claude Chat with a different label. Treat it as an agentic work surface because it can be used for longer tasks and may connect to tools depending on the tenant.
- Claude Code Desktop and Claude Code CLI are different surfaces over related Claude Code capabilities. Use the one that fits your workflow and governance.
- A more capable model is not a substitute for clearer context, safer permissions, or human review.

Anti-patterns:

- Turning on more autonomy because the prompt is vague
- Using Bypass permissions on a real work machine
- Choosing the most expensive model for every task
- Treating Cowork, Code, and Chat as having the same data and tool boundaries
- Assuming a mode is approved just because it exists in the UI

## Project Instructions

[Back to Start Here](#start-here-pick-your-problem)

**Project instructions are durable context** the AI loads before it starts work in a repo, folder, or workspace.

**Why it matters:** project instructions remove repeated setup prompts. Instead of saying "use pnpm, run these tests, follow this architecture, avoid these files" every session, the AI starts with those expectations already in context.

**How it changes the workflow:** you move from "I must remember to explain the repo every time" to "the repo explains itself." New users and experienced users get more consistent AI behavior.

Use project instructions for:

- Stable facts about the repo or workspace
- Test, build, lint, and formatting commands
- Architecture rules
- Review standards
- Security requirements
- Writing style
- Project-specific vocabulary
- "Ask before doing X" rules
- Team definitions of done

Pros:

- Low setup cost
- Easy to review in code review
- Works before the user writes a detailed prompt
- Good for shared team standards

Cons and tradeoffs:

- Too much text can crowd out task context
- Stale instructions can mislead the AI
- Long procedures become hard to follow
- Private personal preferences can conflict with team rules

**Difference from a prompt:** a prompt is for this task. Project instructions are for every task in this workspace.

**Difference from a skill:** project instructions describe standing context and rules. A skill describes a repeatable workflow with steps, examples, and outputs.

> **Do not bury long procedures in project instructions.** If a section becomes a multi-step workflow, turn it into a skill.

Anti-patterns:

- Turning `CLAUDE.md` into a full wiki
- Storing secrets or client-confidential details in instructions
- Adding rules nobody owns or updates
- Mixing personal preferences with team requirements
- Using project instructions for workflows that should be skills

### CLAUDE.md

Claude Code uses `CLAUDE.md` for project instructions and memory-style guidance.

Example:

```md
# CLAUDE.md

## Repository expectations

- Prefer concise Markdown.
- Link to official docs when describing Claude Code behavior.
- Do not copy long sections from official docs.
- Keep examples understandable to non-engineering readers.

## Definition of done

- Run Markdown formatting if available.
- Check all links added in the change.
- Final response must include changed files and any unverified assumptions.
```

Claude Code can load project and user guidance so teams do not need to repeat the same context in every session.

Official docs:

- Claude Code memory and instructions: https://code.claude.com/docs/en/memory
- Claude Code settings: https://code.claude.com/docs/en/settings

Courses:

- Claude Code in Action: https://anthropic.skilljar.com/claude-code-in-action

## Choosing the Right Mechanism

[Back to Start Here](#start-here-pick-your-problem)

> **The main mistake is putting everything into the prompt.** Prompts are useful, but they are not the only place to put instructions.

| Mechanism | Best for | Avoid using it for | Main tradeoff |
| --- | --- | --- | --- |
| Prompt | One-time task details | Stable team rules | Fast, but easy to forget next time |
| Project instructions | Standing repo or team context | Long step-by-step procedures | Consistent, but can become stale |
| Skill | Repeatable workflow | Tiny preferences | Reusable, but needs ownership |
| Hook | Mechanical automation | Human judgment | Enforces behavior, but can run code |
| MCP | Access to external tools or data | Data you are not allowed to expose | Powerful, but expands access surface |
| Plugin | Shared bundle of skills, hooks, MCP, or app setup | One small local experiment | Distributable, but must be reviewed as a package |
| Subagent | Independent workstream | Shared-file edits without coordination | Parallelizes work, but adds merge/review overhead |
| Settings or permissions | Tool behavior and access limits | Task instructions | Strong guardrail, but needs admin/user ownership |

**Rule of thumb:** keep one-off instructions in the prompt, stable context in project instructions, repeated procedures in skills, automatic checks in hooks, external access in MCP, and shared bundles in plugins.

Anti-patterns:

- Putting everything into one giant prompt
- Creating a plugin for a single untested prompt
- Adding hooks before the manual workflow is understood
- Connecting external tools before data boundaries are approved
- Creating several overlapping skills for the same workflow

## Skills

[Back to Start Here](#start-here-pick-your-problem)

**A skill is a reusable workflow or capability** that the AI can load when the task matches.

Think of it as a **recipe card** the AI can pick up when the task matches.

**Why it matters:** skills reduce boilerplate and improve consistency. If people keep pasting the same checklist, output template, role instruction, or process into chat, that workflow should probably become a skill.

**How it changes the workflow:** instead of writing a long setup prompt, the user can invoke or trigger a named workflow. The AI reads the skill instructions only when needed, so the main prompt stays focused on the actual task.

Use a skill when:

- You repeatedly paste the same instructions
- A checklist has more than a few steps
- The task needs examples, templates, or reference files
- The workflow should be shared with other people
- The AI should know when to use the workflow automatically

Pros:

- Reduces repeated prompt setup
- Makes work easier to teach and share
- Can include examples, references, and scripts
- Works well for workflows that need consistent output

Cons and tradeoffs:

- Poorly scoped skills trigger at the wrong time
- Too many overlapping skills create confusion
- Skills need maintenance when the workflow changes
- A skill can hide assumptions if users do not review it

**Difference from project instructions:** project instructions are always-on context for a workspace. Skills are task-specific workflows that should load only when relevant.

**Difference from plugins:** a skill is the workflow. A plugin is a package that can distribute skills plus other setup such as MCP, hooks, or app integrations.

> **Do not use a skill for every small preference.** Put stable facts in project instructions. Put one-off needs in the prompt.

### Good Skill Candidates

- Review a pull request using team-specific risk criteria
- Summarize customer calls into a standard CRM format
- Convert meeting notes into decisions, owners, and follow-ups
- Generate release notes from a diff and ticket list
- Check policy drafts for required legal language
- Prepare an incident review using the company template
- Run a project-specific verification workflow

### Skill Anti-Patterns

- "Use bullet points"
- "Be concise"
- One-off research
- A secret or credential
- A rule that must apply to every conversation
- A vague skill that triggers for too many tasks
- A skill copied from the internet without review

### Claude Code Skill Example

Claude Code skills use a `SKILL.md` file. A project skill can live under `.claude/skills/<skill-name>/SKILL.md`.

```md
---
description: Turn rough meeting notes into decisions, owners, deadlines, and unresolved questions. Use when the user asks to summarize meeting notes or prepare follow-up notes.
---

# Meeting Follow-Up Skill

Read the provided notes or transcript.

Return:

1. Executive summary in 5 bullets or fewer
2. Decisions made
3. Action items with owner and due date
4. Open questions
5. Risks or dependencies

If an owner or date is missing, write "Unassigned" or "No date".
Do not invent decisions.
```

Official docs:

- Claude Code skills: https://code.claude.com/docs/en/skills
- Agent skills standard: https://agentskills.io

Courses:

- Introduction to agent skills: https://anthropic.skilljar.com/introduction-to-agent-skills
- Claude Code in Action: https://anthropic.skilljar.com/claude-code-in-action

### Where To Find Skills

[Back to Start Here](#start-here-pick-your-problem)

For free/open-source skill starting points, begin with official or standards-aligned sources:

- Claude Code skills docs: https://code.claude.com/docs/en/skills
- Agent Skills standard: https://agentskills.io
- Anthropic Claude cookbooks: https://github.com/anthropics/claude-cookbooks

Community collections can be useful for inspiration, but treat them as examples to review and adapt, not as automatically approved company assets:

- Awesome Claude Code: https://github.com/hesreallyhim/awesome-claude-code
- Build with Claude collection: https://github.com/davepoon/buildwithclaude
- Multi-harness agent and skill collection: https://github.com/wshobson/agents
- Spec-driven development skills and workflows: https://github.com/gotalab/cc-sdd
- Agentic skill library and bundles: https://github.com/sickn33/antigravity-awesome-skills

**Before reusing a skill, check:**

- What instructions it injects into the AI's context
- Whether it asks the AI to run commands or use tools
- Whether it mentions secrets, credentials, external services, or data export
- Whether the license allows company use
- Whether it should be copied as-is, adapted, or rewritten internally
- Whether customer policy allows the skill, tool, or workflow in that environment

### Skill Writing Tips

**Write skills like operating instructions, not essays.**

Good skill descriptions include:

- What the skill does
- When it should trigger
- When it should not trigger, if the boundary is important
- Keywords users naturally say

Good skill bodies include:

- Inputs expected
- Steps to follow
- Output format
- Validation criteria
- Examples only when they improve consistency

**Keep the main `SKILL.md` short.** Put long references, examples, scripts, or templates in supporting files when the platform supports that pattern.

## Hooks

[Back to Start Here](#start-here-pick-your-problem)

> **Advanced mechanism:** use hooks after the manual workflow is understood and the command or script has an owner.

**A hook is automation** that runs around the AI's work.

**Why it matters:** hooks move repeatable checks out of memory and into automation. If a check should happen every time, relying on every user to remember it is weak.

**How it changes the workflow:** the AI or tool lifecycle triggers a script at a known moment, such as before tool use, after tool use, at session start, or when a turn stops.

Use hooks for things that are mechanical and deterministic:

- Block prompts that appear to contain secrets
- Check a shell command before it runs
- Format files after edits
- Run a quick validation check when a turn stops
- Send approved telemetry to an internal logging system
- Load local context at session start

Pros:

- Enforces checks even when users forget
- Reduces repeated prompt instructions
- Good for formatting, validation, logging, and policy checks
- Can support team-wide guardrails

Cons and tradeoffs:

- Hooks can run code, so they need review
- Bad hooks can slow down work or block valid tasks
- Hooks are a poor fit for judgment-heavy decisions
- Users need a way to inspect, trust, disable, or escalate hook behavior

**Difference from a skill:** a skill is reasoning guidance for a workflow. A hook is automation that runs at a lifecycle event.

**Difference from permissions or rules:** permissions define what is allowed. Hooks can inspect or react around actions, but they should not be the only security boundary.

> **Do not use hooks for vague judgment.** If the task requires reasoning, use a skill or explicit prompt.

**Hooks can run code.** Treat them like any other automation that touches your workstation, repo, or data. Review what they do before trusting them.

Anti-patterns:

- Installing hook scripts without reading them
- Using hooks to make subjective decisions
- Letting hooks send prompts or files to external services without approval
- Blocking normal work without a clear escalation path
- Depending on hooks as the only security control

Official docs:

- Claude Code hooks: https://code.claude.com/docs/en/hooks

Courses:

- Claude Code in Action: https://anthropic.skilljar.com/claude-code-in-action

### Where To Find Hook Examples

[Back to Start Here](#start-here-pick-your-problem)

**Hooks are executable automation**, so be more cautious with them than with prompt-only skills.

Useful starting points:

- Claude Code official plugin directory, which may include hook-based workflows: https://github.com/anthropics/claude-plugins-official
- Awesome Claude Code, which indexes hooks and related tooling: https://github.com/hesreallyhim/awesome-claude-code
- Claude Code hooks docs for supported lifecycle events and config shape: https://code.claude.com/docs/en/hooks
- Gitleaks secret scanning: https://github.com/gitleaks/gitleaks
- TruffleHog secret scanning: https://github.com/trufflesecurity/trufflehog
- Semgrep static analysis: https://github.com/semgrep/semgrep

> **Do not install a hook** until you understand what command it runs, when it runs, what files it can read or write, and whether it sends data anywhere.

External hook tools must be approved for the repo, company, and customer environment. A hook that sends prompts, files, logs, or scan results to an unapproved service can create data leakage, contractual, security, or reputational damage.

## MCP

[Back to Start Here](#start-here-pick-your-problem)

> **Advanced mechanism:** use MCP only for approved tool or data access with clear authentication, permissions, and data boundaries.

**MCP stands for Model Context Protocol.**

**In plain English:** MCP is a standard way for AI tools to connect to other tools and data sources.

**Why it matters:** without MCP, people often copy and paste data into AI manually. That is slow, inconsistent, and can create privacy or security issues. MCP lets access be configured, authenticated, scoped, reused, and audited more deliberately.

**How it changes the workflow:** the AI can use an approved connector or server to read relevant context or take actions in another system, instead of depending only on pasted chat content.

Use MCP when the AI needs current or private context that is not already in the chat:

- Internal docs
- Tickets
- Pull requests
- Error logs
- Figma designs
- Browser state
- Sentry issues
- GitHub issues
- Company-specific tools

**Without MCP**, users often paste data manually. That is slow, inconsistent, and risky. **With MCP**, access can be configured, scoped, authenticated, and reused.

Pros:

- Reduces manual copy-paste
- Gives the AI fresher and more relevant context
- Can centralize authentication and tool access
- Works well for docs, tickets, designs, logs, and repository metadata

Cons and tradeoffs:

- Expands what the AI can access
- Requires approval and maintenance
- Misconfigured tools can expose too much data or allow too many actions
- Users may over-trust output because it came from a tool

**Difference from a plugin:** MCP is a connection pattern for tools and data. A plugin can bundle MCP setup with skills, hooks, and app integrations.

**Difference from web search:** MCP is for approved systems and private or tool-backed context. Web search is for public information and should not be used for private company data.

Examples:

```text
Use the docs MCP server to find the current API guidance, then update this integration plan.
```

```text
Use the GitHub MCP server to inspect the open issues tagged "onboarding" and summarize recurring themes.
```

Official docs:

- Claude Code MCP: https://code.claude.com/docs/en/mcp
- MCP standard: https://modelcontextprotocol.io

Courses:

- Introduction to Model Context Protocol: https://anthropic.skilljar.com/introduction-to-model-context-protocol
- Claude Code in Action: https://anthropic.skilljar.com/claude-code-in-action

### Where To Find MCP Servers

[Back to Start Here](#start-here-pick-your-problem)

For free/open-source MCP server starting points, begin with official protocol and server resources:

- MCP standard and docs: https://modelcontextprotocol.io
- Reference and community MCP servers: https://github.com/modelcontextprotocol/servers
- Claude Code MCP docs: https://code.claude.com/docs/en/mcp
- GitHub MCP server: https://github.com/github/github-mcp-server
- Playwright MCP server: https://github.com/microsoft/playwright-mcp
- Context7 documentation MCP server: https://github.com/upstash/context7
- Chrome DevTools MCP server: https://github.com/ChromeDevTools/chrome-devtools-mcp
- Sentry MCP server: https://github.com/getsentry/sentry-mcp

**Before connecting an MCP server**, check what data it can access, what actions it can take, how authentication works, and whether the company approves that integration.

**Customer environments may have stricter rules than company environments.** Do not connect MCP servers to customer data, logs, repositories, issue trackers, or browsers unless that customer's policy explicitly allows it.

Anti-patterns:

- Connecting broad read/write tools when read-only access would be enough
- Giving AI access to private systems without approval
- Treating MCP output as automatically correct
- Letting one user's credentials become a team automation path
- Using MCP to bypass normal access controls

## Plugins

[Back to Start Here](#start-here-pick-your-problem)

> **Advanced mechanism:** review plugins as packages, because they may bundle skills, hooks, MCP setup, scripts, app connections, and supporting assets.

**A plugin is an installable bundle.**

Use a plugin when you want to share more than one reusable thing, or when setup should travel as a package.

Plugins can include things like:

- Skills
- App connections
- MCP server configuration
- Hooks
- Agents or subagents
- Supporting assets

**Skills are the workflow. Plugins are a distribution mechanism.**

> **Start with a standalone skill when you are experimenting.** Move to a plugin when the workflow should be versioned, installed, enabled, disabled, or shared across teams.

**Why it matters:** plugins make reusable AI setup installable. They are useful when a team wants consistent access to multiple skills, tools, integrations, or assets without asking every user to copy files by hand.

**How it changes the workflow:** users install or enable one package, then get a curated set of capabilities. Teams can version and distribute that package more deliberately than scattered snippets.

Use plugins for:

- Sharing several related skills
- Packaging MCP setup
- Bundling hooks with workflows
- Distributing app integrations
- Creating a team or department toolkit

Pros:

- Easier distribution and onboarding
- Can bundle multiple related capabilities
- Can be enabled, disabled, versioned, and reviewed as a unit
- Good for team-wide reuse

Cons and tradeoffs:

- A plugin can contain more than users realize
- Review must cover skills, hooks, MCP, scripts, and app connections
- Plugin updates can change behavior across many users
- Over-packaging can make simple workflows harder to inspect

**Difference from a skill:** a skill is one reusable workflow. A plugin is a package that may contain one or more skills plus other integration pieces.

**Difference from MCP:** MCP gives tool/data access. A plugin may include MCP setup, but it can also include instructions, hooks, assets, and app connections.

Official docs:

- Claude Code plugins: https://code.claude.com/docs/en/plugins

Courses:

- Introduction to agent skills: https://anthropic.skilljar.com/introduction-to-agent-skills

### Where To Find Plugins

[Back to Start Here](#start-here-pick-your-problem)

For free/open-source plugin starting points, begin with official plugin directories and docs:

- Claude Code official plugins: https://github.com/anthropics/claude-plugins-official
- Claude Code plugin docs: https://code.claude.com/docs/en/plugins

Community resources:

- Awesome Claude Code plugin and workflow index: https://github.com/hesreallyhim/awesome-claude-code
- Multi-harness plugin and agent collection: https://github.com/wshobson/agents
- Build with Claude plugin and marketplace collection: https://github.com/davepoon/buildwithclaude
- Claude HUD plugin example: https://github.com/jarrodwatts/claude-hud

**Before installing a plugin**, check whether it bundles skills, hooks, MCP servers, app connections, or scripts. A plugin is a package, so review the whole package, not only the feature you wanted.

**Plugins in company or customer environments must be approved before installation.** A plugin can change workflows, access external tools, run hooks, send data to services, or introduce supply-chain and license risk.

Anti-patterns:

- Installing a plugin because one bundled skill looks useful
- Ignoring hooks, scripts, MCP servers, or app connections inside the plugin
- Letting plugin updates change team behavior without review
- Installing community plugins into client environments without explicit approval
- Treating install count or GitHub stars as a security review

## Subagents and Parallel Work

[Back to Start Here](#start-here-pick-your-problem)

> **Advanced mechanism:** use subagents when work can be split cleanly and someone owns reconciling the results.

**Use subagents when work can be split into independent tracks.**

**Why it matters:** one AI thread has limited attention and can get pulled between competing goals. Subagents let you delegate focused workstreams such as research, review, testing, or implementation planning.

**How it changes the workflow:** instead of asking one agent to do everything, you assign narrow tasks to separate agents and merge the results.

Use subagents for:

- Researching separate areas
- Reviewing from different perspectives
- Investigating independent modules
- Comparing options
- Running focused audits
- Splitting large planning work

Pros:

- Faster exploration
- Less context mixing
- Better separation of review perspectives
- Useful for large or ambiguous work

Cons and tradeoffs:

- More outputs to review and reconcile
- Risk of conflicting conclusions
- Risk of edit conflicts if multiple agents touch the same files
- Requires clear task boundaries

**Difference from a skill:** a skill defines how to do a recurring workflow. A subagent is a separate worker for a specific task.

**Difference from a parallel thread:** a subagent is usually launched within or from an agent workflow. A parallel thread is a separate session the user manages.

Good examples:

- One agent researches docs while another inspects code
- One agent reviews security while another reviews test coverage
- Multiple agents migrate independent packages
- One agent drafts release notes while another checks the diff

Bad examples:

- Two agents editing the same file
- A task with unclear ownership
- A task where the subagent cannot verify its result
- A task where merging results requires more effort than doing it once
- Subagents with broad access and vague goals
- Multiple agents making independent decisions that should be centralized

**Give each subagent a narrow brief:**

```text
Inspect only the payments module.
Find risks in the proposed migration.
Do not edit files.
Return findings with file references and severity.
```

Official docs:

- Claude Code subagents: https://code.claude.com/docs/en/sub-agents

Courses:

- Introduction to subagents: https://anthropic.skilljar.com/introduction-to-subagents

### Where To Find Subagents

[Back to Start Here](#start-here-pick-your-problem)

For free/open-source subagent and agent setup starting points, begin with official and source resources:

- Claude Code subagents docs: https://code.claude.com/docs/en/sub-agents

Community resources:

- Claude Code subagent collection: https://github.com/VoltAgent/awesome-claude-code-subagents
- Awesome Claude Code agent and subagent index: https://github.com/hesreallyhim/awesome-claude-code
- Multi-harness agent collection: https://github.com/wshobson/agents
- Spec-driven multi-agent workflow: https://github.com/gotalab/cc-sdd
- Build with Claude agent and workflow collection: https://github.com/davepoon/buildwithclaude

**Use public subagents as patterns.** For company work, rewrite prompts and permissions around internal standards, approved tools, and clear definitions of done.

> **Do not run public agents or subagents against customer code, client data, internal repos, or production context** unless policy explicitly approves the tool, permissions, and data flow.

## Permissions and Safety

[Back to Start Here](#start-here-pick-your-problem)

**AI agents can read files, edit files, run commands, and call tools** depending on the environment.

> **Permissions are part of the work, not an afterthought.**

**Basic safety rules:**

- Do not paste secrets, credentials, private keys, or sensitive personal data unless the approved environment and policy allow it.
- Ask the AI to explain risky actions before it runs them.
- Review diffs before committing.
- Prefer read-only exploration before edits.
- Keep destructive commands manual unless there is a deliberate approval process.
- Use project instructions for security rules that always apply.
- Use hooks or rules for mechanical enforcement.

Anti-patterns:

- Approving commands you do not understand
- Letting the AI run destructive commands without an explicit reason
- Giving write access when read-only exploration is enough
- Reviewing only the final summary instead of the diff or tool actions
- Ignoring approval prompts because the task feels routine

Useful prompt:

```text
Before editing files, inspect the repo and propose a plan.
Call out any command that could modify files, delete data, expose secrets, or contact external services.
Ask before running those commands.
```

Official docs:

- Claude Code permissions: https://code.claude.com/docs/en/permissions

Courses:

- Claude Code in Action: https://anthropic.skilljar.com/claude-code-in-action

## External Tools and Open-Source Resources

[Back to Start Here](#start-here-pick-your-problem)

**Open-source tools, skills, plugins, hooks, MCP servers, and agents can be useful starting points.** They can also introduce real company and customer risk.

> **Treat any external AI tool or GitHub repository as unapproved** until the relevant company or customer policy says otherwise.

External tools can create damage through:

- Data leakage
- Client contract violations
- Unauthorized access to systems
- Supply-chain compromise
- License or intellectual-property issues
- Incorrect automation at scale
- Reputational harm if private data or bad output is exposed
- Loss of customer trust

Before using an external tool with company or customer work, check:

- Who maintains it
- What license it uses
- Whether it runs code locally or remotely
- Whether it sends data to a third party
- What permissions it requests
- Whether it stores logs, prompts, files, or outputs
- Whether it is approved for the customer, tenant, repo, and data class

**Safe default:** use external resources as inspiration, then adapt the workflow into an internally reviewed skill, instruction file, hook, MCP setup, or plugin.

Anti-patterns:

- Treating "open source" as "safe"
- Installing tools directly from a README into a client environment
- Using GitHub stars as a substitute for review
- Copying public skills without reading their instructions
- Connecting external tools to private data before approval

## Approved External Resource Policy

[Back to Start Here](#start-here-pick-your-problem)

This section is the place for the company's approval policy for external AI resources. It applies to public or third-party resources such as skills, plugins, hooks, MCP servers, agents, prompt libraries, browser extensions, command-line tools, packages, templates, datasets, and example repositories.

> **Default rule:** external resources are examples until approved. Do not run, install, connect, or distribute them in company or client environments just because they are public, popular, or open source.

### What Counts As An External Resource

Treat these as external resources when they come from outside the company or outside the approved client environment:

- Claude Code skills
- Plugins
- Hooks
- MCP servers
- Agents or subagents
- Prompt libraries
- Automation scripts
- Browser extensions
- Command-line tools
- NPM, Python, container, or binary packages
- GitHub repositories
- Templates, starter kits, or example projects
- Evaluation datasets or benchmark sets
- Connectors to third-party systems

If the resource can read files, run code, connect to systems, call APIs, change output behavior, or send data elsewhere, it needs review before work use.

### Approval Status

Fill in approved resources here after review.

| Resource | Type | Approved scope | Restrictions | Owner | Review date |
| --- | --- | --- | --- | --- | --- |
| To be added | Skill / plugin / hook / MCP / agent / package / other | To be added | To be added | To be added | To be added |
| To be added | Skill / plugin / hook / MCP / agent / package / other | To be added | To be added | To be added | To be added |
| To be added | Skill / plugin / hook / MCP / agent / package / other | To be added | To be added | To be added | To be added |

Approval should be scoped. A resource may be approved for:

- Inspiration only
- Personal experimentation with public or synthetic data
- Internal company data
- A specific team or repository
- A specific client environment
- Read-only use
- Local-only use
- Packaged team distribution

Do not assume approval in one scope means approval everywhere.

### Review Checklist

Before approving an external resource, review:

- Purpose: what problem does it solve?
- Source: who maintains it?
- License: can the company use, modify, and distribute it?
- Maintenance: is it active enough to trust?
- Runtime behavior: what code runs, when, and where?
- Data flow: what prompts, files, logs, outputs, or metadata can leave the environment?
- Permissions: what files, commands, browsers, APIs, systems, or credentials can it access?
- Dependencies: what packages, services, containers, or binaries does it pull in?
- Configuration: does it require secrets, tokens, environment variables, or broad scopes?
- Update behavior: can it change after installation without review?
- Auditability: can users inspect what it does?
- Rollback: can it be disabled or removed cleanly?
- Ownership: who answers questions and updates it?
- Fit: does it match company and client policy?

For prompt-only resources, review the instructions they inject into context.

For executable resources, review them like code.

For connectors, MCP servers, browser tools, and plugins, review both the instructions and the access they enable.

### Minimum Approval Record

Keep a short approval record for each approved resource.

Minimum fields:

- Resource name
- Resource type
- Source location
- Version, commit, release, or date reviewed
- Approved scope
- Data classes allowed
- Data classes prohibited
- Required configuration
- Required reviewers
- Known risks
- Owner
- Review date
- Next review date

Use this template:

```text
Resource:
Type:
Source:
Version reviewed:
Approved scope:
Allowed data:
Prohibited data:
Required setup:
Required reviewers:
Known risks:
Owner:
Review date:
Next review date:
Decision:
```

### Safe Reuse Pattern

When a public resource looks useful:

1. Read what it does.
2. Decide whether it is inspiration, a copy candidate, or an install candidate.
3. Review instructions, code, dependencies, data flow, permissions, and license.
4. Remove unnecessary access and behavior.
5. Rewrite prompts, skills, or agents around company standards.
6. Test with public, synthetic, or sanitized data first.
7. Get the required owner approval.
8. Document scope, owner, and review date.
9. Share only the reviewed version, not a random upstream snapshot.

Preferred pattern:

- Use public resources for ideas.
- Create an internally reviewed version.
- Keep the internal version small, readable, and owned.
- Re-review before major updates or wider rollout.

### Prohibited Without Explicit Approval

Do not use external resources for company or client work if they:

- Ask for secrets, tokens, credentials, cookies, or private keys
- Send prompts, files, logs, screenshots, or outputs to an unapproved service
- Require broad read/write access when the task does not need it
- Run unknown scripts during installation
- Install binaries or containers that have not been reviewed
- Modify shell startup files, editor settings, browser settings, or global environment state without review
- Claim to bypass permissions, monitoring, policy, or review
- Auto-update behavior in a way the company cannot inspect
- Lack a clear license for company use
- Cannot be removed cleanly

### User Responsibilities

Before using an external resource, the user should be able to answer:

- Is this resource approved for my tool, tenant, project, client, and data class?
- What does it read?
- What does it write?
- What commands or code can it run?
- What services can it contact?
- What data can leave the environment?
- Who owns it internally?
- What should I do if it behaves unexpectedly?

If the answer is unclear, do not use the resource for work data.

Anti-patterns:

- Installing a plugin because one bundled skill looks useful
- Running setup commands from a public README without review
- Treating a prompt library as harmless because it does not contain code
- Letting public agents operate on client repositories
- Copying a skill that changes behavior in ways users cannot see
- Approving a tool once and never reviewing updates
- Using personal access tokens for team automation
- Confusing "works well" with "approved and safe"

## Measuring AI Quality

[Back to Start Here](#start-here-pick-your-problem)

> **Do not judge an AI approach from one impressive answer.** Compare approaches on the same task with the same input.

Better can mean:

- More correct
- More complete
- Easier to review
- Less risky
- Faster
- More consistent
- Better aligned with team standards
- Less follow-up prompting

**Quick measurement process:**

1. Pick 3 to 5 real tasks that represent the work.
2. Run the old approach and save the output.
3. Run the new approach with the same input.
4. Score both outputs with the same rubric.
5. Keep the approach only if it improves the score or saves meaningful time without increasing risk.

Simple rubric:

| Dimension | 1 | 3 | 5 |
| --- | --- | --- | --- |
| Correctness | Contains clear errors | Mostly right, needs fixes | Accurate and verified |
| Completeness | Misses key requirements | Covers main points | Covers requirements and edge cases |
| Usefulness | Hard to apply | Usable with editing | Directly usable |
| Context fit | Generic | Some local fit | Matches audience, repo, or business context |
| Review effort | Requires heavy review | Requires normal review | Easy to review |
| Safety | Risky or leaks data | Some concerns | Follows data and permission boundaries |

**For prompts**, measure whether the improved prompt reduces follow-up messages.

**For project instructions**, measure whether new sessions follow team rules without extra reminders.

**For skills**, measure whether repeated workflows produce more consistent outputs.

**For hooks**, measure whether they catch real issues without blocking normal work too often.

**For MCP or plugins**, measure whether they reduce copy-paste and improve source quality without expanding access too broadly.

Anti-patterns:

- Measuring only speed and ignoring correctness or safety
- Comparing different tasks instead of the same input
- Keeping a new workflow because it feels impressive once
- Counting fewer prompts as success when review effort increased
- Ignoring failures because the average output looks better

Example:

```text
Task: summarize a customer call into action items.
Old approach: free-form prompt.
New approach: meeting-summary skill.
Measure: correctness, missing owners, missing dates, review time, sensitive data leakage.
Decision: keep the skill only if it reduces review time and does not invent owners or dates.
```

Open-source evaluation resources:

- promptfoo: https://github.com/promptfoo/promptfoo
- Giskard testing framework: https://github.com/Giskard-AI/giskard

Evaluation tools can store prompts, expected outputs, model outputs, and test cases. Use sanitized datasets unless company or customer policy explicitly allows real data.

## Ownership and Maintenance

[Back to Start Here](#start-here-pick-your-problem)

AI guidance gets stale quickly. Models change, product surfaces change, company tenants change, client restrictions change, and teams discover better workflows. Treat this guide as a maintained internal enablement asset, not a one-time document.

### Ownership

Every AI guide needs named owners.

Recommended ownership model:

| Area | Suggested owner | Owns |
| --- | --- | --- |
| Overall guide | AI enablement, engineering productivity, or operations owner | Structure, readability, training usefulness, and update cadence |
| Security and privacy | Security, privacy, or data protection owner | Data boundaries, secrets, approved tools, and escalation paths |
| Legal, compliance, HR, finance-sensitive use | Relevant functional owner | Required reviewers, prohibited uses, and role-specific constraints |
| Tooling and integrations | Platform, IT, or developer experience owner | Approved tenants, connectors, MCP servers, plugins, hooks, and account setup |
| Role examples | Department leads or nominated practitioners | Realistic examples and workflow fit |

If ownership is unclear, do not treat the guide as approved policy. Use it as draft guidance and escalate.

### Review Cadence

Review the guide:

- At least quarterly
- When a major Claude, Codex, or company AI tool changes
- When new models, surfaces, connectors, or permission modes are rolled out
- When company policy or client requirements change
- After a serious AI-related mistake, near miss, or support pattern
- After feedback from new users or non-technical readers

Each review should check:

- Are product names, model names, links, and feature descriptions still accurate?
- Are approved tools, tenants, and accounts still current?
- Are data rules clear enough for real coworkers?
- Are examples realistic and safe?
- Are advanced mechanisms still appropriate for the intended audience?
- Are repeated questions from coworkers reflected in the FAQ or examples?

### Change Process

Use lightweight change control for low-risk writing improvements and stricter review for policy-adjacent changes.

Low-risk changes:

- Clarifying language
- Fixing typos
- Improving examples without changing policy meaning
- Adding links to already-approved resources
- Making navigation easier

Higher-risk changes:

- New guidance about sensitive data
- New approved or unapproved tools
- New model, tenant, connector, MCP, plugin, hook, or agent guidance
- New role-specific advice for HR, legal, finance, security, compliance, or customer commitments
- Any change that could be read as permission to use real client, employee, regulated, or confidential data

Higher-risk changes should be reviewed by the relevant owner before publication.

### Versioning

At minimum, track:

- Last reviewed date
- Source check date
- Main owner
- Approvers for policy-adjacent sections
- Known gaps or pending approvals

Useful status labels:

- Draft: useful but not approved as official guidance
- Reviewed: checked by relevant owners for the current rollout
- Approved: accepted as official internal guidance for a defined scope
- Deprecated: kept for history but no longer current

### Feedback Loop

Give coworkers a simple way to report:

- Confusing sections
- Missing examples
- Unsafe or outdated advice
- Links that no longer work
- Claude features that do not match the company tenant
- Workflows that deserve a skill, instruction file, hook, MCP integration, or plugin

Anti-patterns:

- Letting one enthusiastic user own company-wide AI guidance alone
- Updating tool recommendations without security, privacy, or platform review
- Treating a draft as approved because it is well written
- Adding advanced mechanisms without naming a maintainer
- Keeping stale screenshots, model names, or feature descriptions because they are hard to update

## Role-Based Guidance

[Back to Start Here](#start-here-pick-your-problem)

### Everyone

Use AI for:

- Summaries
- Drafts
- Rewrites
- Decision memos
- Meeting follow-ups
- Brainstorming
- Checklists
- Explaining unfamiliar topics

Do:

- Say who the output is for
- Say what decision it supports
- Ask for assumptions and unknowns
- Ask for a concise final format
- Ask it not to invent facts

Example:

```text
Summarize this transcript for people who did not attend.
Separate decisions, action items, risks, and open questions.
Do not include personal opinions.
If something is unclear, mark it as unclear instead of guessing.
```

### HR, People, Operations, Finance, Legal, and Business Teams

Use AI for:

- Summarizing meetings
- Drafting policy explanations
- Comparing options
- Creating onboarding checklists
- Preparing stakeholder updates
- Turning messy notes into structured outputs

Be careful with:

- Personal data
- Compensation data
- Legal claims
- Compliance language
- Performance feedback
- Anything that affects employment decisions

Good pattern:

```text
Act as an internal communications editor.
Rewrite this policy explanation for employees.
Keep the policy meaning unchanged.
Use plain language.
Flag any sentence that sounds like legal advice or needs review.
```

Reusable skill candidates:

- Meeting follow-up formatter
- Policy readability reviewer
- Onboarding checklist generator
- Stakeholder update formatter

### Product, Design, Research, and Customer Teams

Use AI for:

- Turning research notes into themes
- Drafting PRDs
- Extracting requirements
- Preparing launch notes
- Comparing customer feedback
- Reviewing designs against acceptance criteria

Good pattern:

```text
Act as a product partner.
Read these customer notes and identify recurring problems.
Separate evidence from interpretation.
Return themes, supporting quotes, possible product bets, and open questions.
```

Reusable skill candidates:

- Research synthesis template
- PRD reviewer
- Launch readiness checklist
- Customer feedback classifier

### Engineers

Use AI for:

- Exploring unfamiliar code
- Writing tests
- Debugging failures
- Refactoring
- Reviewing diffs
- Updating docs
- Generating migration plans
- Checking edge cases

Good pattern:

```text
Explore the codebase before editing.
Find the smallest change to implement this behavior.
Use existing patterns.
Run relevant tests.
Do not introduce a new dependency without asking.
```

Reusable skill candidates:

- Project-specific code review
- Dependency upgrade workflow
- Test generation workflow
- Incident reproduction workflow
- Release note generator

Project instruction candidates:

- Test commands
- Package manager
- Architecture rules
- Security rules
- Review checklist
- Local setup notes

### Tech Leads and Managers

Your job is not to make everyone memorize every feature.

Your job is to reduce repeated context and make good behavior easy.

Focus on:

- Standard project instructions
- Shared definitions of done
- A small library of useful skills
- Approved integrations
- Guardrails for sensitive data and risky commands
- Review norms for AI-generated work

Good team prompt:

```text
Review this repo's current AI setup.
Identify repeated instructions that should move into CLAUDE.md.
Identify workflows that should become skills.
Identify checks that are mechanical enough for hooks.
Return a prioritized plan with low-risk first steps.
```

Cross-role anti-patterns:

- Using AI to avoid reading the source material
- Treating AI output as neutral when the prompt was biased
- Reusing another role's workflow without adapting risk and audience
- Forgetting that sensitive data rules differ by function

## Experience-Based Learning Paths

[Back to Start Here](#start-here-pick-your-problem)

### If You Use AI Once a Day

Read first:

- [Should I Use AI For This Task?](#should-i-use-ai-for-this-task)
- [Generative AI Refresher](#generative-ai-refresher)
- [Glossary](#glossary)
- [Mental Model](#mental-model)
- [Core Prompting Pattern](#core-prompting-pattern)
- [Definition of Done](#definition-of-done)
- [Do Not Blindly Trust AI](#do-not-blindly-trust-ai)
- [Security, Privacy, and Data Use](#security-privacy-and-data-use)
- [Company-Specific Rules](#company-specific-rules)

Practice:

- Use [Prompt Examples](#prompt-examples) to summarize a meeting, draft an update, or convert notes into action items.
- Use [Review Checklist for AI Output](#review-checklist-for-ai-output) before sending or reusing the result.
- Use [FAQ](#faq) when you are unsure about privacy, hallucinations, ownership, review, or cost.

Avoid:

- Pasting sensitive data casually
- Accepting factual claims without sources
- Asking broad questions with no audience or output format

### If You Use AI Many Times a Day

Read first:

- [Token Usage and Reasonable Use](#token-usage-and-reasonable-use)
- [Context Is Fuel](#context-is-fuel)
- [Practical Prompting Techniques](#practical-prompting-techniques)
- [Project Instructions](#project-instructions)
- [Choosing the Right Mechanism](#choosing-the-right-mechanism)
- [Skills](#skills)
- [Measuring AI Quality](#measuring-ai-quality)

Practice:

- Create one project instruction file using [Project Instructions](#project-instructions).
- Convert one repeated prompt into a skill using [Skills](#skills).
- Add a checklist to your definition of done using [Definition of Done](#definition-of-done).
- Ask AI to critique your prompt using [Core Prompting Pattern](#core-prompting-pattern).

Avoid:

- Hiding team rules in private prompts
- Creating many overlapping skills
- Letting long chats drift without restating the target

### If You Are an Advanced User

Read first:

- [Daily Use vs Advanced Claude Code](#daily-use-vs-advanced-claude-code)
- [Hooks](#hooks)
- [MCP](#mcp)
- [Plugins](#plugins)
- [Subagents and Parallel Work](#subagents-and-parallel-work)
- [Permissions and Safety](#permissions-and-safety)
- [Work, Client, and Personal Boundaries](#work-client-and-personal-boundaries)
- [External Tools and Open-Source Resources](#external-tools-and-open-source-resources)
- [Approved External Resource Policy](#approved-external-resource-policy)

Practice:

- Create one team skill using [Skills](#skills) and review reuse through [Plugins](#plugins).
- Add one approved MCP integration using [MCP](#mcp).
- Add one low-risk hook using [Hooks](#hooks).
- Document when to use parallel agents using [Subagents and Parallel Work](#subagents-and-parallel-work).
- Build a small review workflow using [Review Checklist for AI Output](#review-checklist-for-ai-output) and [Measuring AI Quality](#measuring-ai-quality).

Avoid:

- Automating before the manual workflow is understood
- Giving broad tool access without a reason
- Using hooks for unclear judgment
- Letting multiple agents edit the same files without isolation

Learning anti-patterns:

- Trying to learn every advanced feature before improving basic prompts
- Copying another team's setup without understanding their workflow
- Measuring adoption by tool usage instead of work quality
- Training only engineers when business users also handle sensitive AI tasks

## Common Anti-Patterns

### The Giant Prompt

Problem: one massive prompt tries to explain everything.

Fix: move stable context into project instructions, repeated procedure into a skill, and task-specific details into the prompt.

### The Mystery Agent

Problem: the AI edits, runs commands, and changes direction without a clear plan.

Fix:

```text
Explore first.
Propose a plan.
Wait for approval before editing.
```

### The No-Verification Task

Problem: the AI produces output but nobody knows whether it is correct.

Fix: include a definition of done and verification step.

### The Private Team Standard

Problem: one person has a great private prompt, but the team keeps repeating mistakes.

Fix: move shared rules into `CLAUDE.md` or a shared skill.

### The Over-Automated Setup

Problem: hooks, plugins, and MCP are added before the workflow is understood.

Fix: run the workflow manually, write it down, turn it into a skill, then automate only the deterministic pieces.

## Prompt Examples

### Meeting Summary

```text
Act as an operations partner.
Summarize this meeting transcript for people who did not attend.

Return:
1. Executive summary
2. Decisions
3. Action items with owner and date
4. Open questions
5. Risks

Do not invent owners or dates.
Mark missing information clearly.
```

### Strategy Review

```text
Act as a skeptical but constructive strategy reviewer.
Review this proposal for clarity, feasibility, risks, and missing assumptions.
Separate high-confidence issues from questions.
Return a table with severity, finding, why it matters, and suggested fix.
```

### Codebase Exploration

```text
Act as a senior engineer joining this codebase.
Explain how user authentication works.
Start by reading relevant files.
Do not edit anything.
Return the main flow, key files, security-sensitive areas, and questions.
```

### Bug Fix

```text
Investigate this bug before editing.
Reproduce or explain the likely reproduction path.
Find the root cause.
Propose the smallest safe fix.
After I approve, implement it and run relevant tests.
```

### PR Review

```text
Review this diff for correctness bugs, missing tests, security risks, and maintainability issues.
Prioritize serious issues.
Do not comment on style unless it affects behavior or readability.
Return findings with file references and suggested fixes.
```

### Create a Skill From a Repeated Prompt

```text
I paste the following prompt every week.
Turn it into a reusable skill.
Keep the skill focused.
Include a clear description for when it should trigger.
Suggest where it should live for personal use and for team use.
```

Prompt example anti-patterns:

- Copying examples without adapting audience, context, or data boundary
- Using examples that include hidden assumptions
- Treating examples as policy
- Keeping old examples after the workflow changes

## Review Standards By Output Type

[Back to Start Here](#start-here-pick-your-problem)

> **Do not review every AI output the same way.** The question is not only "does this look good?" The question is "what would make this specific output wrong, risky, or misleading?"

| Output type | Main risk | Minimum review standard |
| --- | --- | --- |
| Meeting summary | Invented decisions, owners, deadlines, or action items. | Check decisions and action items against notes or transcript. Mark missing owners and dates instead of filling them in. |
| Action plan | Unrealistic sequence, unclear owner, missing dependency, hidden approval need. | Confirm owner, deadline, dependency, risk, and next step for each action. |
| Internal update | Polished wording that hides uncertainty, blockers, or tradeoffs. | Check whether status, risks, asks, and decisions are explicit. |
| Client-facing email or document | Wrong promise, wrong tone, confidential detail, or unsupported claim. | Verify facts, commitments, tone, audience, confidentiality, and approval requirements. |
| Decision memo | Biased options, weak assumptions, missing risks, or false certainty. | Require options, assumptions, evidence, tradeoffs, recommendation, and open questions. |
| Research brief | Outdated source, fabricated citation, cherry-picked evidence, or missing uncertainty. | Check source quality, dates, citations, claim-to-source mapping, and unknowns. |
| Analysis or spreadsheet narrative | Incorrect numbers, bad formula interpretation, or correlation presented as cause. | Reconcile figures to source data. Check formulas, assumptions, definitions, and caveats. |
| Code change | Wrong behavior, regression, insecure pattern, or local convention mismatch. | Review diff, run relevant tests, check edge cases, errors, secrets, permissions, and local patterns. |
| Code review | Style noise, missed behavior bug, or unsupported severity. | Prioritize correctness, security, regressions, tests, and maintainability. Require file references. |
| Incident, bug, or root-cause analysis | Guessing cause before evidence, missing timeline, or unverified fix. | Require timeline, evidence, contributing factors, customer impact, mitigation, prevention, and owner. |
| Support response | Wrong entitlement, overpromising, bad empathy, or leaking internal information. | Verify customer facts, policy, tone, allowed commitments, and escalation path. |
| HR, legal, security, privacy, or compliance-sensitive text | Inappropriate advice, policy error, bias, or missing required reviewer. | Use AI only for drafting or structuring. Required human owner must review before use. |
| External-tool setup, skill, hook, plugin, MCP server, or agent | Data leakage, malicious code, license issue, unstable maintenance, or excessive permissions. | Review source, license, data flow, runtime behavior, permissions, owner, and approval status. |

**Use this simple review prompt when the output type matters:**

```text
Review this output as a [output type].
Focus on the failure modes that matter for that output type.
Return:
1. Must-fix issues
2. Claims or facts to verify
3. Missing context
4. Sensitive data or policy concerns
5. Whether this needs human escalation before use
```

Anti-patterns:

- Reviewing only grammar and tone
- Using the same checklist for a meeting summary, legal draft, and code change
- Letting a polished structure hide missing evidence
- Asking AI to approve its own high-risk output
- Treating "no issues found" as sufficient without source checks

## Review Checklist for AI Output

[Back to Start Here](#start-here-pick-your-problem)

**Before you use AI output, ask:**

- Did I give it enough context?
- Did it separate facts from assumptions?
- Did it cite sources when sources matter?
- Did it preserve constraints?
- Did it verify the result?
- Did it change only what it should?
- Could this expose sensitive data?
- Would I be comfortable owning this work?

**For code:**

- Does the diff match the request?
- Are tests present or intentionally omitted?
- Are edge cases handled?
- Are errors handled?
- Are secrets, logs, and permissions safe?
- Did generated code follow local patterns?

**For business documents:**

- Is the audience clear?
- Are decisions and recommendations explicit?
- Are risks visible?
- Is the tone appropriate?
- Are claims sourced when needed?
- Is sensitive information removed or handled correctly?

Review anti-patterns:

- Reviewing only grammar and tone
- Ignoring assumptions because the output is well structured
- Skipping source checks for factual claims
- Letting the AI review its own high-risk output without a human owner

## Claude Courses

[Back to Start Here](#start-here-pick-your-problem)

Course availability can change. As of the 2026-06-25 source check, Anthropic Academy course pages show "Register | FREE" and are hosted on Skilljar. Skilljar registration is separate from a Claude account, and Skilljar collects learning activity such as progress, lesson completion, quiz scores, and time spent.

- Anthropic Academy course catalog: https://anthropic.skilljar.com/
- Claude 101: https://anthropic.skilljar.com/claude-101
- Claude Code in Action: https://anthropic.skilljar.com/claude-code-in-action
- Building with the Claude API: https://anthropic.skilljar.com/claude-with-the-anthropic-api
- Introduction to Model Context Protocol: https://anthropic.skilljar.com/introduction-to-model-context-protocol
- Introduction to agent skills: https://anthropic.skilljar.com/introduction-to-agent-skills
- Introduction to subagents: https://anthropic.skilljar.com/introduction-to-subagents

Suggested path:

1. Start with Claude 101 for everyday prompting, context, review, and basic Claude use.
2. Use Claude Code in Action for Claude Code, context management, commands, MCP, GitHub integration, hooks, and SDK concepts.
3. Use Introduction to agent skills when you are ready to turn repeated workflows into reusable skills.
4. Use Introduction to Model Context Protocol when you need approved tool or data integrations.
5. Use Introduction to subagents when larger work needs focused delegated workstreams.
6. Use Building with the Claude API for developers building Claude applications, tool use, RAG, MCP, Claude Code, and agentic workflows.

## Official Docs

Claude Code:

- Overview: https://code.claude.com/docs/en/overview
- Best practices: https://code.claude.com/docs/en/best-practices
- Common workflows: https://code.claude.com/docs/en/common-workflows
- Commands: https://code.claude.com/docs/en/commands
- Desktop app, Code tab, and Cowork mention: https://code.claude.com/docs/en/desktop
- Memory and instructions: https://code.claude.com/docs/en/memory
- Model configuration: https://code.claude.com/docs/en/model-config
- Claude models overview: https://platform.claude.com/docs/en/about-claude/models/overview
- Claude API pricing: https://platform.claude.com/docs/en/about-claude/pricing
- Anthropic Academy: https://www.anthropic.com/learn
- Output styles: https://code.claude.com/docs/en/output-styles
- Fast mode: https://code.claude.com/docs/en/fast-mode
- Settings: https://code.claude.com/docs/en/settings
- Skills: https://code.claude.com/docs/en/skills
- Hooks: https://code.claude.com/docs/en/hooks
- MCP: https://code.claude.com/docs/en/mcp
- Plugins: https://code.claude.com/docs/en/plugins
- Subagents: https://code.claude.com/docs/en/sub-agents
- Permissions: https://code.claude.com/docs/en/permissions

Standards:

- Agent Skills: https://agentskills.io
- MCP: https://modelcontextprotocol.io
