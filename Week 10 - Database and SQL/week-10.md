Absolutely. Here is the **final complete SQL + DBMS summary**, including the topics we identified as missing earlier.

# SQL & DBMS — Final Complete Summary

## 1. Database Fundamentals

### Database

An organized collection of data that can be stored, managed, retrieved, and updated efficiently.

### Data

Raw facts or values.

### DBMS

**Database Management System** — software used to create, store, manage, retrieve, update, and control databases.

Examples:

* PostgreSQL
* MySQL
* Oracle
* SQL Server

### RDBMS

**Relational Database Management System** — stores data in tables and establishes relationships between tables.

Examples:

* PostgreSQL
* MySQL
* Oracle
* SQL Server

### DBMS vs RDBMS

| DBMS                                   | RDBMS                          |
| -------------------------------------- | ------------------------------ |
| General database management            | Relational database management |
| May use different data models          | Uses tables                    |
| Relationships may not be central       | Relationships are central      |
| Constraint/relationship support varies | Strong keys and constraints    |

---

## 2. SQL

**SQL — Structured Query Language**

Used to communicate with relational databases.

```sql
SELECT * FROM Students;
```

Used for:

* Creating
* Reading
* Inserting
* Updating
* Deleting
* Joining
* Aggregating
* Transactions
* Managing permissions

---

## 3. SQL vs NoSQL

| SQL                       | NoSQL                              |
| ------------------------- | ---------------------------------- |
| Relational                | Non-relational                     |
| Tables                    | Documents / Key-Value / Graph etc. |
| Usually structured schema | Usually flexible schema            |
| SQL                       | Query method varies                |
| PostgreSQL, MySQL         | MongoDB, Redis                     |

---

# 4. Database vs File System

| File System                      | Database                     |
| -------------------------------- | ---------------------------- |
| Files                            | Tables/managed data          |
| More redundancy                  | Redundancy can be controlled |
| Limited relationships            | Supports relationships       |
| Limited concurrency control      | Concurrency control          |
| Complex querying is harder       | Powerful query language      |
| Application-dependent management | DBMS provides management     |

**Memory:**
File System → Files
Database → Structured + Managed Data

---

# 5. Basic Database Terms

### Table

Data organized into rows and columns.

### Row / Record

One complete data entry.

### Column / Field

An attribute/property.

### Schema

Structure/blueprint of the database.

### Instance

Actual data at a particular time.

**Memory:**

```text
Schema   → Structure
Instance → Actual Data
```

---

# 6. Keys

### Primary Key

Uniquely identifies each row.

* Unique
* Cannot be NULL

```sql
student_id SERIAL PRIMARY KEY
```

### Foreign Key

References a key in another table.

```sql
FOREIGN KEY (department_id)
REFERENCES Departments(department_id)
```

### Candidate Key

A key that can become the primary key.

### Alternate Key

Candidate key not selected as primary key.

### Composite Key

Two or more columns together identify a row.

```sql
PRIMARY KEY (student_id, course_id)
```

### Super Key

Any attribute/set of attributes that uniquely identifies a row, possibly with extra attributes.

### Unique Key

Prevents duplicate values.

---

# 7. Constraints

Main constraints:

```text
PRIMARY KEY
FOREIGN KEY
UNIQUE
NOT NULL
CHECK
DEFAULT
```

### NOT NULL

```sql
name VARCHAR(100) NOT NULL
```

### UNIQUE

```sql
email VARCHAR(100) UNIQUE
```

### CHECK

```sql
age INT CHECK (age >= 18)
```

### DEFAULT

```sql
status VARCHAR(20) DEFAULT 'active'
```

---

# 8. Foreign Key Actions

### CASCADE

```sql
ON DELETE CASCADE
```

Related child rows are automatically affected.

### SET NULL

```sql
ON DELETE SET NULL
```

Foreign-key value becomes NULL.

### RESTRICT

Prevents the operation when dependent rows exist.

### NO ACTION

