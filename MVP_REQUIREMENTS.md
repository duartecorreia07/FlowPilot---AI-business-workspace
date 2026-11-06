# Flow Pilot — MVP Requirements

**Status:** Initial functional baseline  
**Version:** 0.1  
**Audience:** Product owner, designer, architect and development agent

This document captures agreed product scope. Items marked **Proposed quality baseline** are engineering recommendations to validate, not previously approved business requirements.

## 1. Actors and access

### Starter roles

- Owner/Admin
- Manager
- Technician/Workshop Employee
- Sales/Front Desk Employee

### Functional requirements

- **IAM-01:** The system shall support employee accounts within the initial business workspace.
- **IAM-02:** An administrator shall be able to create, duplicate, rename, edit and assign custom roles.
- **IAM-03:** Permissions shall be granular and associated with capabilities/resources, not only hard-coded role names.
- **IAM-04:** An employee may have more than one role.
- **IAM-05:** The system shall enforce permissions in the UI, API/server operations and AI assistant.
- **IAM-06:** Administrators shall be able to review and change role assignments.
- **IAM-07:** Multi-location businesses shall be able to associate employees with one or more locations.

### Acceptance examples

- A technician cannot access financial reports unless explicitly granted permission.
- An employee with permission to update item progress can do so without receiving permission to edit roles.
- The AI assistant cannot reveal a quote or customer record the employee cannot access directly.

## 2. Business locations and facilities

- **LOC-01:** An administrator shall be able to create and edit business locations.
- **LOC-02:** A location may contain facilities such as workshop, warehouse and storefront.
- **LOC-03:** Orders/items shall record their current location when relevant.
- **LOC-04:** Inventory quantities shall be tracked by location.
- **LOC-05:** Stock and items may be transferred between locations with a recorded movement/history.
- **LOC-06:** Users with suitable permissions shall view operations for one location or across locations.

### Acceptance examples

- A user can distinguish two warehouses at different locations.
- A transfer records source, destination, items/quantities, time and responsible user.
- A dashboard can be filtered by location, subject to permissions.

## 3. CRM

- **CRM-01:** The system shall support individual and business customer records.
- **CRM-02:** A business customer may have multiple contacts and addresses.
- **CRM-03:** Customer records shall support contact details and internal notes.
- **CRM-04:** A customer profile shall show its service-order history.
- **CRM-05:** Customer preferences may include intake and return methods.
- **CRM-06:** The system shall support customer-specific pricing/discount information.
- **CRM-07:** Communication history shall be associated with the relevant customer and, where applicable, order.

### Acceptance examples

- A business customer with multiple contacts and addresses can be selected when creating an order.
- Staff can navigate from a customer profile to prior orders.

## 4. Service orders and items

- **ORD-01:** Staff with permission shall create a service order for an individual or business customer.
- **ORD-02:** The order shall record its intake method: shipment received, customer drop-off or employee collection.
- **ORD-03:** A business administrator shall be able to enable/disable intake methods used by that business.
- **ORD-04:** Intake-specific information shall be captured where relevant (for example, incoming courier/tracking details or assigned collecting employee).
- **ORD-05:** One service order shall support multiple individual items.
- **ORD-06:** Each item shall support description/type, quantity, requested service, received condition, processing status and price.
- **ORD-07:** The system shall track order-level status and item-level status separately.
- **ORD-08:** Items shall be assignable to employees or work queues.
- **ORD-09:** Item progress shall be tracked through configurable workflow stages.
- **ORD-10:** Quality control shall record a result and relevant notes.
- **ORD-11:** The system shall preserve a history of significant order and item changes.
- **ORD-12:** The system shall record the current physical location of items/orders when relevant.
- **ORD-13:** The system shall support complete return and partial return.
- **ORD-14:** An order shall not be considered fully complete merely because one item or one partial shipment is complete; order completion rules must account for remaining items and returns.
- **ORD-15:** Staff shall be able to find and filter orders by status, customer, location, intake method and other useful operational fields, subject to permissions.

