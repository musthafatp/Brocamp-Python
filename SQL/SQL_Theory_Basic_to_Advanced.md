# SQL Theory --- Basic to Advanced

A reviewer-ready SQL theory guide arranged from **Basic → Intermediate →
Advanced**.

------------------------------------------------------------------------

# 1. Database

A **database** is an organized collection of data that can be stored,
managed, and retrieved efficiently.

**Example:** A school database can store students, teachers,
departments, exams, and attendance.

------------------------------------------------------------------------

# 2. DBMS

**DBMS (Database Management System)** is software used to create, store,
manage, and retrieve data from databases.

**Examples:** PostgreSQL, MySQL, Oracle, SQL Server.

### Main Functions

-   Store data
-   Retrieve data
-   Insert, update, and delete data
-   Manage security
-   Handle transactions
-   Maintain data integrity

------------------------------------------------------------------------

# 3. RDBMS

**RDBMS (Relational Database Management System)** stores data in tables
consisting of rows and columns and uses relationships between tables.

**Examples:** PostgreSQL, MySQL, Oracle, SQL Server.

------------------------------------------------------------------------

# 4. Non-Relational Database

A **non-relational database** stores data in flexible formats such as
documents, JSON, key-value pairs, graphs, or wide-column structures
rather than requiring a fixed relational table structure.

------------------------------------------------------------------------

# 5. SQL

**SQL (Structured Query Language)** is a language used to communicate
with and manage relational databases.

It is used to: - Create database objects - Retrieve data - Insert data -
Update data - Delete data - Manage permissions - Control transactions

------------------------------------------------------------------------

# 6. SQL Command Categories

## DDL --- Data Definition Language

DDL is used to define and modify the structure of database objects such
as tables, schemas, and indexes.

**Commands:** - `CREATE` - `ALTER` - `DROP` - `TRUNCATE`

------------------------------------------------------------------------

## DML --- Data Manipulation Language

DML is used to manipulate data stored in tables.

**Commands:** - `INSERT` - `UPDATE` - `DELETE`

------------------------------------------------------------------------

## DQL --- Data Query Language

DQL is used to retrieve data.

**Command:** - `SELECT`

------------------------------------------------------------------------

## DCL --- Data Control Language

DCL is used to manage database permissions and access.

**Commands:** - `GRANT` - `REVOKE`

------------------------------------------------------------------------

## TCL --- Transaction Control Language

TCL is used to control transactions.

**Commands:** - `BEGIN` - `COMMIT` - `ROLLBACK` - `SAVEPOINT`

------------------------------------------------------------------------

# 7. PostgreSQL

**PostgreSQL** is a free and open-source object-relational database
management system (ORDBMS) known for SQL support, data integrity,
extensibility, complex queries, advanced data types, and powerful
indexing.

### Advantages

-   Free and open source
-   Reliable and standards-oriented
-   Strong SQL support
-   Excellent JOIN support
-   Supports complex data types
-   Strong data integrity
-   Supports advanced features
-   Powerful indexing options
-   Scales for many workloads

### Disadvantages

-   Can require more memory/resources for some workloads
-   Configuration and administration can be complex
-   May not be the simplest choice for very basic applications

------------------------------------------------------------------------

# 8. PostgreSQL vs MySQL

PostgreSQL and MySQL are both popular relational database systems.

PostgreSQL is often chosen when an application needs advanced SQL
features, complex queries, strong data integrity, extensibility, or
advanced data types.

Common PostgreSQL strengths include: - Advanced SQL features - Strong
JOIN and query capabilities - Rich JSON/JSONB support - Strong data
integrity - Extensive data types and extensions

The correct choice depends on the application's requirements rather than
one database being universally better.

------------------------------------------------------------------------

# 9. Tables, Rows, and Columns

A **table** stores related data.

A **row** represents one record.

A **column** represents one attribute of the data.

Example:

``` text
Students
--------------------------------
id | name | age | department_id
--------------------------------
1  | John | 20  | 101
2  | Alex | 21  | 102
```

------------------------------------------------------------------------

# 10. Primary Key

A **primary key** is a column or combination of columns that uniquely
identifies each row in a table.

### Key Points

-   Values must be unique.
-   It cannot contain `NULL`.
-   A table has one primary key constraint.
-   It may contain multiple columns as a composite primary key.

------------------------------------------------------------------------

# 11. Foreign Key

A **foreign key** is a column or combination of columns that references
a key in another table to establish a relationship between tables.

### Purpose

-   Maintains referential integrity.
-   Prevents invalid references.
-   Connects related tables.

------------------------------------------------------------------------