Rejects the operation if referential integrity would be violated.

---

# 9. Three-Schema Architecture

```text
External
   ↓
Conceptual
   ↓
Internal
```

### External

What users see.

### Conceptual

Logical structure of the complete database.

### Internal

How data is physically stored.

**Memory:**

```text
External   → User View
Conceptual → Logical Structure
Internal   → Physical Storage
```

---

# 10. Data Independence

### Logical Data Independence

Change conceptual structure without unnecessarily affecting external views.

### Physical Data Independence

Change physical storage without affecting the conceptual schema.

**Memory:**

```text
Logical  → Logical Structure
Physical → Storage
```

---

# 11. ER Model

**ER = Entity Relationship**

Used to design a database before creating actual tables.

Main components:

```text
Entity
Attribute
Relationship
```

### Entity

Real-world object.

Examples:

* Student
* Teacher
* Course
* Department

### Attribute

Property of an entity.

Example:

```text
Student
 ├── student_id
 ├── name
 ├── age
 └── email
```

### Relationship

Association between entities.

```text
Student → Enrolls → Course
```

### Entity Set

Collection of similar entities.

### Relationship Set

Collection of similar relationships.

---

# 12. Entity Types

### Strong Entity

* Has its own key
* Can exist independently

### Weak Entity

* Depends on another entity
* Cannot be uniquely identified using its own attributes alone
* Uses owner key + partial key

---

# 13. Attribute Types

### Simple Attribute

Cannot be divided.

Example:

```text
Age
```

### Composite Attribute

Can be divided.

```text
Name
 ├── First Name
 ├── Middle Name
 └── Last Name
```

### Single-Valued

One value per entity.

### Multi-Valued

Multiple values.

Example:

```text
Phone Numbers
```

### Derived

Calculated from another attribute.

Example:

```text
Date of Birth → Age
```

---

# 14. ER Diagram Symbols

| Symbol           | Meaning                  |
| ---------------- | ------------------------ |
| Rectangle        | Entity                   |
| Double Rectangle | Weak Entity              |
| Oval             | Attribute                |
| Double Oval      | Multi-valued Attribute   |
| Dashed Oval      | Derived Attribute        |
| Diamond          | Relationship             |
| Double Diamond   | Identifying Relationship |

---

# 15. Cardinality

Cardinality tells **how many** entities participate.

### 1:1

One-to-One.

```text
Person ↔ Passport
```

### 1:M

One-to-Many.

```text
Department → Employees
```

### M:N

Many-to-Many.

```text
Students ↔ Courses
```

Usually implemented using a junction table:

```text
Students
Courses
Enrollments
```

---

# 16. Participation

### Total Participation

Mandatory participation.

### Partial Participation

Optional participation.

**Memory:**

```text
Cardinality  → How many?
Participation → Mandatory/Optional
```

---

# 17. Degree & Cardinality of Relation

### Degree

Number of columns/attributes.

```text
Students(id, name, age, city)
```

Degree = **4**

### Relation Cardinality

Number of rows.

```text
5 rows → Cardinality = 5
```

**Memory:**

```text
Degree      → Columns
Cardinality → Rows
```

---

# 18. Relationship vs JOIN

### Relationship

Database design concept.

```text
Students → Departments
```

### JOIN

SQL operation used to retrieve related data.

```sql
SELECT *
FROM Students
JOIN Departments
ON Students.department_id = Departments.department_id;
```

**Memory:**

```text
Relationship → Design
JOIN         → Query
```

---

# 19. Normalization

Normalization organizes data to:

* Reduce redundancy
* Prevent anomalies
* Improve consistency

### Data Redundancy

Unnecessary repetition of data.

---

# 20. Data Anomalies

### Insert Anomaly

Cannot insert data without unrelated data.

### Update Anomaly

Same information must be updated in multiple rows.

### Delete Anomaly

Deleting one record accidentally removes useful information.

**Memory:**

```text
INSERT → Insert Anomaly
UPDATE → Update Anomaly
DELETE → Delete Anomaly
```