### Acceptance examples

- A six-item order can show four items ready for return and two still in workshop.
- A partial return can include selected completed items while remaining items stay active.
- The order history explains which items were returned, when and through which shipment/collection.

## 5. Quotes, pricing and payment status

- **FIN-01:** The system shall support a price per service-order item.
- **FIN-02:** The system shall calculate order totals from item prices and applicable adjustments.
- **FIN-03:** Staff shall be able to prepare an estimate/quote before work begins.
- **FIN-04:** Quote status shall distinguish at least draft, sent/pending approval, accepted and rejected/expired (final state set to be confirmed).
- **FIN-05:** The system shall record customer approval or rejection of a quote.
- **FIN-06:** Authorized staff shall be able to add discounts and additional charges with a reason.
- **FIN-07:** The system shall track payment status and relevant amounts.
- **FIN-08:** The MVP shall not process online payments.

**Open decisions:** VAT/tax, currencies, invoice/receipt requirements, rounding, deposits, partial payments, quote expiry and approval channel.

## 6. Shipping and returns

- **SHP-01:** Staff shall record incoming shipments.
- **SHP-02:** Staff shall record outgoing shipments.
- **SHP-03:** A shipment record shall support courier, tracking number, shipping cost and manually updated status.
- **SHP-04:** Shipments shall be linked to service orders.
- **SHP-05:** One order shall support multiple incoming parcels and multiple outgoing shipments.
- **SHP-06:** A partial return shipment shall identify the items/quantities it contains.
- **SHP-07:** Shipment changes shall be retained in a history.
- **SHP-08:** Live courier integrations and label generation are out of MVP scope.

### Acceptance examples

- An order with six items can have one incoming parcel and two outgoing partial-return shipments.
- Staff can see which items are in each outgoing shipment.

## 7. Inventory

- **INV-01:** Authorized users shall manage products, materials and spare parts.
- **INV-02:** Stock quantities shall be tracked per location.
- **INV-03:** The system shall record stock movements and inter-location transfers.
- **INV-04:** Users shall be able to configure minimum-stock thresholds and receive low-stock alerts.
- **INV-05:** Materials/parts consumed during work may be linked to a service order/item.
- **INV-06:** Stock shall distinguish available, reserved and consumed quantities.
- **INV-07:** The system shall retain stock movement history.
- **INV-08:** Supplier management, purchasing and automated replenishment are out of MVP scope.

## 8. Workflow configuration and execution

- **WF-01:** Users shall be able to start workflow setup from AI assistance, a template or manual creation.
- **WF-02:** The MVP shall provide a guided/simple workflow configurator.
- **WF-03:** Users shall be able to configure workflow stages/statuses, assignments, basic conditions/automation and notifications.
- **WF-04:** Workflow definitions shall be separate from the workflow execution/history records.
- **WF-05:** The underlying workflow model shall be designed to support a future visual builder without requiring a separate execution engine.
- **WF-06:** AI-generated workflows shall remain drafts/proposals until an authorized human approves them.
- **WF-07:** The system shall explain the AI's proposed workflow steps and allow review/editing before approval.
- **WF-08:** Workflow definitions shall be versioned.
- **WF-09:** The system shall record workflow activation and execution activity.
- **WF-10:** Authorized users shall be able to deactivate a workflow; safe rollback/recovery behaviour shall be designed.
- **WF-11:** Automatic activation for trusted users is future scope, not enabled by default in the MVP.
- **WF-12:** Advanced drag-and-drop visual workflow builder is later scope.

### Acceptance examples

- An AI-generated workflow cannot become active without explicit approval by an authorized user.
- Editing a workflow does not silently rewrite the history of orders already running on an earlier version.
- A simple workflow can be configured without using the future visual builder.

## 9. Notifications and email

