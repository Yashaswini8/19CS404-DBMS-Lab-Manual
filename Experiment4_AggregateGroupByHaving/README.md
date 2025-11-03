# Experiment 4: Aggregate Functions, Group By and Having Clause

## AIM
To study and implement aggregate functions, GROUP BY, and HAVING clause with suitable examples.

## THEORY

### Aggregate Functions
These perform calculations on a set of values and return a single value.

- **MIN()** – Smallest value  
- **MAX()** – Largest value  
- **COUNT()** – Number of rows  
- **SUM()** – Total of values  
- **AVG()** – Average of values

**Syntax:**
```sql
SELECT AGG_FUNC(column_name) FROM table_name WHERE condition;
```
### GROUP BY
Groups records with the same values in specified columns.
**Syntax:**
```sql
SELECT column_name, AGG_FUNC(column_name)
FROM table_name
GROUP BY column_name;
```
### HAVING
Filters the grouped records based on aggregate conditions.
**Syntax:**
```sql
SELECT column_name, AGG_FUNC(column_name)
FROM table_name
GROUP BY column_name
HAVING condition;
```

**Question 1**
--
What is the most common time slot for appointments for each doctor?

Sample table:Appointments Table



For example:

Result
DoctorID    TimeSlot    TotalAppointments
----------  ----------  -----------------
3           11:00       3
1           09:00       2
9           11:30       2
6           16:00       1
7           09:30       1
8           10:00       1


```sql
WITH AppointmentCounts AS (
    SELECT
        DoctorID,
        TimeSlot,
        COUNT(*) AS TotalAppointments
    FROM
        Appointments
    GROUP BY
        DoctorID,
        TimeSlot
)
SELECT
    DoctorID,
    TimeSlot,
    TotalAppointments
FROM
    AppointmentCounts a
WHERE
    TotalAppointments = (
        SELECT MAX(TotalAppointments)
        FROM AppointmentCounts
        WHERE DoctorID = a.DoctorID
    )
ORDER BY
    DoctorID;
```

**Output:**

<img width="1231" height="677" alt="image" src="https://github.com/user-attachments/assets/e797e2f3-b4b1-461d-9eb8-867d4646cd05" />


**Question 2**
---
How many prescriptions were written for each medication?

Sample tablePrescriptions Table



For example:

Result
Medication     TotalPrescriptions
-------------  ------------------
Ciprofloxacin  1
Doxorubicin    1
Ibuprofen      1
Levothyroxine  1
Lisinopril     1
MMR            1
Pending        1
Prenatal vita  1
Sertraline     1

```sql
SELECT
    Medication,
    COUNT(*) AS TotalPrescriptions
FROM
    Prescriptions
GROUP BY
    Medication
ORDER BY
    Medication;
```

**Output:**

<img width="1278" height="838" alt="image" src="https://github.com/user-attachments/assets/d86a8d78-2257-4517-be65-c75f47a4a8f6" />


**Question 3**

How many patients have insurance coverage valid in each year?

Sample table:Insurance Table

name               type
-----------------  ----------
InsuranceID        INTEGER
PatientID          INTEGER
InsuranceCompany   TEXT
PolicyNumber       TEXT
PolicyHolder       TEXT
ValidityPeriod     TEXT
For example:

Result
ValidityYear  TotalPatients
------------  -------------
2024          3
2025          1
2027          4
2031          2
Answer:(penalty regime: 0 %)How many patients have insurance coverage valid in each year?

Sample table:Insurance Table

name               type
-----------------  ----------
InsuranceID        INTEGER
PatientID          INTEGER
InsuranceCompany   TEXT
PolicyNumber       TEXT
PolicyHolder       TEXT
ValidityPeriod     TEXT
For example:

Result
ValidityYear  TotalPatients
------------  -------------
2024          3
2025          1
2027          4
2031          2
Answer:(penalty regime: 0 %)

```sql
SELECT
    CAST(SUBSTR(ValidityPeriod, 1, 4) AS INTEGER) AS ValidityYear,
    COUNT(DISTINCT PatientID) AS TotalPatients
FROM
    Insurance
GROUP BY
    CAST(SUBSTR(ValidityPeriod, 1, 4) AS INTEGER)
ORDER BY
    ValidityYear;
```

**Output:**

<img width="854" height="501" alt="image" src="https://github.com/user-attachments/assets/29b7caa5-2146-4d5e-a9e7-1c3ef29429cc" />


**Question 4**
---
Write a SQL query to find the minimum purchase amount.

