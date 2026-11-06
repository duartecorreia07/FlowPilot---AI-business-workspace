# Product Decision: Dual Workflow Management

Flow Pilot will provide two distinct workflow management experiences:

## 1. Simple Workflow Configuration

- Guided, form-based configuration.
- Predefined workflow templates.
- Customizable statuses and steps.
- Employee assignments and responsibilities.
- Basic automation and notifications.

## 2. Advanced Visual Workflow Builder

- Drag-and-drop workflow creation.
- Conditional branching.
- Event triggers and automated actions.
- Integrations and AI-powered steps.
- Advanced process customization.

**Architecture principle:**

Both experiences must use the same underlying workflow definition model and execution engine.

The simple configurator must remain accessible to non-technical users, while the visual builder provides advanced capabilities without requiring programming knowledge.

The two experiences must support compatible workflow definitions, validation and versioning.
