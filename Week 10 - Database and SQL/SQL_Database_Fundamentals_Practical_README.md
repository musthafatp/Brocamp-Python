# SQL & Database Fundamentals --- Complete Practical README

A practical command reference for learning and practicing **Database +
SQL Fundamentals with PostgreSQL**.

------------------------------------------------------------------------

# 1. Database Commands

## Create Database

``` sql
CREATE DATABASE practice;
```

## List Databases

``` text
\l
```

## Connect to Database

``` text
\c practice
```

## Drop Database

``` sql
DROP DATABASE practice;
```

------------------------------------------------------------------------

# 2. PostgreSQL Useful Commands

## List Tables

``` text
\dt
```

## Describe Table

``` text
\d Students
```

## List Schemas

``` text
\dn
```

## List Users/Roles

``` text
\du
```

## Quit PostgreSQL

``` text
\q
```

------------------------------------------------------------------------

# 3. CREATE TABLE

``` sql
CREATE TABLE Students (
    student_id SERIAL PRIMARY KEY,
    student_name VARCHAR(100) NOT NULL,
    student_email VARCHAR(150) UNIQUE,
    student_age INT,
    city VARCHAR(50)
);
```

------------------------------------------------------------------------

# 4. Common PostgreSQL Data Types

``` text
INT
BIGINT
DECIMAL
NUMERIC
VARCHAR
TEXT
BOOLEAN
DATE
TIME
TIMESTAMP
JSON
JSONB
ARRAY
UUID
SERIAL
```

## Example

``` sql
CREATE TABLE Example (
    id SERIAL PRIMARY KEY,
    name VARCHAR(100),
    price DECIMAL(10,2),
    active BOOLEAN,
    birth_date DATE,
    data JSONB,
    tags TEXT[]
);
```

------------------------------------------------------------------------

# 5. INSERT

## Insert One Row

``` sql
INSERT INTO Students
(student_name, student_email, student_age, city)
VALUES
('Ali', 'ali@gmail.com', 20, 'Kozhikode');
```

## Insert Multiple Rows

``` sql
INSERT INTO Students
(student_name, student_email, student_age, city)
VALUES
('Ali', 'ali@gmail.com', 20, 'Kozhikode'),
('Ahmed', 'ahmed@gmail.com', 21, 'Kannur'),
('John', 'john@gmail.com', 22, 'Kochi');
```

## Insert NULL

``` sql
INSERT INTO Students
(student_name, student_email, student_age, city)
VALUES
('Rahul', NULL, NULL, 'Kochi');
```

------------------------------------------------------------------------

# 6. SELECT

## Select Everything

``` sql
SELECT *
FROM Students;
```

## Select Specific Columns

``` sql
SELECT student_name, student_age
FROM Students;
```

## Alias

``` sql
SELECT student_name AS name
FROM Students;
```

------------------------------------------------------------------------

# 7. WHERE

``` sql
SELECT *
FROM Students
WHERE student_age > 20;
```

``` sql
SELECT *
FROM Students
WHERE city = 'Kochi';
```

## Comparison Operators

``` text
=
!=
<>
>
<
>=
<=
```

------------------------------------------------------------------------

# 8. AND / OR / NOT

## AND

``` sql
SELECT *
FROM Students
WHERE student_age > 18
AND city = 'Kochi';
```

## OR

``` sql
SELECT *
FROM Students
WHERE city = 'Kochi'
OR city = 'Kannur';
```

## NOT

``` sql
SELECT *
FROM Students
WHERE NOT city = 'Kochi';
```

------------------------------------------------------------------------

# 9. BETWEEN

``` sql
SELECT *
FROM Students
WHERE student_age BETWEEN 18 AND 25;
```

------------------------------------------------------------------------

# 10. IN

``` sql
SELECT *
FROM Students
WHERE city IN ('Kochi', 'Kannur', 'Kozhikode');
```

------------------------------------------------------------------------

# 11. LIKE

## Starts With

``` sql
SELECT *
FROM Students
WHERE student_name LIKE 'A%';
```

## Ends With

``` sql
SELECT *
FROM Students
WHERE student_name LIKE '%i';
```

## Contains

``` sql
SELECT *
FROM Students
WHERE student_name LIKE '%ah%';
```

## One Character

``` sql
SELECT *
FROM Students
WHERE student_name LIKE '_li';
```

------------------------------------------------------------------------

# 12. NULL

## Check NULL

