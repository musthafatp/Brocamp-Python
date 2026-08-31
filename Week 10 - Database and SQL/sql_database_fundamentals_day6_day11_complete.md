# SQL & Database Fundamentals — Complete Day-by-Day Chat

> Complete compilation of the Day 6 through Day 11 study content from this chat, preserving all substantive content.

---

# 🗓️ DAY 6 — SQL CRUD + Query Fundamentals

Today we move from **database design** to actually **working with data using SQL**.

### 🎯 Day 6 Goal

By the end of today, you should be able to:

- Understand CRUD
- `INSERT`
- `SELECT`
- `UPDATE`
- `DELETE`
- `WHERE`
- Comparison operators
- `AND`, `OR`, `NOT`
- `ORDER BY`
- `LIMIT`
- Basic SQL filtering

This is still **fundamental SQL**, not Advanced SQL.

---

# 1. What is CRUD?

CRUD represents the four basic database operations:

```text
C → Create
R → Read
U → Update
D → Delete
```

| CRUD | SQL |
|---|---|
| Create | `INSERT` |
| Read | `SELECT` |
| Update | `UPDATE` |
| Delete | `DELETE` |

---

# 2. Create — INSERT

`INSERT` adds new records.

First create a table:

```sql
CREATE TABLE employees (
    id INT PRIMARY KEY,
    name VARCHAR(100),
    age INT,
    department VARCHAR(100),
    salary DECIMAL(10,2)
);
```

Insert one employee:

```sql
INSERT INTO employees
(id, name, age, department, salary)
VALUES
(1, 'Rahul', 25, 'IT', 40000);
```

Insert multiple employees:

```sql
INSERT INTO employees
(id, name, age, department, salary)
VALUES
(2, 'Anu', 24, 'HR', 35000),
(3, 'Ahmed', 28, 'IT', 50000),
(4, 'Sara', 26, 'Finance', 45000),
(5, 'John', 30, 'IT', 60000);
```

---

# 3. Read — SELECT

`SELECT` retrieves data.

### Get everything

```sql
SELECT * FROM employees;
```

### Get specific columns

```sql
SELECT name, salary
FROM employees;
```

Result:

```text
Rahul   40000
Anu     35000
Ahmed   50000
Sara    45000
John    60000
```

### Remember

```text
* → all columns
```

---

# 4. WHERE

`WHERE` filters records.

Example:

```sql
SELECT *
FROM employees
WHERE department = 'IT';
```

Only IT employees will be returned.

---

# 5. Comparison Operators

SQL provides comparison operators:

| Operator | Meaning |
|---|---|
| `=` | Equal |
| `!=` | Not equal |
| `<>` | Not equal |
| `>` | Greater than |
| `<` | Less than |
| `>=` | Greater than or equal |
| `<=` | Less than or equal |

### Example

Employees older than 25:

```sql
SELECT *
FROM employees
WHERE age > 25;
```

Salary greater than or equal to ₹50,000:

```sql
SELECT *
FROM employees
WHERE salary >= 50000;
```

---

# 6. AND

`AND` means **both conditions must be true**.

```sql
SELECT *
FROM employees
WHERE department = 'IT'
AND salary > 45000;
```

Meaning:

```text
Department = IT
       AND
Salary > 45000
```

---

# 7. OR

`OR` means **at least one condition must be true**.

```sql
SELECT *
FROM employees
WHERE department = 'IT'
OR department = 'HR';
```

---

# 8. NOT

`NOT` reverses a condition.

```sql
SELECT *
FROM employees
WHERE NOT department = 'IT';
```

This returns employees who are **not** in IT.

---

# 9. UPDATE

`UPDATE` modifies existing data.

Example:

```sql
UPDATE employees
SET salary = 55000
WHERE id = 3;
```

Ahmed's salary changes to ₹55,000.

### ⚠️ Important

Always be careful with `WHERE`.

This:

```sql
UPDATE employees
SET salary = 55000;
```

updates **every employee**.

---

# 10. DELETE

`DELETE` removes records.

Example:

```sql
DELETE FROM employees
WHERE id = 5;
```

Employee with ID 5 is deleted.

### ⚠️ Dangerous

```sql
DELETE FROM employees;
```

This deletes **all rows**.

So always understand your `WHERE` condition before executing `UPDATE` or `DELETE`.

---

# 11. ORDER BY

Used to sort results.

### Lowest → Highest

```sql
SELECT *
FROM employees
ORDER BY salary ASC;
```

### Highest → Lowest

```sql
SELECT *
FROM employees
ORDER BY salary DESC;
```

Remember:

```text
ASC  → Ascending
DESC → Descending
```

---

# 12. LIMIT

Used to restrict the number of returned rows.

Example:

```sql
SELECT *
FROM employees
LIMIT 3;
```

Returns only 3 employees.

### Highest salaries

```sql
SELECT *
FROM employees
ORDER BY salary DESC
LIMIT 3;
```

This means:

> Sort employees by salary from highest to lowest, then return the first 3.

---

# 13. DISTINCT

`DISTINCT` removes duplicate values from the result.

```sql
SELECT DISTINCT department
FROM employees;
```

Possible result:

```text
IT
HR
Finance
```

Instead of:

```text
IT
HR
IT
Finance
IT
```

---

# 🧠 SQL Query Flow

For today's basic queries, understand this structure:

```text
SELECT
   ↓
FROM
   ↓
WHERE
   ↓
ORDER BY
   ↓
LIMIT
```

Example:

```sql
SELECT name, salary
FROM employees
WHERE salary > 40000
ORDER BY salary DESC
LIMIT 3;
```

Read it like English:

> Select name and salary from employees where salary is greater than 40,000, sort by salary descending, and show only 3 records.

---

# 🧪 DAY 6 PRACTICAL

Use your `employees` table.

Insert at least **10 employees** with different:

- Names
- Ages
- Departments
- Salaries

Then perform these tasks.

### Task 1

Display all employees.

```sql
SELECT * FROM employees;
```

### Task 2

Display only:

```text
name
department
salary
```

### Task 3

Find employees from IT.

### Task 4

Find employees with salary greater than ₹40,000.

### Task 5

Find employees aged 25 or older.

### Task 6

Find IT employees whose salary is greater than ₹50,000.

### Task 7

Find employees who are not from HR.

### Task 8

Increase one employee's salary.

### Task 9

Delete one employee.

### Task 10

Display employees from highest salary to lowest.

### Task 11

Display the top 3 highest-paid employees.

### Task 12

Display all unique departments.

---

# 🔥 Practical Challenge

Write SQL for these requirements:

### 1.

> Find employees from IT with salary above ₹45,000.

```sql
SELECT *
FROM employees
WHERE department = 'IT'
AND salary > 45000;
```

### 2.

> Find employees from HR or Finance.

```sql
SELECT *
FROM employees
WHERE department = 'HR'
OR department = 'Finance';
```

### 3.

> Find the 5 highest-paid employees.

```sql
SELECT *
FROM employees
ORDER BY salary DESC
LIMIT 5;
```

### 4.

> Increase salary of employee ID 2 by ₹5,000.

```sql
UPDATE employees
SET salary = salary + 5000
WHERE id = 2;
```

---

# 🎤 Reviewer Questions

Try answering without looking:

1. What is CRUD?
2. Which SQL command is used to create records?
3. Which command reads data?
4. Which command updates data?
5. Which command deletes data?
6. What is the purpose of `WHERE`?
7. Difference between `AND` and `OR`?
8. What does `ORDER BY` do?
9. Difference between `ASC` and `DESC`?
10. What does `LIMIT` do?
11. What does `DISTINCT` do?
12. What happens if you run `DELETE FROM employees` without `WHERE`?
13. What happens if you run `UPDATE employees SET salary = 50000` without `WHERE`?
14. How do you find the top 3 highest salaries?

---

# 🧠 Important SQL Commands So Far

Your fundamentals are building like this:

```text
DATABASE
   ↓
CREATE DATABASE
   ↓
CREATE TABLE
   ↓
INSERT
   ↓
SELECT
   ↓
WHERE
   ↓
UPDATE
   ↓
DELETE
   ↓
ORDER BY
   ↓
LIMIT
```