---

# 21. Normal Forms

### 1NF

* Atomic values
* No repeating groups
* No multiple values in one cell

**1NF → Atomic**

### 2NF

* Must be in 1NF
* No partial dependency

**2NF → No Partial Dependency**

### 3NF

* Must be in 2NF
* No transitive dependency

**3NF → No Transitive Dependency**

### BCNF

For every:

```text
A → B
```

A must be a **super key**.

**BCNF → Determinant is Super Key**

---

# 22. Functional Dependency

One attribute/set of attributes determines another.

```text
A → B
```

Means:

```text
A determines B
```

---

# 23. Normalization Order

```text
Unnormalized
     ↓
    1NF
     ↓
    2NF
     ↓
    3NF
     ↓
   BCNF
```

---

# 24. Normalization vs Denormalization

| Normalization      | Denormalization              |
| ------------------ | ---------------------------- |
| Reduces redundancy | Adds some redundancy         |
| Reduces anomalies  | May increase redundancy      |
| More tables        | Fewer joins may be needed    |
| Better consistency | Can improve read performance |

---

# 25. SQL Command Categories

## DDL — Data Definition Language

Structure:

```sql
CREATE
ALTER
DROP
TRUNCATE
```

## DML — Data Manipulation Language

Data modification:

```sql
INSERT
UPDATE
DELETE
```

## DQL — Data Query Language

Data retrieval:

```sql
SELECT
```

## DCL — Data Control Language

Permissions:

```sql
GRANT
REVOKE
```

## TCL — Transaction Control Language

Transactions:

```sql
BEGIN
COMMIT
ROLLBACK
SAVEPOINT
```

**Memory:**

```text
DDL → Structure
DML → Data
DQL → Query
DCL → Permissions
TCL → Transactions
```

---

# 26. CRUD

```text
C → Create
R → Read
U → Update
D → Delete
```

| CRUD   | SQL    |
| ------ | ------ |
| Create | INSERT |
| Read   | SELECT |
| Update | UPDATE |
| Delete | DELETE |

---

# 27. DELETE vs TRUNCATE vs DROP

| DELETE        | TRUNCATE         | DROP              |
| ------------- | ---------------- | ----------------- |
| Removes rows  | Removes all rows | Removes table     |
| WHERE allowed | No normal WHERE  | Structure removed |
| Table remains | Table remains    | Table removed     |
| DML           | DDL              | DDL               |

```sql
DELETE FROM Students WHERE id = 1;
```

```sql
TRUNCATE TABLE Students;
```

```sql
DROP TABLE Students;
```

**Memory:**

```text
DELETE   → Selected Rows
TRUNCATE → All Rows
DROP     → Entire Table
```

---

# 28. JOINS

## INNER JOIN

Only matching rows.

```sql
SELECT *
FROM Students
INNER JOIN Departments
ON Students.department_id = Departments.department_id;
```

## LEFT JOIN

All left rows + matching right rows.

```sql
SELECT *
FROM Students
LEFT JOIN Departments
ON Students.department_id = Departments.department_id;
```

## RIGHT JOIN

All right rows + matching left rows.

```sql
SELECT *
FROM Students
RIGHT JOIN Departments
ON Students.department_id = Departments.department_id;
```

## FULL OUTER JOIN

All rows from both tables.

```sql
SELECT *
FROM Students
FULL OUTER JOIN Departments
ON Students.department_id = Departments.department_id;
```

## CROSS JOIN

Cartesian product.

```sql
SELECT *
FROM Students
CROSS JOIN Departments;
```

If:

```text
Students = 5 rows
Departments = 3 rows

Result = 5 × 3 = 15 rows
```

## SELF JOIN

A table joined with itself.

```sql
SELECT
    e.employee_name,
    m.employee_name AS manager_name
FROM Employees e
JOIN Employees m
ON e.manager_id = m.employee_id;
```

**Memory:**

