# ER Diagram Workshop – Submission Template

## Objective
To understand and apply ER modeling concepts by creating ER diagrams for real-world applications.

## Purpose
Gain hands-on experience in designing ER diagrams that represent database structure including entities, relationships, attributes, and constraints.

---

# Scenario A: City Fitness Club Management

**Business Context:**  
FlexiFit Gym wants a database to manage its members, trainers, and fitness programs.

**Requirements:**  
- Members register with name, membership type, and start date.  
- Each member can join multiple programs (Yoga, Zumba, Weight Training).  
- Trainers assigned to programs; a program may have multiple trainers.  
- Members may book personal training sessions with trainers.  
- Attendance recorded for each session.  
- Payments tracked for memberships and sessions.

### ER Diagram:
<img width="1536" height="1024" alt="fitness" src="https://github.com/user-attachments/assets/6b8b77fd-fe78-468f-b49f-d8f3fb7321ed" />


### Entities and Attributes

| Entity                | Attribute            | PK/FK | Notes                                     |
| --------------------- | -------------------- | ----- | ----------------------------------------- |
| **City**              | city_id              | PK    | Unique identifier for each city           |
|                       | city_name            |       | Name of the city                          |
|                       | state                |       | State or region of the city               |
|                       | country              |       | Country name                              |
| **Fitness Club**      | club_id              | PK    | Unique identifier for each fitness club   |
|                       | club_name            |       | Name of the fitness club                  |
|                       | address              |       | Physical address of the club              |
|                       | city_id              | FK    | References City(city_id)                  |
|                       | phone_number         |       | Contact number of the club                |
| **Member**            | member_id            | PK    | Unique identifier for each member         |
|                       | first_name           |       | Member's first name                       |
|                       | last_name            |       | Member's last name                        |
|                       | dob                  |       | Date of birth                             |
|                       | phone_number         |       | Member's phone number                     |
|                       | email                |       | Member's email address                    |
|                       | club_id              | FK    | References Fitness Club(club_id)          |
| **Trainer**           | trainer_id           | PK    | Unique identifier for each trainer        |
|                       | first_name           |       | Trainer's first name                      |
|                       | last_name            |       | Trainer's last name                       |
|                       | specialty            |       | Trainer's specialty                       |
|                       | club_id              | FK    | References Fitness Club(club_id)          |
| **Membership**        | membership_id        | PK    | Unique identifier for membership plan     |
|                       | membership_type      |       | Type of membership (e.g., monthly)        |
|                       | price                |       | Price of the membership                   |
| **Member_Membership** | member_membership_id | PK    | Unique identifier for member's membership |
|                       | member_id            | FK    | References Member(member_id)              |
|                       | membership_id        | FK    | References Membership(membership_id)      |
|                       | start_date           |       | Membership start date                     |
|                       | end_date             |       | Membership end date                       |

### Relationships and Constraints

| Relationship               | Entities Involved                 | Cardinality                          | Participation                        | Notes                                                                                   |
| -------------------------- | --------------------------------- | ------------------------------------ | ------------------------------------ | --------------------------------------------------------------------------------------- |
| **City - Fitness Club**    | City (1) ↔ Fitness Club (Many)    | 1 to Many                            | City: Total, Club: Partial           | Each city must have at least one fitness club; a club belongs to exactly one city.      |
| **Fitness Club - Member**  | Fitness Club (1) ↔ Member (Many)  | 1 to Many                            | Club: Total, Member: Partial         | Each club can have many members; each member belongs to exactly one club.               |
| **Fitness Club - Trainer** | Fitness Club (1) ↔ Trainer (Many) | 1 to Many                            | Club: Total, Trainer: Partial        | Each club can have multiple trainers; each trainer works at exactly one club.           |
| **Member - Membership**    | Member (Many) ↔ Membership (Many) | Many to Many (via Member_Membership) | Member: Partial, Membership: Partial | Members can have multiple memberships over time; memberships can apply to many members. |
| **Member_Membership**      | Member_Membership (bridge entity) | N/A                                  | N/A                                  | Links members and their memberships with start/end dates.                               |


### Assumptions
Single Club Membership: Each member is registered to only one fitness club at a time.

Trainer Assignment: A trainer can only be assigned to one fitness club, not multiple clubs simultaneously.

Membership Duration: Memberships have defined start and end dates, and members can hold multiple memberships over time but not concurrently


---

# Scenario B: City Library Event & Book Lending System

**Business Context:**  
The Central Library wants to manage book lending and cultural events.

**Requirements:**  
- Members borrow books, with loan and return dates tracked.  
- Each book has title, author, and category.  
- Library organizes events; members can register.  
- Each event has one or more speakers/authors.  
- Rooms are booked for events and study.  
- Overdue fines apply for late returns.

### ER Diagram:
<img width="779" height="430" alt="Screenshot 2025-09-30 112600" src="https://github.com/user-attachments/assets/3dbdbd1a-e296-4c00-a131-9a09d01624ce" />