You should now be comfortable with the basic **CRUD cycle**:

```text
Create → INSERT
Read   → SELECT
Update → UPDATE
Delete → DELETE
```

---

# ✅ DAY 6 CHECKLIST

### Theory

- [ ] CRUD
- [ ] INSERT
- [ ] SELECT
- [ ] UPDATE
- [ ] DELETE
- [ ] WHERE
- [ ] Comparison operators
- [ ] AND
- [ ] OR
- [ ] NOT
- [ ] ORDER BY
- [ ] ASC
- [ ] DESC
- [ ] LIMIT
- [ ] DISTINCT

### Practical

- [ ] Create employees table
- [ ] Insert 10+ employees
- [ ] Select all records
- [ ] Select specific columns
- [ ] Filter using WHERE
- [ ] Use AND / OR / NOT
- [ ] Update records
- [ ] Delete records
- [ ] Sort records
- [ ] Limit results
- [ ] Find distinct values

### 🎯 Day 6 Success Condition

You should be able to receive a requirement like:

> **"Find the 3 highest-paid IT employees earning more than ₹50,000."**

and immediately think:

```sql
SELECT *
FROM employees
WHERE department = 'IT'
AND salary > 50000
ORDER BY salary DESC
LIMIT 3;
```

**Next → Day 7: SQL Functions + Aggregation — `COUNT()`, `SUM()`, `AVG()`, `MIN()`, `MAX()` and `GROUP BY`.**

---

# 🗓️ DAY 7 — SQL Functions + Aggregation

Today you'll learn how to **calculate and summarize data**.

This is still **SQL Fundamentals**, not Advanced SQL.

### 🎯 Day 7 Goal

Understand and practice:

- Aggregate Functions
- `COUNT()`
- `SUM()`
- `AVG()`
- `MIN()`
- `MAX()`
- `GROUP BY`
- `HAVING`
- Difference between `WHERE` and `HAVING`

---

# 1. What are Aggregate Functions?

Aggregate functions perform a calculation on **multiple rows** and return a result.

Example:

Suppose we have:

| id | name | department | salary |
|---:|---|---|---:|
| 1 | Rahul | IT | 40000 |
| 2 | Anu | HR | 35000 |
| 3 | Ahmed | IT | 50000 |
| 4 | Sara | Finance | 45000 |
| 5 | John | IT | 60000 |

We can ask:

> How many employees are there?

> What is the total salary?

> What is the average salary?

> What is the highest salary?

That's where aggregate functions are used.

---

# 2. COUNT()

`COUNT()` counts rows or values.

### Count all employees

```sql
SELECT COUNT(*)
FROM employees;
```

Result:

```text
5
```

### Count employees in IT

```sql
SELECT COUNT(*)
FROM employees
WHERE department = 'IT';
```

Result:

```text
3
```

---

# 3. SUM()

`SUM()` calculates the total.

```sql
SELECT SUM(salary)
FROM employees;
```

If salaries are:

```text
40000
35000
50000
45000
60000
```

Total:

```text
230000
```

---

# 4. AVG()

`AVG()` calculates the average.

```sql
SELECT AVG(salary)
FROM employees;
```

Formula:

```text
Total salary
─────────────
Number of employees
```

---

# 5. MIN()

`MIN()` finds the smallest value.

```sql
SELECT MIN(salary)
FROM employees;
```

Result:

```text
35000
```

---

# 6. MAX()

`MAX()` finds the largest value.

```sql
SELECT MAX(salary)
FROM employees;
```

Result:

```text
60000
```

---

# 7. Using Multiple Aggregate Functions

You can use several functions together:

```sql
SELECT
    COUNT(*) AS employee_count,
    SUM(salary) AS total_salary,
    AVG(salary) AS average_salary,
    MIN(salary) AS minimum_salary,
    MAX(salary) AS maximum_salary
FROM employees;
```

This gives you a summary of the entire table.

---

# 8. What is GROUP BY?

`GROUP BY` groups rows that have the same value.

Example:

```sql
SELECT department
FROM employees
GROUP BY department;
```

Result:

```text
IT
HR
Finance
```

But the real power comes when you combine `GROUP BY` with aggregate functions.

---

# 9. GROUP BY + COUNT()

Question:

> How many employees are in each department?

```sql
SELECT
    department,
    COUNT(*) AS employee_count
FROM employees
GROUP BY department;
```

Result:

| department | employee_count |
|---|---:|
| IT | 3 |
| HR | 1 |
| Finance | 1 |

Think of it as:

```text
All employees
      ↓
Group by department
      ↓
IT       → 3
HR       → 1
Finance  → 1
```

---

# 10. GROUP BY + AVG()

Question:

> What is the average salary in each department?

```sql
SELECT
    department,
    AVG(salary) AS average_salary
FROM employees
GROUP BY department;
```

---

# 11. GROUP BY + SUM()

Question:

> What is the total salary paid by each department?

```sql
SELECT
    department,
    SUM(salary) AS total_salary
FROM employees
GROUP BY department;
```

---

# 12. GROUP BY + MAX()

Question:

> What is the highest salary in each department?

```sql
SELECT
    department,
    MAX(salary) AS highest_salary
FROM employees
GROUP BY department;
```

---

# 13. GROUP BY + MIN()

Question:

> What is the lowest salary in each department?

```sql
SELECT
    department,
    MIN(salary) AS lowest_salary
FROM employees
GROUP BY department;
```

---

# 14. WHERE vs HAVING

This is **very important**.

### WHERE

Filters **individual rows before grouping**.

Example:

```sql
SELECT *
FROM employees
WHERE salary > 40000;
```

---

### HAVING

Filters **groups after `GROUP BY`**.

Example:

> Show departments where the average salary is greater than ₹40,000.

```sql
SELECT
    department,
    AVG(salary) AS average_salary
FROM employees
GROUP BY department
HAVING AVG(salary) > 40000;
```

### Easy Memory

```text
WHERE
 ↓
Filter rows

GROUP BY
 ↓
Create groups

HAVING
 ↓
Filter groups
```

---

# 15. WHERE + GROUP BY + HAVING

You can combine them.

Question:

> Find the average salary of IT employees and show the department only if the average is greater than ₹45,000.

```sql
SELECT
    department,
    AVG(salary) AS average_salary
FROM employees
WHERE department = 'IT'
GROUP BY department
HAVING AVG(salary) > 45000;
```

The logical flow is:

```text
employees
    ↓
WHERE
    ↓
Filter rows
    ↓
GROUP BY
    ↓
Create groups
    ↓
HAVING
    ↓
Filter groups
```

---

# 16. SQL Query Execution Order

For today, understand this basic logical order:

```text
FROM
 ↓
WHERE
 ↓
GROUP BY
 ↓
HAVING
 ↓
SELECT
 ↓
ORDER BY
 ↓
LIMIT
```

Example:

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

Don't worry about memorizing every internal database optimization yet. Just understand the **logical processing order**.

---

# 🧪 DAY 7 PRACTICAL

Use your `employees` table from Day 6.

### Task 1

Count all employees.

```sql
SELECT COUNT(*)
FROM employees;
```

### Task 2

Find total salary.

```sql
SELECT SUM(salary)
FROM employees;
```

### Task 3

Find average salary.

```sql
SELECT AVG(salary)
FROM employees;
```

### Task 4

Find highest salary.

```sql
SELECT MAX(salary)
FROM employees;
```

### Task 5

Find lowest salary.

```sql
SELECT MIN(salary)
FROM employees;
```

### Task 6

Count employees in each department.

```sql
SELECT department, COUNT(*)
FROM employees
GROUP BY department;
```

### Task 7

Find average salary for each department.

```sql
SELECT department, AVG(salary)
FROM employees
GROUP BY department;
```

### Task 8

Find total salary for each department.

```sql
SELECT department, SUM(salary)
FROM employees
GROUP BY department;
```

### Task 9

Show only departments with more than 2 employees.

```sql
SELECT
    department,
    COUNT(*) AS employee_count
FROM employees
GROUP BY department
HAVING COUNT(*) > 2;
```

### Task 10

Find departments whose average salary is above ₹45,000.

```sql
SELECT
    department,
    AVG(salary) AS average_salary
FROM employees
GROUP BY department
HAVING AVG(salary) > 45000;
```

