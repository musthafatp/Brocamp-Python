## General Practice Table — `Employees`

```sql
CREATE TABLE Employees (
    employee_id INT PRIMARY KEY,
    employee_name VARCHAR(50),
    department VARCHAR(50),
    job_role VARCHAR(50),
    salary NUMERIC(10,2),
    joining_date DATE,
    city VARCHAR(50),
    experience_years INT,
    manager_id INT,
    performance_score NUMERIC(3,1)
);
```

### Sample Data

```sql
INSERT INTO Employees
(employee_id, employee_name, department, job_role, salary, joining_date, city, experience_years, manager_id, performance_score)
VALUES
(1, 'Arun',    'IT',      'Developer', 60000, '2021-01-15', 'Kochi',      4, NULL, 8.5),
(2, 'Rahul',   'IT',      'Developer', 52000, '2022-03-10', 'Calicut',    3, 1,    7.8),
(3, 'Sneha',   'HR',      'HR Manager', 70000, '2020-06-20', 'Kochi',      6, NULL, 9.0),
(4, 'Vishnu',  'IT',      'Tester',    45000, '2023-01-05', 'Kannur',     2, 1,    7.2),
(5, 'Anjali',  'Finance', 'Accountant', 55000, '2021-08-12', 'Kochi',      4, 8,    8.1),
(6, 'Fahad',   'Finance', 'Analyst',    48000, '2022-11-01', 'Malappuram', 3, 8,    7.5),
(7, 'Meera',   'HR',      'Recruiter',  42000, '2023-04-18', 'Calicut',    2, 3,    8.3),
(8, 'Suresh',  'Finance', 'Manager',    75000, '2019-09-25', 'Kochi',      7, NULL, 9.2),
(9, 'Nikhil',  'IT',      'Developer', 68000, '2020-12-11', 'Kannur',     5, 1,    8.9),
(10,'Diya',    'HR',      'Assistant',  35000, '2024-02-01', 'Kochi',      1, 3,    7.0),
(11,'Akhil',   'Finance', 'Accountant', 51000, '2023-07-15', 'Calicut',    2, 8,    7.9),
(12,'Neethu',  'IT',      'Designer',   58000, '2021-05-22', 'Kochi',      4, 1,    8.6);
```

---

# SQL Practical Practice

### Basic → Advanced

Try to solve these **without looking at solutions**.

---

## 🟢 Level 1 — Basic SQL

### SELECT

**1.** Display all employees.

**2.** Display only employee name, department and salary.

**3.** Display employee name and job role.

**4.** Display all unique departments.

**5.** Display all unique cities.

---

### WHERE

**6.** Find employees whose salary is greater than `50000`.

**7.** Find employees who work in the `IT` department.

**8.** Find employees whose experience is greater than `3` years.

**9.** Find employees from `Kochi`.

**10.** Find employees whose performance score is greater than `8.0`.

---

### AND / OR / NOT

**11.** Find IT employees whose salary is greater than `55000`.

**12.** Find employees from Kochi who have more than `3` years of experience.

**13.** Find employees who are either from Kochi or Calicut.

**14.** Find employees who are not from the IT department.

**15.** Find employees whose salary is greater than `50000` and performance score is greater than `8`.

---

## 🟢 Level 2 — Filtering & Sorting

### BETWEEN / IN / LIKE

**16.** Find employees whose salary is between `45000` and `60000`.

**17.** Find employees whose experience is between `2` and `5` years.

**18.** Find employees working in either `IT` or `Finance`.

**19.** Find employees whose city is either Kochi or Kannur.

**20.** Find employees whose name starts with `A`.

**21.** Find employees whose name ends with `a`.

**22.** Find employees whose name contains `ee`.

---

### ORDER BY

**23.** Display employees from highest salary to lowest salary.

**24.** Display employees from lowest salary to highest salary.

**25.** Display employees according to performance score from highest to lowest.

**26.** Display employees according to experience from highest to lowest.

**27.** Sort employees by department alphabetically and salary from highest to lowest within each department.

---

### LIMIT / OFFSET

**28.** Find the highest-paid employee.

**29.** Find the top 3 highest-paid employees.

**30.** Find the 3 lowest-paid employees.

**31.** Find the second-highest-paid employee using `ORDER BY` and `LIMIT/OFFSET`.

**32.** Display employees ranked from 4th to 6th according to salary.

---

# 🟡 Level 3 — Aggregate Functions

Practice:

`COUNT()`
`SUM()`
`AVG()`
`MIN()`
`MAX()`

**33.** Find the total number of employees.

**34.** Find the total salary of all employees.

**35.** Find the average salary.

**36.** Find the highest salary.

**37.** Find the lowest salary.

**38.** Find the average performance score.

**39.** Find the total number of employees in the IT department.

**40.** Find the average salary of Finance employees.

---

# 🟡 Level 4 — GROUP BY

**41.** Count employees in each department.

**42.** Find the average salary of each department.

**43.** Find the highest salary in each department.

**44.** Find the lowest salary in each department.

**45.** Find the total salary paid by each department.

**46.** Find the average performance score for each department.

**47.** Count employees in each city.

**48.** Find the average salary for each city.

---

# 🟡 Level 5 — HAVING

**49.** Display departments having more than 3 employees.

**50.** Display departments whose average salary is greater than `55000`.

**51.** Display departments whose maximum salary is greater than `70000`.

**52.** Display cities having at least 2 employees.

**53.** Display departments whose total salary is greater than `150000`.

**54.** Display departments whose average performance score is greater than `8`.

---

# 🟠 Level 6 — CASE