``` sql
SELECT *
FROM Students
WHERE student_email IS NULL;
```

## Check NOT NULL

``` sql
SELECT *
FROM Students
WHERE student_email IS NOT NULL;
```

### Important

Do not use:

``` sql
WHERE student_email = NULL;
```

Use:

``` sql
WHERE student_email IS NULL;
```

------------------------------------------------------------------------

# 13. DISTINCT

``` sql
SELECT DISTINCT city
FROM Students;
```

------------------------------------------------------------------------

# 14. ORDER BY

## Ascending

``` sql
SELECT *
FROM Students
ORDER BY student_age ASC;
```

## Descending

``` sql
SELECT *
FROM Students
ORDER BY student_age DESC;
```

## Multiple Columns

``` sql
SELECT *
FROM Students
ORDER BY city ASC, student_age DESC;
```

------------------------------------------------------------------------

# 15. LIMIT and OFFSET

## LIMIT

``` sql
SELECT *
FROM Students
LIMIT 5;
```

## OFFSET

``` sql
SELECT *
FROM Students
LIMIT 5 OFFSET 10;
```

------------------------------------------------------------------------

# 16. UPDATE

## Update One Row

``` sql
UPDATE Students
SET city = 'Kochi'
WHERE student_id = 1;
```

## Update Multiple Columns

``` sql
UPDATE Students
SET city = 'Kochi',
    student_age = 21
WHERE student_id = 1;
```

### Important

Without `WHERE`, every row can be updated.

------------------------------------------------------------------------

# 17. DELETE

## Delete Specific Row

``` sql
DELETE FROM Students
WHERE student_id = 5;
```

## Delete Using Condition

``` sql
DELETE FROM Students
WHERE student_age < 18;
```

## Delete All Rows

``` sql
DELETE FROM Students;
```

------------------------------------------------------------------------

# 18. TRUNCATE

## Remove All Rows

``` sql
TRUNCATE TABLE Students;
```

## Reset SERIAL Identity

``` sql
TRUNCATE TABLE Students RESTART IDENTITY;
```

## Multiple Tables

``` sql
TRUNCATE TABLE Students, Courses;
```

------------------------------------------------------------------------

# 19. ALTER TABLE

## Add Column

``` sql
ALTER TABLE Students
ADD COLUMN phone_number VARCHAR(15);
```

## Drop Column

``` sql
ALTER TABLE Students
DROP COLUMN phone_number;
```

## Rename Column

``` sql
ALTER TABLE Students
RENAME COLUMN student_name TO name;
```

## Rename Table

``` sql
ALTER TABLE Students
RENAME TO Students_New;
```

## Change Data Type

``` sql
ALTER TABLE Students
ALTER COLUMN student_age TYPE BIGINT;
```

## Set Default

``` sql
ALTER TABLE Students
ALTER COLUMN city SET DEFAULT 'Kozhikode';
```

## Remove Default

``` sql
ALTER TABLE Students
ALTER COLUMN city DROP DEFAULT;
```

## Set NOT NULL

``` sql
ALTER TABLE Students
ALTER COLUMN student_name SET NOT NULL;
```

## Remove NOT NULL

``` sql
ALTER TABLE Students
ALTER COLUMN student_name DROP NOT NULL;
```

------------------------------------------------------------------------

# 20. Constraints

The main constraints are:

``` text
PRIMARY KEY
FOREIGN KEY
UNIQUE
NOT NULL
CHECK
DEFAULT
```

------------------------------------------------------------------------

# 21. PRIMARY KEY

## During Table Creation

``` sql
CREATE TABLE Students (
    student_id SERIAL PRIMARY KEY,
    student_name VARCHAR(100)
);
```

## Add Primary Key Later

``` sql
ALTER TABLE Students
ADD CONSTRAINT student_pk
PRIMARY KEY (student_id);
```

A primary key:

-   Uniquely identifies a row.
-   Cannot contain NULL.
-   A table normally has one primary key constraint.

------------------------------------------------------------------------

# 22. UNIQUE

## During Table Creation

``` sql
CREATE TABLE Students (
    student_id SERIAL PRIMARY KEY,
    student_email VARCHAR(150) UNIQUE
);
```

## Add UNIQUE Later

``` sql
ALTER TABLE Students
ADD CONSTRAINT student_email_unique
UNIQUE (student_email);
```

------------------------------------------------------------------------

# 23. CHECK