# 12. Candidate Key

A **candidate key** is a column or combination of columns that can
uniquely identify a row and is eligible to become the primary key.

A table can have multiple candidate keys, but only one is selected as
the primary key.

------------------------------------------------------------------------

# 13. Super Key

A **super key** is any column or combination of columns that can
uniquely identify a row.

Every candidate key is a super key, but not every super key is a
candidate key.

------------------------------------------------------------------------

# 14. Composite Key

A **composite key** consists of two or more columns that together
uniquely identify a row.

Example:

``` sql
PRIMARY KEY (student_id, course_id)
```

Composite keys are commonly used in junction tables.

------------------------------------------------------------------------

# 15. Constraints

Constraints are rules applied to table columns to ensure that stored
data is valid and consistent.

### Common Constraints

-   `PRIMARY KEY`
-   `FOREIGN KEY`
-   `UNIQUE`
-   `NOT NULL`
-   `CHECK`
-   `DEFAULT`

------------------------------------------------------------------------

# 16. UNIQUE Constraint

The `UNIQUE` constraint prevents duplicate values in a column or
combination of columns.

Example:

``` sql
email VARCHAR(100) UNIQUE
```

A `UNIQUE` constraint is different from a primary key; handling of
`NULL` values can differ by database system.

------------------------------------------------------------------------

# 17. NOT NULL Constraint

The `NOT NULL` constraint ensures that a column cannot contain `NULL`.

``` sql
name VARCHAR(50) NOT NULL
```

------------------------------------------------------------------------

# 18. CHECK Constraint

A `CHECK` constraint ensures that values satisfy a specified condition.

``` sql
age INT CHECK (age >= 18)
```

------------------------------------------------------------------------

# 19. DEFAULT Constraint

A `DEFAULT` value is automatically used when an insert does not provide
a value for that column.

``` sql
status VARCHAR(20) DEFAULT 'Active'
```

------------------------------------------------------------------------

# 20. NULL

`NULL` represents a missing, unknown, or undefined value.

`NULL` is not the same as: - `0` - `''` - `FALSE`

Use:

``` sql
WHERE salary IS NULL
```

or:

``` sql
WHERE salary IS NOT NULL
```

------------------------------------------------------------------------

# 21. WHERE

`WHERE` filters individual rows according to a condition.

``` sql
SELECT *
FROM Employees
WHERE salary > 50000;
```

------------------------------------------------------------------------

# 22. ORDER BY

`ORDER BY` sorts query results.

``` sql
SELECT *
FROM Employees
ORDER BY salary DESC;
```

-   `ASC` --- ascending
-   `DESC` --- descending

------------------------------------------------------------------------

# 23. LIMIT

`LIMIT` restricts the number of rows returned.

``` sql
SELECT *
FROM Employees
LIMIT 5;
```

------------------------------------------------------------------------

# 24. OFFSET

`OFFSET` skips a specified number of rows before returning results.

``` sql
SELECT *
FROM Employees
LIMIT 5 OFFSET 10;
```

`LIMIT` and `OFFSET` are commonly used for pagination.

------------------------------------------------------------------------

# 25. DISTINCT

`DISTINCT` removes duplicate rows from the selected result.

``` sql
SELECT DISTINCT department_id
FROM Employees;
```

------------------------------------------------------------------------

# 26. Aliases

An **alias** temporarily gives a table or column another name within a
query.

``` sql
SELECT name AS employee_name
FROM Employees;
```

Table alias:

``` sql
SELECT e.name
FROM Employees AS e;
```

------------------------------------------------------------------------

# 27. Aggregate Functions

Aggregate functions perform calculations across multiple rows.

### Common Aggregate Functions

-   `COUNT()`
-   `SUM()`
-   `AVG()`
-   `MIN()`
-   `MAX()`

Example:

``` sql
SELECT AVG(salary)
FROM Employees;
```

------------------------------------------------------------------------

# 28. GROUP BY

`GROUP BY` groups rows with the same values so aggregate functions can
be applied to each group.

``` sql
SELECT department_id, COUNT(*)
FROM Employees
GROUP BY department_id;
```

------------------------------------------------------------------------

# 29. HAVING

`HAVING` filters groups after `GROUP BY`.

``` sql
SELECT department_id, COUNT(*)
FROM Employees
GROUP BY department_id
HAVING COUNT(*) > 5;
```

### Easy Difference

``` text
WHERE  → filters rows
HAVING → filters groups
```

------------------------------------------------------------------------

# 30. SQL Logical Query Processing Order

Although SQL is written in a different order, the logical processing
order is generally:

``` text
FROM
JOIN
WHERE
GROUP BY
HAVING
SELECT
DISTINCT
ORDER BY
LIMIT / OFFSET
```

Understanding this order helps explain why `WHERE` and `HAVING` behave
differently.

------------------------------------------------------------------------

# 31. Relationships

A relationship defines how entities/tables are connected.

### Common Relationships

-   One-to-One
-   One-to-Many
-   Many-to-Many

A many-to-many relationship is commonly implemented using a **junction
table**.

------------------------------------------------------------------------

# 32. JOIN

A JOIN combines data from two or more tables using related columns.

Common JOIN types: - `INNER JOIN` - `LEFT JOIN` - `RIGHT JOIN` -
`FULL OUTER JOIN` - `CROSS JOIN`

------------------------------------------------------------------------

# 33. INNER JOIN

An `INNER JOIN` returns only rows that have matching values in both
tables.

``` sql
SELECT *
FROM Students s
INNER JOIN Departments d
ON s.department_id = d.department_id;
```

------------------------------------------------------------------------

# 34. LEFT JOIN

A `LEFT JOIN` returns all rows from the left table and matching rows
from the right table.

If no match exists, right-side columns contain `NULL`.

------------------------------------------------------------------------

# 35. RIGHT JOIN

A `RIGHT JOIN` returns all rows from the right table and matching rows
from the left table.

------------------------------------------------------------------------

# 36. FULL OUTER JOIN

A `FULL OUTER JOIN` returns: - Matching rows - Unmatched rows from the
left table - Unmatched rows from the right table

------------------------------------------------------------------------

# 37. CROSS JOIN

A `CROSS JOIN` produces the Cartesian product of two tables.

If Table A has 3 rows and Table B has 4 rows:

``` text
3 × 4 = 12 rows
```

------------------------------------------------------------------------

# 38. Referential Integrity

Referential integrity ensures that relationships between tables remain
valid.

A foreign key should reference an existing related key unless the design
allows `NULL`.

------------------------------------------------------------------------

# 39. Cascading

Cascading controls what happens to related rows when referenced data is
updated or deleted.

Common options: - `ON DELETE CASCADE` - `ON DELETE SET NULL` -
`ON UPDATE CASCADE`

`ON DELETE CASCADE` can automatically delete related child rows when a
parent row is deleted.

------------------------------------------------------------------------

# 40. Scalar Functions

A **scalar function** operates on individual values and returns a value
for each input row.

Examples: - `UPPER()` - `LOWER()` - `LENGTH()` - `ROUND()` - `ABS()` -
`COALESCE()`

------------------------------------------------------------------------

# 41. String Functions

String functions manipulate text values.

Common examples: - `UPPER()` - `LOWER()` - `LENGTH()` - `SUBSTRING()` -
`REPLACE()` - `TRIM()` - `CONCAT()`

------------------------------------------------------------------------

# 42. Numeric Functions

Numeric functions perform operations on numerical values.

Examples: - `ROUND()` - `CEIL()` - `FLOOR()` - `ABS()` - `MOD()`

------------------------------------------------------------------------

# 43. Date and Time Functions

Date/time functions work with dates, times, and timestamps.

Common PostgreSQL examples: - `CURRENT_DATE` - `CURRENT_TIMESTAMP` -
`EXTRACT()` - `AGE()` - Date arithmetic

------------------------------------------------------------------------

# 44. Conditional Functions

Conditional functions allow SQL to handle conditions and `NULL` values.

Important examples: - `CASE` - `COALESCE()` - `NULLIF()`

------------------------------------------------------------------------

# 45. CASE Statement

`CASE` performs conditional logic in SQL.

``` sql
SELECT name,
       CASE
           WHEN salary >= 70000 THEN 'High'
           WHEN salary >= 40000 THEN 'Medium'
           ELSE 'Low'
       END AS salary_level
FROM Employees;
```

It is similar to `if / else if / else`.

------------------------------------------------------------------------

# 46. COALESCE

`COALESCE()` returns the first non-`NULL` value.

``` sql
SELECT COALESCE(phone, 'Not Available')
FROM Students;
```

------------------------------------------------------------------------

# 47. NULLIF

`NULLIF()` returns `NULL` if two expressions are equal.

``` sql
SELECT NULLIF(10, 10);
```

Result:

``` text
NULL
```

It can also help prevent division-by-zero problems.

------------------------------------------------------------------------

# 48. Type Conversion

Type conversion changes a value from one data type to another.

PostgreSQL supports:

``` sql
CAST(value AS type)
```

and:

``` sql
value::type
```

Example:

``` sql
SELECT CAST('100' AS INTEGER);
```

