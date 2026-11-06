# Title: Inventory Tracking

Context: The system requires location-aware inventory management to track available, reserved, and consumed quantities across multiple locations. A clear strategy is needed to ensure accurate stock levels and prevent over- or under-allocation.

*Decision:* Implement a location-aware inventory system with:

- Three quantity states: `available`, `reserved`, and `consumed`
- Per-location tracking of item quantities
- Integration with service order item processing to update inventory in real-time

*Consequences:* This approach ensures accurate stock management but requires careful synchronization across locations. It provides visibility into stock levels while supporting complex workflows involving multiple facilities.