``` sql
ALTER TABLE Students
ADD CONSTRAINT age_check
CHECK (student_age >= 18);
```

Another example:

``` sql
CREATE TABLE Employees (
    id SERIAL PRIMARY KEY,
    salary NUMERIC CHECK (salary > 0)
);
```

------------------------------------------------------------------------

# 24. DEFAULT

``` sql
ALTER TABLE Students
ALTER COLUMN city SET DEFAULT 'Kozhikode';
```

Now if city is not provided:

``` sql
INSERT INTO Students
(student_name, student_email, student_age)
VALUES
('Aisha', 'aisha@gmail.com', 20);
```

The city will use the default value.

------------------------------------------------------------------------

# 25. DROP CONSTRAINT

``` sql
ALTER TABLE Students
DROP CONSTRAINT age_check;
```

------------------------------------------------------------------------

# 26. FOREIGN KEY

A foreign key creates a relationship between tables.

## Parent Table

``` sql
CREATE TABLE Departments (
    department_id SERIAL PRIMARY KEY,
    department_name VARCHAR(100)
);
```

## Child Table

``` sql
CREATE TABLE Employees (
    employee_id SERIAL PRIMARY KEY,
    employee_name VARCHAR(100),
    department_id INT,
    FOREIGN KEY (department_id)
    REFERENCES Departments(department_id)
);
```

The `department_id` in `Employees` refers to:

``` text
Departments.department_id
```

------------------------------------------------------------------------

# 27. Add FOREIGN KEY Later

``` sql
ALTER TABLE Employees
ADD CONSTRAINT employee_department_fk
FOREIGN KEY (department_id)
REFERENCES Departments(department_id);
```

------------------------------------------------------------------------

# 28. FOREIGN KEY Actions

``` sql
FOREIGN KEY (department_id)
REFERENCES Departments(department_id)
ON DELETE CASCADE
ON UPDATE CASCADE;
```

Common actions:

``` text
ON DELETE CASCADE
ON DELETE SET NULL
ON DELETE RESTRICT
ON DELETE NO ACTION

ON UPDATE CASCADE
```

## CASCADE

If the parent row is deleted, related child rows can also be deleted.

## SET NULL

The foreign key value in the child becomes NULL.

## RESTRICT

Prevents the parent operation when dependent rows exist.

------------------------------------------------------------------------

# 29. AGGREGATE FUNCTIONS

## COUNT

``` sql
SELECT COUNT(*)
FROM Students;
```

## COUNT Specific Column

``` sql
SELECT COUNT(student_email)
FROM Students;
```

## SUM

``` sql
SELECT SUM(student_age)
FROM Students;
```

## AVG

``` sql
SELECT AVG(student_age)
FROM Students;
```

## MIN

``` sql
SELECT MIN(student_age)
FROM Students;
```

## MAX

``` sql
SELECT MAX(student_age)
FROM Students;
```

------------------------------------------------------------------------

# 30. GROUP BY

## Count Students by City

``` sql
SELECT city, COUNT(*)
FROM Students
GROUP BY city;
```

## Average Age by City

``` sql
SELECT city, AVG(student_age)
FROM Students
GROUP BY city;
```

------------------------------------------------------------------------

# 31. HAVING

``` sql
SELECT city, COUNT(*)
FROM Students
GROUP BY city
HAVING COUNT(*) > 2;
```

### WHERE vs HAVING

``` text
WHERE
→ Filters individual rows before grouping.

HAVING
→ Filters groups after GROUP BY.
```

------------------------------------------------------------------------

# 32. JOINS

Assume:

``` text
Students
----------------
student_id
student_name
course_id
```

``` text
Courses
----------------
course_id
course_name
```

------------------------------------------------------------------------

# 33. INNER JOIN

Returns matching rows from both tables.

``` sql
SELECT *
FROM Students
INNER JOIN Courses
ON Students.course_id = Courses.course_id;
```

------------------------------------------------------------------------

# 34. LEFT JOIN

Returns all rows from the left table and matching rows from the right
table.

``` sql
SELECT *
FROM Students
LEFT JOIN Courses
ON Students.course_id = Courses.course_id;
```

------------------------------------------------------------------------

# 35. RIGHT JOIN

Returns all rows from the right table and matching rows from the left
table.

``` sql
SELECT *
FROM Students
RIGHT JOIN Courses
ON Students.course_id = Courses.course_id;
```

------------------------------------------------------------------------