---

# 🔥 DAY 7 Challenge

Try these without looking at the answers.

### Challenge 1

> Find the highest salary in the IT department.

### Challenge 2

> Find the average salary of HR employees.

### Challenge 3

> Count how many employees are in each department.

### Challenge 4

> Find departments that have at least 3 employees.

### Challenge 5

> Find the department with the highest total salary.

### Challenge 6

> Find the average salary for departments where employees earn more than ₹30,000.

---

# 🎤 Reviewer Questions

Try answering these verbally:

1. What is an aggregate function?
2. What does `COUNT()` do?
3. What does `SUM()` do?
4. What does `AVG()` do?
5. What does `MIN()` do?
6. What does `MAX()` do?
7. What is `GROUP BY`?
8. Why do we use `GROUP BY` with aggregate functions?
9. What is `HAVING`?
10. Difference between `WHERE` and `HAVING`?
11. Can we use `WHERE` to filter groups?
12. Can we use `HAVING` without `GROUP BY`?
13. Explain the logical SQL execution order.
14. How do you find the average salary for each department?
15. How do you find departments having more than 5 employees?

---

# 🧠 Important Commands So Far

Your SQL fundamentals are now becoming:

```text
CREATE
INSERT
SELECT
WHERE
UPDATE
DELETE
ORDER BY
LIMIT
DISTINCT
        ↓
COUNT
SUM
AVG
MIN
MAX
        ↓
GROUP BY
        ↓
HAVING
```

---

# ✅ DAY 7 CHECKLIST

### Theory

- [ ] Aggregate Functions
- [ ] COUNT()
- [ ] SUM()
- [ ] AVG()
- [ ] MIN()
- [ ] MAX()
- [ ] GROUP BY
- [ ] HAVING
- [ ] WHERE vs HAVING
- [ ] SQL logical execution order

### Practical

- [ ] Count records
- [ ] Calculate total
- [ ] Calculate average
- [ ] Find minimum
- [ ] Find maximum
- [ ] Group by department
- [ ] Count each group
- [ ] Calculate average per group
- [ ] Calculate total per group
- [ ] Filter groups with HAVING

### 🎯 Day 7 Success Condition

If a reviewer asks:

> **"How many employees are there in each department, and show only departments having more than 3 employees?"**

You should immediately think:

```sql
SELECT
    department,
    COUNT(*) AS employee_count
FROM employees
GROUP BY department
HAVING COUNT(*) > 3;
```

**Next → Day 8: SQL JOINs — INNER JOIN, LEFT JOIN, RIGHT JOIN, and how Primary Key + Foreign Key relationships are actually used in queries.**

---

# 🗓️ DAY 8 — SQL JOINs

Today is one of the **most important SQL days** because real databases usually contain multiple related tables.

You already learned:

```text
Day 3 → Primary Key + Foreign Key + Relationships
Day 5 → Normalization
Day 6 → CRUD
Day 7 → Aggregation
```

Now we use those concepts together with **JOINs**.

### 🎯 Day 8 Goal

By the end of today, you should understand:

- Why JOINs are needed
- What is a JOIN?
- `INNER JOIN`
- `LEFT JOIN`
- `RIGHT JOIN`
- `FULL OUTER JOIN`
- Joining using Primary Key and Foreign Key
- Multiple-table JOINs
- JOIN + `WHERE`
- JOIN + `GROUP BY`
- Practical JOIN exercises

---

# 1. Why Do We Need JOINs?

Because normalized databases store information in **different tables**.

For example:

### Students

| student_id | name |
|---:|---|
| 1 | Rahul |
| 2 | Anu |
| 3 | Ahmed |

### Courses

| course_id | course_name |
|---:|---|
| 101 | Python |
| 102 | Django |
| 103 | SQL |

### Student_Courses

| student_id | course_id |
|---:|---:|
| 1 | 101 |
| 1 | 102 |
| 2 | 103 |
| 3 | 101 |

Now someone asks:

> "Show me the student's name and the course they enrolled in."

The information is spread across **three tables**.

We need a **JOIN**.

---

# 2. What is a JOIN?

A JOIN combines data from **two or more tables** using a related column.

Usually:

```text
Primary Key
     ↓
Foreign Key
```

Example:

```text
students.student_id
        ↓
student_courses.student_id
```

---

# 3. INNER JOIN

`INNER JOIN` returns only records that have a **match in both tables**.

Example:

```sql
SELECT
    students.name,
    student_courses.course_id
FROM students
INNER JOIN student_courses
    ON students.student_id = student_courses.student_id;
```

Result:

| name | course_id |
|---|---:|
| Rahul | 101 |
| Rahul | 102 |
| Anu | 103 |
| Ahmed | 101 |

### Easy memory

> **INNER JOIN = Only matching records**

---

# 4. JOIN Students + Courses

We want actual course names instead of IDs.

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

Result:

| name | course_name |
|---|---|
| Rahul | Python |
| Rahul | Django |
| Anu | SQL |
| Ahmed | Python |

This is a **multiple-table JOIN**.

---

# 5. Understanding the JOIN

Look at this:

```sql
INNER JOIN student_courses
ON students.student_id = student_courses.student_id
```

It means:

> Find the rows where `students.student_id` matches `student_courses.student_id`.

Then:

```sql
INNER JOIN courses
ON student_courses.course_id = courses.course_id
```

means:

> Find the course whose ID matches the student's course ID.

---

# 6. LEFT JOIN

`LEFT JOIN` returns:

> **All records from the left table + matching records from the right table.**

Example:

```sql
SELECT
    students.name,
    student_courses.course_id
FROM students
LEFT JOIN student_courses
    ON students.student_id = student_courses.student_id;
```

Suppose:

### Students

| student_id | name |
|---:|---|
| 1 | Rahul |
| 2 | Anu |
| 3 | Ahmed |
| 4 | Sara |

But Sara has not enrolled in any course.

Result:

| name | course_id |
|---|---:|
| Rahul | 101 |
| Rahul | 102 |
| Anu | 103 |
| Ahmed | 101 |
| Sara | NULL |

Sara is still shown.

### Easy memory

> **LEFT JOIN = Keep everything from the left table**

---

# 7. RIGHT JOIN

`RIGHT JOIN` is the opposite.

It returns:

> **All records from the right table + matching records from the left table.**

Example:

```sql
SELECT
    students.name,
    student_courses.course_id
FROM students
RIGHT JOIN student_courses
    ON students.student_id = student_courses.student_id;
```

### Easy memory

```text
LEFT JOIN
→ Keep left table

RIGHT JOIN
→ Keep right table
```

In practice, you can often rewrite a `RIGHT JOIN` as a `LEFT JOIN` by switching the table order.

---

# 8. FULL OUTER JOIN

`FULL OUTER JOIN` returns:

> All matching and non-matching records from **both tables**.

Conceptually:

```text
Table A
   +
Table B
   ↓
Everything from both
```

Example:

```sql
SELECT
    students.name,
    student_courses.course_id
FROM students
FULL OUTER JOIN student_courses
    ON students.student_id = student_courses.student_id;
```

It includes:

```text
Matching records
+
Students without matches
+
Course-enrollment records without matching students
```

### Important

Support for `FULL OUTER JOIN` differs by database. **PostgreSQL supports it; MySQL does not provide a native `FULL OUTER JOIN` syntax.**

Since you've been considering PostgreSQL for this week, you can practice it there.

---

# 9. JOIN Visual Memory

Think of tables like this:

```text
        INNER
       ┌───────┐
       │   A   │
       │   ∩   │
       │   B   │
       └───────┘
       Matching
```

### LEFT JOIN

```text
┌─────────┐
│ A       │████
│         │████
└─────────┘
   +
matches from B
```

### RIGHT JOIN

```text
     ┌─────────┐
████ │    B    │
████ │         │
     └─────────┘
     +
matches from A
```

---

# 10. JOIN with WHERE

You can filter joined data.

Question:

> Show students enrolled in Python.

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

Result:

| name | course_name |
|---|---|
| Rahul | Python |
| Ahmed | Python |

---

# 11. JOIN with GROUP BY

Question:

> How many courses has each student enrolled in?

