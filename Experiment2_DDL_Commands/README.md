# Experiment 2: DDL Commands

## AIM
To study and implement DDL commands and different types of constraints.

## THEORY

### 1. CREATE
Used to create a new relation (table).

**Syntax:**
```sql
CREATE TABLE (
  field_1 data_type(size),
  field_2 data_type(size),
  ...
);
```
### 2. ALTER
Used to add, modify, drop, or rename fields in an existing relation.
(a) ADD
```sql
ALTER TABLE std ADD (Address CHAR(10));
```
(b) MODIFY
```sql
ALTER TABLE relation_name MODIFY (field_1 new_data_type(size));
```
(c) DROP
```sql
ALTER TABLE relation_name DROP COLUMN field_name;
```
(d) RENAME
```sql
ALTER TABLE relation_name RENAME COLUMN old_field_name TO new_field_name;
```
### 3. DROP TABLE
Used to permanently delete the structure and data of a table.
```sql
DROP TABLE relation_name;
```
### 4. RENAME
Used to rename an existing database object.
```sql
RENAME TABLE old_relation_name TO new_relation_name;
```
### CONSTRAINTS
Constraints are used to specify rules for the data in a table. If there is any violation between the constraint and the data action, the action is aborted by the constraint. It can be specified when the table is created (using CREATE TABLE) or after it is created (using ALTER TABLE).
### 1. NOT NULL
When a column is defined as NOT NULL, it becomes mandatory to enter a value in that column.
Syntax:
```sql
CREATE TABLE Table_Name (
  column_name data_type(size) NOT NULL
);
```
### 2. UNIQUE
Ensures that values in a column are unique.
Syntax:
```sql
CREATE TABLE Table_Name (
  column_name data_type(size) UNIQUE
);
```
### 3. CHECK
Specifies a condition that each row must satisfy.
Syntax:
```sql
CREATE TABLE Table_Name (
  column_name data_type(size) CHECK (logical_expression)
);
```
### 4. PRIMARY KEY
Used to uniquely identify each record in a table.
Properties:
Must contain unique values.
Cannot be null.
Should contain minimal fields.
Syntax:
```sql
CREATE TABLE Table_Name (
  column_name data_type(size) PRIMARY KEY
);
```
### 5. FOREIGN KEY
Used to reference the primary key of another table.
Syntax:
```sql
CREATE TABLE Table_Name (
  column_name data_type(size),
  FOREIGN KEY (column_name) REFERENCES other_table(column)
);
```
### 6. DEFAULT
Used to insert a default value into a column if no value is specified.

Syntax:
```sql
CREATE TABLE Table_Name (
  col_name1 data_type,
  col_name2 data_type,
  col_name3 data_type DEFAULT 'default_value'
);
```

**Question 1**
--
1.Create a table named Products with the following columns:

ProductID as INTEGER
ProductName as TEXT
Price as REAL
Stock as INTEGER
For example:

Test	Result
pragma table_info('Products');
cid   name        type        notnull     dflt_value  pk
----  ----------  ----------  ----------  ----------  ----------
0     ProductID   INTEGER     0                       0
1     ProductNam  TEXT        0                       0
2     Price       REAL        0                       0
3     Stock       INTEGER     0                       0

```sql


Create TABLE Products(
ProductID INTEGER,
ProductName TEXT,
Price REAL,
Stock INTEGER);
```

**Output:**

<img width="1300" height="294" alt="image" src="https://github.com/user-attachments/assets/95807ee8-5351-43fc-a0f5-8d90ac206940" />


**Question 2**
Create a table named Employees with the following constraints:

EmployeeID should be the primary key.
FirstName and LastName should be NOT NULL.
Email should be unique.
Salary should be greater than 0.
DepartmentID should be a foreign key referencing the Departments table.
For example:

Test	Result
-- Attempt to insert a record with NULL FirstName
INSERT INTO Employees (EmployeeID, FirstName, LastName, Email, Salary, DepartmentID)
VALUES (1, NULL, 'Doe', 'john.doe@example.com', 50000, 1);
Error: NOT NULL constraint failed: Employees.FirstName