# 36. FULL OUTER JOIN

Returns matching and non-matching rows from both tables.

``` sql
SELECT *
FROM Students
FULL OUTER JOIN Courses
ON Students.course_id = Courses.course_id;
```

------------------------------------------------------------------------

# 37. CROSS JOIN

Creates combinations of every row from both tables.

``` sql
SELECT *
FROM Students
CROSS JOIN Courses;
```

If Students has 5 rows and Courses has 3 rows:

``` text
5 × 3 = 15 rows
```

------------------------------------------------------------------------

# 38. JOIN with Aliases

``` sql
SELECT
    s.student_name,
    c.course_name
FROM Students s
JOIN Courses c
ON s.course_id = c.course_id;
```

------------------------------------------------------------------------

# 39. SELF JOIN

A table can be joined with itself.

Example:

``` text
Employees
----------------
employee_id
employee_name
manager_id
```

``` sql
SELECT
    e.employee_name,
    m.employee_name AS manager
FROM Employees e
JOIN Employees m
ON e.manager_id = m.employee_id;
```

------------------------------------------------------------------------

# 40. SUBQUERIES

## Subquery with WHERE

``` sql
SELECT *
FROM Students
WHERE student_age >
(
    SELECT AVG(student_age)
    FROM Students
);
```

## Subquery with IN

``` sql
SELECT *
FROM Students
WHERE city IN
(
    SELECT city
    FROM Students
    WHERE student_age > 20
);
```

------------------------------------------------------------------------

# 41. EXISTS

``` sql
SELECT *
FROM Students s
WHERE EXISTS (
    SELECT 1
    FROM Courses c
    WHERE c.course_id = s.course_id
);
```

------------------------------------------------------------------------

# 42. CASE

``` sql
SELECT
    student_name,
    student_age,
    CASE
        WHEN student_age >= 18 THEN 'Adult'
        ELSE 'Minor'
    END AS status
FROM Students;
```

------------------------------------------------------------------------

# 43. COALESCE

Used to replace NULL with another value.

``` sql
SELECT
    student_name,
    COALESCE(city, 'Unknown')
FROM Students;
```

------------------------------------------------------------------------

# 44. STRING FUNCTIONS

## UPPER

``` sql
SELECT UPPER(student_name)
FROM Students;
```

## LOWER

``` sql
SELECT LOWER(student_name)
FROM Students;
```

## LENGTH

``` sql
SELECT LENGTH(student_name)
FROM Students;
```

## CONCAT

``` sql
SELECT CONCAT(student_name, ' - ', city)
FROM Students;
```

------------------------------------------------------------------------

# 45. DATE / TIME

## Current Date

``` sql
SELECT CURRENT_DATE;
```

## Current Timestamp

``` sql
SELECT CURRENT_TIMESTAMP;
```

## NOW

``` sql
SELECT NOW();
```

------------------------------------------------------------------------

# 46. TRANSACTIONS

A transaction groups multiple operations into one logical unit.

## BEGIN

``` sql
BEGIN;
```

## Example Operation

``` sql
UPDATE Students
SET city = 'Kochi'
WHERE student_id = 1;
```

## COMMIT

Save the transaction permanently:

``` sql
COMMIT;
```

## ROLLBACK

Undo the transaction:

``` sql
ROLLBACK;
```

------------------------------------------------------------------------

# 47. SAVEPOINT

``` sql
BEGIN;
```

``` sql
UPDATE Students
SET city = 'Kochi'
WHERE student_id = 1;
```

``` sql
SAVEPOINT point1;
```

``` sql
UPDATE Students
SET city = 'Kannur'
WHERE student_id = 2;
```

Rollback only to the savepoint:

``` sql
ROLLBACK TO point1;
```

Finish the transaction:

``` sql
COMMIT;
```

------------------------------------------------------------------------

# 48. TRANSACTION COMMAND SUMMARY

``` text
BEGIN
→ Start transaction.

COMMIT
→ Save transaction permanently.

ROLLBACK
→ Undo transaction.

SAVEPOINT
→ Create a point inside a transaction.

ROLLBACK TO SAVEPOINT
→ Return to that point.
```

------------------------------------------------------------------------

# 49. INDEXING

Indexes help the database find rows faster for suitable queries.

## Create Index

``` sql
CREATE INDEX idx_student_email
ON Students(student_email);
```

## Multi-Column Index

``` sql
CREATE INDEX idx_city_age
ON Students(city, student_age);
```