**55.** Create a column called `salary_level`:

* Salary >= 65000 → `High`
* Salary >= 50000 → `Medium`
* Otherwise → `Low`

**56.** Create an `experience_level` column:

* Experience >= 5 → `Senior`
* Experience >= 3 → `Mid-Level`
* Otherwise → `Junior`

**57.** Create a `performance_level` column:

* Score >= 8.5 → `Excellent`
* Score >= 7.5 → `Good`
* Otherwise → `Needs Improvement`

---

# 🟠 Level 7 — String & NULL Functions

**58.** Display employee names in uppercase.

**59.** Display employee names in lowercase.

**60.** Display the length of each employee's name.

**61.** Display employee name along with their department using concatenation.

**62.** Find employees whose `manager_id` is NULL.

**63.** Replace NULL `manager_id` with `0` using `COALESCE()`.

**64.** Use `NULLIF()` to avoid division by zero in a suitable calculation.

**65.** Convert salary into another numeric type using `CAST()`.

---

# 🟠 Level 8 — Date Functions

**66.** Display each employee's joining year.

**67.** Find employees who joined after `2022-01-01`.

**68.** Find employees who joined between `2021-01-01` and `2023-12-31`.

**69.** Sort employees according to joining date.

**70.** Find the earliest joining employee.

**71.** Find the most recently joined employee.

---

# 🔵 Level 9 — Subqueries

**72.** Find employees whose salary is greater than the average salary of all employees.

**73.** Find the employee with the highest salary.

**74.** Find the employee with the second-highest salary.

**75.** Find employees who earn more than the highest-paid employee in Finance.

**76.** Find employees whose salary is equal to the highest salary in the IT department.

**77.** Find employees who earn more than **ALL** employees in HR.

**78.** Find employees who earn more than **ANY** employee in Finance.

**79.** Find employees whose salary is greater than the average salary of their department.

**80.** Find the department of the employee who has the highest salary.

---

# 🔵 Level 10 — Self JOIN

Use `manager_id` and `employee_id`.

**81.** Display employee name and their manager's name.

**82.** Display all employees who have a manager.

**83.** Display each manager and the number of employees reporting to them.

**84.** Find employees whose salary is greater than their manager's salary.

**85.** Find employees who work under the manager named `Arun`.

---

# 🔵 Level 11 — CTE

**86.** Create a CTE containing employees whose salary is greater than `50000`.

**87.** Using a CTE, calculate the average salary of employees.

**88.** Using a CTE, find employees earning above the company average.

**89.** Create a CTE that calculates average salary by department and display departments whose average salary is above `55000`.

**90.** Create two CTEs:

* One containing IT employees.
* One containing Finance employees.

Combine their results.

**91.** Create a CTE that ranks employees according to salary and display the top 3.

---

# 🔴 Level 12 — Window Functions

Practice:

`RANK()`
`DENSE_RANK()`
`ROW_NUMBER()`
`PARTITION BY`
`OVER()`

**92.** Rank all employees according to salary.

**93.** Rank employees within each department according to salary.

**94.** Assign a row number to employees ordered by salary.

**95.** Find the highest-paid employee in each department using a window function.

**96.** Find the second-highest-paid employee in each department.

**97.** Calculate the average salary of each employee's department while still displaying individual employees.

**98.** Calculate the difference between each employee's salary and their department's average salary.

---

# 🔴 Level 13 — Set Operations

Practice:

`UNION`
`UNION ALL`
`INTERSECT`
`EXCEPT`

**99.** Get the cities containing IT employees and Finance employees using `UNION`.

**100.** Find cities that contain both IT and Finance employees using `INTERSECT`.

**101.** Find cities containing IT employees but no Finance employees using `EXCEPT`.

**102.** Combine employee names from IT and HR using `UNION ALL`.

---

# 🔴 Level 14 — Views

**103.** Create a view containing:

```text
employee_name
department
salary
```

for employees earning more than `50000`.

**104.** Query the view.

**105.** Create a view containing department-wise average salary.

**106.** Query the view to find departments whose average salary is above `55000`.

---

# 🔴 Level 15 — Advanced Mixed Questions

These are closer to **review/practical-test level**.

**107.** Find the highest-paid employee from each department.

**108.** Find the second-highest salary in each department.

**109.** Find employees whose salary is greater than their department's average salary.

**110.** Find the department having the highest average salary.

**111.** Find the department having the highest total salary.

**112.** Find the employee with the highest performance score in each department.

**113.** Find employees who earn more than their manager.

**114.** Find managers who have more than one employee reporting to them.

**115.** Find the top 2 highest-paid employees from each department.

**116.** Find employees who belong to a department whose average salary is greater than the company-wide average salary.

**117.** Display each employee with:

```text
employee_name
department
salary
department_average_salary
salary_difference
```

**118.** Rank employees by salary within their department and display only rank 1.

**119.** Find the department with the highest-performing employee.

**120.** Find employees who have a higher performance score than the average performance score of their department.

---

## 🔥 Final Challenge

Try this without looking at previous questions:

> **Find the top 2 highest-paid employees from every department, display their employee name, department, salary, department average salary, salary difference from the department average, and their salary rank within the department.**

This single question combines:

**CTE + Window Function + PARTITION BY + RANK + AVG + ORDER BY**

So this gives you a complete progression:

**SELECT → WHERE → Operators → ORDER BY → LIMIT → Aggregation → GROUP BY → HAVING → CASE → Functions → Dates → Subqueries → Self JOIN → CTE → Window Functions → Set Operations → Views → Advanced Mixed Queries.**
