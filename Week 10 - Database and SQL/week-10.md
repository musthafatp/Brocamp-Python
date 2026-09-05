
# DATABASE & SQL — ONE PAGE REVISION

## 1. DATABASE FUNDAMENTALS

**Database** → Organized collection of data.

**Data** → Raw facts/values.

**DBMS** → Software used to create, store, manage, retrieve, and update databases.

**RDBMS** → DBMS that stores data in relational tables and manages relationships.

**SQL** → Language used to communicate with relational databases.

**SQL vs NoSQL**
- SQL → Relational, tables, structured schema.
- NoSQL → Non-relational, documents/key-value/graph/etc., flexible schema.
- SQL: PostgreSQL, MySQL
- NoSQL: MongoDB, Redis, Cassandra, Neo4j

**Table** → Rows + Columns.

**Row/Record** → One complete data entry.

**Column/Field** → Attribute/property.

**Schema** → Database structure/blueprint.

**Instance** → Actual data at a particular time.

### Keys

| Key | Meaning |
|---|---|
| Primary Key | Uniquely identifies each row; UNIQUE + NOT NULL |
| Foreign Key | References key in another table |
| Candidate Key | Can become Primary Key |
| Alternate Key | Candidate Key not selected as Primary |
| Composite Key | Multiple columns together form a key |
| Super Key | Any attribute set that uniquely identifies a row |
| Unique Key | Prevents duplicate values |

**Constraints:** `PRIMARY KEY`, `FOREIGN KEY`, `UNIQUE`, `NOT NULL`, `CHECK`, `DEFAULT`

---

# 2. DATABASE ARCHITECTURE

### Three-Schema Architecture

```text
External
   ↓
Conceptual
   ↓
Internal
````

**External Level** → What users/applications see.

**Conceptual Level** → Complete logical database structure: tables, columns, relationships, keys, constraints.

**Internal Level** → How data is physically stored: files, pages, indexes, storage.

### Data Independence

**Logical Data Independence** → Change conceptual schema without unnecessarily affecting external views/applications.

**Physical Data Independence** → Change physical storage without affecting conceptual schema.

> Physical Data Independence is generally easier than Logical Data Independence.

---

# 3. ER MODEL

**ER Model** → Conceptual model used to design database before creating tables.

**Entity** → Real-world object.

**Attribute** → Property of an entity.

**Relationship** → Association between entities.

**Entity Set** → Collection of similar entities.

**Relationship Set** → Collection of similar relationships.

### Entity Types

**Strong Entity**

* Has its own key.
* Can exist independently.

**Weak Entity**

* Cannot be uniquely identified by its own attributes alone.
* Depends on a strong/owner entity.
* Usually uses owner's key + partial key.

### Attribute Types

**Simple** → Cannot be meaningfully divided.
Example: Age

**Composite** → Can be divided into meaningful parts.
Example: Name → First, Middle, Last

**Single-Valued** → One value per entity.
Example: Date of Birth

**Multi-Valued** → Multiple values per entity.
Example: Phone Numbers

**Derived** → Calculated from other data.
Example: Age from Date of Birth

### ER Diagram Symbols

```text
Rectangle        → Entity
Double Rectangle → Weak Entity
Oval             → Attribute
Double Oval      → Multi-Valued Attribute
Dashed Oval      → Derived Attribute
Diamond          → Relationship
Double Diamond   → Identifying Relationship
```

### Cardinality

```text
1:1 → One-to-One
1:M → One-to-Many
M:N → Many-to-Many
```

**1:1** → Person ↔ Passport

**1:M** → Department → Employees

**M:N** → Students ↔ Courses
Usually implemented using a junction/associative table.

### Participation

**Total** → Mandatory participation.

**Partial** → Optional participation.

> Cardinality → HOW MANY?
> Participation → MANDATORY OR OPTIONAL?

---

# 4. TRANSACTIONS

**Transaction** → One logical unit of database work.

Example:

```sql
BEGIN;

UPDATE Accounts
SET balance = balance - 1000
WHERE account_id = 1;

UPDATE Accounts
SET balance = balance + 1000
WHERE account_id = 2;

COMMIT;
```

If something fails:

```sql
ROLLBACK;
```

### ACID

| Property    | Meaning                                            |
| ----------- | -------------------------------------------------- |
| Atomicity   | All or Nothing                                     |
| Consistency | Database remains valid                             |
| Isolation   | Concurrent transactions don't improperly interfere |
| Durability  | Committed changes survive system failure           |

### Transaction Commands

**BEGIN** → Starts transaction.

**COMMIT** → Permanently applies changes.

**ROLLBACK** → Undoes uncommitted changes and ends transaction.

**SAVEPOINT** → Creates checkpoint inside transaction.

```sql
BEGIN;

