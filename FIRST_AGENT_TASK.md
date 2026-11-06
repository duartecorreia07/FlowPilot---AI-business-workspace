# First Agent Task — Flow Pilot Architecture & Implementation Plan (Read-Only)

Paste the prompt below into your terminal coding agent from the root of the Flow Pilot repository.

---

You are helping plan Flow Pilot. **This is a read-only discovery and planning task. Do not modify files, install dependencies, initialize a framework, generate code, or change Git state.**

## Read first

1. `AGENTS.md`
2. `PROJECT_BRIEF.md`
3. `MVP_REQUIREMENTS.md`
4. Existing `README.md` and all relevant repository files.

## Your task

Produce an architecture and implementation plan for the agreed MVP. The project owner is learning agentic development, so explain the reasoning and trade-offs rather than giving only a list of technologies.

### Step 1 — Repository inspection

- Report the current branch, Git status and repository structure.
- Identify existing code, configuration, documentation and dependencies.
- Do not assume the repository is empty or that a framework has been selected.
- Flag any mismatch between the repository and the product documents.

### Step 2 — Domain model proposal

Propose the core domain entities and relationships. At minimum, consider:

- Business/workspace (future tenant boundary)
- Location and facility
- Employee/user, role and permission
- Customer, contact and address
- Service Order and Service Order Item
- Service type / requested work
- Workflow definition, version, step and execution
- Assignment and quality-control result
- Quote, quote line/adjustment and payment record/status
- Incoming/outgoing shipment and shipment item
- Inventory item, stock balance and stock movement
- Notification and communication record
- Audit event

For each entity, explain its purpose and the important relationships. Highlight decisions that still need product-owner input. Do not over-model speculative features.

### Step 3 — Critical business rules

Describe how the design should handle:

- Order-level status versus item-level status.
- Multiple items in one order.
- Partial returns and multiple outgoing shipments.
- Multiple incoming parcels.
- Item location and inter-location transfers.
- Available, reserved and consumed inventory.
- Quote approval and payment-status tracking without payment processing.
- Workflow versioning while orders are in progress.
- Human approval before AI-generated workflows activate.
- Permission enforcement for both UI/API and AI assistant.

Identify edge cases and propose safe defaults, but label recommendations as recommendations.

### Step 4 — Architecture options

Compare a maximum of three realistic approaches for:

- Frontend/application architecture.
- Backend/API architecture.
- Database and data access.
- Authentication and authorization.
- Background jobs/notifications.
- AI integration, including how a local Qwen model might fit without assuming its serving interface.
- Hosting/deployment.

Do not select a stack based on popularity alone. Evaluate:

- Suitability for the MVP.
- Complexity for a developer with some coding experience.
- Learning/portfolio value.
- Cost and local-development requirements.
- Maintainability and future multi-business SaaS support.
- Testing and deployment experience.

Recommend a coherent stack only after explaining the trade-offs. **Do not install or configure it.**

### Step 5 — System boundaries and security

Propose:

- Main application modules and their responsibilities.
- Trust boundaries and server-side authorization approach.
- Audit and data-integrity strategy.
- AI permission boundary and human-approval flow.
- Sensitive data and secrets handling.
- Backup/recovery and observability concerns.

### Step 6 — Delivery roadmap

Break the MVP into small, demonstrable milestones with dependencies. Start with the foundation and a thin end-to-end Service Order flow; avoid implementing every module in parallel.

For each milestone include:

- Goal and user-visible outcome.
- Main domain areas/files likely involved (if inferable).
- Dependencies.
- Tests and acceptance checks.
- What should be demonstrated to the project owner.

Keep later-scope items separate: customer portal, advanced visual workflow builder, live courier integrations, online payments, SMS/WhatsApp, supplier purchasing, autonomous AI actions and full retail POS.

### Step 7 — Open questions and risks

List:

- Decisions that must be made before implementation.
- Decisions that can safely wait.
- Major technical/product risks.
- Any contradictions or gaps in the documents.

Ask **only the single most important blocking question** at the end, if one exists. Otherwise state that planning can proceed to owner review.

## Required output

Return a structured report with these headings:

1. Repository findings
2. Product and technical constraints
3. Proposed domain model
4. Critical business rules
5. Architecture options and recommendation
6. Security, permissions and AI safety
7. Milestone roadmap
8. Risks and open questions
9. Recommended next action

Be explicit about what is known, what you inferred, and what you recommend. Cite filenames/paths when referring to repository evidence.

**Stop after delivering the report and wait for the project owner's feedback. Do not implement anything.**
