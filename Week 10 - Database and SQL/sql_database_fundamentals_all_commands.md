# SQL & Database Fundamentals — Complete Command Collection

> Every fenced SQL command block from the original Day 6–Day 11 compilation is included below, in the same order and without removing or rewriting the SQL commands. Duplicate commands are intentionally preserved.

**Total SQL code blocks preserved: 152**

## 2. Create — INSERT

### Command Block 1

```sql
CREATE TABLE employees (
    id INT PRIMARY KEY,
    name VARCHAR(100),
    age INT,
    department VARCHAR(100),
    salary DECIMAL(10,2)
);
```

### Command Block 2

```sql
INSERT INTO employees
(id, name, age, department, salary)
VALUES
(1, 'Rahul', 25, 'IT', 40000);
```

### Command Block 3

```sql
INSERT INTO employees
(id, name, age, department, salary)
VALUES
(2, 'Anu', 24, 'HR', 35000),
(3, 'Ahmed', 28, 'IT', 50000),
(4, 'Sara', 26, 'Finance', 45000),
(5, 'John', 30, 'IT', 60000);
```

## Get everything

### Command Block 4

```sql
SELECT * FROM employees;
```

## Get specific columns

### Command Block 5

```sql
SELECT name, salary
FROM employees;
```

## 4. WHERE

### Command Block 6

```sql
SELECT *
FROM employees
WHERE department = 'IT';
```

## Example

### Command Block 7

```sql
SELECT *
FROM employees
WHERE age > 25;
```

### Command Block 8

```sql
SELECT *
FROM employees
WHERE salary >= 50000;
```

## 6. AND

### Command Block 9

```sql
SELECT *
FROM employees
WHERE department = 'IT'
AND salary > 45000;
```

## 7. OR

### Command Block 10

```sql
SELECT *
FROM employees
WHERE department = 'IT'
OR department = 'HR';
```

## 8. NOT

### Command Block 11

```sql
SELECT *
FROM employees
WHERE NOT department = 'IT';
```

## 9. UPDATE

### Command Block 12

```sql
UPDATE employees
SET salary = 55000
WHERE id = 3;
```

## ⚠️ Important

### Command Block 13

```sql
UPDATE employees
SET salary = 55000;
```

## 10. DELETE

### Command Block 14

```sql
DELETE FROM employees
WHERE id = 5;
```

## ⚠️ Dangerous

### Command Block 15

```sql
DELETE FROM employees;
```

## Lowest → Highest

### Command Block 16

```sql
SELECT *
FROM employees
ORDER BY salary ASC;
```

## Highest → Lowest

### Command Block 17

```sql
SELECT *
FROM employees
ORDER BY salary DESC;
```

## 12. LIMIT

### Command Block 18

```sql
SELECT *
FROM employees
LIMIT 3;
```

## Highest salaries

### Command Block 19

```sql
SELECT *
FROM employees
ORDER BY salary DESC
LIMIT 3;
```

## 13. DISTINCT

### Command Block 20

```sql
SELECT DISTINCT department
FROM employees;
```

## 🧠 SQL Query Flow

### Command Block 21

```sql
SELECT name, salary
FROM employees
WHERE salary > 40000
ORDER BY salary DESC
LIMIT 3;
```

## Task 1

### Command Block 22

```sql
SELECT * FROM employees;
```

## 1.

### Command Block 23

```sql
SELECT *
FROM employees
WHERE department = 'IT'
AND salary > 45000;
```

## 2.

### Command Block 24

```sql
SELECT *
FROM employees
WHERE department = 'HR'
OR department = 'Finance';
```

## 3.

### Command Block 25

```sql
SELECT *
FROM employees
ORDER BY salary DESC
LIMIT 5;
```

## 4.

### Command Block 26

```sql
UPDATE employees
SET salary = salary + 5000
WHERE id = 2;
```

## 🎯 Day 6 Success Condition

### Command Block 27

```sql
SELECT *
FROM employees
WHERE department = 'IT'
AND salary > 50000
ORDER BY salary DESC
LIMIT 3;
```