## Unique Index

``` sql
CREATE UNIQUE INDEX idx_unique_email
ON Students(student_email);
```

## Drop Index

``` sql
DROP INDEX idx_student_email;
```

------------------------------------------------------------------------

# 50. EXPLAIN

Used to inspect how PostgreSQL plans to execute a query.

``` sql
EXPLAIN
SELECT *
FROM Students
WHERE student_email = 'ali@gmail.com';
```

For actual execution statistics:

``` sql
EXPLAIN ANALYZE
SELECT *
FROM Students
WHERE student_email = 'ali@gmail.com';
```

------------------------------------------------------------------------

# 51. VIEWS

A view is a stored query that can be queried like a table.

## Create View

``` sql
CREATE VIEW adult_students AS
SELECT *
FROM Students
WHERE student_age >= 18;
```

## Use View

``` sql
SELECT *
FROM adult_students;
```

## Drop View

``` sql
DROP VIEW adult_students;
```

------------------------------------------------------------------------

# 52. UNION

Combines the results of two compatible SELECT queries and removes
duplicates.

``` sql
SELECT city FROM Students
UNION
SELECT city FROM Employees;
```

## UNION ALL

Keeps duplicates.

``` sql
SELECT city FROM Students
UNION ALL
SELECT city FROM Employees;
```

------------------------------------------------------------------------

# 53. USERS / ROLES

## Create User

``` sql
CREATE USER app_user WITH PASSWORD 'password';
```

## Create Role

``` sql
CREATE ROLE developer;
```

## GRANT

``` sql
GRANT SELECT, INSERT
ON Students
TO app_user;
```

## REVOKE

``` sql
REVOKE INSERT
ON Students
FROM app_user;
```

------------------------------------------------------------------------

# 54. SQL QUERY EXECUTION ORDER

Although we usually write SQL like this:

``` sql
SELECT
FROM
JOIN
WHERE
GROUP BY
HAVING
ORDER BY
LIMIT;
```

The conceptual processing order is approximately:

``` text
FROM
JOIN
WHERE
GROUP BY
HAVING
SELECT
ORDER BY
LIMIT
```

Example:

``` sql
SELECT city, COUNT(*) AS total
FROM Students
WHERE student_age >= 18
GROUP BY city
HAVING COUNT(*) > 2
ORDER BY total DESC
LIMIT 5;
```

------------------------------------------------------------------------

# 55. DELETE vs TRUNCATE vs DROP

  Command      Removes Rows   Removes Table   WHERE
  ---------- -------------- --------------- -------
  DELETE                Yes              No     Yes
  TRUNCATE              Yes              No      No
  DROP                  Yes             Yes      No

## DELETE

``` sql
DELETE FROM Students
WHERE student_id = 1;
```

Deletes selected rows.

## TRUNCATE

``` sql
TRUNCATE TABLE Students;
```

Removes all rows quickly while keeping the table structure.

## DROP

``` sql
DROP TABLE Students;
```

Removes the table itself.

------------------------------------------------------------------------

# 56. PRIMARY KEY vs FOREIGN KEY

  Feature                    PRIMARY KEY                  FOREIGN KEY
  -------------------------- ---------------------------- -------------------------------
  Purpose                    Identifies a row             Creates relationship
  Unique                     Yes                          Not necessarily
  NULL                       Not allowed                  Can be NULL unless restricted
  References another table   No                           Usually yes
  Number per table           One primary key constraint   Can have multiple

------------------------------------------------------------------------

# 57. SQL FUNDAMENTALS PRACTICAL CHECKLIST

Use this as your practice checklist:

``` text
[ ] CREATE DATABASE
[ ] CONNECT DATABASE
[ ] CREATE TABLE
[ ] PostgreSQL Data Types
[ ] INSERT
[ ] SELECT
[ ] WHERE
[ ] AND
[ ] OR
[ ] NOT
[ ] BETWEEN
[ ] IN
[ ] LIKE
[ ] IS NULL
[ ] IS NOT NULL
[ ] DISTINCT
[ ] ORDER BY
[ ] LIMIT
[ ] OFFSET
[ ] UPDATE
[ ] DELETE
[ ] TRUNCATE
[ ] ALTER TABLE
[ ] PRIMARY KEY
[ ] FOREIGN KEY
[ ] UNIQUE
[ ] NOT NULL
[ ] CHECK
[ ] DEFAULT
[ ] DROP CONSTRAINT
[ ] ON DELETE
[ ] ON UPDATE
[ ] COUNT
[ ] SUM
[ ] AVG
[ ] MIN
[ ] MAX
[ ] GROUP BY
[ ] HAVING
[ ] INNER JOIN
[ ] LEFT JOIN
[ ] RIGHT JOIN
[ ] FULL OUTER JOIN
[ ] CROSS JOIN
[ ] SELF JOIN
[ ] JOIN ALIASES
[ ] SUBQUERY
[ ] EXISTS
[ ] CASE
[ ] COALESCE
[ ] STRING FUNCTIONS
[ ] DATE / TIME
[ ] BEGIN
[ ] COMMIT
[ ] ROLLBACK
[ ] SAVEPOINT
[ ] INDEX
[ ] UNIQUE INDEX
[ ] EXPLAIN
[ ] EXPLAIN ANALYZE
[ ] VIEW
[ ] UNION
[ ] UNION ALL
[ ] CREATE USER
[ ] CREATE ROLE
[ ] GRANT
[ ] REVOKE
[ ] PostgreSQL psql commands
```

------------------------------------------------------------------------

# 58. Recommended Practical Order

Practice the topics in this order:

``` text
1. Database
   ↓
2. Tables
   ↓
3. Data Types
   ↓
4. Constraints
   ↓
5. INSERT
   ↓
6. SELECT
   ↓
7. Filtering
   ↓
8. Sorting / Limiting
   ↓
9. UPDATE
   ↓
10. DELETE / TRUNCATE / DROP
   ↓
11. ALTER TABLE
   ↓
12. PRIMARY KEY
   ↓
13. FOREIGN KEY
   ↓
14. Aggregate Functions
   ↓
15. GROUP BY / HAVING
   ↓
16. JOINS
   ↓
17. Subqueries
   ↓
18. CASE / COALESCE
   ↓
19. Transactions
   ↓
20. Indexing
   ↓
21. Views
   ↓
22. UNION
   ↓
23. Users / Roles
   ↓
24. EXPLAIN
```

------------------------------------------------------------------------

# 59. Important Database Theory Topics

The practical commands above should be studied together with these
database fundamentals:

``` text
Database
DBMS
RDBMS
SQL
SQL vs NoSQL
DBMS vs RDBMS
Database Architecture
Three-Schema Architecture
External Schema
Conceptual Schema
Internal Schema
Data Independence
ER Diagram
Entity
Attribute
Relationship
Cardinality
Primary Key
Foreign Key
Candidate Key
Super Key
Composite Key
Constraints
Normalization
1NF
2NF
3NF
BCNF
Denormalization
ACID Properties
Atomicity
Consistency
Isolation
Durability
Transactions
CAP Theorem
Indexes
B-Tree Index
Query Performance
```

------------------------------------------------------------------------

# 60. Final SQL Fundamentals Map

``` text
DATABASE FUNDAMENTALS
│
├── DBMS / RDBMS
├── SQL / NoSQL
├── Database Architecture
├── Three-Schema Architecture
├── ER Diagram
├── Keys
├── Constraints
├── Normalization
├── ACID
└── CAP Theorem
        │
        ↓
SQL PRACTICAL
│
├── Database
├── Tables
├── Data Types
├── CREATE
├── INSERT
├── SELECT
├── WHERE
├── UPDATE
├── DELETE
├── TRUNCATE
├── ALTER
├── Constraints
├── Foreign Keys
├── Aggregate Functions
├── GROUP BY
├── HAVING
├── JOINS
├── Subqueries
├── CASE
├── Transactions
├── Indexing
├── Views
├── UNION
├── Users / Roles
└── EXPLAIN
```

------------------------------------------------------------------------

# Final Goal

By completing this practical checklist, you should be able to:

-   Create and manage PostgreSQL databases.
-   Create and modify tables.
-   Insert, retrieve, update, and delete data.
-   Use constraints correctly.
-   Build relationships using foreign keys.
-   Write filtering and sorting queries.
-   Perform aggregation and grouping.
-   Join multiple tables.
-   Write subqueries.
-   Use transactions and savepoints.
-   Create and understand indexes.
-   Create and use views.
-   Understand query execution and `EXPLAIN`.
-   Manage basic PostgreSQL users and permissions.
-   Connect practical SQL commands with database fundamentals such as
    keys, normalization, ACID, and database architecture.