```text
INNER → Matching
LEFT  → All Left
RIGHT → All Right
FULL  → All Both
CROSS → Every Combination
SELF  → Same Table
```

---

# 29. Indexing

### Index

A data structure that can speed up data retrieval.

```sql
CREATE INDEX idx_students_name
ON Students(student_name);
```

Search:

```sql
SELECT *
FROM Students
WHERE student_name = 'Ali';
```

### Advantages

* Faster reads/searches
* Can improve joins and lookups

### Disadvantages

* Uses storage
* Adds maintenance cost to INSERT/UPDATE/DELETE

**Memory:**

```text
Index → Faster Reads + Extra Storage + Write Cost
```

---

# 30. Transactions

Transaction = logical unit of work.

Example:

```text
Account A → -₹1000
Account B → +₹1000
```

Both operations should succeed together.

### BEGIN

```sql
BEGIN;
```

### COMMIT

```sql
COMMIT;
```

Saves the transaction's changes.

### ROLLBACK

```sql
ROLLBACK;
```

Undoes uncommitted changes in the current transaction.

### SAVEPOINT

```sql
SAVEPOINT point1;
```

Creates a checkpoint.

Example:

```sql
BEGIN;

INSERT INTO Students(student_name)
VALUES ('Ali');

SAVEPOINT point1;

INSERT INTO Students(student_name)
VALUES ('Ahmed');

ROLLBACK TO SAVEPOINT point1;

COMMIT;
```

**Memory:**

```text
BEGIN    → Start
COMMIT   → Save
ROLLBACK → Undo
SAVEPOINT → Checkpoint
```

---

# 31. ACID

```text
A → Atomicity
C → Consistency
I → Isolation
D → Durability
```

### Atomicity

All or nothing.

### Consistency

Database moves from one valid state to another while preserving constraints and business rules.

### Isolation

Concurrent transactions are controlled so they do not improperly interfere.

### Durability

Committed changes remain saved even after system failure.

**Memory:**

```text
Atomicity  → All or Nothing
Consistency → Valid State
Isolation   → Controlled Concurrency
Durability  → Saved Permanently
```

---

# 32. Transaction Anomalies

### Dirty Read

Reading another transaction's uncommitted data.

### Non-Repeatable Read

Reading the same row twice and getting different values.

### Phantom Read

Repeating a query and getting a different set of matching rows.

---

# 33. Isolation Levels

```text
READ UNCOMMITTED
        ↓
READ COMMITTED
        ↓
REPEATABLE READ
        ↓
SERIALIZABLE
```

| Level            | Dirty Read | Non-Repeatable | Phantom        |
| ---------------- | ---------- | -------------- | -------------- |
| READ UNCOMMITTED | Yes        | Yes            | Yes            |
| READ COMMITTED   | No         | Yes            | Yes            |
| REPEATABLE READ  | No         | No             | DBMS-dependent |
| SERIALIZABLE     | No         | No             | No             |

### PostgreSQL Important Points

```text
Default → READ COMMITTED
READ UNCOMMITTED → Treated as READ COMMITTED
```

PostgreSQL's `REPEATABLE READ` also prevents phantom reads through its implementation.

---

# 34. Aggregate Functions

Main aggregate functions:

```text
COUNT()
SUM()
AVG()
MIN()
MAX()
```

### COUNT

```sql
SELECT COUNT(*) FROM Students;
```

Counts rows.

```sql
COUNT(*)     → All rows
COUNT(column) → Non-NULL values
```

### SUM

```sql
SELECT SUM(marks) FROM Students;
```

Total.

### AVG

```sql
SELECT AVG(marks) FROM Students;
```

Average.

### MIN

```sql
SELECT MIN(marks) FROM Students;
```

Smallest.

### MAX

```sql
SELECT MAX(marks) FROM Students;
```

Largest.

---

# 35. WHERE + Aggregate

WHERE filters rows before aggregation.

```sql
SELECT AVG(marks)
FROM Students
WHERE marks >= 80;
```