## Count all employees

### Command Block 28

```sql
SELECT COUNT(*)
FROM employees;
```

## Count employees in IT

### Command Block 29

```sql
SELECT COUNT(*)
FROM employees
WHERE department = 'IT';
```

## 3. SUM()

### Command Block 30

```sql
SELECT SUM(salary)
FROM employees;
```

## 4. AVG()

### Command Block 31

```sql
SELECT AVG(salary)
FROM employees;
```

## 5. MIN()

### Command Block 32

```sql
SELECT MIN(salary)
FROM employees;
```

## 6. MAX()

### Command Block 33

```sql
SELECT MAX(salary)
FROM employees;
```

## 7. Using Multiple Aggregate Functions

### Command Block 34

```sql
SELECT
    COUNT(*) AS employee_count,
    SUM(salary) AS total_salary,
    AVG(salary) AS average_salary,
    MIN(salary) AS minimum_salary,
    MAX(salary) AS maximum_salary
FROM employees;
```

## 8. What is GROUP BY?

### Command Block 35

```sql
SELECT department
FROM employees
GROUP BY department;
```

## 9. GROUP BY + COUNT()

### Command Block 36

```sql
SELECT
    department,
    COUNT(*) AS employee_count
FROM employees
GROUP BY department;
```

## 10. GROUP BY + AVG()

### Command Block 37

```sql
SELECT
    department,
    AVG(salary) AS average_salary
FROM employees
GROUP BY department;
```

## 11. GROUP BY + SUM()

### Command Block 38

```sql
SELECT
    department,
    SUM(salary) AS total_salary
FROM employees
GROUP BY department;
```

## 12. GROUP BY + MAX()

### Command Block 39

```sql
SELECT
    department,
    MAX(salary) AS highest_salary
FROM employees
GROUP BY department;
```

## 13. GROUP BY + MIN()

### Command Block 40

```sql
SELECT
    department,
    MIN(salary) AS lowest_salary
FROM employees
GROUP BY department;
```

## WHERE

### Command Block 41

```sql
SELECT *
FROM employees
WHERE salary > 40000;
```

## HAVING

### Command Block 42

```sql
SELECT
    department,
    AVG(salary) AS average_salary
FROM employees
GROUP BY department
HAVING AVG(salary) > 40000;
```

## 15. WHERE + GROUP BY + HAVING

### Command Block 43

```sql
SELECT
    department,
    AVG(salary) AS average_salary
FROM employees
WHERE department = 'IT'
GROUP BY department
HAVING AVG(salary) > 45000;
```

## 16. SQL Query Execution Order

### Command Block 44

```sql
SELECT
    department,
    AVG(salary) AS average_salary
FROM employees
WHERE salary > 30000
GROUP BY department
HAVING AVG(salary) > 40000
ORDER BY average_salary DESC;
```

## Task 1

### Command Block 45

```sql
SELECT COUNT(*)
FROM employees;
```

## Task 2

### Command Block 46

```sql
SELECT SUM(salary)
FROM employees;
```

## Task 3

### Command Block 47

```sql
SELECT AVG(salary)
FROM employees;
```

## Task 4

### Command Block 48

```sql
SELECT MAX(salary)
FROM employees;
```

## Task 5

### Command Block 49

```sql
SELECT MIN(salary)
FROM employees;
```

## Task 6

### Command Block 50

```sql
SELECT department, COUNT(*)
FROM employees
GROUP BY department;
```

## Task 7

### Command Block 51

```sql
SELECT department, AVG(salary)
FROM employees
GROUP BY department;
```

## Task 8

### Command Block 52

```sql
SELECT department, SUM(salary)
FROM employees
GROUP BY department;
```

## Task 9

### Command Block 53

```sql
SELECT
    department,
    COUNT(*) AS employee_count
FROM employees
GROUP BY department
HAVING COUNT(*) > 2;
```

## Task 10

### Command Block 54

```sql
SELECT
    department,
    AVG(salary) AS average_salary
FROM employees
GROUP BY department
HAVING AVG(salary) > 45000;
```