```sql
SELECT
    students.name,
    COUNT(student_courses.course_id) AS course_count
FROM students
LEFT JOIN student_courses
    ON students.student_id = student_courses.student_id
GROUP BY students.student_id, students.name;
```

Example result:

| name | course_count |
|---|---:|
| Rahul | 2 |
| Anu | 1 |
| Ahmed | 1 |
| Sara | 0 |

Notice why we used `LEFT JOIN`:

We want **Sara included even though she has no course**.

---

# 12. JOIN + GROUP BY + HAVING

Question:

> Find students enrolled in more than one course.

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

Result:

```text
Rahul → 2
```

---

# 13. Table Aliases

When queries become longer, aliases make them easier to read.

Instead of:

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

You can write:

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

This is much cleaner.

```text
s  → students
sc → student_courses
c  → courses
```

---

# 14. JOIN Types — Remember This

| JOIN | What it returns |
|---|---|
| `INNER JOIN` | Matching rows from both tables |
| `LEFT JOIN` | All left + matching right |
| `RIGHT JOIN` | All right + matching left |
| `FULL OUTER JOIN` | Everything from both sides |

### Most important

For your fundamentals:

> **Master INNER JOIN and LEFT JOIN first.**

These are the ones you'll use constantly.

---

# 🧪 DAY 8 PRACTICAL

Create these tables.

### Students

```sql
CREATE TABLE students (
    student_id INT PRIMARY KEY,
    name VARCHAR(100)
);
```

### Courses

```sql
CREATE TABLE courses (
    course_id INT PRIMARY KEY,
    course_name VARCHAR(100)
);
```

### Student Courses

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

---

## Insert Data

```sql
INSERT INTO students
VALUES
(1, 'Rahul'),
(2, 'Anu'),
(3, 'Ahmed'),
(4, 'Sara');
```

```sql
INSERT INTO courses
VALUES
(101, 'Python'),
(102, 'Django'),
(103, 'SQL');
```

```sql
INSERT INTO student_courses
VALUES
(1, 101),
(1, 102),
(2, 103),
(3, 101);
```

Notice:

```text
Sara → No course
```

This will help you understand `LEFT JOIN`.

---

# 🧪 Practical Exercises

### Task 1

Show student names and their course IDs.

### Task 2

Show student names and course names.

### Task 3

Show only students enrolled in Python.

### Task 4

Show all students, including students who haven't enrolled in any course.

### Task 5

Count courses for each student.

### Task 6

Find students enrolled in more than one course.

### Task 7

Show all courses and the students enrolled in them.

### Task 8

Find courses with no students enrolled.

---

# 🔥 Day 8 Challenge

Without looking at the answer, solve:

> **"Display each student's name, course name, and show students even if they haven't enrolled in a course."**

Think:

```text
Students
   ↓
LEFT JOIN
   ↓
Student_Courses
   ↓
LEFT JOIN
   ↓
Courses
```

Then write the SQL.

---

# 🎤 Reviewer Questions

Try answering these verbally:

1. What is a JOIN?
2. Why do we need JOINs?
3. How does a JOIN relate to Primary Keys and Foreign Keys?
4. What is an INNER JOIN?
5. What is a LEFT JOIN?
6. What is a RIGHT JOIN?
7. What is a FULL OUTER JOIN?
8. Difference between INNER JOIN and LEFT JOIN?
9. Why does a LEFT JOIN sometimes return `NULL`?
10. What is a table alias?
11. Can we JOIN more than two tables?
12. Can we use `WHERE` with JOIN?
13. Can we use `GROUP BY` with JOIN?
14. Which JOIN would you use to find students who haven't enrolled in any course?

---

# 🧠 The Most Important Concept Today

Remember this:

```text
Normalized Database
       ↓
Multiple Tables
       ↓
Primary Key ↔ Foreign Key
       ↓
       JOIN
       ↓
Combined Result
```

For example:

```text
students
   │
   │ student_id
   ↓
student_courses
   │
   │ course_id
   ↓
courses
```

Then SQL can bring the information back together:

```text
Rahul → Python
Rahul → Django
Anu   → SQL
Ahmed → Python
```

That's the real purpose of JOINs.

---

# ✅ DAY 8 CHECKLIST

### Theory

- [ ] What is JOIN?
- [ ] Why JOINs are needed
- [ ] INNER JOIN
- [ ] LEFT JOIN
- [ ] RIGHT JOIN
- [ ] FULL OUTER JOIN
- [ ] PK ↔ FK relationship
- [ ] Table aliases
- [ ] JOIN + WHERE
- [ ] JOIN + GROUP BY
- [ ] JOIN + HAVING

### Practical

- [ ] Create 3 related tables
- [ ] Insert sample data
- [ ] INNER JOIN
- [ ] LEFT JOIN
- [ ] RIGHT JOIN
- [ ] FULL OUTER JOIN
- [ ] Multiple-table JOIN
- [ ] JOIN with WHERE
- [ ] JOIN with GROUP BY
- [ ] JOIN with HAVING

### 🎯 Day 8 Success Condition

If your reviewer asks:

> **"I have students, courses, and a student_courses table. Show me every student with their course name, including students who haven't enrolled in anything."**

You should immediately think:

```text
students
   ↓
LEFT JOIN student_courses
   ↓
LEFT JOIN courses
   ↓
SELECT student name + course name
```

**Next → Day 9: Constraints + Keys — `PRIMARY KEY`, `FOREIGN KEY`, `UNIQUE`, `NOT NULL`, `DEFAULT`, `CHECK`, and how database constraints protect your data.**

---

# 🗓️ DAY 9 — SQL Constraints & Keys

Today we're focusing on **protecting data quality**.

You already learned Primary Key and Foreign Key on earlier days. Today you'll go deeper into **constraints and keys**, because these are fundamental to designing reliable databases.

### 🎯 Day 9 Goal

Understand and practice:

- What are Constraints?
- `PRIMARY KEY`
- `FOREIGN KEY`
- `UNIQUE`
- `NOT NULL`
- `DEFAULT`
- `CHECK`
- Composite Primary Key
- Candidate Key — basic concept
- Surrogate Key — basic concept
- `ON DELETE`
- `ON UPDATE`

---

# 1. What is a Constraint?

A **constraint** is a rule that controls what data can be stored in a table.

Example:

> An employee's salary should not be negative.

We can enforce that using:

```sql
CHECK (salary >= 0)
```

Instead of relying only on the application code, the database itself protects the data.

### Simple definition

> **Constraint = A rule enforced by the database to maintain valid data.**

---

# 2. Why Do We Need Constraints?

Without constraints, invalid data could enter your database.

For example:

```text
id
Name: Rahul
Age: -500
Email: NULL
Salary: -100000
```

That doesn't make sense.

Constraints help prevent such problems.

---

# 3. PRIMARY KEY

A Primary Key uniquely identifies each row.

```sql
CREATE TABLE students (
    student_id INT PRIMARY KEY,
    name VARCHAR(100)
);
```

Rules:

```text
Unique
+
NOT NULL
+
Identifies a row
```

Example:

| student_id | name |
|---:|---|
| 1 | Rahul |
| 2 | Anu |
| 3 | Ahmed |

You cannot insert:

```sql
INSERT INTO students
VALUES (1, 'John');
```

because `1` already exists.

---

# 4. FOREIGN KEY

A Foreign Key creates a relationship between tables.

```sql
CREATE TABLE orders (
    order_id INT PRIMARY KEY,
    customer_id INT,

    FOREIGN KEY (customer_id)
        REFERENCES customers(customer_id)
);
```

The database ensures that the referenced customer exists, subject to the constraint behavior you define.

Example:

```text
customers
    │
    │ customer_id
    ↓
orders
```

---

# 5. UNIQUE

`UNIQUE` ensures that values don't repeat in a column/constraint.

Example:

```sql
CREATE TABLE users (
    id INT PRIMARY KEY,
    email VARCHAR(255) UNIQUE
);
```

This is valid:

```text
rahul@gmail.com
anu@gmail.com
```

But this isn't:

```text
rahul@gmail.com
rahul@gmail.com ❌
```

### Primary Key vs UNIQUE

