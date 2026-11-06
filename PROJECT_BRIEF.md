# Flow Pilot — Project Brief

**Status:** Discovery baseline  
**Version:** 0.1  
**Product stage:** MVP definition; no technology stack selected

## 1. Product vision

Flow Pilot is a configurable business-operations workspace for small businesses that receive customer items, perform services such as repair, sharpening or maintenance, and return those items to customers.

It combines customer and service-order management, workshop operations, inventory, shipping records, employee permissions, operational visibility and an AI assistant.

The product must adapt to different business processes rather than forcing every business to follow one fixed workflow.

## 2. Initial target customer

The first target segment is small service and repair businesses that receive, process and return customer-owned items.

The first real-world case study is a business that sharpens carpentry and woodworking tools and saws, has retail activity, and operates across more than one physical location. Its work commonly involves receiving and sending shipments. Other businesses may rely more heavily on customer drop-off or employee collection.

The case study informs the first templates and examples; it must not hard-code the product around saw sharpening.

## 3. Product principles

1. **Configurable, not hard-coded:** businesses can adapt intake methods, statuses, steps and responsibilities.
2. **Different entry paths, one order model:** shipment receipt, customer drop-off and employee collection all create service orders in the same system.
3. **Track the detail:** a service order can contain multiple items, and each item can progress independently.
4. **Human control over AI:** AI proposes; an authorized person reviews and approves before generated workflows become active. Automatic activation may be introduced later for trusted users and explicitly selected workflow types.
5. **Permission-aware assistance:** the AI assistant must never expose information or perform actions beyond the current employee's permissions.
6. **Location-aware operations:** orders, items, inventory and employees can be associated with business locations and facilities.
7. **Build the core first:** internal operations precede the customer portal and advanced visual workflow builder.
8. **Design for future SaaS:** the first release serves one business, but architecture should avoid decisions that make future independent business accounts prohibitively difficult.

## 4. MVP product scope

### Core workspace

- One business account in the initial MVP.
- Employee accounts and access.
- Four starter roles: Owner/Admin, Manager, Technician/Workshop Employee, Sales/Front Desk.
- Administrators can create, duplicate, rename, edit and assign custom roles and granular permissions.
- Employees may have more than one role.
- Multiple business locations, with facilities such as workshop, warehouse and storefront within a location.

### CRM

- Individual and business customers.
- Multiple contacts and addresses for a business customer.
- Contact details, notes and customer history.
- Preferred intake and return methods.
- Customer-specific pricing or discounts.
- Communication history.

### Service Orders

- Intake methods: shipment received, customer drop-off and employee collection; businesses can enable the methods they use.
- One order can contain multiple items.
- Each item has its own description/type, quantity, requested service, received condition, processing status and price.
- Order-level status alongside item-level status.
- Assign work to employees and track workshop progress.
- Quality-control stage and result.
- Support both complete return and partial return.
- Preserve item and order histories.
- Track the current location of an order/item where applicable.

### Quotes, pricing and payment tracking

- Price services per item and calculate order totals.
- Create estimates/quotes before work starts.
- Record customer acceptance or rejection of quotes.
- Allow discounts and additional charges with a reason.
- Track payment status and amounts.
- No integrated payment processing in the initial MVP.

### Shipping

- Record incoming and outgoing shipments.
- Store courier, tracking number and shipping cost.
- Manually update shipment status.
- Link shipments to service orders.
- Support multiple incoming parcels and multiple outgoing/partial-return shipments for one order.
- Keep shipment history.
- No live courier integrations or label generation in the initial MVP.

### Inventory

- Products, materials and spare parts.
- Quantities per location.
- Stock movements and inter-location transfers.
- Minimum-stock alerts.
- Record materials/parts consumed by a service order.
- Distinguish available, reserved and consumed stock.
- Stock movement history.
- Advanced purchasing, supplier management and automated replenishment are later scope.

### Workflow management