## 🎯 Day 7 Success Condition

### Command Block 55

```sql
SELECT
    department,
    COUNT(*) AS employee_count
FROM employees
GROUP BY department
HAVING COUNT(*) > 3;
```

## 3. INNER JOIN

### Command Block 56

```sql
SELECT
    students.name,
    student_courses.course_id
FROM students
INNER JOIN student_courses
    ON students.student_id = student_courses.student_id;
```

## 4. JOIN Students + Courses

### Command Block 57

```sql
SELECT
    students.name,
    courses.course_name
FROM students
INNER JOIN student_courses
    ON students.student_id = student_courses.student_id
INNER JOIN courses
    ON student_courses.course_id = courses.course_id;
```

## 5. Understanding the JOIN

### Command Block 58

```sql
INNER JOIN student_courses
ON students.student_id = student_courses.student_id
```

### Command Block 59

```sql
INNER JOIN courses
ON student_courses.course_id = courses.course_id
```

## 6. LEFT JOIN

### Command Block 60

```sql
SELECT
    students.name,
    student_courses.course_id
FROM students
LEFT JOIN student_courses
    ON students.student_id = student_courses.student_id;
```

## 7. RIGHT JOIN

### Command Block 61

```sql
SELECT
    students.name,
    student_courses.course_id
FROM students
RIGHT JOIN student_courses
    ON students.student_id = student_courses.student_id;
```

## 8. FULL OUTER JOIN

### Command Block 62

```sql
SELECT
    students.name,
    student_courses.course_id
FROM students
FULL OUTER JOIN student_courses
    ON students.student_id = student_courses.student_id;
```

## 10. JOIN with WHERE

### Command Block 63

```sql
SELECT
    students.name,
    courses.course_name
FROM students
INNER JOIN student_courses
    ON students.student_id = student_courses.student_id
INNER JOIN courses
    ON student_courses.course_id = courses.course_id
WHERE courses.course_name = 'Python';
```

## 11. JOIN with GROUP BY

### Command Block 64

```sql
SELECT
    students.name,
    COUNT(student_courses.course_id) AS course_count
FROM students
LEFT JOIN student_courses
    ON students.student_id = student_courses.student_id
GROUP BY students.student_id, students.name;
```

## 12. JOIN + GROUP BY + HAVING

### Command Block 65

```sql
SELECT
    students.name,
    COUNT(student_courses.course_id) AS course_count
FROM students
INNER JOIN student_courses
    ON students.student_id = student_courses.student_id
GROUP BY students.student_id, students.name
HAVING COUNT(student_courses.course_id) > 1;
```

## 13. Table Aliases

### Command Block 66

```sql
SELECT
    students.name,
    courses.course_name
FROM students
INNER JOIN student_courses
    ON students.student_id = student_courses.student_id
INNER JOIN courses
    ON student_courses.course_id = courses.course_id;
```

### Command Block 67

```sql
SELECT
    s.name,
    c.course_name
FROM students AS s
INNER JOIN student_courses AS sc
    ON s.student_id = sc.student_id
INNER JOIN courses AS c
    ON sc.course_id = c.course_id;
```

## Students

### Command Block 68

```sql
CREATE TABLE students (
    student_id INT PRIMARY KEY,
    name VARCHAR(100)
);
```

## Courses

### Command Block 69

```sql
CREATE TABLE courses (
    course_id INT PRIMARY KEY,
    course_name VARCHAR(100)
);
```

## Student Courses

### Command Block 70

```sql
CREATE TABLE student_courses (
    student_id INT,
    course_id INT,

    PRIMARY KEY (student_id, course_id),

    FOREIGN KEY (student_id)
        REFERENCES students(student_id),

    FOREIGN KEY (course_id)
        REFERENCES courses(course_id)
);
```

## Insert Data

### Command Block 71

```sql
INSERT INTO students
VALUES
(1, 'Rahul'),
(2, 'Anu'),
(3, 'Ahmed'),
(4, 'Sara');
```

### Command Block 72

