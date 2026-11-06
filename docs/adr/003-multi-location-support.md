# Title: Multi-Location Support

Context: The MVP requires multi-location support to handle facilities like workshops, warehouses, and storefronts. A flexible architecture is needed to manage location-specific operations while maintaining a unified system view.

*Decision:* Design the system with:

- A `Location` entity containing address, capacity, and operational hours
- Location-aware service orders and inventory tracking
- Centralized management of location relationships
- Support for cross-location shipments and inventory transfers

*Consequences:* This architecture enables multi-location operations but increases complexity in data modeling and synchronization. It provides scalability for future expansion into multiple business locations.