------------------------------------------------------------------------

# 49. Subquery

A **subquery** is a query written inside another SQL query.

Example:

``` sql
SELECT *
FROM Employees
WHERE salary > (
    SELECT AVG(salary)
    FROM Employees
);
```

------------------------------------------------------------------------

# 50. Scalar Subquery

A scalar subquery returns a single value.

``` sql
SELECT *
FROM Employees
WHERE salary > (
    SELECT AVG(salary)
    FROM Employees
);
```

------------------------------------------------------------------------

# 51. Multiple-Row Subquery

A multiple-row subquery returns multiple values.

Common operators: - `IN` - `ANY` - `ALL`

Example:

``` sql
SELECT *
FROM Employees
WHERE department_id IN (
    SELECT department_id
    FROM Departments
    WHERE location = 'Kochi'
);
```

------------------------------------------------------------------------

# 52. Correlated Subquery

A correlated subquery references a column from the outer query.

It is logically evaluated in relation to each row processed by the outer
query.

Example:

``` sql
SELECT e.name, e.salary
FROM Employees e
WHERE e.salary > (
    SELECT AVG(e2.salary)
    FROM Employees e2
    WHERE e2.department_id = e.department_id
);
```

------------------------------------------------------------------------

# 53. Non-Correlated Subquery

A non-correlated subquery does not depend on the outer query and can
execute independently of it.

Example:

``` sql
SELECT *
FROM Employees
WHERE salary > (
    SELECT AVG(salary)
    FROM Employees
);
```

------------------------------------------------------------------------

# 54. EXISTS

`EXISTS` checks whether a subquery returns at least one row.

It returns a Boolean result.

``` sql
SELECT *
FROM Departments d
WHERE EXISTS (
    SELECT 1
    FROM Employees e
    WHERE e.department_id = d.department_id
);
```

------------------------------------------------------------------------

# 55. NOT EXISTS

`NOT EXISTS` checks whether a subquery returns no rows.

It is useful for finding records that have no matching related records.

------------------------------------------------------------------------

# 56. Set Operations

Set operations combine the results of two or more queries.

Common set operations: - `UNION` - `UNION ALL` - `INTERSECT` - `EXCEPT`

The participating queries must have compatible result structures.

------------------------------------------------------------------------

# 57. UNION

`UNION` combines results and removes duplicate rows.

------------------------------------------------------------------------

# 58. UNION ALL

`UNION ALL` combines results while keeping duplicate rows.

------------------------------------------------------------------------

# 59. INTERSECT

`INTERSECT` returns rows common to both query results.

------------------------------------------------------------------------

# 60. EXCEPT

`EXCEPT` returns rows from the first query that are not present in the
second query.

------------------------------------------------------------------------

# 61. Common Table Expression (CTE)

A **CTE (Common Table Expression)** is a named temporary result set
defined using the `WITH` clause and available to the statement that
follows it.

Example:

``` sql
WITH high_salary AS (
    SELECT *
    FROM Employees
    WHERE salary > 50000
)
SELECT *
FROM high_salary;
```

### Advantages

-   Improves readability
-   Breaks complex queries into steps
-   Allows multiple CTEs in one query
-   Supports recursive queries

------------------------------------------------------------------------

# 62. Non-Recursive CTE

A non-recursive CTE does not reference itself.

It is commonly used to simplify complex queries.

------------------------------------------------------------------------

# 63. Recursive CTE

A recursive CTE references itself and repeatedly processes data.

It is useful for: - Hierarchical data - Organizational structures - Tree
structures - Sequential data

Example hierarchy:

``` text
CEO
 └── Manager
      └── Employee
```

------------------------------------------------------------------------

# 64. Window Functions

A **window function** performs calculations across related rows without
collapsing those rows into one result row.

Common window functions: - `ROW_NUMBER()` - `RANK()` - `DENSE_RANK()` -
`LAG()` - `LEAD()` - Aggregate functions with `OVER()`

------------------------------------------------------------------------

# 65. OVER()

`OVER()` defines the window of rows on which a window function operates.

Example:

``` sql
SELECT name,
       salary,
       RANK() OVER (ORDER BY salary DESC) AS salary_rank
FROM Employees;
```

------------------------------------------------------------------------

# 66. PARTITION BY

`PARTITION BY` divides rows into groups for a window function without
collapsing the rows.

Example:

``` sql
RANK() OVER (
    PARTITION BY department_id
    ORDER BY salary DESC
)
```

This ranks employees within each department.

------------------------------------------------------------------------

# 67. ROW_NUMBER()

