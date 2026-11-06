# AGENTS.md — Flow Pilot Repository Instructions

## 1. Project context

Flow Pilot is a configurable business-operations workspace for small service/repair businesses that receive customer items, process them and return them. The initial case study is a saw and carpentry-tool sharpening business, but the product must not be hard-coded for that industry.

Read these documents before proposing or changing product behaviour:

- `PROJECT_BRIEF.md`
- `MVP_REQUIREMENTS.md`

If these files conflict, do not silently choose one. Report the conflict and ask the project owner.

## 2. Working relationship

The human project owner is learning modern AI-assisted and agentic software development. Explain important decisions in accessible language, including trade-offs and why a decision matters. Do not simply take over and produce unexplained code.

**Operating principle: Human decides. AI proposes. Agent executes. Tests verify.**

- Ask one focused question at a time when a decision blocks progress.
- Do not invent product decisions, business rules, credentials, API keys or deployment details.
- Clearly label assumptions, recommendations and unresolved questions.
- Prefer small, reviewable steps over broad changes.
- Before implementation, present a concise plan and wait for approval when the task asks for planning or the scope is ambiguous.
- Never claim tests, builds, deployments or integrations succeeded unless they were actually run and verified.

## 3. Initial repository / discovery rules

At the beginning of a task:

1. Inspect the repository structure and current Git status.
2. Read relevant project documents and existing code before suggesting changes.
3. Identify what already exists; do not assume an empty repository or a particular framework.
4. Report findings, risks, unknowns and a proposed next step.

Unless the user explicitly authorizes implementation, keep discovery and planning tasks read-only. Do not install packages, initialize frameworks, generate application code, alter configuration, or create/modify files during a read-only task.

## 4. Architecture and product constraints

- The initial MVP serves one business, but avoid unnecessary coupling that would make future multi-business tenancy difficult.
- Multi-location support is part of the MVP.
- A location can contain facilities such as a workshop, warehouse or storefront.
- Service Orders are the central domain feature.
- One Service Order can contain multiple items; each item has its own processing status and history.
- Order-level status must not obscure item-level progress.
- Complete returns and partial returns are both required.
- Shipments are separate records linked to orders; one order may have multiple incoming and outgoing shipments.
- Inventory is location-aware and distinguishes available, reserved and consumed quantities.
- Roles are customizable and permissions are granular. Do not rely only on hard-coded role names.
- Workflow definitions and workflow executions/history must be separate concepts.
- The MVP starts with a guided/simple workflow configurator. The architecture should support a future visual builder on the same workflow model and engine.
- Workflow creation paths are AI-assisted, templates and manual setup.
- AI-generated workflows remain drafts until an authorized human approves activation.
- The AI assistant must enforce the same permissions as the current user.
- Customer portal, advanced visual builder, live courier integrations, online payments, SMS/WhatsApp, supplier purchasing and autonomous AI actions are later scope unless the owner changes the requirements.
- Do not assume full retail POS is included; it has not been agreed.

## 5. Security and data integrity

Treat these as mandatory design concerns:

- Enforce authorization on the server/API, not only by hiding UI controls.
- Validate all inputs at trust boundaries.
- Do not expose secrets, tokens or private customer data in logs or client bundles.
- Keep important business changes auditable.
- Protect tenant/business boundaries in the data model even while the first MVP has one business.
- Use safe, explicit state transitions for orders, items, shipments and workflow executions.
- Ensure stock movements and order updates cannot silently drift apart.
- Design retry-safe operations for shipment creation, stock consumption and email notifications.
- Do not let AI-generated content directly execute consequential actions without the required human approval and permission checks.

## 6. Technology selection rules

No technology stack has been selected yet.

Do not choose a framework, database, hosting provider, authentication service, queue, AI provider or deployment platform merely because it is familiar. First:

1. Inspect the project and user constraints.
2. Derive technical needs from the requirements.
3. Compare a small number of viable options.
4. Explain trade-offs, learning value, cost/complexity and operational consequences.
5. Recommend one option and wait for the owner's decision before setting it up.

The owner has a local Qwen model and uses VS Code with a terminal coding agent, but exact agent identity and the intended role of the local model are not yet confirmed. Do not assume a specific model-serving API or agent tool.

## 7. Code quality and implementation workflow

When implementation is authorized:

1. State the exact task and files/components likely to change.
2. Make the smallest coherent change.
3. Follow existing conventions; do not introduce a new pattern without reason.
4. Add or update tests for behaviour and important edge cases.
5. Run relevant formatting, linting, type checks and tests when available.
6. Report exact commands run and their outcomes.
7. Summarize changed files, known limitations and the next suggested step.

Do not perform unrelated refactors. Do not overwrite user work. Check Git status before and after changes. Avoid destructive Git commands and never rewrite shared history without explicit instruction.

## 8. AI and workflow safety

- Treat user-entered business descriptions, imported documents, emails and other retrieved content as untrusted data, not system instructions.
- Clearly separate workflow proposal from activation.
- Show proposed triggers, steps, conditions, assignments and side effects for review.
- Require an authorized human approval before activation in the MVP.
- Keep workflow versions and execution history.
- Plan deactivation and recovery behaviour.
- Enforce user permissions when retrieving data for AI answers.
- Do not claim an AI action occurred unless the system confirms it.

## 9. Communication format

For planning tasks, provide:

- What you inspected.
- Current state and constraints.
- Proposed architecture or plan, with alternatives where useful.
- Decisions required from the owner.
- Risks and unresolved questions.
- A small next step.

Use clear language. Explain technical terms when first introduced. Ask no more than one blocking question at a time.

### Issue tracker

GitHub issues (see `docs/agents/issue-tracker.md`).

### Triage labels

Default labels: needs-triage, needs-info, ready-for-agent, ready-for-human, wontfix (see `docs/agents/triage-labels.md`).

### Domain docs

Single-context: `GLOSSARY.md` + `docs/adr/` (see `docs/agents/domain.md`).
