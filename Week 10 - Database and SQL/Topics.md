# 🗄️ SQL WEEK — DATABASE & SQL FUNDAMENTALS

> **Goal:** Build a strong foundation in Database concepts and SQL before moving into Advanced SQL.

---

# 📚 PART 1 — DATABASE FUNDAMENTALS

## 1. What is a Database?

### Definition

A **database** is an organized collection of data that can be stored, accessed, managed, and updated efficiently.

### Example

A college database may contain:

```text
Students
Teachers
Courses
Departments
Marks
```

---

## 2. Database vs File System

### File System

Data is stored in separate files such as:

```text
students.txt
employees.csv
orders.xlsx
```

### Problems with File Systems

* Data duplication
* Difficult data searching
* Difficult relationships
* Poor security
* Difficult concurrent access
* Data inconsistency

### Database

A database provides:

* Structured data storage
* Faster searching
* Relationships
* Security
* Concurrency control
* Backup and recovery
* Data integrity

---

## 3. DBMS

### Definition

**DBMS (Database Management System)** is software used to create, store, manage, retrieve, and control data in databases.

### Examples

* PostgreSQL
* MySQL
* Oracle Database
* Microsoft SQL Server

### Responsibilities of DBMS

* Store data
* Retrieve data
* Update data
* Delete data
* Manage users
* Provide security
* Maintain data integrity
* Handle transactions
* Manage concurrent users
* Backup and recovery

---

# 4. DBMS vs RDBMS

| DBMS                                     | RDBMS                                          |
| ---------------------------------------- | ---------------------------------------------- |
| General database management system       | Relational database management system          |
| May not use tables/relationships         | Uses tables and relationships                  |
| Relationships may not be enforced        | Relationships are commonly enforced using keys |
| Example: some document/key-value systems | PostgreSQL, MySQL, Oracle                      |

### Simple Explanation

> **RDBMS is a type of DBMS that stores data using related tables.**

---

# 5. SQL vs NoSQL

## SQL

SQL databases are generally relational and store data in tables.

Examples:

* PostgreSQL
* MySQL
* Oracle

Good for:

* Structured data
* Complex relationships
* Transactions
* Financial systems
* ERP systems

## NoSQL

NoSQL databases use models such as:

* Document
* Key-value
* Wide-column
* Graph

Examples:

* MongoDB
* Redis
* Cassandra
* Neo4j

Good for:

* Flexible data structures
* Very large-scale distributed systems
* Rapidly changing schemas
* Certain high-throughput workloads

### Simple Difference

> **SQL → structured, relational data**
>
> **NoSQL → flexible, non-relational data models**

---

# 6. Database Terminology

## Database

Container for organized data.

## Table

Stores related data in rows and columns.

## Row

One complete record.

## Column

One attribute/field of the data.

### Example

```text
employees

id | name | salary
---|------|-------
1  | John | 50000
2  | Sara | 60000
```

Here:

```text
Database → CompanyDB
Table    → employees
Row      → 1, John, 50000
Column   → name
```

---

# 7. Entity

### Definition

An **entity** is a real-world object or concept about which we store data.

Examples:

```text
Student
Employee
Customer
Product
Order
Department
```

---

# 8. Attribute

### Definition

An **attribute** describes an entity.

Example:

```text
Student
│
├── student_id
├── name
├── email
└── age
```

Here:

* Student → Entity
* name → Attribute
* email → Attribute

---

# 9. Relationships

A relationship describes how entities are connected.

## One-to-One (1:1)

One record is related to one record.

Example:

```text
Person ─── Passport
```

One person has one passport.

---

## One-to-Many (1:M)

One record can have many related records.

Example:

```text
Department
    │
    ├── Employee
    ├── Employee
    └── Employee
```

One department can have many employees.

---

## Many-to-Many (M:M)

Many records can be related to many records.

Example:

```text
Students ←→ Courses
```

A student can take many courses.

A course can have many students.

Usually implemented using a junction table:

```text
students
courses
enrollments
```

---

# 10. ER Diagram