### Entities and Attributes
| Entity               | Attribute         | PK/FK | Notes                                          |
| -------------------- | ----------------- | ----- | ---------------------------------------------- |
| **Library**          | library_id        | PK    | Unique identifier for each library             |
|                      | library_name      |       | Name of the library                            |
|                      | address           |       | Physical address of the library                |
|                      | phone_number      |       | Contact number for the library                 |
|                      | city              |       | City where the library is located              |
| **Book**             | book_id           | PK    | Unique identifier for each book                |
|                      | title             |       | Title of the book                              |
|                      | author            |       | Author(s) of the book                          |
|                      | publisher         |       | Publisher of the book                          |
|                      | year_published    |       | Year book was published                        |
|                      | library_id        | FK    | References Library(library_id)                 |
|                      | copies_available  |       | Number of available copies                     |
| **Member**           | member_id         | PK    | Unique identifier for each library member      |
|                      | first_name        |       | Member's first name                            |
|                      | last_name         |       | Member's last name                             |
|                      | date_of_birth     |       | Member's birth date                            |
|                      | phone_number      |       | Member's contact number                        |
|                      | email             |       | Member's email address                         |
|                      | library_id        | FK    | References Library(library_id)                 |
| **Book_Lending**     | lending_id        | PK    | Unique identifier for each lending transaction |
|                      | book_id           | FK    | References Book(book_id)                       |
|                      | member_id         | FK    | References Member(member_id)                   |
|                      | lending_date      |       | Date when the book was lent                    |
|                      | due_date          |       | Due date for returning the book                |
|                      | return_date       |       | Actual return date (nullable if not returned)  |
| **Event**            | event_id          | PK    | Unique identifier for each event               |
|                      | event_name        |       | Name of the event                              |
|                      | event_date        |       | Date of the event                              |
|                      | description       |       | Brief description of the event                 |
|                      | library_id        | FK    | References Library(library_id)                 |
| **Event_Attendance** | attendance_id     | PK    | Unique identifier for each attendance record   |
|                      | event_id          | FK    | References Event(event_id)                     |
|                      | member_id         | FK    | References Member(member_id)                   |
|                      | attendance_status |       | Status (e.g., registered, attended, canceled)  |


### Relationships and Constraints:
| Relationship                  | Entities Involved                    | Cardinality | Participation                        | Notes                                                                                       |
| ----------------------------- | ------------------------------------ | ----------- | ------------------------------------ | ------------------------------------------------------------------------------------------- |
| **Library - Book**            | Library (1) ↔ Book (Many)            | 1 to Many   | Library: Total, Book: Partial        | Each library must have at least one book; each book belongs to exactly one library.         |
| **Library - Member**          | Library (1) ↔ Member (Many)          | 1 to Many   | Library: Total, Member: Partial      | Each library manages many members; each member is registered to exactly one library.        |
| **Library - Event**           | Library (1) ↔ Event (Many)           | 1 to Many   | Library: Total, Event: Partial       | Each library hosts many events; each event belongs to exactly one library.                  |
| **Book - Book_Lending**       | Book (1) ↔ Book_Lending (Many)       | 1 to Many   | Book: Total, Lending: Partial        | Each book can be lent multiple times; each lending record relates to exactly one book.      |
| **Member - Book_Lending**     | Member (1) ↔ Book_Lending (Many)     | 1 to Many   | Member: Total, Lending: Partial      | Each member can borrow multiple books over time; each lending record belongs to one member. |
| **Event - Event_Attendance**  | Event (1) ↔ Event_Attendance (Many)  | 1 to Many   | Event: Total, Attendance: Partial    | Each event has many attendance records; each attendance belongs to exactly one event.       |
| **Member - Event_Attendance** | Member (1) ↔ Event_Attendance (Many) | 1 to Many   | Member: Partial, Attendance: Partial | Members may attend zero or more events; attendance links members to events.                 |


### Assumptions
Single Library Membership: A member is registered to only one library branch at a time.

Book Copies Tracking: Multiple copies of the same book can exist in a library, and the system tracks availability based on copies.

Event Attendance Optional: Members are not required to attend events, and attendance is recorded only if they choose to participate.





---

# Scenario C: Restaurant Table Reservation & Ordering

**Business Context:**  
A popular restaurant wants to manage reservations, orders, and billing.

**Requirements:**  
- Customers can reserve tables or walk in.  
- Each reservation includes date, time, and number of guests.  
- Customers place food orders linked to reservations.  
- Each order contains multiple dishes; dishes belong to categories (starter, main, dessert).  
- Bills generated per reservation, including food and service charges.  
- Waiters assigned to serve reservations.

### ER Diagram:
<img width="1080" height="790" alt="Screenshot 2025-10-06 140525" src="https://github.com/user-attachments/assets/e95d2b69-2819-4ff4-a775-8620e8e1af46" />