| PRIMARY KEY | UNIQUE |
|---|---|
| Uniquely identifies row | Prevents duplicate values |
| Cannot be NULL | NULL behavior depends on DBMS |
| One primary-key constraint per table | Multiple UNIQUE constraints can exist |

---

# 6. NOT NULL

`NOT NULL` means a value must be provided.

```sql
CREATE TABLE employees (
    id INT PRIMARY KEY,
    name VARCHAR(100) NOT NULL
);
```

This is invalid:

```sql
INSERT INTO employees (id)
VALUES (1);
```

because `name` cannot be NULL.

---

# 7. DEFAULT

`DEFAULT` provides a value automatically when one isn't supplied.

Example:

```sql
CREATE TABLE employees (
    id INT PRIMARY KEY,
    name VARCHAR(100) NOT NULL,
    department VARCHAR(100) DEFAULT 'IT'
);
```

Then:

```sql
INSERT INTO employees (id, name)
VALUES (1, 'Rahul');
```

The database automatically uses:

```text
department = IT
```

---

# 8. CHECK

`CHECK` enforces a condition.

Example:

```sql
CREATE TABLE employees (
    id INT PRIMARY KEY,
    name VARCHAR(100),
    age INT CHECK (age >= 18),
    salary DECIMAL(10,2) CHECK (salary >= 0)
);
```

This should fail:

```sql
INSERT INTO employees
VALUES (1, 'Rahul', 15, 30000);
```

because:

```text
age >= 18
```

is violated.

---

# 9. Combining Constraints

You can use multiple constraints together.

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

Now the database protects several rules.

---

# 10. Composite Primary Key

Sometimes **one column isn't enough** to uniquely identify a row.

Example:

### Student_Courses

| student_id | course_id |
|---:|---:|
| 1 | 101 |
| 1 | 102 |
| 2 | 101 |

A student can enroll in many courses, and a course can have many students.

The combination:

```text
student_id + course_id
```

uniquely identifies an enrollment.

So:

```sql
CREATE TABLE student_courses (
    student_id INT,
    course_id INT,

    PRIMARY KEY (student_id, course_id)
);
```

This is called a **Composite Primary Key**.

### Easy memory

> **Composite Key = Multiple columns together form the key.**

---

# 11. Candidate Key

A **candidate key** is a column or combination of columns that **could uniquely identify a row**.

Example:

```text
employees
----------------
employee_id
email
phone
name
```

Suppose:

```text
employee_id → unique
email       → unique
phone       → unique
```

Then potentially:

```text
employee_id
email
phone
```

are candidate keys.

One candidate key is selected as the **Primary Key**.

---

# 12. Surrogate Key

A **surrogate key** is an artificial/generated identifier with no business meaning.

Example:

```text
id
1
2
3
4
```

The number itself doesn't describe the employee.

It simply identifies the record.

Example:

```sql
id INT GENERATED ALWAYS AS IDENTITY PRIMARY KEY
```

In PostgreSQL, this is one modern way to create an automatically generated integer identifier.

---

# 13. ON DELETE

What happens when a referenced record is deleted?

Example:

```text
Customer
   ↓
Orders
```

What should happen to orders if the customer is deleted?

We can specify behavior.

### CASCADE

Delete related records too.

```sql
FOREIGN KEY (customer_id)
REFERENCES customers(customer_id)
ON DELETE CASCADE
```

Meaning:

```text
Delete Customer
      ↓
Delete related Orders
```

### SET NULL

Set the foreign key to `NULL`.

```sql
ON DELETE SET NULL
```

This requires the foreign-key column to allow NULL.

### RESTRICT / NO ACTION

Prevent the deletion if related records exist, depending on the DBMS's constraint behavior.

---

# 14. ON UPDATE

Similar idea for updates.

```sql
ON UPDATE CASCADE
```

If the referenced key changes, the related foreign-key values can be updated automatically.

However, primary keys usually aren't changed in normal application design.

---

# 🧠 Constraint Summary

| Constraint | Purpose |
|---|---|
| `PRIMARY KEY` | Uniquely identifies a row |
| `FOREIGN KEY` | Creates/enforces relationship |
| `UNIQUE` | Prevents duplicate values |
| `NOT NULL` | Value is required |
| `DEFAULT` | Supplies a default value |
| `CHECK` | Enforces a condition |

Remember:

```text
PRIMARY KEY → Who is this row?
FOREIGN KEY → Which other row is it related to?
UNIQUE      → Don't duplicate this value
NOT NULL    → This must have a value
DEFAULT     → Use this value if none is provided
CHECK       → This condition must be true
```

---

# 🧪 DAY 9 PRACTICAL

Create a `users` table with:

```text
id
username
email
age
status
```

Requirements:

- `id` → Primary Key
- `username` → Required
- `email` → Unique + Required
- `age` → Must be 18 or above
- `status` → Default `'active'`

Write:

```sql
CREATE TABLE users (
    id INT PRIMARY KEY,
    username VARCHAR(100) NOT NULL,
    email VARCHAR(255) NOT NULL UNIQUE,
    age INT CHECK (age >= 18),
    status VARCHAR(20) DEFAULT 'active'
);
```

---

# 🧪 Test Your Constraints

### Test 1 — Valid

```sql
INSERT INTO users (id, username, email, age)
VALUES (1, 'rahul', 'rahul@gmail.com', 21);
```

Expected:

```text
Success ✅
```

`status` should automatically become:

```text
active
```

---

### Test 2 — Duplicate Email

```sql
INSERT INTO users (id, username, email, age)
VALUES (2, 'anu', 'rahul@gmail.com', 22);
```

Expected:

```text
Error ❌
```

because of `UNIQUE`.

---

### Test 3 — Missing Username

```sql
INSERT INTO users (id, email, age)
VALUES (3, 'test@gmail.com', 20);
```

Expected:

```text
Error ❌
```

because of `NOT NULL`.

---

### Test 4 — Invalid Age

```sql
INSERT INTO users (id, username, email, age)
VALUES (4, 'john', 'john@gmail.com', 15);
```

Expected:

```text
Error ❌
```

because:

```text
age >= 18
```

---

# 🧪 Foreign Key Practical

Create:

```sql
CREATE TABLE departments (
    department_id INT PRIMARY KEY,
    department_name VARCHAR(100) NOT NULL
);
```

Then:

```sql
CREATE TABLE employees (
    employee_id INT PRIMARY KEY,
    name VARCHAR(100) NOT NULL,
    department_id INT,

    FOREIGN KEY (department_id)
        REFERENCES departments(department_id)
);
```

Insert a department:

```sql
INSERT INTO departments
VALUES (1, 'IT');
```

Valid employee:

```sql
INSERT INTO employees
VALUES (101, 'Rahul', 1);
```

But:

```sql
INSERT INTO employees
VALUES (102, 'Anu', 99);
```

should fail because department `99` doesn't exist.

---

# 🔥 Day 9 Challenge

Design an **E-commerce Product table**.

Requirements:

```text
product_id → Primary Key
product_name → Required
price → Must be greater than 0
stock → Cannot be negative
sku → Unique
status → Default 'active'
```

Try writing the `CREATE TABLE` yourself.

---

# 🎤 Reviewer Questions

Try answering these without looking:

1. What is a constraint?
2. Why do we need constraints?
3. What is a Primary Key?
4. What is a Foreign Key?
5. What is `UNIQUE`?
6. What is `NOT NULL`?
7. What is `DEFAULT`?
8. What is `CHECK`?
9. What is a Composite Primary Key?
10. What is a Candidate Key?
11. What is a Surrogate Key?
12. Primary Key vs UNIQUE?
13. Foreign Key vs Primary Key?
14. What happens when a Foreign Key references a non-existing record?
15. What does `ON DELETE CASCADE` do?
16. What is the purpose of `ON DELETE SET NULL`?

---

# ✅ DAY 9 CHECKLIST

### Theory

- [ ] Constraints
- [ ] Primary Key
- [ ] Foreign Key
- [ ] UNIQUE
- [ ] NOT NULL
- [ ] DEFAULT
- [ ] CHECK
- [ ] Composite Primary Key
- [ ] Candidate Key
- [ ] Surrogate Key
- [ ] ON DELETE
- [ ] ON UPDATE
- [ ] CASCADE
- [ ] SET NULL