### Definition

An **ER Diagram (Entity Relationship Diagram)** visually represents:

* Entities
* Attributes
* Relationships

Example:

```text
DEPARTMENT
    │
    │ 1:M
    ↓
EMPLOYEE
```

Many-to-many:

```text
STUDENT
   │
   │ M:M
   ↓
ENROLLMENT
   ↑
   │
COURSE
```

### Practical

Draw ER diagrams for:

* College Management System
* E-commerce System
* Banking System

---

# 11. Three Schema Architecture

Three levels of database architecture:

```text
External Schema
      ↓
Conceptual Schema
      ↓
Internal Schema
```

## External Schema

What a particular user/application sees.

Example:

A student sees:

```text
Name
Course
Marks
```

The administrator may see more information.

---

## Conceptual Schema

The overall logical structure of the database.

Example:

```text
Students
Courses
Teachers
Departments
```

---

## Internal Schema

How data is physically stored.

Example:

* Files
* Storage pages
* Indexes
* Physical storage structures

### Simple Memory Trick

```text
External   → User View
Conceptual → Logical Structure
Internal   → Physical Storage
```

---

# 🔑 PART 2 — DATABASE KEYS

# 12. Primary Key

Uniquely identifies each row.

```sql
id INT PRIMARY KEY
```

Properties:

* Unique
* Cannot be NULL

Example:

```text
student_id
-----------
1
2
3
```

---

# 13. Foreign Key

Connects one table to another table.

Example:

```sql
FOREIGN KEY (dept_id)
REFERENCES departments(dept_id)
```

Purpose:

> Maintains a relationship between tables and helps enforce referential integrity.

---

# 14. Unique Key

Ensures values are not duplicated.

```sql
email VARCHAR(100) UNIQUE
```

Example:

```text
abc@gmail.com
xyz@gmail.com
```

Two rows cannot have the same email.

---

# 15. Candidate Key

A column or combination of columns that **can uniquely identify a row**.

Example:

```text
student_id
email
```

Both may uniquely identify a student.

One can be selected as the Primary Key.

---

# 16. Super Key

Any column or combination of columns that uniquely identifies a row.

Example:

```text
student_id
student_id + name
student_id + email
```

---

# 17. Alternate Key

A candidate key that was **not selected as the Primary Key**.

Example:

```text
student_id → Primary Key
email      → Alternate Key
```

---

# 18. Composite Key

A key made using multiple columns.

Example:

```sql
PRIMARY KEY (student_id, course_id)
```

Useful for junction tables.

Example:

```text
enrollments

student_id | course_id
-----------|----------
1          | 101
1          | 102
2          | 101
```

---

# 19. Natural Key vs Surrogate Key

## Natural Key

A real-world value used as an identifier.

Example:

```text
email
phone_number
passport_number
```

## Surrogate Key

Artificially generated identifier.

Example:

```text
id = 1
id = 2
id = 3
```

Common examples:

```text
SERIAL
BIGSERIAL
UUID
```

---

# 🔒 PART 3 — CONSTRAINTS

A **constraint** is a rule applied to data.

## 20. NOT NULL

Value cannot be NULL.

```sql
name VARCHAR(50) NOT NULL
```

---

## 21. UNIQUE

Prevents duplicate values.

```sql
email VARCHAR(100) UNIQUE
```

---

## 22. PRIMARY KEY

Uniquely identifies a row.

```sql
id INT PRIMARY KEY
```

---

## 23. FOREIGN KEY

Creates a relationship between tables.

```sql
FOREIGN KEY (dept_id)
REFERENCES departments(dept_id)
```

---

## 24. CHECK

Ensures a condition is true.

```sql
salary DECIMAL(10,2)
CHECK (salary > 0)
```

---

## 25. DEFAULT

Provides a default value.

```sql
city VARCHAR(50) DEFAULT 'Kozhikode'
```

---

# 💻 PART 4 — SQL COMMAND CATEGORIES

## 26. DDL — Data Definition Language

Used to define or change database structure.