- Three workflow creation paths: AI-assisted setup, templates and manual creation.
- Simple guided workflow configuration in the MVP.
- Configurable statuses, steps, assignments, basic conditions/automation and notifications.
- A shared workflow definition/execution model should be capable of supporting a future visual builder.
- Advanced drag-and-drop visual builder is later scope.
- AI-generated workflows require human review and approval before activation.
- Preserve workflow versions and execution/activity history; provide safe deactivation and a recovery/rollback strategy.

### Notifications

- Internal notifications for new orders, assignments, status events requiring attention, quality-control outcomes, items ready for return, low stock and quote approvals.
- Basic customer email notifications for order received, quote approval, work progress/completion, partial shipment dispatch and collection readiness.
- Notification rules should be configurable by workflow/event.
- Keep a record of sent messages and delivery status where the email provider supports it.
- SMS and WhatsApp are later integrations.

### Operations dashboard and reporting

- New, active and completed orders.
- Orders requiring attention.
- Items in workshop, awaiting quality control or ready for return.
- Employee workload.
- Orders and stock by location.
- Revenue/order value, outstanding quotes and unpaid orders.
- Low-stock alerts.
- Role-aware visibility.

### AI assistant

- Answer questions about operational business data.
- Natural-language search across customers, orders and inventory.
- Summarize service orders and customer histories.
- Suggest workflow improvements.
- Identify operational issues such as overdue orders and stock shortages.
- Help create or modify workflows, subject to human approval.
- Enforce the same permissions as the requesting employee.
- Autonomous execution of business actions is not part of the initial MVP.

## 5. Explicitly later scope

- Customer-facing portal (design for it, build after internal operations and order management).
- Advanced visual drag-and-drop workflow builder.
- Courier API integrations, live tracking and label generation.
- SMS and WhatsApp messaging.
- Integrated online payments.
- Supplier management, purchase orders and automated replenishment.
- Broad autonomous AI execution.
- Multi-business SaaS onboarding and billing. The MVP is for one business, while the architecture should remain tenant-ready.

## 6. Initial end-to-end example

A customer sends several saw blades by courier.

1. A staff member records the customer and incoming shipment.
2. A service order is created with multiple individual items.
3. Each item is described, its received condition is recorded and the requested service is selected.
4. A quote may be prepared and sent for customer approval.
5. Once accepted, work is assigned and items move through configurable workshop stages.
6. Completed items pass through quality control.
7. The business either waits until all items are ready or creates a partial return for completed items.
8. Outgoing shipment records, courier details and tracking numbers are recorded.
9. The order and each item retain their own histories and final statuses.

The same order model must also support customer drop-off and employee collection.

## 7. Success criteria for the MVP

The MVP should let a pilot business:

- Configure its basic service workflow without developer intervention.
- Create and manage customers and multi-item service orders.
- Receive items through any enabled intake method.
- Track each item independently through workshop and quality control.
- Quote work and track payment status.
- Return all items together or partially.
- Record shipments and stock movements across locations.
- Give employees access according to configurable roles and permissions.
- See operational bottlenecks in a dashboard.
- Ask the AI assistant questions without bypassing permissions.
- Review and approve AI-proposed workflows before activation.

## 8. Important constraints and open questions

The following are not yet decided and must not be silently assumed:

- Technology stack, hosting, database and deployment approach.
- Authentication provider and exact account invitation process.
- Detailed data retention, backup, privacy and regulatory requirements.
- Exact service-order status catalogue and which transitions are configurable.
- Whether quote approval is recorded internally, by email link, or both.
- Tax/VAT handling, currencies, invoice numbering and accounting integrations.
- Whether retail point-of-sale functionality is needed; retail exists in the case study, but a full POS was not agreed for the MVP.
- Exact inventory costing method and whether negative stock is ever permitted.
- Exact email provider and template editor.
- Detailed reporting definitions and accounting treatment.
- Whether the first pilot uses one or multiple locations at launch.

Resolve these through discovery and architecture review before implementation.
