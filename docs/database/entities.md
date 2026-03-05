# Database Entities

## Core Tables

1. Users
2. Roles
3. UserRoles
4. Events
5. Rooms
6. Seats
7. Bookings
8. Payments
9. Notifications
10. AuditLogs
11. ApprovalRequests
12. SystemSettings

## Relationships

Users ↔ Roles (Many-to-Many)

Rooms → Seats (One-to-Many)

Rooms → Events (One-to-Many)

Events → Bookings (One-to-Many)

Users → Bookings (One-to-Many)

Bookings → Payments (One-to-One)