`ROW_NUMBER()` assigns a unique sequential number to each row.

``` text
100 → 1
90  → 2
90  → 3
80  → 4
```

------------------------------------------------------------------------

# 68. RANK()

`RANK()` assigns the same rank to tied values and skips the next rank.

``` text
100 → 1
90  → 2
90  → 2
80  → 4
```

------------------------------------------------------------------------

# 69. DENSE_RANK()

`DENSE_RANK()` assigns the same rank to tied values without skipping the
next rank.

``` text
100 → 1
90  → 2
90  → 2
80  → 3
```

------------------------------------------------------------------------

# 70. LAG()

`LAG()` accesses a value from a previous row in the window.

It is useful for comparing the current row with a previous row.

------------------------------------------------------------------------

# 71. LEAD()

`LEAD()` accesses a value from a following row in the window.

It is useful for comparing the current row with a future row.

------------------------------------------------------------------------

# 72. Window Aggregate Functions

Aggregate functions can also be used as window functions.

Example:

``` sql
SELECT name,
       department_id,
       salary,
       AVG(salary) OVER (
           PARTITION BY department_id
       ) AS department_average
FROM Employees;
```

Unlike normal `GROUP BY`, the individual employee rows remain visible.

------------------------------------------------------------------------

# 73. View

A **view** is a virtual table defined by a SQL query.

Example:

``` sql
CREATE VIEW employee_details AS
SELECT name, salary
FROM Employees;
```

A normal view stores the query definition rather than storing a separate
physical copy of its result.

### Uses

-   Simplify complex queries
-   Reuse queries
-   Restrict access to selected data
-   Provide a controlled data interface

------------------------------------------------------------------------

# 74. Materialized View

A **materialized view** stores the result of a query physically.

It can improve performance for expensive or frequently used queries, but
the stored result needs to be refreshed when the underlying data
changes.

------------------------------------------------------------------------

# 75. User-Defined Function (UDF)

A **User-Defined Function** is a function created by the developer to
perform a specific reusable task and return a value or result.

A function can accept parameters and can be called from SQL statements
where appropriate.

------------------------------------------------------------------------

# 76. Stored Procedure

A **stored procedure** is a set of SQL statements and procedural logic
stored in the database that can be executed to perform a specific task.

It can contain: - Parameters - Variables - Conditions - Loops - SQL
statements

### Uses

-   Automating database operations
-   Reusing database logic
-   Performing multiple operations
-   Implementing database-side workflows

------------------------------------------------------------------------

# 77. Trigger

A **trigger** is a database object that automatically executes a
specified function or action in response to events such as `INSERT`,
`UPDATE`, or `DELETE`.

Example use:

``` text
Employee salary updated
        ↓
Trigger executes
        ↓
Audit record created
```

------------------------------------------------------------------------

# 78. Transactions

A **transaction** is a group of database operations treated as a single
logical unit of work.

Example:

``` sql
BEGIN;

UPDATE Accounts
SET balance = balance - 1000
WHERE id = 1;

UPDATE Accounts
SET balance = balance + 1000
WHERE id = 2;

COMMIT;
```

------------------------------------------------------------------------

# 79. COMMIT

`COMMIT` permanently saves the changes made by the current transaction.

------------------------------------------------------------------------

# 80. ROLLBACK

`ROLLBACK` undoes changes made during the current transaction that have
not been committed.

------------------------------------------------------------------------

# 81. SAVEPOINT

A `SAVEPOINT` creates a point inside a transaction to which the
transaction can partially roll back.

``` sql
SAVEPOINT point1;
```

------------------------------------------------------------------------

# 82. ACID Properties

ACID properties ensure reliable transaction processing.

## Atomicity

All operations in a transaction are completed successfully or none of
them are applied.

## Consistency

A transaction moves the database from one valid state to another valid
state.

## Isolation

Concurrent transactions should not incorrectly interfere with each
other.

## Durability

Once a transaction is committed, its changes remain stored even after a
system failure.

------------------------------------------------------------------------

# 83. Transaction Isolation

Transaction isolation controls how concurrent transactions can see each
other's changes.

It helps control problems such as: - Dirty reads - Non-repeatable
reads - Phantom reads

------------------------------------------------------------------------

# 84. Locks

A lock is a mechanism used by the database to control concurrent access
to data.

Common concepts include: - Shared locks - Exclusive locks

Locks help maintain consistency when multiple transactions access the
same data.

------------------------------------------------------------------------

# 85. Deadlock

A **deadlock** occurs when two or more transactions wait for resources
locked by each other, so none can continue.

Example:

``` text
Transaction A → locks Row 1 → waits for Row 2
Transaction B → locks Row 2 → waits for Row 1
```

------------------------------------------------------------------------

# 86. Race Condition

A **race condition** occurs when concurrent operations access or modify
shared data and the final result depends on the timing of those
operations.

------------------------------------------------------------------------

# 87. Normalization

**Normalization** is the process of organizing data into related tables
to reduce unnecessary redundancy and improve data integrity.

It helps reduce: - Insert anomalies - Update anomalies - Delete
anomalies

------------------------------------------------------------------------

# 88. First Normal Form (1NF)

A table is in 1NF when: - Values are atomic. - Each cell contains a
single value. - Repeating groups are eliminated.

------------------------------------------------------------------------

# 89. Second Normal Form (2NF)

A table is in 2NF when: - It is already in 1NF. - No non-key attribute
depends on only part of a composite key.

This removes **partial dependency**.

------------------------------------------------------------------------

# 90. Third Normal Form (3NF)

A table is in 3NF when: - It is already in 2NF. - It has no
inappropriate transitive dependency of non-key attributes on a key.

Simple idea:

``` text
Primary Key → Column A → Column B
```

If Column B depends on Column A rather than directly on the key, the
design may need decomposition.

------------------------------------------------------------------------

# 91. BCNF

**BCNF (Boyce-Codd Normal Form)** is a stronger form of 3NF.

Rule:

> Every determinant must be a candidate key.

------------------------------------------------------------------------

# 92. Denormalization

**Denormalization** is the intentional introduction of controlled
redundancy into a database to reduce expensive joins or improve read
performance.

### Normalization

``` text
Less redundancy
More related tables
```

### Denormalization

``` text
More controlled redundancy
Potentially fewer joins
Potentially faster reads
```

It should be used carefully because it can increase storage and create
consistency challenges.

------------------------------------------------------------------------

# 93. Indexing

**Indexing** is a technique used to speed up data retrieval by
maintaining an additional data structure that helps the database locate
rows efficiently.

Example:

``` sql
CREATE INDEX idx_employee_name
ON Employees(name);
```

### Advantages

-   Faster searches
-   Faster sorting in some cases
-   Can improve JOIN/filter performance

### Disadvantages

-   Requires additional storage
-   Can make `INSERT`, `UPDATE`, and `DELETE` more expensive

------------------------------------------------------------------------

# 94. B-tree Index

A B-tree is a common index structure used for efficient searches, range
queries, and ordering.

It is suitable for queries involving operators such as:

``` text
=
<
>
<=
>=
BETWEEN
```

------------------------------------------------------------------------

# 95. Hash Index

A hash index uses a hash-based structure and is primarily useful for
equality comparisons.

Conceptually:

``` text
WHERE id = 100
```

is a typical equality lookup.

------------------------------------------------------------------------

# 96. Clustered Index

A clustered index is an index organization where table data is
physically organized or maintained according to an index key.

The exact implementation differs between database systems.

**PostgreSQL note:** PostgreSQL does not use a traditional permanently
clustered-index storage model like SQL Server. PostgreSQL's `CLUSTER`
command can physically reorder a table according to an index, but that
ordering is not automatically maintained after subsequent changes.

------------------------------------------------------------------------

# 97. Non-Clustered Index

A non-clustered index is a separate index structure that stores indexed
values and references the corresponding table rows.

The exact implementation and terminology differ between database
systems.

------------------------------------------------------------------------

# 98. Query Optimization

Query optimization is the process of improving a query so that it
executes efficiently and uses appropriate database resources.

Common techniques: - Proper indexes - Selecting only required columns -
Filtering efficiently - Avoiding unnecessary joins - Checking execution
plans - Writing appropriate query conditions

------------------------------------------------------------------------

# 99. EXPLAIN

`EXPLAIN` shows the execution plan the database chooses for a query.

``` sql
EXPLAIN
SELECT *
FROM Employees
WHERE salary > 50000;
```

It helps understand how the database plans to execute the query.

------------------------------------------------------------------------

# 100. EXPLAIN ANALYZE

`EXPLAIN ANALYZE` executes the query and provides actual execution
statistics.

It can help compare estimated execution behavior with actual
performance.

------------------------------------------------------------------------

# 101. Database Scalability

Scalability is the ability of a database system to handle increasing
users, data, and workload while maintaining acceptable performance.

## Vertical Scaling

Increase the resources of a single server:

``` text
More CPU
More RAM
More Storage
```

## Horizontal Scaling

Add more servers and distribute the workload.

------------------------------------------------------------------------

# 102. Replication

Replication is the process of maintaining copies of database data on
multiple database servers.