### Practical

- [ ] Create constrained table
- [ ] Test UNIQUE violation
- [ ] Test NOT NULL violation
- [ ] Test CHECK violation
- [ ] Test DEFAULT
- [ ] Create Foreign Key
- [ ] Test invalid Foreign Key
- [ ] Test Composite Primary Key
- [ ] Practice ON DELETE behavior

### 🎯 Day 9 Success Condition

You should now understand that **database design isn't only about storing data**.

```text
Table
  ↓
Columns
  ↓
Keys
  ↓
Relationships
  ↓
Constraints
  ↓
Valid + Reliable Data
```

**Next → Day 10: SQL Subqueries + `IN`, `EXISTS`, `BETWEEN`, `LIKE`, and `NULL` handling.**

---

# 🗓️ DAY 10 — SQL Filtering, NULL & Subqueries

Today we'll strengthen your **SQL fundamentals** before moving into more advanced topics.

### 🎯 Day 10 Goal

Learn:

- `LIKE`
- `IN`
- `BETWEEN`
- `IS NULL`
- `IS NOT NULL`
- `COALESCE()`
- Subqueries
- Scalar subqueries
- Subquery with `IN`
- Subquery with `EXISTS`
- Correlated subquery — basic understanding

---

# 1. LIKE

`LIKE` is used for **pattern matching**.

Suppose:

```text
Rahul
Ahmed
Anu
Sara
John
```

### Names starting with R

```sql
SELECT *
FROM employees
WHERE name LIKE 'R%';
```

`%` means **zero or more characters**.

So:

```text
R%
```

matches:

```text
Rahul
Ravi
Rohan
```

---

## Names ending with `a`

```sql
SELECT *
FROM employees
WHERE name LIKE '%a';
```

Matches:

```text
Anu
Sara
```

---

## Names containing `ah`

```sql
SELECT *
FROM employees
WHERE name LIKE '%ah%';
```

---

# 2. `%` vs `_`

Two important wildcard characters:

### `%`

Matches **zero or more characters**.

```text
A%
```

### `_`

Matches **exactly one character**.

Example:

```sql
SELECT *
FROM employees
WHERE name LIKE 'A__';
```

This matches names with exactly 3 characters starting with `A`, such as:

```text
Ali
Anu
```

---

# 3. IN

`IN` checks whether a value exists in a list.

Instead of:

```sql
SELECT *
FROM employees
WHERE department = 'IT'
OR department = 'HR'
OR department = 'Finance';
```

You can write:

```sql
SELECT *
FROM employees
WHERE department IN ('IT', 'HR', 'Finance');
```

Much cleaner.

### Easy memory

> `IN` = Match one of these values.

---

# 4. NOT IN

Opposite of `IN`.

```sql
SELECT *
FROM employees
WHERE department NOT IN ('HR', 'Finance');
```

This returns employees who are not in HR or Finance.

### ⚠️ NULL warning

`NOT IN` can behave unexpectedly when the list/subquery contains `NULL`. For reliable NULL-aware logic, understand `NOT EXISTS` as well.

---

# 5. BETWEEN

`BETWEEN` checks whether a value falls within a range.

Example:

```sql
SELECT *
FROM employees
WHERE salary BETWEEN 40000 AND 60000;
```

This includes the boundary values:

```text
40000 ✅
50000 ✅
60000 ✅
```

So:

> `BETWEEN` is generally inclusive.

---

# 6. NOT BETWEEN

```sql
SELECT *
FROM employees
WHERE salary NOT BETWEEN 40000 AND 60000;
```

Returns salaries outside that range.

---

# 7. NULL

This is extremely important.

`NULL` means:

> **Missing / unknown / no value**

It does **not** mean:

```text
0
```

and it does not mean:

```text
''
```

and it does not mean:

```text
False
```

Example:

| id | name | phone |
|---:|---|---|
| 1 | Rahul | 9876543210 |
| 2 | Anu | NULL |

Anu's phone number is unknown/not provided.

---

# 8. IS NULL

You cannot correctly check NULL using:

```sql
WHERE phone = NULL
```

❌ Don't do this.

Use:

```sql
SELECT *
FROM employees
WHERE phone IS NULL;
```

---

# 9. IS NOT NULL

Find records that have a value:

```sql
SELECT *
FROM employees
WHERE phone IS NOT NULL;
```

### Remember

```text
NULL
 ↓
IS NULL
IS NOT NULL
```

Not:

```text
= NULL
!= NULL
```

---

# 10. COALESCE()

`COALESCE()` returns the first non-NULL value.

Example:

```sql
SELECT
    name,
    COALESCE(phone, 'Not Provided') AS phone
FROM employees;
```

If phone is NULL:

```text
NULL
 ↓
Not Provided
```

This is useful when displaying data.

---

# 11. What is a Subquery?

A **subquery** is a query inside another query.

Example:

> Find employees who earn more than the average salary.

First:

```sql
SELECT AVG(salary)
FROM employees;
```

Then use that result:

```sql
SELECT *
FROM employees
WHERE salary > (
    SELECT AVG(salary)
    FROM employees
);
```

The inner query:

```sql
SELECT AVG(salary)
FROM employees
```

is the **subquery**.

---

# 12. Subquery Flow

Think:

```text
Outer Query
    ↓
Needs some value
    ↓
Inner Query
    ↓
Produces value
    ↓
Outer Query uses it
```

Example:

```text
Find employees
      ↓
salary > ?
      ↓
Find average salary
      ↓
Compare
```

---

# 13. Subquery with IN

Suppose we have:

### Employees

| id | name | department_id |
|---:|---|---:|
| 1 | Rahul | 10 |
| 2 | Anu | 20 |
| 3 | Ahmed | 10 |

### Departments

| department_id | department_name |
|---:|---|
| 10 | IT |
| 20 | HR |

Question:

> Find employees who belong to IT.

You could use a JOIN, but let's understand the subquery version.

```sql
SELECT *
FROM employees
WHERE department_id IN (
    SELECT department_id
    FROM departments
    WHERE department_name = 'IT'
);
```

The inner query finds:

```text
10
```

Then the outer query finds employees with:

```text
department_id = 10
```

---

# 14. EXISTS

`EXISTS` checks whether the subquery returns **at least one row**.

Example:

> Find customers who have at least one order.

```sql
SELECT *
FROM customers c
WHERE EXISTS (
    SELECT 1
    FROM orders o
    WHERE o.customer_id = c.customer_id
);
```

Think:

```text
Customer
   ↓
Does an order exist?
   ↓
YES → return customer
NO  → don't return customer
```

---

# 15. EXISTS vs IN

For fundamentals, remember:

### `IN`

You compare a value against a set of values.

```sql
WHERE department_id IN (...)
```

### `EXISTS`

You check whether matching rows exist.

```sql
WHERE EXISTS (...)
```

Both can sometimes solve similar problems, but their semantics and performance can differ depending on the database and query.

---

# 16. Correlated Subquery

A correlated subquery refers to a value from the **outer query**.

Example:

> Find employees whose salary is greater than the average salary of their own department.

```sql
SELECT e.name, e.department, e.salary
FROM employees e
WHERE e.salary > (
    SELECT AVG(e2.salary)
    FROM employees e2
    WHERE e2.department = e.department
);
```

Notice:

```text
Outer query
    ↓
e.department
    ↓
Inner query uses it
```

This is a **correlated subquery**.

For today, understand the concept. Don't worry about optimization yet.

---

# 🧠 JOIN vs Subquery

This is important.

Sometimes the same requirement can be solved using either a JOIN or a subquery.

### JOIN

```text
Combine related tables
```

### Subquery

```text
Use the result of one query inside another query
```

Don't think:

> "Subquery is always better than JOIN."

Or:

> "JOIN is always better than subquery."

The appropriate choice depends on the problem, readability, and database execution plan.

---

# 🧪 DAY 10 PRACTICAL

Use your `employees` table.

### Task 1

Find employees whose names start with `A`.

### Task 2

Find employees whose names contain `an`.

### Task 3

Find employees from IT, HR, or Finance using `IN`.

### Task 4

Find employees with salary between ₹40,000 and ₹60,000.

### Task 5

Find employees whose phone number is NULL.