**WHERE → Filter Rows**

---

# 36. GROUP BY

Groups rows before aggregation.

```sql
SELECT
    department_id,
    AVG(marks)
FROM Students
GROUP BY department_id;
```

Flow:

```text
Rows
 ↓
GROUP BY
 ↓
Groups
 ↓
Aggregate
 ↓
Result
```

---

# 37. HAVING

Filters groups after aggregation.

```sql
SELECT
    department_id,
    AVG(marks)
FROM Students
GROUP BY department_id
HAVING AVG(marks) > 80;
```

### WHERE vs HAVING

```text
WHERE  → Filters Rows
HAVING → Filters Groups
```

---

# 38. NULL & Aggregate Functions

Most aggregate functions ignore NULL.

Example:

```text
80
70
NULL
```

```sql
AVG(marks)
```

Calculates:

```text
(80 + 70) / 2
```

Not:

```text
(80 + 70) / 3
```

Important:

```text
COUNT(*)       → Counts rows
COUNT(column)  → Counts non-NULL values
```

---

# 39. CAP Theorem

CAP applies to distributed systems.

```text
C → Consistency
A → Availability
P → Partition Tolerance
```

### Consistency

Reads see data according to the system's consistency guarantee.

### Availability

Every request receives a response.

### Partition Tolerance

System continues operating despite network communication failures between nodes.

### Key Idea

When a network partition occurs, a distributed system has to make a trade-off between consistency and availability.

**Memory:**

```text
CAP
C → Consistency
A → Availability
P → Partition Tolerance
```

---

# 40. FINAL MASTER MEMORY SHEET

```text
DATABASE
→ Organized collection of data

DBMS
→ Manages databases

RDBMS
→ Tables + Relationships

SQL
→ Communicates with relational databases

SCHEMA
→ Structure

INSTANCE
→ Actual Data

PRIMARY KEY
→ Identifies a row

FOREIGN KEY
→ Connects tables

CANDIDATE KEY
→ Can become Primary Key

ALTERNATE KEY
→ Candidate Key not selected

COMPOSITE KEY
→ Multiple columns together

SUPER KEY
→ Any unique-identifying attribute set

UNIQUE
→ Prevents duplicates

ENTITY
→ Real-world object

ATTRIBUTE
→ Property

RELATIONSHIP
→ Association

CARDINALITY
→ How many?

PARTICIPATION
→ Mandatory / Optional

DEGREE
→ Number of columns

RELATION CARDINALITY
→ Number of rows

1:1
→ One-to-One

1:M
→ One-to-Many

M:N
→ Many-to-Many

NORMALIZATION
→ Reduce redundancy

1NF
→ Atomic

2NF
→ No Partial Dependency

3NF
→ No Transitive Dependency

BCNF
→ Determinant is Super Key

DDL
→ Structure

DML
→ Data Modification

DQL
→ Data Retrieval

DCL
→ Permissions

TCL
→ Transactions

CRUD
→ Create, Read, Update, Delete

INNER JOIN
→ Matching rows

LEFT JOIN
→ All Left + Matches

RIGHT JOIN
→ All Right + Matches

FULL JOIN
→ All Both

CROSS JOIN
→ Cartesian Product

SELF JOIN
→ Same Table

INDEX
→ Faster Retrieval

TRANSACTION
→ Logical Unit of Work

BEGIN
→ Start

COMMIT
→ Save

ROLLBACK
→ Undo

SAVEPOINT
→ Checkpoint

ACID
→ Atomicity + Consistency + Isolation + Durability

ATOMICITY
→ All or Nothing

CONSISTENCY
→ Valid State → Valid State

ISOLATION
→ Controlled Concurrency

DURABILITY
→ Committed Data Persists

COUNT()
→ Number

SUM()
→ Total

AVG()
→ Average

MIN()
→ Smallest

MAX()
→ Largest

WHERE
→ Filter Rows

GROUP BY
→ Create Groups

HAVING
→ Filter Groups
