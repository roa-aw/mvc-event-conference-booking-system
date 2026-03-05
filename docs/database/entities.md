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

# Table Structures

## Users

UserId (PK, int)  
FullName (nvarchar(100))  
Email (nvarchar(150), unique)  
PasswordHash (nvarchar(255))  
IsActive (bit)  
CreatedAt (datetime)

---

## Roles

RoleId (PK, int)  
RoleName (nvarchar(50))  
Description (nvarchar(200))

---

## UserRoles

UserRoleId (PK, int)  
UserId (FK → Users.UserId)  
RoleId (FK → Roles.RoleId)  
AssignedAt (datetime)

---

## Rooms

RoomId (PK, int)  
RoomName (nvarchar(100))  
Location (nvarchar(200))  
Capacity (int)  
CreatedAt (datetime)

---

## Seats

SeatId (PK, int)  
RoomId (FK → Rooms.RoomId)  
SeatNumber (nvarchar(10))  
RowNumber (nvarchar(10))  
IsActive (bit)

---

## Events

EventId (PK, int)  
EventName (nvarchar(150))  
Description (nvarchar(500))  
RoomId (FK → Rooms.RoomId)  
OrganizerId (FK → Users.UserId)  
EventDate (datetime)  
TicketPrice (decimal)  
Status (nvarchar(20))  
CreatedAt (datetime)

---

## Bookings

BookingId (PK, int)  
UserId (FK → Users.UserId)  
EventId (FK → Events.EventId)  
SeatId (FK → Seats.SeatId)  
BookingDate (datetime)  
Status (nvarchar(20))  
TotalAmount (decimal)

---

## Payments

PaymentId (PK, int)  
BookingId (FK → Bookings.BookingId)  
Amount (decimal)  
PaymentDate (datetime)  
PaymentMethod (nvarchar(50))  
PaymentStatus (nvarchar(20))

---

## Notifications

NotificationId (PK, int)  
UserId (FK → Users.UserId)  
Title (nvarchar(150))  
Message (nvarchar(500))  
IsRead (bit)  
CreatedAt (datetime)

---

## AuditLogs

AuditLogId (PK, int)  
UserId (FK → Users.UserId)  
Action (nvarchar(200))  
EntityName (nvarchar(100))  
EntityId (int)  
Timestamp (datetime)

---

## ApprovalRequests

ApprovalId (PK, int)  
EventId (FK → Events.EventId)  
RequestedBy (FK → Users.UserId)  
ApprovedBy (FK → Users.UserId)  
Status (nvarchar(20))  
RequestDate (datetime)  
ApprovalDate (datetime)

---

## SystemSettings

SettingId (PK, int)  
SettingKey (nvarchar(100))  
SettingValue (nvarchar(500))  
UpdatedAt (datetime)