### Task 6

Find employees whose phone number is not NULL.

### Task 7

Display `Not Provided` when phone is NULL.

### Task 8

Find employees earning more than the average salary.

### Task 9

Find employees belonging to the IT department using a subquery.

### Task 10

Find customers who have at least one order using `EXISTS`.

---

# 🔥 Day 10 Challenge

Don't look at the answer first.

### Challenge 1

> Find employees whose salary is greater than the average salary.

Think:

```text
Employee salary
       >
Average salary
       ↓
   Subquery
```

---

### Challenge 2

> Find employees whose names start with "R" and salary is between ₹40,000 and ₹70,000.

You need:

```text
LIKE
+
BETWEEN
```

---

### Challenge 3

> Find employees who belong to either IT or HR and whose salary is greater than ₹50,000.

You need:

```text
IN
+
AND
```

---

### Challenge 4

> Find customers who have at least one order.

Think:

```text
EXISTS
```

---

# 🎤 Reviewer Questions

Try answering without looking:

1. What is `LIKE`?
2. What does `%` mean in `LIKE`?
3. What does `_` mean?
4. What is `IN`?
5. What is `BETWEEN`?
6. Is `BETWEEN` inclusive?
7. What is `NULL`?
8. Is `NULL` equal to zero?
9. How do you check for NULL?
10. Why can't we use `= NULL`?
11. What is `COALESCE()`?
12. What is a subquery?
13. What is a scalar subquery?
14. What is `EXISTS`?
15. Difference between `IN` and `EXISTS`?
16. What is a correlated subquery?
17. JOIN vs subquery?

---

# ✅ DAY 10 CHECKLIST

### Theory

- [ ] `LIKE`
- [ ] `%`
- [ ] `_`
- [ ] `IN`
- [ ] `NOT IN`
- [ ] `BETWEEN`
- [ ] `NOT BETWEEN`
- [ ] `NULL`
- [ ] `IS NULL`
- [ ] `IS NOT NULL`
- [ ] `COALESCE()`
- [ ] Subqueries
- [ ] Scalar subquery
- [ ] `IN` subquery
- [ ] `EXISTS`
- [ ] Correlated subquery
- [ ] JOIN vs Subquery

### Practical

- [ ] Pattern matching
- [ ] `IN`
- [ ] `BETWEEN`
- [ ] NULL filtering
- [ ] `COALESCE()`
- [ ] Average salary subquery
- [ ] `IN` subquery
- [ ] `EXISTS` query
- [ ] Correlated subquery

---

# 🎯 Day 10 Success Condition

If your reviewer asks:

> **"Find employees whose salary is greater than the average salary."**

You should be able to write:

```sql
SELECT *
FROM employees
WHERE salary > (
    SELECT AVG(salary)
    FROM employees
);
```

And if they ask:

> **"What's the difference between WHERE and HAVING?"**

You should immediately remember:

```text
WHERE
 ↓
Filters rows

GROUP BY
 ↓
Creates groups

HAVING
 ↓
Filters groups
```

---

## 📚 Your Fundamentals Progress

You've now covered a substantial part of your Database + SQL fundamentals:

```text
DAY 1  → Database + DBMS + RDBMS + SQL
DAY 2  → Basic Database/SQL Practice
DAY 3  → Schema Architecture + ER Diagrams
DAY 4  → Transactions + ACID + CAP
DAY 5  → Normalization
DAY 6  → CRUD + Basic Queries
DAY 7  → Aggregation + GROUP BY + HAVING
DAY 8  → JOINs
DAY 9  → Constraints + Keys
DAY 10 → Filtering + NULL + Subqueries
```

**Next → Day 11: SQL Views + Indexes + basic query performance.**

---

# 🗓️ DAY 11 — SQL Views & Indexes

Today we start learning two important database concepts:

- **Views** → simplify and control access to queries/data
- **Indexes** → make data searching faster

This is still within your **Database + SQL Fundamentals**. We won't go deeply into query optimization yet.

### 🎯 Day 11 Goal

By the end of today, you should understand:

- What is a View?
- Why do we use Views?
- Creating a View
- Querying a View
- Updating/deleting Views
- What is an Index?
- Why indexes improve searching
- Creating an Index
- Single-column Index
- Composite Index — basic concept
- Advantages and disadvantages of indexes
- When to use an Index
- When not to use an Index

---

# 1. What is a VIEW?

A **View** is a virtual table based on a SQL query.

It doesn't normally store a separate copy of the underlying data.

Think:

```text
Table
  ↓
SQL Query
  ↓
VIEW
  ↓
Looks like a table
```

Example:

Suppose we have:

```text
employees
```

with:

```text
id
name
department
salary
```

We frequently need:

> Employees from IT.

Instead of repeatedly writing:

```sql
SELECT id, name, salary
FROM employees
WHERE department = 'IT';
```

we can create a View.

---

# 2. Creating a VIEW

```sql
CREATE VIEW it_employees AS
SELECT
    id,
    name,
    salary
FROM employees
WHERE department = 'IT';
```

Now you can query it like a table:

```sql
SELECT *
FROM it_employees;
```

Result:

```text
id | name  | salary
-------------------
1  | Rahul | 40000
3  | Ahmed | 50000
5  | John  | 60000
```

---

# 3. Why Use Views?

Views are useful for:

### 1. Simplifying complex queries

Instead of repeatedly writing:

```sql
SELECT ...
JOIN ...
WHERE ...
GROUP BY ...
```

you can save the query as a View.

---

### 2. Security

Suppose your employee table contains:

```text
id
name
email
salary
password
```

You don't want every database user/application to see everything.

You can create:

```sql
CREATE VIEW employee_public AS
SELECT
    id,
    name,
    email
FROM employees;
```

Now the View exposes only selected columns.

```text
Original Table
      ↓
 ┌───────────────┐
 │ id            │
 │ name          │
 │ email         │
 │ salary        │
 │ password      │
 └───────────────┘
      ↓
     VIEW
      ↓
 ┌───────────────┐
 │ id            │
 │ name          │
 │ email         │
 └───────────────┘
```

---

# 4. View with JOIN

Views become especially useful when queries involve multiple tables.

Example:

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

Now:

```sql
SELECT *
FROM student_courses_view;
```

can give:

| student_name | course_name |
|---|---|
| Rahul | Python |
| Rahul | Django |
| Anu | SQL |
| Ahmed | Python |

Instead of writing that JOIN every time.

---

# 5. CREATE OR REPLACE VIEW

If you want to modify the View definition:

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

The exact syntax can vary slightly between database systems.

---

# 6. DROP VIEW

If you don't need a View:

```sql
DROP VIEW it_employees;
```

This removes the View.

It does **not normally delete the underlying table data**.

Remember:

```text
DROP VIEW
   ↓
Delete the View definition

Not:
Delete underlying table rows
```

---

# 7. Is a VIEW a Real Table?

Conceptually:

```text
Table → stores data
View  → stores a query definition
```

A normal View generally doesn't store its own copy of the underlying rows.

When you query it, the database uses the View definition.

Some databases also support **materialized views**, which are different because they store the query result and need refreshing. You only need the basic View concept for now.

---

# 8. What is an INDEX?

An **Index** is a database structure used to make finding rows more efficient.

Think about a book.

Without an index:

```text
Search "Database"
        ↓
Read page 1
Read page 2
Read page 3
...
```

With an index:

```text
Database
   ↓
Page 57
```

You can go directly toward the relevant location.

A database index serves a similar purpose.

---

# 9. Why Do We Need Indexes?

Suppose we have:

```text
employees
```

with **1,000,000 rows**.

You run:

```sql
SELECT *
FROM employees
WHERE email = 'rahul@gmail.com';
```

Without a suitable index, the database may need to inspect many rows.

With an index on `email`:

```sql
CREATE INDEX idx_employees_email
ON employees(email);
```

the database can often locate matching rows much more efficiently.

---

# 10. Creating an INDEX

Basic syntax:

```sql
CREATE INDEX index_name
ON table_name(column_name);
```

Example:

```sql
CREATE INDEX idx_employee_email
ON employees(email);
```

---

# 11. Index on Department

If you frequently search:

```sql
SELECT *
FROM employees
WHERE department = 'IT';
```