### Entities and Attributes

| Entity          | Attribute        | PK/FK | Notes                                             |
| --------------- | ---------------- | ----- | ------------------------------------------------- |
| **Restaurant**  | restaurant_id    | PK    | Unique identifier for the restaurant              |
|                 | name             |       | Name of the restaurant                            |
|                 | address          |       | Physical address                                  |
|                 | phone_number     |       | Contact phone number                              |
| **Table**       | table_id         | PK    | Unique identifier for each table                  |
|                 | restaurant_id    | FK    | References Restaurant(restaurant_id)              |
|                 | table_number     |       | Table number or identifier                        |
|                 | seats            |       | Number of seats at the table                      |
|                 | location_desc    |       | Description of table location (e.g., window side) |
| **Customer**    | customer_id      | PK    | Unique identifier for each customer               |
|                 | first_name       |       | Customer first name                               |
|                 | last_name        |       | Customer last name                                |
|                 | phone_number     |       | Customer contact number                           |
|                 | email            |       | Customer email address                            |
| **Reservation** | reservation_id   | PK    | Unique identifier for each reservation            |
|                 | customer_id      | FK    | References Customer(customer_id)                  |
|                 | table_id         | FK    | References Table(table_id)                        |
|                 | reservation_date |       | Date of reservation                               |
|                 | reservation_time |       | Time of reservation                               |
|                 | number_of_guests |       | Number of guests for the reservation              |
| **Menu_Item**   | menu_item_id     | PK    | Unique identifier for each menu item              |
|                 | restaurant_id    | FK    | References Restaurant(restaurant_id)              |
|                 | item_name        |       | Name of the menu item                             |
|                 | description      |       | Description of the menu item                      |
|                 | price            |       | Price of the item                                 |
| **Order**       | order_id         | PK    | Unique identifier for each order                  |
|                 | reservation_id   | FK    | References Reservation(reservation_id)            |
|                 | order_date       |       | Date when order was placed                        |
|                 | total_amount     |       | Total amount of the order                         |
| **Order_Item**  | order_item_id    | PK    | Unique identifier for each order item             |
|                 | order_id         | FK    | References Order(order_id)                        |
|                 | menu_item_id     | FK    | References Menu_Item(menu_item_id)                |
|                 | quantity         |       | Quantity ordered                                  |
|                 | item_price       |       | Price of the item at the time of order            |



### Relationships and Constraints

| Relationship               | Entities Involved                 | Cardinality | Participation                         | Notes                                                                                    |
| -------------------------- | --------------------------------- | ----------- | ------------------------------------- | ---------------------------------------------------------------------------------------- |
| **Restaurant - Table**     | Restaurant (1) ↔ Table (Many)     | 1 to Many   | Restaurant: Total, Table: Partial     | Each restaurant has many tables; each table belongs to exactly one restaurant.           |
| **Restaurant - Menu_Item** | Restaurant (1) ↔ Menu_Item (Many) | 1 to Many   | Restaurant: Total, Menu_Item: Partial | Each restaurant offers many menu items; each menu item belongs to one restaurant.        |
| **Customer - Reservation** | Customer (1) ↔ Reservation (Many) | 1 to Many   | Customer: Partial, Reservation: Total | Customers may have zero or more reservations; each reservation belongs to one customer.  |
| **Table - Reservation**    | Table (1) ↔ Reservation (Many)    | 1 to Many   | Table: Partial, Reservation: Total    | Each table can have multiple reservations over time; each reservation is for one table.  |
| **Reservation - Order**    | Reservation (1) ↔ Order (Many)    | 1 to Many   | Reservation: Total, Order: Partial    | Each reservation can have multiple orders; each order is tied to one reservation.        |
| **Order - Order_Item**     | Order (1) ↔ Order_Item (Many)     | 1 to Many   | Order: Total, Order_Item: Partial     | Each order can have multiple order items; each order item belongs to one order.          |
| **Menu_Item - Order_Item** | Menu_Item (1) ↔ Order_Item (Many) | 1 to Many   | Menu_Item: Total, Order_Item: Partial | Each menu item can appear in many order items; each order item references one menu item. |


### Assumptions
Single Table per Reservation: Each reservation is linked to only one table for a specific date and time.

Menu Item Pricing: The price of a menu item can vary over time, so the price is stored with each order item to maintain historical accuracy.

Multiple Orders per Reservation: Customers can place multiple orders during a single reservation (e.g., appetizers first, then main course).


---

## Instructions for Students

1. Complete **all three scenarios** (A, B, C).  
2. Identify entities, relationships, and attributes for each.  
3. Draw ER diagrams using **draw.io / diagrams.net** or hand-drawn & scanned.  
4. Fill in all tables and assumptions for each scenario.  
5. Export the completed Markdown (with diagrams) as **a single PDF**
