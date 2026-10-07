# SQL + Python Database — Complete Roadmap

## 1. SQL Fundamentals

* What is SQL?
* What is a database?
* DBMS
* RDBMS
* Relational database
* Tables
* Rows
* Columns
* Schema
* Entity
* Attribute
* Relationships
* SQL vs PostgreSQL/MySQL

### SQL command categories

* DDL
* DML
* DQL
* DCL
* TCL

### Basic commands

* `CREATE`
* `ALTER`
* `DROP`
* `TRUNCATE`
* `INSERT`
* `SELECT`
* `UPDATE`
* `DELETE`

---

# 2. SQL Data Types

* `INT`
* `BIGINT`
* `DECIMAL`
* `FLOAT`
* `CHAR`
* `VARCHAR`
* `TEXT`
* `BOOLEAN`
* `DATE`
* `TIME`
* `TIMESTAMP`
* `UUID`
* `JSON`
* `JSONB`
* `ARRAY`
* `BLOB` / binary data

Important comparisons:

* `CHAR` vs `VARCHAR`
* `INT` vs `BIGINT`
* `SERIAL` vs `BIGSERIAL`
* `JSON` vs `JSONB`

---

# 3. Keys and Constraints

### Keys

* Primary key
* Foreign key
* Candidate key
* Alternate key
* Super key
* Composite key
* Natural key
* Surrogate key
* Unique key

### Constraints

* `PRIMARY KEY`
* `FOREIGN KEY`
* `UNIQUE`
* `NOT NULL`
* `CHECK`
* `DEFAULT`

---

# 4. Basic SQL Queries

* `SELECT`
* `DISTINCT`
* `WHERE`
* `AND`
* `OR`
* `NOT`
* `IN`
* `NOT IN`
* `BETWEEN`
* `LIKE`
* `ILIKE`
* `IS NULL`
* `IS NOT NULL`

### Sorting

* `ORDER BY`
* `ASC`
* `DESC`

### Limiting

* `LIMIT`
* `OFFSET`

---

# 5. SQL Functions

### Aggregate functions

* `COUNT()`
* `SUM()`
* `AVG()`
* `MIN()`
* `MAX()`

### Scalar functions

* `LOWER()`
* `UPPER()`
* `LENGTH()`
* `TRIM()`
* `SUBSTRING()`
* `CONCAT()`
* `REPLACE()`
* `ROUND()`
* `CEIL()`
* `FLOOR()`
* `ABS()`

### Date functions

* `CURRENT_DATE`
* `CURRENT_TIME`
* `CURRENT_TIMESTAMP`
* Date arithmetic

### Conditional functions

* `CASE`
* `COALESCE()`
* `NULLIF()`

---

# 6. GROUP BY and HAVING

* `GROUP BY`
* `HAVING`
* Aggregation
* Grouping multiple columns
* `WHERE` vs `HAVING`

Practical problems:

* Average salary by department
* Number of employees per department
* Departments with more than 2 employees
* Highest average salary department

---

# 7. SQL Joins

* INNER JOIN
* LEFT JOIN
* RIGHT JOIN
* FULL OUTER JOIN
* CROSS JOIN
* SELF JOIN

Important:

* `JOIN` vs `UNION`
* `LEFT JOIN` vs `LEFT OUTER JOIN`
* Multiple joins
* Joining 3+ tables

---

# 8. UNION and Set Operations

* `UNION`
* `UNION ALL`
* `INTERSECT`
* `EXCEPT`

Understand **JOIN vs UNION** very clearly.

---

# 9. Subqueries

* What is a subquery?
* Scalar subquery
* Single-row subquery
* Multi-row subquery
* Subquery in `WHERE`
* Subquery in `FROM`
* Subquery in `SELECT`

### Important

* Correlated subquery
* Non-correlated subquery
* Correlated vs non-correlated

Practical:

* Employees earning above average
* Second-highest salary
* Department of least-paid employee
* Customers whose order is above average

---

# 10. CTE

* What is CTE?
* `WITH`
* CTE vs subquery
* Multiple CTEs
* Recursive CTE
* CTE with `SELECT`
* CTE with `UPDATE`
* CTE with `DELETE`