Sample table: orders

ord_no      purch_amt   ord_date    customer_id  salesman_id

----------  ----------  ----------  -----------  -----------

70001       150.5       2012-10-05  3005         5002

70009       270.65      2012-09-10  3001         5005

70002       65.26       2012-10-05  3002         5001

 

For example:

Result
MINIMUM
----------
65.26


```sql
SELECT 
    MIN(purch_amt) AS MINIMUM
FROM 
    orders;
```

**Output:**

<img width="863" height="440" alt="image" src="https://github.com/user-attachments/assets/9a6d1079-0d82-4fc2-990d-0980e9440ab2" />


**Question 5**
---
Write a SQL query to find  how many employees work in California?

Table: employee

name        type
----------  ----------
id          INTEGER
name        TEXT
age         INTEGER
city        TEXT
income      INTEGER
 

For example:

Result
employees_in_california
-----------------------
2


```sql
**SELECT 
    COUNT(*) AS employees_in_california
FROM 
    employee
WHERE 
    city = 'California';**
```

**Output:**

<img width="863" height="442" alt="image" src="https://github.com/user-attachments/assets/b3b416a1-c166-4d19-8626-9559f1652ffc" />


**Question 6**
---

Write a SQL query to find the customer with longest name?

Table: customer

name        type
----------  ----------
id          INTEGER
name        TEXT
city        TEXT
email       TEXT
phone       INTEGER
For example:

Result
name          length
------------  ----------
Preeti Patel  12

```sql
SELECT 
    name, 
    LENGTH(name) AS length
FROM 
    customer
ORDER BY 
    LENGTH(name) DESC
LIMIT 1;
```

**Output:**

<img width="835" height="432" alt="image" src="https://github.com/user-attachments/assets/553b5818-1cda-48ce-a7d4-9d722ee849f0" />


**Question 7**
---
Write a SQL query to  find the average salary of all employees?

Table: employee

name        type
----------  ----------
id          INTEGER
name        TEXT
age         INTEGER
city        TEXT
income      INTEGER
 

For example:

Result
Average_Salary
--------------
1568750.0

```sql
SELECT 
    AVG(income) AS Average_Salary
FROM 
    employee;
```

**Output:**

<img width="844" height="436" alt="image" src="https://github.com/user-attachments/assets/427d1609-96dc-4209-b821-66f52d651deb" />


**Question 8**
---
Write the SQL query that achieves the grouping of data by age intervals using the expression (age/5)5, calculates the average age for each group, and excludes groups where the average age is not less than 24.

Sample table: customer1



For example:

Result
age_group   AVG(age)
----------  ----------
20          23.0


```sql
SELECT
  FLOOR(age / 5) * 5 AS age_group,
  AVG(age) AS avg_age
FROM
  customeri
GROUP BY
  FLOOR(age / 5) * 5
HAVING
  AVG(age) < 24;
```

**Output:**

<img width="852" height="754" alt="image" src="https://github.com/user-attachments/assets/df938d26-274d-488f-8c66-97bf6a8173a2" />


**Question 9**
---
Write the SQL query that achieves the grouping of data by occupation, calculates the minimum work hours for each occupation, and excludes occupations where the minimum work hour is not greater than 8.

Sample table: employee1



For example:

Result
occupation  MIN(workhour)
----------  -------------
Business    10
Doctor      15
Engineer    12
Teacher     9


```sql
SELECT occupation, MIN(workhour)
FROM employee1
GROUP BY occupation
HAVING MIN(workhour) > 8;
```

**Output:**

<img width="859" height="617" alt="image" src="https://github.com/user-attachments/assets/7bcb9222-2389-45d2-a234-16ba936adfc2" />


**Question 10**
---
Write the SQL query that achieves the selection of product names and the maximum price for each category from the "products" table, and includes only those products where the maximum price is greater than 15.

Sample table: products



For example:

Result
category_id  product_name  Price
-----------  ------------  ----------
1            Orange        15.5
2            Monitor       25


```sql
SELECT p.category_id, p.product_name, p.price AS Price
FROM products p
WHERE p.price = (
    SELECT MAX(price)
    FROM products
    WHERE category_id = p.category_id
)
AND p.price > 15;
```

**Output:**

<img width="848" height="511" alt="image" src="https://github.com/user-attachments/assets/01586c5d-62d0-4eb0-9943-64d76c673cf3" />



## RESULT
Thus, the SQL queries to implement aggregate functions, GROUP BY, and HAVING clause have been executed successfully.