```text
CREATE
ALTER
DROP
TRUNCATE
RENAME
```

---

## 27. DML — Data Manipulation Language

Used to modify data.

```text
INSERT
UPDATE
DELETE
```

---

## 28. DQL — Data Query Language

Used to retrieve data.

```text
SELECT
```

---

## 29. DCL — Data Control Language

Used for permissions.

```text
GRANT
REVOKE
```

---

## 30. TCL — Transaction Control Language

Used to manage transactions.

```text
COMMIT
ROLLBACK
SAVEPOINT
```

---

# 🔄 PART 5 — CRUD

CRUD means:

```text
C → Create
R → Read
U → Update
D → Delete
```

## Create

```sql
INSERT INTO employees
VALUES (1, 'John', 50000);
```

## Read

```sql
SELECT * FROM employees;
```

## Update

```sql
UPDATE employees
SET salary = 55000
WHERE id = 1;
```

## Delete

```sql
DELETE FROM employees
WHERE id = 1;
```

---

# 🏗️ PART 6 — DDL PRACTICALS

## Create Table

```sql
CREATE TABLE employees (
    id INT PRIMARY KEY,
    name VARCHAR(50),
    salary DECIMAL(10,2)
);
```

## Add Column

```sql
ALTER TABLE employees
ADD COLUMN email VARCHAR(100);
```

## Rename Table

```sql
ALTER TABLE employees
RENAME TO staff;
```

## Rename Column

```sql
ALTER TABLE employees
RENAME COLUMN name TO employee_name;
```

## Change Data Type

```sql
ALTER TABLE employees
ALTER COLUMN salary TYPE NUMERIC(10,2);
```

## Drop Column

```sql
ALTER TABLE employees
DROP COLUMN email;
```

## Truncate

```sql
TRUNCATE TABLE employees;
```

## Drop Table

```sql
DROP TABLE employees;
```

### Important

```text
DELETE    → Removes rows
TRUNCATE  → Removes all rows
DROP      → Removes table structure
```

---

# 🔎 PART 7 — SELECT & FILTERING

## SELECT

```sql
SELECT * FROM employees;
```

Specific columns:

```sql
SELECT name, salary
FROM employees;
```

---

## WHERE

```sql
SELECT *
FROM employees
WHERE salary > 50000;
```

---

## AND

```sql
SELECT *
FROM employees
WHERE salary > 50000
AND city = 'Kozhikode';
```

---

## OR

```sql
SELECT *
FROM employees
WHERE city = 'Kozhikode'
OR city = 'Kochi';
```

---

## IN

```sql
SELECT *
FROM employees
WHERE city IN ('Kozhikode', 'Kochi');
```

---

## BETWEEN

```sql
SELECT *
FROM employees
WHERE salary BETWEEN 30000 AND 60000;
```

`BETWEEN` is inclusive.

---

## LIKE

```sql
SELECT *
FROM employees
WHERE name LIKE 'A%';
```

Examples:

```text
'A%' → starts with A
'%A' → ends with A
'%A%' → contains A
```

---

## NULL

```sql
SELECT *
FROM employees
WHERE email IS NULL;
```

Do not use:

```sql
email = NULL
```

Use:

```sql
IS NULL
IS NOT NULL
```

---

# ↕️ PART 8 — SORTING & LIMITING

## ORDER BY

Ascending:

```sql
SELECT *
FROM employees
ORDER BY salary ASC;
```

Descending:

```sql
SELECT *
FROM employees
ORDER BY salary DESC;
```

---

## LIMIT

```sql
SELECT *
FROM employees
ORDER BY salary DESC
LIMIT 5;
```

Finds the top 5 highest-paid employees.

---

## DISTINCT

```sql
SELECT DISTINCT city
FROM employees;
```

Returns unique cities.

---

# 📊 PART 9 — AGGREGATE FUNCTIONS

## COUNT

```sql
SELECT COUNT(*)
FROM employees;
```

## SUM

```sql
SELECT SUM(salary)
FROM employees;
```

## AVG