It can be used for: - High availability - Read scaling - Disaster
recovery

------------------------------------------------------------------------

# 103. Backup

A database backup is a copy of database data that can be used to restore
the database after data loss, corruption, or system failure.

------------------------------------------------------------------------

# 104. Connection Pooling

Connection pooling maintains a pool of reusable database connections.

Instead of creating a new database connection for every operation,
applications can reuse existing connections.

### Benefits

-   Reduces connection creation overhead
-   Improves application performance
-   Helps manage database connection limits

------------------------------------------------------------------------

# 105. ODBC

**ODBC (Open Database Connectivity)** is a standard API that allows
applications to connect to different database systems through a common
interface.

It provides a standard way for applications to communicate with
databases using appropriate drivers.

------------------------------------------------------------------------

# 106. SQL Injection

SQL injection is a security vulnerability in which malicious input is
used to alter the intended SQL query.

It can potentially allow unauthorized data access or modification.

### Prevention

-   Parameterized queries
-   Prepared statements
-   Input validation
-   Least-privilege permissions
-   Avoid constructing SQL directly from untrusted input

------------------------------------------------------------------------

# 107. Role-Based Access Control (RBAC)

RBAC is a security model where permissions are assigned to roles and
users are assigned to those roles.

``` text
Permissions
     ↓
   Role
     ↓
   User
```

Example:

``` text
Admin  → SELECT, INSERT, UPDATE, DELETE
Staff  → SELECT, INSERT
Viewer → SELECT
```

------------------------------------------------------------------------

# 108. GRANT

`GRANT` gives privileges to users or roles.

Example:

``` sql
GRANT SELECT ON Employees TO analyst;
```

------------------------------------------------------------------------

# 109. REVOKE

`REVOKE` removes previously granted privileges.

Example:

``` sql
REVOKE SELECT ON Employees FROM analyst;
```

------------------------------------------------------------------------

# 110. Data Integrity

**Data integrity** means maintaining the accuracy, consistency, and
validity of data throughout its lifecycle.

Important forms include: - Entity integrity - Referential integrity -
Domain integrity

------------------------------------------------------------------------

# 111. Entity Integrity

Entity integrity ensures that each row can be uniquely identified.

A primary key provides the main mechanism for entity integrity.

------------------------------------------------------------------------

# 112. Domain Integrity

Domain integrity ensures that values stored in a column follow the
appropriate data type, range, format, or business rule.

Example:

``` sql
age INT CHECK (age >= 0)
```

------------------------------------------------------------------------

# 113. Database Administration

Database administration involves managing and maintaining databases.

Common DBA responsibilities: - User and role management - Permissions -
Backup and recovery - Performance monitoring - Index management -
Security - Database maintenance - Availability and reliability

------------------------------------------------------------------------

# 114. Database Design

Database design is the process of planning tables, columns, keys,
relationships, constraints, and other database objects before
implementation.

A good design aims for: - Data integrity - Appropriate normalization -
Minimal unnecessary redundancy - Efficient queries - Clear
relationships - Scalability

------------------------------------------------------------------------

# 115. ER Diagram

An **ER (Entity-Relationship) Diagram** is a graphical representation of
entities, attributes, and relationships in a database.

### Common ER Components

**Entity:** Represents a real-world object and is commonly drawn as a
rectangle.

**Attribute:** Describes an entity and is traditionally drawn as an
oval.

**Relationship:** Shows a connection between entities and is
traditionally represented by a diamond in classic ER notation.

------------------------------------------------------------------------

# 116. Three-Schema Architecture

The three-schema architecture separates a database system into three
levels of abstraction.

## External Level

Describes what individual users or applications see.

## Conceptual Level

Describes the complete logical structure of the database.

## Internal Level

Describes how data is physically stored.

``` text
External Level
      ↓
Conceptual Level
      ↓
Internal Level
```

------------------------------------------------------------------------

# 117. Data Independence

Data independence means that changes at one level of the database
architecture can be made with minimal impact on higher levels.

## Logical Data Independence

Changes to the conceptual schema do not require changes to external
views or applications in an ideal architecture.

## Physical Data Independence

Changes to the internal storage structure do not require changes to the
conceptual schema.

------------------------------------------------------------------------

# 118. Data Redundancy

Data redundancy means storing the same piece of data unnecessarily in
multiple places.

Excessive redundancy can cause: - Update anomalies - Insert anomalies -
Delete anomalies - Increased storage usage

Normalization helps reduce unnecessary redundancy.

------------------------------------------------------------------------

# 119. Anomalies

Database anomalies are problems caused by poorly designed or redundant
tables.