```sql
INSERT INTO courses
VALUES
(101, 'Python'),
(102, 'Django'),
(103, 'SQL');
```

### Command Block 73

```sql
INSERT INTO student_courses
VALUES
(1, 101),
(1, 102),
(2, 103),
(3, 101);
```

## 1. What is a Constraint?

### Command Block 74

```sql
CHECK (salary >= 0)
```

## 3. PRIMARY KEY

### Command Block 75

```sql
CREATE TABLE students (
    student_id INT PRIMARY KEY,
    name VARCHAR(100)
);
```

### Command Block 76

```sql
INSERT INTO students
VALUES (1, 'John');
```

## 4. FOREIGN KEY

### Command Block 77

```sql
CREATE TABLE orders (
    order_id INT PRIMARY KEY,
    customer_id INT,

    FOREIGN KEY (customer_id)
        REFERENCES customers(customer_id)
);
```

## 5. UNIQUE

### Command Block 78

```sql
CREATE TABLE users (
    id INT PRIMARY KEY,
    email VARCHAR(255) UNIQUE
);
```

## 6. NOT NULL

### Command Block 79

```sql
CREATE TABLE employees (
    id INT PRIMARY KEY,
    name VARCHAR(100) NOT NULL
);
```

### Command Block 80

```sql
INSERT INTO employees (id)
VALUES (1);
```

## 7. DEFAULT

### Command Block 81

```sql
CREATE TABLE employees (
    id INT PRIMARY KEY,
    name VARCHAR(100) NOT NULL,
    department VARCHAR(100) DEFAULT 'IT'
);
```

### Command Block 82

```sql
INSERT INTO employees (id, name)
VALUES (1, 'Rahul');
```

## 8. CHECK

### Command Block 83

```sql
CREATE TABLE employees (
    id INT PRIMARY KEY,
    name VARCHAR(100),
    age INT CHECK (age >= 18),
    salary DECIMAL(10,2) CHECK (salary >= 0)
);
```

### Command Block 84

```sql
INSERT INTO employees
VALUES (1, 'Rahul', 15, 30000);
```

## 9. Combining Constraints

### Command Block 85

```sql
CREATE TABLE employees (
    id INT PRIMARY KEY,
    name VARCHAR(100) NOT NULL,
    email VARCHAR(255) UNIQUE,
    age INT CHECK (age >= 18),
    salary DECIMAL(10,2) CHECK (salary >= 0),
    department VARCHAR(100) DEFAULT 'IT'
);
```

## Student_Courses

### Command Block 86

```sql
CREATE TABLE student_courses (
    student_id INT,
    course_id INT,

    PRIMARY KEY (student_id, course_id)
);
```

## 12. Surrogate Key

### Command Block 87

```sql
id INT GENERATED ALWAYS AS IDENTITY PRIMARY KEY
```

## CASCADE

### Command Block 88

```sql
FOREIGN KEY (customer_id)
REFERENCES customers(customer_id)
ON DELETE CASCADE
```

## SET NULL

### Command Block 89

```sql
ON DELETE SET NULL
```

## 14. ON UPDATE

### Command Block 90

```sql
ON UPDATE CASCADE
```

## 🧪 DAY 9 PRACTICAL

### Command Block 91

```sql
CREATE TABLE users (
    id INT PRIMARY KEY,
    username VARCHAR(100) NOT NULL,
    email VARCHAR(255) NOT NULL UNIQUE,
    age INT CHECK (age >= 18),
    status VARCHAR(20) DEFAULT 'active'
);
```

## Test 1 — Valid

### Command Block 92

```sql
INSERT INTO users (id, username, email, age)
VALUES (1, 'rahul', 'rahul@gmail.com', 21);
```

## Test 2 — Duplicate Email

### Command Block 93

```sql
INSERT INTO users (id, username, email, age)
VALUES (2, 'anu', 'rahul@gmail.com', 22);
```

## Test 3 — Missing Username

### Command Block 94

```sql
INSERT INTO users (id, email, age)
VALUES (3, 'test@gmail.com', 20);
```