```sql
SELECT AVG(salary)
FROM employees;
```

## MIN

```sql
SELECT MIN(salary)
FROM employees;
```

## MAX

```sql
SELECT MAX(salary)
FROM employees;
```

---

# 10. GROUP BY

Groups rows based on a column.

```sql
SELECT dept_id, COUNT(*)
FROM employees
GROUP BY dept_id;
```

---

# 11. HAVING

Filters groups.

```sql
SELECT dept_id, AVG(salary)
FROM employees
GROUP BY dept_id
HAVING AVG(salary) > 50000;
```

### Remember

```text
WHERE  → filters rows
HAVING → filters groups
```

---

# 🔗 PART 10 — RELATIONSHIPS & JOINS

## One-to-One

```text
Person → Passport
```

## One-to-Many

```text
Department → Employees
```

## Many-to-Many

```text
Students ←→ Courses
```

Implemented with:

```text
Students
Courses
Enrollments
```

---

# 12. INNER JOIN

Returns matching records from both tables.

```sql
SELECT e.name, d.dept_name
FROM employees e
INNER JOIN departments d
ON e.dept_id = d.dept_id;
```

---

# 13. LEFT JOIN

Returns all rows from the left table and matching rows from the right.

```sql
SELECT c.customer_name, o.order_id
FROM customers c
LEFT JOIN orders o
ON c.customer_id = o.customer_id;
```

Useful for:

> Finding customers who have no orders.

---

# 14. RIGHT JOIN

Returns all rows from the right table and matching rows from the left.

```sql
SELECT c.customer_name, o.order_id
FROM customers c
RIGHT JOIN orders o
ON c.customer_id = o.customer_id;
```

---

# 15. FULL OUTER JOIN

Returns matching and non-matching rows from both tables.

```sql
SELECT *
FROM customers c
FULL OUTER JOIN orders o
ON c.customer_id = o.customer_id;
```

---

# 🧹 PART 11 — NORMALIZATION

## Why Normalize?

Normalization reduces:

* Data duplication
* Data redundancy
* Update problems
* Insert problems
* Delete problems

---

## 1NF — First Normal Form

Requirements:

* Atomic values
* No repeating groups

Bad:

```text
student_id | courses
-----------|----------------
1          | SQL, Python
```

Better:

```text
student_id | course
-----------|--------
1          | SQL
1          | Python
```

---

## 2NF — Second Normal Form

Must:

* Be in 1NF
* Have no partial dependency on a composite key

---

## 3NF — Third Normal Form

Must:

* Be in 2NF
* Have no transitive dependency

### Simple idea

```text
A → B
B → C

Therefore A → C
```

This creates transitive dependency.

---

# 💳 PART 12 — TRANSACTIONS

## What is a Transaction?

A transaction is a group of database operations treated as one logical unit.

Example:

```text
Transfer ₹1000

Account A → -₹1000
Account B → +₹1000
```

Both operations should succeed together.

---

# ACID Properties

## A — Atomicity

All operations happen or none happen.

> All or nothing.

## C — Consistency

Database remains valid before and after the transaction.

## I — Isolation

Concurrent transactions should not incorrectly interfere with each other.

## D — Durability

Once committed, changes remain saved even after failure.

---

# Transaction Commands

## COMMIT

Saves changes.

```sql
COMMIT;
```

## ROLLBACK

Undoes uncommitted changes.

```sql
ROLLBACK;
```

## SAVEPOINT

Creates a point that you can roll back to.

```sql
SAVEPOINT point1;
```

---

# 📇 PART 13 — BASIC INDEXING

## What is an Index?

An index is a database structure that helps the database find rows more efficiently.

Example:

```sql
CREATE INDEX idx_employee_name
ON employees(name);
```

### Without Index

Database may need to scan many rows.

### With Index

Database can often locate matching rows more efficiently.

### Advantages

* Faster searches
* Faster filtering
* Can improve sorting/join performance in suitable queries

### Disadvantages

* Uses storage
* Inserts/updates/deletes may become more expensive
* Too many indexes can hurt performance