---

# 11. Window Functions

* `OVER()`
* `PARTITION BY`
* `ORDER BY`

Functions:

* `ROW_NUMBER()`
* `RANK()`
* `DENSE_RANK()`
* `LAG()`
* `LEAD()`
* `FIRST_VALUE()`
* `LAST_VALUE()`

Practicals:

* Second-highest employee per department
* Rank employees by salary
* Highest salary per department
* Running salary total
* Previous employee's salary

---

# 12. Database Design

* Entity
* Attribute
* Relationship
* Cardinality
* ER diagram
* One-to-one
* One-to-many
* Many-to-many
* Junction table

---

# 13. Normalization

* Data redundancy
* Insert anomaly
* Update anomaly
* Delete anomaly
* Functional dependency
* Partial dependency
* Transitive dependency

### Normal forms

* 1NF
* 2NF
* 3NF
* BCNF
* 4NF
* 5NF

Especially master:

**1NF → 2NF → 3NF → transitive dependency**

---

# 14. Views

* What is a view?
* Why use views?
* Creating views
* Updating views
* Dropping views
* Types of views
* Materialized views
* View vs table
* View vs materialized view

---

# 15. Indexing

* What is indexing?
* Why indexing?
* How indexes work
* Advantages
* Disadvantages
* B-tree index
* Hash index
* Composite index
* Unique index
* Partial index
* Functional/expression index
* Clustered index concept
* Non-clustered index concept
* When to use indexes
* When to avoid indexes

---

# 16. Query Optimization

* Query execution
* Query planner
* Query optimizer
* `EXPLAIN`
* `EXPLAIN ANALYZE`
* Sequential scan
* Index scan
* Query cost
* Query optimization techniques

---

# 17. Transactions

* What is a transaction?
* ACID properties
* Atomicity
* Consistency
* Isolation
* Durability
* `COMMIT`
* `ROLLBACK`
* `SAVEPOINT`
* TCL

### Concurrency

* Isolation levels
* Dirty read
* Non-repeatable read
* Phantom read
* Lost update
* Locks
* Deadlocks

---

# 18. Stored Procedures

* What is a stored procedure?
* Creating procedure
* Calling procedure
* Parameters
* IN/OUT parameters
* Procedure vs function
* Advantages
* Disadvantages

Practicals:

* Increase salary by 10%
* Increase salary for specific department
* Exclude Marketing
* Generate department salary report

---

# 19. SQL Functions / UDF

* User-defined function
* Scalar function
* Return values
* Function parameters
* Function vs procedure
* SQL function vs stored procedure

Practical:

> Calculate total salary of employees who aren't assigned to a project.

---

# 20. Triggers

* What is a trigger?
* Why triggers?
* BEFORE trigger
* AFTER trigger
* INSERT trigger
* UPDATE trigger
* DELETE trigger
* Row-level trigger
* Statement-level trigger
* Trigger function
* Advantages
* Disadvantages

Practical:

> Prevent salary from being less than 1000.

---

# 21. Referential Integrity

* Foreign key
* Parent/child tables
* `ON DELETE`
* `ON UPDATE`

Actions:

* `CASCADE`
* `SET NULL`
* `SET DEFAULT`
* `RESTRICT`
* `NO ACTION`

---

# 22. DELETE / TRUNCATE / DROP

Understand deeply:

```text
DELETE
TRUNCATE
DROP
```

Including:

* What gets removed?
* Can `WHERE` be used?
* Transaction behavior
* When to use each

---

# 23. SQL Security

* SQL injection
* How SQL injection happens
* Parameterized queries
* Prepared statements
* SQL escaping
* Why string concatenation is dangerous
* Principle of least privilege
* Database users/roles
* Permissions
* `GRANT`
* `REVOKE`

---

# 🐍 24. Python + SQL Connection ⭐⭐⭐⭐⭐

Now the **Python integration part** starts.

Learn:

* Why connect Python to a database?
* Database drivers
* DB-API 2.0
* Connection
* Cursor
* SQL execution
* Fetching results
* Transactions
* Closing connection

Basic flow:

```text
Python
   ↓
Database Driver
   ↓
Database Connection
   ↓
Cursor
   ↓
SQL Query
   ↓
Database
   ↓
Result
   ↓
Python
```

---

# 25. Python PostgreSQL Connection

For PostgreSQL, learn a driver such as:

* `psycopg`
* connection
* cursor
* `execute()`
* `fetchone()`
* `fetchmany()`
* `fetchall()`
* `commit()`
* `rollback()`
* `close()`

Basic structure:

```python
import psycopg

connection = psycopg.connect(
    "dbname=testdb user=postgres password=secret"
)

cursor = connection.cursor()

cursor.execute("SELECT * FROM employees")

rows = cursor.fetchall()

for row in rows:
    print(row)

cursor.close()
connection.close()
```

---

# 26. Python CRUD with SQL

Practice all four:

### Create

```python
cursor.execute(
    "INSERT INTO employees (name, salary) VALUES (%s, %s)",
    ("John", 50000)
)
```

### Read

```python
cursor.execute("SELECT * FROM employees")
rows = cursor.fetchall()
```

### Update

```python
cursor.execute(
    "UPDATE employees SET salary = %s WHERE id = %s",
    (60000, 1)
)
```

### Delete

```python
cursor.execute(
    "DELETE FROM employees WHERE id = %s",
    (1,)
)
```

---

# 27. Parameterized Queries ⭐⭐⭐⭐⭐

This is extremely important.

Never:

```python
query = f"SELECT * FROM users WHERE username = '{username}'"
```

Instead:

```python
cursor.execute(
    "SELECT * FROM users WHERE username = %s",
    (username,)
)
```

Understand:

* Parameterized query
* Prepared statement
* SQL injection
* User input
* Safe query construction

---

# 28. Python Transactions

Learn:

```python
connection.commit()
connection.rollback()
```

Understand:

```text
BEGIN
 ↓
SQL operations
 ↓
Success?
 ├── YES → COMMIT
 └── NO  → ROLLBACK
```

Practical:

> Transfer money from Account A to Account B.

Both updates must succeed together.

---

# 29. Python Exception Handling with Database

Combine:

```python
try:
    ...
except Exception as e:
    ...
finally:
    ...
```

Understand:

* Database errors
* Connection errors
* SQL errors
* Rollback on failure
* Closing resources

---

# 30. Context Managers

Learn Python's:

```python
with
```

for database resources.

Understand:

* Why `with` is useful
* Automatic cleanup
* Connection context
* Cursor context
* Exception handling

---

# 31. Python Database Modules / Drivers

Know the difference between:

* `sqlite3`
* PostgreSQL drivers
* MySQL drivers
* ODBC
* DB-API

### SQLite

Python has built-in:

```python
import sqlite3
```

### PostgreSQL

Use a PostgreSQL driver such as `psycopg`.

### MySQL

Common Python drivers include:

* `mysql-connector-python`
* `PyMySQL`

---

# 32. Python + SQL Architecture

Understand:

```text
Python Application
       ↓
Database Driver
       ↓
Connection
       ↓
Cursor
       ↓
SQL
       ↓
Database
```

And concepts:

* Client
* Server
* Connection
* Cursor
* Query
* Result set
* Transaction

---

# 33. Connection Management

* Connection pooling
* Why connection pooling is needed
* Opening/closing connections
* Reusing connections
* Connection limits
* Connection timeout
* Database credentials
* Environment variables

---

# 34. Python + SQL Security

Master:

* Parameterized queries
* SQL injection
* Password hashing
* Never storing plaintext passwords
* Environment variables
* Database permissions
* Least privilege
* Secure connection credentials

---

# 35. Python + SQL Practical Projects

### Beginner

1. Student database
2. Employee database
3. Customer database
4. Library database

### Intermediate

5. Employee management system
6. Student management system
7. Bank account system
8. Inventory management system

### Advanced

9. Python + PostgreSQL CRUD application
10. Transaction-based money transfer
11. Employee salary management
12. Customer order management
13. Python reporting system using CTE/window functions
14. Python application using stored procedures
15. Python application using transactions and rollback

---