## Test 4 — Invalid Age

### Command Block 95

```sql
INSERT INTO users (id, username, email, age)
VALUES (4, 'john', 'john@gmail.com', 15);
```

## 🧪 Foreign Key Practical

### Command Block 96

```sql
CREATE TABLE departments (
    department_id INT PRIMARY KEY,
    department_name VARCHAR(100) NOT NULL
);
```

### Command Block 97

```sql
CREATE TABLE employees (
    employee_id INT PRIMARY KEY,
    name VARCHAR(100) NOT NULL,
    department_id INT,

    FOREIGN KEY (department_id)
        REFERENCES departments(department_id)
);
```

### Command Block 98

```sql
INSERT INTO departments
VALUES (1, 'IT');
```

### Command Block 99

```sql
INSERT INTO employees
VALUES (101, 'Rahul', 1);
```

### Command Block 100

```sql
INSERT INTO employees
VALUES (102, 'Anu', 99);
```

## Names starting with R

### Command Block 101

```sql
SELECT *
FROM employees
WHERE name LIKE 'R%';
```

## Names ending with `a`

### Command Block 102

```sql
SELECT *
FROM employees
WHERE name LIKE '%a';
```

## Names containing `ah`

### Command Block 103

```sql
SELECT *
FROM employees
WHERE name LIKE '%ah%';
```

## `_`

### Command Block 104

```sql
SELECT *
FROM employees
WHERE name LIKE 'A__';
```

## 3. IN

### Command Block 105

```sql
SELECT *
FROM employees
WHERE department = 'IT'
OR department = 'HR'
OR department = 'Finance';
```

### Command Block 106

```sql
SELECT *
FROM employees
WHERE department IN ('IT', 'HR', 'Finance');
```

## 4. NOT IN

### Command Block 107

```sql
SELECT *
FROM employees
WHERE department NOT IN ('HR', 'Finance');
```

## 5. BETWEEN

### Command Block 108

```sql
SELECT *
FROM employees
WHERE salary BETWEEN 40000 AND 60000;
```

## 6. NOT BETWEEN

### Command Block 109

```sql
SELECT *
FROM employees
WHERE salary NOT BETWEEN 40000 AND 60000;
```

## 8. IS NULL

### Command Block 110

```sql
WHERE phone = NULL
```

### Command Block 111

```sql
SELECT *
FROM employees
WHERE phone IS NULL;
```

## 9. IS NOT NULL

### Command Block 112

```sql
SELECT *
FROM employees
WHERE phone IS NOT NULL;
```

## 10. COALESCE()

### Command Block 113

```sql
SELECT
    name,
    COALESCE(phone, 'Not Provided') AS phone
FROM employees;
```

## 11. What is a Subquery?

### Command Block 114

```sql
SELECT AVG(salary)
FROM employees;
```

### Command Block 115

```sql
SELECT *
FROM employees
WHERE salary > (
    SELECT AVG(salary)
    FROM employees
);
```

### Command Block 116

```sql
SELECT AVG(salary)
FROM employees
```

## Departments

### Command Block 117

```sql
SELECT *
FROM employees
WHERE department_id IN (
    SELECT department_id
    FROM departments
    WHERE department_name = 'IT'
);
```

## 14. EXISTS

### Command Block 118

```sql
SELECT *
FROM customers c
WHERE EXISTS (
    SELECT 1
    FROM orders o
    WHERE o.customer_id = c.customer_id
);
```

## `IN`

### Command Block 119

```sql
WHERE department_id IN (...)
```

## `EXISTS`

### Command Block 120

```sql
WHERE EXISTS (...)
```

## 16. Correlated Subquery

### Command Block 121

```sql
SELECT e.name, e.department, e.salary
FROM employees e
WHERE e.salary > (
    SELECT AVG(e2.salary)
    FROM employees e2
    WHERE e2.department = e.department
);
```

## 🎯 Day 10 Success Condition

### Command Block 122

```sql
SELECT *
FROM employees
WHERE salary > (
    SELECT AVG(salary)
    FROM employees
);
```