- **NTF-01:** The system shall generate internal notifications for new orders, assignments, operational status events, quality-control outcomes, return readiness, low stock and quote approvals.
- **NTF-02:** The system shall support basic customer emails for order receipt, quote approval, work progress/completion, partial shipment dispatch and collection readiness.
- **NTF-03:** Notification rules shall be configurable by workflow/event.
- **NTF-04:** The system shall retain a record of sent messages and delivery status where supported by the provider.
- **NTF-05:** SMS and WhatsApp are later scope.

## 10. Operations dashboard and reports

- **DASH-01:** The dashboard shall summarize new, active and completed service orders.
- **DASH-02:** It shall highlight orders requiring attention.
- **DASH-03:** It shall show items in workshop, awaiting quality control and ready for return.
- **DASH-04:** It shall show employee workload.
- **DASH-05:** It shall provide location-aware views of orders and inventory.
- **DASH-06:** It shall surface revenue/order values, outstanding quotes and unpaid orders, subject to permissions.
- **DASH-07:** It shall surface low-stock alerts.
- **DASH-08:** Dashboard content shall respect role permissions.

## 11. AI assistant

- **AI-01:** The assistant shall answer questions about business operations using authorized business data.
- **AI-02:** It shall support natural-language search across customers, service orders and inventory.
- **AI-03:** It shall summarize service orders and customer histories.
- **AI-04:** It shall suggest workflow improvements.
- **AI-05:** It shall identify operational issues such as overdue orders and stock shortages.
- **AI-06:** It shall help draft new workflows and proposed changes to existing workflows.
- **AI-07:** A human with appropriate permission must approve workflow changes before activation.
- **AI-08:** The assistant shall enforce the requesting user's access permissions.
- **AI-09:** Broad autonomous execution of business actions is out of MVP scope.

**Proposed quality baseline:** AI answers about operational data should identify the relevant records or evidence where practical, distinguish facts from suggestions, and ask for confirmation before any consequential action.

## 12. Later scope / exclusions

- Customer portal.
- Advanced visual workflow builder.
- Courier API integrations and label generation.
- SMS and WhatsApp.
- Online payment processing.
- Supplier management and purchase orders.
- Automated replenishment.
- Autonomous AI execution.
- Multi-business registration, tenant administration and SaaS billing.
- Full retail POS (not yet agreed).

## 13. Proposed cross-cutting quality requirements

These are recommended engineering baselines to validate during architecture planning:

- **Security:** enforce authorization server-side; protect customer and business data.
- **Auditability:** retain actor, action, timestamp and relevant before/after values for important business changes.
- **Reliability:** prevent duplicate order, shipment, inventory and notification effects when requests are retried.
- **Data integrity:** use explicit state transitions and transactional updates for stock and order operations.
- **Privacy:** collect only necessary customer data; define retention and deletion rules before production.
- **Accessibility/usability:** ensure common operational tasks are usable on desktop and mobile-sized screens.
- **Observability:** log errors and key operational events without exposing secrets or unnecessary personal data.
- **Testing:** cover permissions, order/item states, partial returns, stock movements, workflow versioning and AI approval boundaries.
- **Backup/recovery:** define backup frequency and recovery expectations before production use.

## 14. Release acceptance scenario

The MVP is ready for a pilot when a business user can:

1. Set up a business with at least one location and facilities.
2. Configure intake methods and a simple service workflow.
3. Create customer records and custom employee roles.
4. Register an incoming shipment or an in-person/employee collection.
5. Create an order with multiple items and record their conditions/services.
6. Quote the work and record customer approval.
7. Assign items, update workshop stages and record quality-control outcomes.
8. Consume materials from location-specific inventory.
9. Return all items or create partial returns with shipment records.
10. Send configured customer emails and view internal notifications.
11. Use the dashboard to identify work needing attention.
12. Ask the AI assistant about authorized records and propose a workflow that stays inactive until human approval.
