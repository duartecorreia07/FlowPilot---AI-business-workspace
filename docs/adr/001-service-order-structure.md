# Title: Service Order Structure

Context: Service Orders are the central domain feature, containing multiple items with individual processing statuses. A clear structure is needed to manage order-level status without obscuring
item-level progress.

## Decision: Implement a service order with

- An array of items, each tracking quantity, condition, and processing steps
- Separate status fields for the order and each item
- Historical records for completed actions

## Consequences

This structure enables granular tracking of item progress while maintaining order-level context. It requires additional storage but improves clarity for both users and automated workflows.