## 1. What is a VIEW?

### Command Block 123

```sql
SELECT id, name, salary
FROM employees
WHERE department = 'IT';
```

## 2. Creating a VIEW

### Command Block 124

```sql
CREATE VIEW it_employees AS
SELECT
    id,
    name,
    salary
FROM employees
WHERE department = 'IT';
```

### Command Block 125

```sql
SELECT *
FROM it_employees;
```

## 1. Simplifying complex queries

### Command Block 126

```sql
SELECT ...
JOIN ...
WHERE ...
GROUP BY ...
```

## 2. Security

### Command Block 127

```sql
CREATE VIEW employee_public AS
SELECT
    id,
    name,
    email
FROM employees;
```

## 4. View with JOIN

### Command Block 128

```sql
CREATE VIEW student_courses_view AS
SELECT
    s.name AS student_name,
    c.course_name
FROM students s
INNER JOIN student_courses sc
    ON s.student_id = sc.student_id
INNER JOIN courses c
    ON sc.course_id = c.course_id;
```

### Command Block 129

```sql
SELECT *
FROM student_courses_view;
```

## 5. CREATE OR REPLACE VIEW

### Command Block 130

```sql
CREATE OR REPLACE VIEW it_employees AS
SELECT
    id,
    name,
    salary,
    age
FROM employees
WHERE department = 'IT';
```

## 6. DROP VIEW

### Command Block 131

```sql
DROP VIEW it_employees;
```

## 9. Why Do We Need Indexes?

### Command Block 132

```sql
SELECT *
FROM employees
WHERE email = 'rahul@gmail.com';
```

### Command Block 133

```sql
CREATE INDEX idx_employees_email
ON employees(email);
```

## 10. Creating an INDEX

### Command Block 134

```sql
CREATE INDEX index_name
ON table_name(column_name);
```

### Command Block 135

```sql
CREATE INDEX idx_employee_email
ON employees(email);
```

## 11. Index on Department

### Command Block 136

```sql
SELECT *
FROM employees
WHERE department = 'IT';
```

### Command Block 137

```sql
CREATE INDEX idx_employee_department
ON employees(department);
```

## 12. Unique Index

### Command Block 138

```sql
CREATE UNIQUE INDEX idx_employee_email
ON employees(email);
```

## 13. Composite Index

### Command Block 139

```sql
CREATE INDEX idx_employee_department_salary
ON employees(department, salary);
```

## 14. Column Order Matters

### Command Block 140

```sql
CREATE INDEX idx_employee_department_salary
ON employees(department, salary);
```

### Command Block 141

```sql
CREATE INDEX ...
ON employees(salary, department);
```

## 18. Which Columns Often Need Indexes?

### Command Block 142

```sql
WHERE
JOIN
ORDER BY
```

### Command Block 143

```sql
SELECT *
FROM orders
WHERE customer_id = 10;
```

## 19. Primary Keys and Indexes

### Command Block 144

```sql
id INT PRIMARY KEY
```

## Task 1 — Create a View

### Command Block 145

```sql
CREATE VIEW it_employees AS
SELECT
    id,
    name,
    salary
FROM employees
WHERE department = 'IT';
```

### Command Block 146

```sql
SELECT *
FROM it_employees;
```

## Task 4 — Create an Index

### Command Block 147

```sql
CREATE INDEX idx_employee_email
ON employees(email);
```

## Task 5 — Create a Composite Index

### Command Block 148

```sql
CREATE INDEX idx_department_salary
ON employees(department, salary);
```

## Task 6 — Remove an Index

### Command Block 149

```sql
DROP INDEX idx_employee_email;
```

## Challenge 3

### Command Block 150

```sql
SELECT *
FROM orders
WHERE customer_id = 101;
```

## Challenge 4

### Command Block 151

```sql
SELECT *
FROM employees
WHERE department = 'IT'
AND salary > 50000;
```

## 🎯 Day 11 Success Condition

### Command Block 152

```sql
CREATE INDEX idx_employee_email
ON employees(email);
```