```sql
CREATE TABLE Employees (
    EmployeeID INT PRIMARY KEY,
    FirstName NOT NULL,
    LastName NOT NULL,
    Email  UNIQUE,
    Salary DECIMAL(10, 2) CHECK (Salary > 0),
    DepartmentID INT,
    FOREIGN KEY (DepartmentID) REFERENCES Departments(DepartmentID)
);

```

**Output:**

<img width="1380" height="257" alt="image" src="https://github.com/user-attachments/assets/403c0591-982f-4d39-a4cc-cf3f4ec8c763" />


**Question 3**
---
Write a SQL query to Add a new column mobilenumber as number in the Student_details table.

Sample table: Student_details

 cid              name             type   notnull     dflt_value  pk
---------------  ---------------  -----  ----------  ----------  ----------
0                RollNo           int    0                       1
1                Name             VARCH  1                       0
2                Gender           TEXT   1                       0
3                Subject          VARCH  0                       0
4                MARKS            INT (  0                       0
For example:

Test	Result
pragma table_info('Student_details');
cid         name        type        notnull     dflt_value  pk
----------  ----------  ----------  ----------  ----------  ----------
0           RollNo      int         0                       1
1           Name        VARCHAR(10  1                       0
2           Gender      TEXT        1                       0
3           Subject     VARCHAR(30  0                       0
4           MARKS       INT (3)     0                       0
5           mobilenumb  number      0                       0


```sql
ALTER TABLE Student_details
ADD COLUMN mobilenumber number;
```

**Output:**

<img width="1662" height="352" alt="image" src="https://github.com/user-attachments/assets/83ee0827-694d-42a1-a805-e1917ea39c16" />


**Question 4**
---
Insert all products from Discontinued_products into Products.

Table attributes are ProductID, ProductName, Price, Stock

For example:

Test	Result
select * from Products;
ProductID   ProductName     Price       Stock
----------  --------------  ----------  ----------
101         Old Smartphone  199.99      0
102         Vintage Laptop  399.99      10
103         Classic Tablet  149.99      5

```sql
INSERT INTO Products
SELECT ProductID,ProductName,Price,Stock FROM Discontinued_products;
```

**Output:**

<img width="1188" height="282" alt="image" src="https://github.com/user-attachments/assets/22131989-7066-45e7-b35f-e1161544ccb4" />

**Question 5**
---
Insert the following products into the Products table:

Name        Category     Price       Stock
----------  -----------  ----------  ----------
Smartphone  Electronics  800         150
Headphones  Accessories  200         300
For example:

Test	Result
SELECT Name, Category, Price, Stock FROM Products;

Name        Category     Price       Stock
----------  -----------  ----------  ----------
Smartphone  Electronics  800         150
Headphones  Accessories  200         300

```sql
INSERT INTO Products(Name,Category,Price,Stock)
VALUES ('Smartphone','Electronics',800,150),
('Headphones','Accessories',200,300);
```

**Output:**

<img width="1661" height="444" alt="image" src="https://github.com/user-attachments/assets/84ce2961-9ff3-4688-be45-8656c521c53a" />


**Question 6**
---
Write a SQL query to add a column named Date_of_birth as Date in the Student_details table.

For example:

Test	Result
pragma table_info('Student_details');
cid    name             type             notnu  dflt_value  pk
-----  ---------------  ---------------  -----  ----------  ----------
0      RollNo           int              0                  1
1      Name             VARCHAR(100)     1                  0
2      Gender           TEXT             1                  0
3      Subject          VARCHAR(30)      0                  0
4      MARKS            INT (3)          0                  0
5      Date_of_birth    Date             0                  0


```sql
ALTER TABLE Student_details
ADD COLUMN Date_of_birth Date;
```

**Output:**

<img width="1387" height="323" alt="image" src="https://github.com/user-attachments/assets/a0c6c9df-a87e-47f3-940f-8f22814c45d0" />


**Question 7**
---
Create a new table named contacts with the following specifications:
contact_id as INTEGER and primary key.
first_name as TEXT and not NULL.
last_name as TEXT and not NULL.
email as TEXT.
phone as TEXT and not NULL with a check constraint to ensure the length of phone is at least 10 characters.
For example:

Test	Result
INSERT INTO contacts (contact_id, first_name, last_name, email, phone) VALUES (1, 'John', 'Doe', 'john.doe@example.com', '1234567890');
SELECT * FROM contacts;
contact_id  first_name  last_name   email                 phone
----------  ----------  ----------  --------------------  ----------
1           John        Doe         john.doe@example.com  1234567890


```sql
CREATE TABLE contacts(
contact_id INTEGER PRIMARY KEY,
first_name TEXT NOT NULL,
last_name  TEXT NOT NULL,
email TEXT,
phone TEXT NOT NULL CHECK(LENGTH(phone)>=10));
```

**Output:**

<img width="1471" height="217" alt="image" src="https://github.com/user-attachments/assets/7c33b00e-6138-458e-9a1c-70d6f262eed5" />

**Question 8**
---
Create a table named Bonuses with the following constraints:
BonusID as INTEGER should be the primary key.
EmployeeID as INTEGER should be a foreign key referencing Employees(EmployeeID).
BonusAmount as REAL should be greater than 0.
BonusDate as DATE.
Reason as TEXT should not be NULL.
For example:

Test	Result
INSERT INTO Bonuses (BonusID, EmployeeID, BonusAmount, BonusDate, Reason) VALUES (1, 6, 1000.0, '2024-08-01', 'Outstanding performance');
SELECT * FROM Bonuses;
BonusID     EmployeeID  BonusAmount  BonusDate   Reason
----------  ----------  -----------  ----------  -----------------------
1           6           1000.0       2024-08-01  Outstanding performance


```sql
CREATE TABLE Bonuses (
    BonusID INTEGER PRIMARY KEY,
    EmployeeID INTEGER,
    BonusAmount REAL CHECK (BonusAmount > 0),
    BonusDate DATE,
    Reason TEXT NOT NULL,
    FOREIGN KEY (EmployeeID) REFERENCES Employees(EmployeeID)
);
```

**Output:**

<img width="1502" height="213" alt="image" src="https://github.com/user-attachments/assets/6b02a481-11c4-41e4-b878-33a90a21be7e" />


**Question 9**
---
Create a table named Shipments with the following constraints:
ShipmentID as INTEGER should be the primary key.
ShipmentDate as DATE.
SupplierID as INTEGER should be a foreign key referencing Suppliers(SupplierID).
OrderID as INTEGER should be a foreign key referencing Orders(OrderID).
For example:

Test	Result
INSERT INTO Shipments (ShipmentID, ShipmentDate, SupplierID, OrderID) VALUES (2, '2024-08-03', 99, 1);
Error: FOREIGN KEY constraint failed


```sql
CREATE TABLE Shipments(
ShipmentID INTEGER PRIMARY KEY,
ShipmentDate DATE,
SupplierID INTEGER,
OrderID INTEGER,
FOREIGN KEY(SupplierID)REFERENCES Suppliers(SupplierID),
FOREIGN KEY(OrderID)REFERENCES Orders(OrderID)
);
```

**Output:**
<img width="1177" height="168" alt="image" src="https://github.com/user-attachments/assets/5667fffb-a4d0-4643-9ee5-0c392398a05d" />



**Question 10**
---
Insert a book with ISBN 978-1234567890, Title Data Science Essentials, Author Jane Doe, Publisher TechBooks, and Year 2024 into the Books table.

For example:

Test	Result
SELECT * FROM Books;
ISBN            Title                    Author      Publisher   Year
--------------  -----------------------  ----------  ----------  ----------
978-1234567890  Data Science Essentials  Jane Doe    TechBooks   2024


```sql
INSERT INTO Books(ISBN,Title,Author,Publisher,Year)
VALUES ('978-1234567890','Data Science Essentials','Jane Doe','TechBooks',2024);
```

**Output:**
<img width="1387" height="169" alt="image" src="https://github.com/user-attachments/assets/c35a87fe-1aec-4298-abc7-6e7d996d8d5f" />



## RESULT
Thus, the SQL queries to implement different types of constraints and DDL commands have been executed successfully.