INSERT INTO Students(student_name)
VALUES ('Ali');

SAVEPOINT sp1;

INSERT INTO Students(student_name)
VALUES ('Ahmed');

ROLLBACK TO SAVEPOINT sp1;

COMMIT;
```

> `ROLLBACK` → Undo whole current transaction
> `ROLLBACK TO SAVEPOINT` → Undo after savepoint and continue

---

# 5. TRANSACTION ISOLATION

### Problems

**Dirty Read** → Reading another transaction's uncommitted data.

**Non-Repeatable Read** → Same row gives different values when read twice.

**Phantom Read** → Same query returns a different set of rows.

### Isolation Levels

```text
READ UNCOMMITTED
        ↓
READ COMMITTED
        ↓
REPEATABLE READ
        ↓
SERIALIZABLE
```

| Level            | Dirty | Non-Repeatable | Phantom        |
| ---------------- | ----- | -------------- | -------------- |
| READ UNCOMMITTED | Yes   | Yes            | Yes            |
| READ COMMITTED   | No    | Yes            | Yes            |
| REPEATABLE READ  | No    | No             | DBMS-dependent |
| SERIALIZABLE     | No    | No             | No             |

**PostgreSQL**

* Default → `READ COMMITTED`
* `READ UNCOMMITTED` behaves like `READ COMMITTED`
* `REPEATABLE READ` also prevents phantom reads in PostgreSQL
* `SERIALIZABLE` → Strongest standard isolation

---

# 6. AGGREGATE FUNCTIONS

Aggregate functions perform calculations on multiple rows.

```text
COUNT() → How many?
SUM()   → Total?
AVG()   → Average?
MIN()   → Smallest?
MAX()   → Largest?
```

### COUNT()

```sql
SELECT COUNT(*) FROM Students;
```

Counts rows.

```sql
SELECT COUNT(marks) FROM Students;
```

Counts non-NULL values.

### SUM()

```sql
SELECT SUM(marks) FROM Students;
```

Returns total.

### AVG()

```sql
SELECT AVG(marks) FROM Students;
```

Returns average.

### MIN()

```sql
SELECT MIN(marks) FROM Students;
```

Returns smallest value.

### MAX()

```sql
SELECT MAX(marks) FROM Students;
```

Returns largest value.

### All Together

```sql
SELECT
    COUNT(*) AS total_students,
    SUM(marks) AS total_marks,
    AVG(marks) AS average_marks,
    MIN(marks) AS lowest_marks,
    MAX(marks) AS highest_marks
FROM Students;
```

### GROUP BY

Groups rows before aggregation.

```sql
SELECT department, AVG(marks)
FROM Students
GROUP BY department;
```

### WHERE vs HAVING

```text
WHERE  → Filters rows
GROUP BY → Creates groups
HAVING → Filters groups
```

Example:

```sql
SELECT department, AVG(marks)
FROM Students
GROUP BY department
HAVING AVG(marks) > 80;
```

### NULL

Most aggregate functions ignore `NULL`.

```text
COUNT(*)      → Counts all rows
COUNT(column) → Counts non-NULL values
SUM()         → Ignores NULL
AVG()         → Ignores NULL
MIN()         → Ignores NULL
MAX()         → Ignores NULL
```

---

# FINAL MEMORY

```text
DATABASE
→ Organized Data

DBMS
→ Manages Database

RDBMS
→ Tables + Relationships

SQL
→ Communicates with Database

SCHEMA
→ Structure

INSTANCE
→ Actual Data

PRIMARY KEY
→ Identifies Row

FOREIGN KEY
→ Connects Tables

ENTITY
→ Real-World Object

ATTRIBUTE
→ Property

RELATIONSHIP
→ Association

CARDINALITY
→ How Many?

PARTICIPATION
→ Mandatory/Optional

TRANSACTION
→ Logical Unit of Work

ACID
→ Atomicity, Consistency, Isolation, Durability

BEGIN
→ Start

COMMIT
→ Save

ROLLBACK
→ Undo

SAVEPOINT
→ Checkpoint

COUNT
→ Number

SUM
→ Total

AVG
→ Average

MIN
→ Smallest

MAX
→ Largest

WHERE
→ Filter Rows

GROUP BY
→ Create Groups

HAVING
→ Filter Groups
```