### Basic Rule

> Don't create indexes blindly. Create them where they provide useful query performance benefits.

---

# 🧪 PRACTICAL WORK

# Practical 1 — Create Database

```sql
CREATE DATABASE company_db;
```

---

# Practical 2 — Create Tables

Create:

```text
departments
employees
customers
products
orders
```

---

# Practical 3 — Add Constraints

Practice:

```text
PRIMARY KEY
FOREIGN KEY
UNIQUE
NOT NULL
CHECK
DEFAULT
```

---

# Practical 4 — Insert Data

Practice:

* [ ] Insert one row
* [ ] Insert multiple rows
* [ ] Batch insert

---

# Practical 5 — CRUD

Practice:

* [ ] INSERT
* [ ] SELECT
* [ ] UPDATE
* [ ] DELETE

---

# Practical 6 — Table Modification

Practice:

* [ ] Add column
* [ ] Drop column
* [ ] Rename table
* [ ] Rename column
* [ ] Modify data type
* [ ] Add constraint
* [ ] Drop constraint

---

# Practical 7 — Filtering

Write queries to:

* [ ] Find employees with salary > 50,000
* [ ] Find employees from a specific city
* [ ] Find employees between two salary values
* [ ] Find employees whose names start with A
* [ ] Find employees whose names end with N
* [ ] Find employees from multiple cities
* [ ] Find employees with NULL values
* [ ] Sort employees by salary
* [ ] Find top 5 salaries
* [ ] Find unique cities

---

# Practical 8 — Aggregation

Write queries to:

* [ ] Count employees
* [ ] Calculate total salary
* [ ] Calculate average salary
* [ ] Find highest salary
* [ ] Find lowest salary
* [ ] Count employees per department
* [ ] Find average salary per department
* [ ] Find departments with average salary > 50,000

---

# Practical 9 — Relationships

Create:

```text
students
courses
enrollments
```

Practice:

* [ ] One-to-Many relationship
* [ ] Many-to-Many relationship
* [ ] Foreign Keys
* [ ] Composite Key

---

# Practical 10 — JOINs

Using:

```text
customers
orders
products
```

Practice:

* [ ] INNER JOIN
* [ ] LEFT JOIN
* [ ] RIGHT JOIN
* [ ] FULL OUTER JOIN
* [ ] Customer + Orders
* [ ] Orders + Products
* [ ] Customer + Orders + Products
* [ ] Customers without orders
* [ ] Products without orders

---

# Practical 11 — Normalization

Take an unnormalized table:

```text
student_id
student_name
course1
course2
course3
teacher_name
teacher_phone
```

Convert it into:

```text
students
courses
teachers
enrollments
```

Identify:

* [ ] Repeating groups
* [ ] Duplicate data
* [ ] Partial dependency
* [ ] Transitive dependency
* [ ] 1NF
* [ ] 2NF
* [ ] 3NF

---

# Practical 12 — Transactions

Create a simple banking example.

Practice:

* [ ] BEGIN transaction
* [ ] Update Account A
* [ ] Update Account B
* [ ] COMMIT
* [ ] ROLLBACK
* [ ] SAVEPOINT

Example:

```sql
BEGIN;

UPDATE accounts
SET balance = balance - 1000
WHERE account_id = 1;

UPDATE accounts
SET balance = balance + 1000
WHERE account_id = 2;

COMMIT;
```

---

# Practical 13 — Index

Create:

```sql
CREATE INDEX idx_employee_name
ON employees(name);
```

Practice:

* [ ] Create index
* [ ] Check indexes
* [ ] Drop index
* [ ] Understand why the index is useful

---

# 🎯 PRACTICAL REVIEW QUESTIONS

Before finishing the week, you should be able to solve these without copying:

### Basic

* [ ] Create a database
* [ ] Create tables
* [ ] Add constraints
* [ ] Insert multiple records
* [ ] Update records
* [ ] Delete records
* [ ] Rename table
* [ ] Rename column
* [ ] Add column
* [ ] Drop column
* [ ] Change column datatype