you might create:

```sql
CREATE INDEX idx_employee_department
ON employees(department);
```

---

# 12. Unique Index

You can create a unique index:

```sql
CREATE UNIQUE INDEX idx_employee_email
ON employees(email);
```

This means:

```text
email
 ↓
must be unique
```

However, if uniqueness is a **data integrity rule**, it's generally better to express it as a `UNIQUE` constraint rather than treating an index alone as the business rule.

---

# 13. Composite Index

A composite index contains **multiple columns**.

Example:

```sql
CREATE INDEX idx_employee_department_salary
ON employees(department, salary);
```

This index is on:

```text
department + salary
```

It can be useful for queries involving those columns in appropriate patterns.

---

# 14. Column Order Matters

This is important.

Suppose:

```sql
CREATE INDEX idx_employee_department_salary
ON employees(department, salary);
```

The order is:

```text
department
    ↓
salary
```

This is **not simply the same thing** as:

```sql
CREATE INDEX ...
ON employees(salary, department);
```

The order of columns in a composite index matters because it affects which query conditions can efficiently use the index.

For fundamentals, remember:

> **Composite index = multiple columns, and column order matters.**

---

# 15. Indexes Don't Automatically Make Everything Faster

Indexes have a cost.

When you:

```text
INSERT
UPDATE
DELETE
```

the database may also need to maintain affected indexes.

So:

```text
More indexes
     ↓
Faster reads sometimes
     +
More storage
     +
More write/maintenance cost
```

---

# 16. Advantages of Indexes

### ✅ Faster searches

Especially for selective queries on large tables.

### ✅ Faster sorting/joining in some cases

Depending on the query and database optimizer.

### ✅ Useful for frequently searched columns

For example:

```text
email
username
customer_id
order_id
```

---

# 17. Disadvantages of Indexes

### ❌ Takes storage

Indexes consume disk space.

### ❌ Slower writes

Indexes need to be updated when indexed data changes.

### ❌ Too many indexes are bad

Don't create an index on every column automatically.

---

# 18. Which Columns Often Need Indexes?

Good candidates can include columns frequently used in:

```sql
WHERE
JOIN
ORDER BY
```

For example:

```sql
SELECT *
FROM orders
WHERE customer_id = 10;
```

An index on:

```text
customer_id
```

may be useful.

---

# 19. Primary Keys and Indexes

When you define:

```sql
id INT PRIMARY KEY
```

the database typically creates or uses an index structure to enforce the uniqueness and efficiently locate rows.

So you generally **don't need to manually create another ordinary index on the same primary-key column**.

Similarly, a `UNIQUE` constraint is commonly backed by a unique index internally, depending on the database.

---

# 20. Index ≠ Constraint

Don't confuse them.

### Constraint

Protects data.

```text
PRIMARY KEY
UNIQUE
FOREIGN KEY
CHECK
NOT NULL
```

### Index

Primarily helps database access/search performance.

```text
CREATE INDEX
```

Example:

```text
UNIQUE
 ↓
Data must not duplicate

INDEX
 ↓
Can make searching more efficient
```

---

# 🧠 VIEW vs INDEX

| View | Index |
|---|---|
| Virtual query-based table | Data access structure |
| Simplifies queries | Can speed up data retrieval |
| Can expose selected data | Helps locate rows efficiently |
| Doesn't normally store its own result | Stores index data |
| Created with `CREATE VIEW` | Created with `CREATE INDEX` |

---

# 🧪 DAY 11 PRACTICAL

Use your existing `employees` table.

## Task 1 — Create a View

Create a View containing only IT employees:

```sql
CREATE VIEW it_employees AS
SELECT
    id,
    name,
    salary
FROM employees
WHERE department = 'IT';
```

Then:

```sql
SELECT *
FROM it_employees;
```

---

## Task 2 — Create a Public Employee View

Show only:

```text
id
name
department
```

Do not expose salary.

---

## Task 3 — Create a JOIN View

Using your:

```text
students
student_courses
courses
```

tables, create:

```text
student_courses_view
```

that shows:

```text
student name
course name
```

---

## Task 4 — Create an Index

Create an index on:

```text
employees.email
```

```sql
CREATE INDEX idx_employee_email
ON employees(email);
```

---

## Task 5 — Create a Composite Index

Create an index on:

```text
department + salary
```

```sql
CREATE INDEX idx_department_salary
ON employees(department, salary);
```

---

## Task 6 — Remove an Index

```sql
DROP INDEX idx_employee_email;
```

**Note:** Exact `DROP INDEX` syntax can vary by DBMS, so follow your chosen database's syntax.

---

# 🔥 DAY 11 CHALLENGES

### Challenge 1

Create a View that shows:

```text
Employee Name
Department
Salary
```

but only employees earning more than ₹50,000.

---

### Challenge 2

Create a View that shows:

```text
Department
Average Salary
```

for each department.

Hint:

```text
GROUP BY
+
AVG()
```

---

### Challenge 3

Suppose you frequently execute:

```sql
SELECT *
FROM orders
WHERE customer_id = 101;
```

What column would you consider indexing?

---

### Challenge 4

Suppose you frequently execute:

```sql
SELECT *
FROM employees
WHERE department = 'IT'
AND salary > 50000;
```

What type of index could you consider?

---

# 🎤 Reviewer Questions

Try answering without looking:

1. What is a View?
2. Why do we use Views?
3. Does a normal View store a separate copy of the data?
4. How do you create a View?
5. How do you delete a View?
6. What is an Index?
7. Why do we use indexes?
8. Give a real-life analogy for an Index.
9. What are the disadvantages of indexes?
10. Why shouldn't we create indexes on every column?
11. What is a composite index?
12. Why does column order matter in a composite index?
13. Primary Key vs Index?
14. Constraint vs Index?
15. Can an index improve JOIN performance?
16. Can indexes slow down INSERT/UPDATE/DELETE?

---

# 🧠 Most Important Concept

Remember:

```text
VIEW
 ↓
Makes queries easier
 ↓
Simplifies / controls access to data
```

While:

```text
INDEX
 ↓
Helps database find data efficiently
 ↓
Can improve read performance
```

And:

```text
CONSTRAINT
 ↓
Protects data correctness
```

So:

```text
Constraint → Data Integrity
View       → Query/Data Abstraction
Index      → Query Performance
```

---

# ✅ DAY 11 CHECKLIST

### Theory

- [ ] What is a View?
- [ ] Why Views are used
- [ ] Create View
- [ ] Query View
- [ ] Replace View
- [ ] Drop View
- [ ] View with JOIN
- [ ] View vs Table
- [ ] What is an Index?
- [ ] Why Indexes are used
- [ ] Create Index
- [ ] Unique Index
- [ ] Composite Index
- [ ] Index column order
- [ ] Advantages of Indexes
- [ ] Disadvantages of Indexes
- [ ] Constraint vs Index

### Practical

- [ ] Create a View
- [ ] Query a View
- [ ] Create a JOIN View
- [ ] Create an Index
- [ ] Create a Composite Index
- [ ] Drop an Index
- [ ] Identify columns that could benefit from indexing

### 🎯 Day 11 Success Condition

If your reviewer asks:

> **"Our application frequently searches employees by email. What can you do to improve lookup performance?"**

You should be able to answer:

> **I can consider creating an index on the email column, assuming that query pattern and data distribution make it beneficial.**

```sql
CREATE INDEX idx_employee_email
ON employees(email);
```

And if they ask:

> **"What is the difference between a View and an Index?"**

Your answer:

> **A View is a saved query that presents data as a virtual table, while an Index is a database structure designed to make certain data access operations more efficient.**

---

## 📚 Your SQL Fundamentals Progress

```text
DAY 1  → Database Fundamentals
DAY 2  → DBMS / RDBMS / SQL Basics
DAY 3  → Schema Architecture + ER Diagrams
DAY 4  → ACID + CAP + Transactions
DAY 5  → Normalization
DAY 6  → CRUD + Basic Queries
DAY 7  → Aggregation + GROUP BY + HAVING
DAY 8  → JOINs
DAY 9  → Constraints + Keys
DAY 10 → Filtering + NULL + Subqueries
DAY 11 → Views + Indexes
```
