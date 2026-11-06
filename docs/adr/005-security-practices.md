# Title: Security and Data Integrity Practices

Context: The system must protect tenant/business boundaries, validate inputs, and prevent data drift between order states and inventory movements.

*Decision:*

- Enforce **server-side authorization** (e.g., via middleware) to ensure all operations respect user permissions.
- Validate **all inputs at trust boundaries** (e.g., API endpoints, CLI commands).
- Log **critical state transitions** (e.g., "Order status changed from 'Pending' to 'Completed'") for auditing.
- Use **immutable records** for order history and shipment logs.

*Consequences:*

- Reduces risk of unauthorized access or data corruption.
- Ensures compliance with security best practices for multi-tenant systems.
