# DOMAIN_MODEL.md

## 1. Domain Overview & Modelling Principles

**Core Principles:**

- **Single Business Focus:** MVP serves one business but supports future multi-tenancy
- **Location Awareness:** All entities track location associations
- **Item-Level Tracking:** Service orders contain multiple items with independent statuses
- **Workflow Separation:** Definitions ≠ Executions
- **Permission First:** AI actions require explicit authorization
- **Audit Trail:** All critical operations are logged with actor, timestamp, and before/after states
- **Resilient State Transitions:** Ensure safe, retryable state changes for orders, items, shipments, and workflow executions
- **Data Integrity:** Prevent silent divergence between stock movements and order updates

## 2. Entity Descriptions & Responsibilities

### Workspace & Permissions

- **Workspace**: Container for business data (1 per MVP)
- **Location**: Physical facilities (workshop, warehouse) within a workspace
- **Facility**: Sub-division of locations (e.g., "Tool Sharpening Area")
- **User (Employee)**: Human actors with multiple roles
- **WorkspaceMembership**: Explicit link between user and workspace (1:N)
- **Role**: Configurable permissions set (Owner/Admin, Technician, etc.)
- **Permission**: Granular access control (view/edit inventory, approve quotes)
- **RoleAssignment**: Many-to-many relationship between users and roles

## 3. Entity Descriptions & Responsibilities

### Customers

- **Customer**: Individual or business entity
- **Contact**: Person associated with a customer
- **Address**: Physical address (shipping/billing) with historical snapshots
- **Preference**: Intake method preferences (shipment, drop-off)
- **BusinessCustomer**: Specialized type with multiple contacts and addresses
- **AddressSnapshot**: Historical record of address changes for shipments

### Service Orders

- **ServiceOrder**: Central domain object with:
  - Status: Configurable lifecycle (Draft → Approved → In Progress → Completed)
  - Items: Multiple ServiceOrderItem records
- **ServiceOrderItem**:
  - Description, quantity, requested service, condition
  - Independent processing status and history
  - Linked to specific inventory items
  - Distinguished from inventory materials
- **OrderStatusHistory**: Record of all status changes with timestamp and actor

### Shipments

- **Shipment**: Records incoming/outgoing shipments
- **ShipmentItem**: Explicit allocation of items in a shipment with quantity and condition
- **Tracking**: Courier details, tracking numbers, status updates
- **ShipmentPackage**: Optional container for multiple parcels with shared tracking
- **ShipmentDirection**: Explicit field to distinguish incoming vs outgoing

### Inventory

- **ProductCatalog**: Master list of products/materials
- **InventoryBalance**: Location-specific stock levels (available/reserved/consumed)
- **StockMovement**: Record of transfers/usage between locations
- **StockReservation**: Temporary allocation for service orders
- **AvailableQuantity**: Calculated field = Available - Reserved
- **ConsumedTracking**: Explicit record of inventory used during processing
- **TransferRequest**: Formal request to move stock between locations

### Workflow Engine

- **WorkflowDefinition**: Immutable template for process steps
- **WorkflowVersion**: Versioned definition with change history
- **WorkflowExecution**: Runtime instance tied to a specific version
- **WorkflowStep**: Executable action with conditions and assignments

## 3. Key Relationships & Cardinalities

| Entities | Relationship | Cardinality |
| --------- | ------------- | ------------ |
| Workspace ←→ Location | Contains | 1:N |
| Location ←→ Facility | Has | 1:N |
| User ←→ Role | Has | N:N (many roles per user) |
| Customer ←→ Contact | Has | 1:N |
| ServiceOrder ←→ ServiceOrderItem | Contains | 1:N |
| Shipment ←→ ServiceOrder | Linked | 1:N (outgoing) |
| InventoryBalance ←→ StockMovement | Tracks | N:1 |
| WorkflowDefinition ←→ WorkflowVersion | Has | 1:N |
| WorkflowExecution ←→ WorkflowStep | Executes | 1:N |

## 4. Mermaid ER Diagram

```mermaid
erDiagram
  Workspace ||--o{ Location : contains
  Location ||--o{ Facility : has
  User }--|{ RoleAssignment : has
  RoleAssignment }--o{ Permission : grants
  Customer }--|{ Contact : has
  ServiceOrder }--||{ ServiceOrderItem : contains
  Shipment }--|{ ShipmentItem : includes
  ShipmentItem }--o{ InventoryBalance : references
  InventoryBalance ||--o{ StockMovement : tracks
  InventoryBalance ||--o{ StockReservation : reserves
  ServiceOrder }--|{ Shipment : linked
  WorkflowDefinition ||--o{ WorkflowVersion : has
  WorkflowVersion ||--o{ WorkflowExecution : runs
  WorkflowExecution }--|{ WorkflowStep : executes
```

## 5. Business Rules & Invariants

1. **Partial Returns:** ShipmentItem records must specify quantity returned
2. **Location Awareness:** All inventory operations track source/destination locations
3. **Workflow Approval:** AI-generated workflows require human approval before activation
4. **Audit Trail:** Every order/item update must record actor, timestamp, and previous state
5. **Stock Reservations:** Cannot exceed available quantities
6. **Quote Lifecycle:** Must track draft → sent → accepted → rejected states
7. **Permission Enforcement:** AI actions cannot bypass user permissions
8. **Order Completion:** Requires all items to be processed or explicitly marked as complete

## 6. Key Operational Scenarios

1. **Shipment Receipt:**
   - Record incoming shipment with tracking details
   - Create service order with multiple items
   - Assign items to technicians
2. **Partial Return Process:**
   - Create outgoing shipment for completed items
   - Update inventory balances
   - Record return in order history
3. **Workflow Activation:**
   - AI proposes workflow steps
   - Manager reviews and approves
   - Execution begins with versioned definition

## 7. Workspace & Permission Boundaries

- Workspaces are tenant-isolated
- Permissions are role-based with explicit grant/revoke
- No hard-coded ownership relationships
- All operations require valid authentication

## 8. Audit Requirements

- Log all changes to:
  - User permissions
  - Service order status updates
  - Inventory movements
  - Workflow activations
- Retain at least 90 days of audit records
- Implement data retention policy for customer data

## 9. Unresolved Decisions

1. **Technology Stack:** Not yet selected
2. **Inventory Costing Method:** FIFO/LIFO/AVCO to be determined
3. **Quote Approval Channels:** Email link vs internal system
4. **Multi-Tenancy Implementation:** Architecture ready but no implementation yet
5. **AI Autonomy Level:** Currently requires human approval for all actions

## 10. Validation Checks

- All entities appear in ER diagram
- Cardinalities match between text and diagram
- Partial returns and multiple shipments are supported
- Stock reservations are distinct from physical movements
- Workflow definitions ≠ executions
- Tenant boundaries consistently represented
- No contradictions with project documentation