### Querying

* [ ] Find highest salary
* [ ] Find lowest salary
* [ ] Find employees above a salary
* [ ] Find employees between salaries
* [ ] Find employees by name pattern
* [ ] Find unique departments
* [ ] Sort employees
* [ ] Limit results

### Aggregation

* [ ] Count employees
* [ ] Calculate total salary
* [ ] Calculate average salary
* [ ] Group employees by department
* [ ] Filter groups using HAVING

### JOINs

* [ ] INNER JOIN
* [ ] LEFT JOIN
* [ ] RIGHT JOIN
* [ ] FULL JOIN
* [ ] Find records with no match

### Database Design

* [ ] Identify entities
* [ ] Identify attributes
* [ ] Identify relationships
* [ ] Create ER diagram
* [ ] Choose Primary Keys
* [ ] Choose Foreign Keys
* [ ] Normalize a simple database

### Transactions

* [ ] Explain ACID
* [ ] Use COMMIT
* [ ] Use ROLLBACK
* [ ] Use SAVEPOINT

---

# 🧠 FINAL MEMORY MAP

```text
DATABASE
   ↓
DBMS / RDBMS
   ↓
TABLES
   ↓
ENTITIES + ATTRIBUTES
   ↓
RELATIONSHIPS
   ↓
PRIMARY KEY + FOREIGN KEY
   ↓
CONSTRAINTS
   ↓
SQL
   ↓
DDL / DML / DQL / DCL / TCL
   ↓
CRUD
   ↓
SELECT + WHERE
   ↓
ORDER BY + LIMIT + DISTINCT
   ↓
AGGREGATE FUNCTIONS
   ↓
GROUP BY + HAVING
   ↓
JOINS
   ↓
NORMALIZATION
   ↓
TRANSACTIONS + ACID
   ↓
BASIC INDEXING
```

---

# 🚫 ADVANCED SQL — SAVE FOR LATER

Do **not** make these your main focus this week:

* CTE
* Recursive CTE
* Window Functions
* Stored Procedures
* Advanced Functions
* Triggers
* Cursors
* Materialized Views
* Advanced Index Types
* Query Optimization
* EXPLAIN ANALYZE
* MVCC Internals
* Sharding
* CAP Theorem
* Advanced Subqueries
* PostgreSQL Table Inheritance
* Advanced PostgreSQL features

These can be studied after your **Database + SQL fundamentals are strong**.

---

# ✅ WEEK COMPLETION CHECKLIST

## Theory

* [ ] Database vs File System
* [ ] DBMS
* [ ] DBMS vs RDBMS
* [ ] SQL vs NoSQL
* [ ] Database terminology
* [ ] Entities
* [ ] Attributes
* [ ] Relationships
* [ ] ER Diagram
* [ ] Three Schema Architecture
* [ ] Keys
* [ ] Constraints
* [ ] SQL command categories
* [ ] CRUD
* [ ] SELECT and filtering
* [ ] Aggregate functions
* [ ] GROUP BY / HAVING
* [ ] JOINs
* [ ] Normalization
* [ ] Transactions
* [ ] ACID
* [ ] Basic Indexing

## Practical

* [ ] Create database
* [ ] Create tables
* [ ] Create relationships
* [ ] Add constraints
* [ ] Insert data
* [ ] Read data
* [ ] Update data
* [ ] Delete data
* [ ] Modify tables
* [ ] Filtering queries
* [ ] Aggregate queries
* [ ] GROUP BY / HAVING
* [ ] JOIN queries
* [ ] Normalize a table
* [ ] Transaction with COMMIT
* [ ] Transaction with ROLLBACK
* [ ] SAVEPOINT
* [ ] Create an index

# 🏆 End Goal

By the end of this week, you should be able to:

> **Design a basic relational database, create tables with proper keys and constraints, insert and manage data, write SQL queries, use aggregate functions, connect tables using JOINs, understand normalization, and perform basic transactions and indexing.**

**Once these fundamentals are strong → move to Advanced SQL.**