### Insert Anomaly

Difficulty inserting data because unrelated information is required.

### Update Anomaly

The same information must be updated in multiple rows.

### Delete Anomaly

Deleting one piece of information unintentionally removes another
important piece of information.

------------------------------------------------------------------------

# 120. Database Security

Database security protects data from unauthorized access, modification,
disclosure, and destruction.

Important techniques: - Authentication - Authorization - Roles and
permissions - Encryption - Parameterized queries - Backups - Auditing -
Least-privilege access

------------------------------------------------------------------------

# Quick Reviewer Revision

  -----------------------------------------------------------------------
  Topic                               One-Line Definition
  ----------------------------------- -----------------------------------
  Database                            Organized collection of data

  DBMS                                Software that manages databases

  RDBMS                               Database system based on related
                                      tables

  Non-Relational DB                   Database using flexible/non-tabular
                                      data models

  SQL                                 Language used to interact with
                                      relational databases

  PostgreSQL                          Open-source
                                      relational/object-relational
                                      database system

  Primary Key                         Uniquely identifies each row

  Foreign Key                         References a related key in another
                                      table

  Candidate Key                       Possible key eligible to become
                                      primary key

  Super Key                           Any key that uniquely identifies a
                                      row

  Composite Key                       Key containing multiple columns

  Constraint                          Rule that maintains data validity

  WHERE                               Filters rows

  ORDER BY                            Sorts results

  GROUP BY                            Creates groups

  HAVING                              Filters groups

  Aggregate Function                  Calculates across multiple rows

  Scalar Function                     Operates on individual values

  JOIN                                Combines related table data

  INNER JOIN                          Returns matching rows

  LEFT JOIN                           All left rows + matching right rows

  RIGHT JOIN                          All right rows + matching left rows

  FULL OUTER JOIN                     Matching + all unmatched rows

  CROSS JOIN                          Cartesian product

  NULL                                Missing/unknown value

  Subquery                            Query inside another query

  Correlated Subquery                 Depends on outer query

  EXISTS                              Checks whether rows exist

  UNION                               Combines results and removes
                                      duplicates

  UNION ALL                           Combines results including
                                      duplicates

  INTERSECT                           Returns common rows

  EXCEPT                              Returns rows only in first result

  CTE                                 Named temporary result for a
                                      statement

  Recursive CTE                       CTE that references itself

  Window Function                     Calculates across rows without
                                      collapsing them

  PARTITION BY                        Divides rows into window groups

  RANK                                Ranking with gaps after ties

  DENSE_RANK                          Ranking without gaps after ties

  ROW_NUMBER                          Unique sequential row number

  LAG                                 Accesses a previous row

  LEAD                                Accesses a following row

  View                                Virtual table based on a query

  Materialized View                   Physically stored query result

  UDF                                 User-created reusable function

  Stored Procedure                    Stored database program for
                                      performing tasks

  Trigger                             Automatically executes in response
                                      to events

  Transaction                         Group of operations treated as one
                                      unit

  ACID                                Reliable transaction properties

  Normalization                       Organizes data to reduce
                                      redundancy/anomalies

  1NF                                 Atomic values/no repeating groups

  2NF                                 Removes partial dependency

  3NF                                 Removes inappropriate transitive
                                      dependency

  BCNF                                Stronger form of 3NF

  Denormalization                     Controlled redundancy for practical
                                      performance benefits

  Index                               Data structure that can speed up
                                      retrieval

  Query Optimization                  Improving query execution
                                      efficiency

  EXPLAIN                             Shows query execution plan

  Scalability                         Ability to handle increasing
                                      workload

  Replication                         Maintaining copies of data

  Connection Pooling                  Reusing database connections

  ODBC                                Standard API for database
                                      connectivity

  SQL Injection                       Malicious manipulation of SQL
                                      through untrusted input

  RBAC                                Access control based on roles

  ER Diagram                          Graphical database model

  Data Independence                   Ability to change one schema level
                                      with minimal impact on others
  -----------------------------------------------------------------------

------------------------------------------------------------------------

# Reviewer Answer Formula

For most SQL theory questions, use this structure:

**1. Definition → 2. Key Points → 3. Example → 4. Real-world Use**

Example:

> **What is a CTE?**\
> A CTE, or Common Table Expression, is a named temporary result set
> defined using the `WITH` clause. It is mainly used to make complex
> queries easier to read and can also be used for recursive queries. For
> example, I can first create a CTE containing high-salary employees and
> then query that CTE in the main query.

This format helps you explain the **definition, working, and practical
purpose** instead of giving only a one-line definition.
