# DJANGO ORM — COMPLETE MASTER NOTES

---

# PART A — DJANGO ORM COMPLETE THEORY

## 1. What is Django?

**Django** is a high-level Python web framework used to build web applications.

It follows the **MVT architecture**:

```text
M → Model
V → View
T → Template
```

For ORM, our main focus is the **Model layer**.

---

# 2. What is ORM?

**ORM = Object Relational Mapping**

ORM allows us to communicate with a relational database using programming-language objects instead of manually writing SQL for every operation.

### Simple definition

> Django ORM allows Python code to interact with database tables and records.

Example:

```python
Student.objects.filter(age__gte=18)
```

instead of:

```sql
SELECT * FROM student WHERE age >= 18;
```

---

# 3. Why use ORM?

ORM provides:

* Less SQL code
* Python-based database operations
* Database abstraction
* Easier CRUD
* Relationship management
* Query chaining
* Query optimization tools
* Model validation integration
* Migration support
* Protection against many common SQL injection mistakes when using ORM correctly

---

# 4. ORM Mapping

The most important mapping:

```text
Django Model       → Database Table
Model Field        → Database Column
Model Object       → Database Row
Manager            → Query interface
QuerySet           → Collection of results
```

---

# 5. Django Model

A model is a Python class that represents a database table.

```python
class Student(models.Model):
    name = models.CharField(max_length=100)
    age = models.IntegerField()
```

Conceptually:

```text
Student
----------------
id
name
age
```

Django automatically adds an ID primary key if you don't define one yourself.

---

# 6. Model Fields

Common Django fields:

```text
AutoField
BigAutoField
BigIntegerField
BooleanField
CharField
TextField
IntegerField
PositiveIntegerField
FloatField
DecimalField
DateField
DateTimeField
TimeField
EmailField
URLField
UUIDField
FileField
ImageField
JSONField
SlugField
DurationField
GenericIPAddressField
```

---

# 7. Important Field Options

Common options:

```text
null
blank
default
unique
primary_key
db_index
editable
choices
verbose_name
help_text
db_column
```

Example:

```python
name = models.CharField(
    max_length=100,
    unique=True,
    db_index=True
)
```

---

# 8. `null=True`

Controls whether the database can store SQL `NULL`.

```python
age = models.IntegerField(null=True)
```

---

# 9. `blank=True`

Controls whether Django validation allows the field to be empty.

```python
name = models.CharField(
    max_length=100,
    blank=True
)
```

### Important

```text
null=True   → database level
blank=True  → validation level
```

---

# 10. `default`

Provides a default value.

```python
age = models.IntegerField(default=18)
```

---

# 11. `unique`

Ensures values are unique.

```python
email = models.EmailField(unique=True)
```

---

# 12. `primary_key`

Defines the primary key.

```python
student_id = models.IntegerField(primary_key=True)
```

If no primary key is specified, Django automatically creates one.

---

# 13. `db_index`

Creates a database index.

```python
email = models.EmailField(db_index=True)
```

Indexes can improve lookup performance, but they also have storage and write/update costs.

---

# 14. `choices`

Restricts a field to predefined choices.

```python
STATUS_CHOICES = [
    ("P", "Passed"),
    ("F", "Failed"),
]

status = models.CharField(
    max_length=1,
    choices=STATUS_CHOICES
)
```

---

# 15. `__str__()`

Defines the human-readable representation of a model object.

```python
def __str__(self):
    return self.name
```

Useful in:

* Django shell
* Admin
* debugging
* templates

---

# 16. Model Meta Class

`Meta` contains model-level configuration.

Example:

```python
class Meta:
    ordering = ["name"]
    db_table = "students"
```

Common Meta options:

```text
ordering
db_table
verbose_name
verbose_name_plural
constraints
indexes
unique_together
```

Modern Django code generally prefers explicit `UniqueConstraint` instead of `unique_together`.

---

# 17. Model Constraints

Constraints enforce rules at the database level.

Important constraints:

```text
UniqueConstraint
CheckConstraint
```

Example:

```python
class Meta:
    constraints = [
        models.CheckConstraint(
            condition=models.Q(age__gte=18),
            name="student_adult"
        )
    ]
```

---

# 18. Database Indexes

Indexes help databases find rows faster.

Example:

```python
class Meta:
    indexes = [
        models.Index(fields=["name"]),
        models.Index(fields=["city", "age"]),
    ]
```

---

# 19. Manager

A Manager provides the interface for database operations.

Default manager:

```python
objects
```

Example:

```python
Student.objects.all()
```

---

# 20. Custom Manager

You can create your own manager.

```python
class AdultStudentManager(models.Manager):

    def get_queryset(self):
        return super().get_queryset().filter(age__gte=18)
```

Then:

```python
class Student(models.Model):
    ...
    adults = AdultStudentManager()
```

---

# 21. QuerySet

A QuerySet represents a collection of database results.

```python
students = Student.objects.all()
```

---

# 22. QuerySet Characteristics

QuerySets are:

* Lazy
* Chainable
* Reusable
* Filterable
* Sliceable

Example:

```python
Student.objects.filter(
    marks__gte=70
).order_by("-marks")[:5]
```

---

# 23. Lazy Evaluation

Django normally doesn't execute a QuerySet immediately.

```python
students = Student.objects.filter(marks__gte=80)
```

The query is generally evaluated when results are needed.

Examples of evaluation:

```python
list(students)
```

```python
for student in students:
    ...
```

```python
len(students)
```

```python
bool(students)
```

```python
students.exists()
```

---

# 24. QuerySet Caching

After evaluation, a QuerySet may cache its results.

This is one reason repeated iteration over the same evaluated QuerySet can behave differently from repeatedly constructing fresh QuerySets.

Don't confuse:

```python
Student.objects.all()
```

with:

```python
students = Student.objects.all()
```

and then repeatedly executing separate new QuerySets.

---

# 25. CRUD

CRUD:

```text
C → Create
R → Read
U → Update
D → Delete
```

---

# 26. Create

```python
Student.objects.create(...)
```

or:

```python
student = Student(...)
student.save()
```

---

# 27. Read

```python
Student.objects.all()
```

---

# 28. Update

```python
student.age = 22
student.save()
```

or:

```python
Student.objects.filter(id=1).update(age=22)
```

---

# 29. Delete

```python
student.delete()
```

or:

```python
Student.objects.filter(age__lt=18).delete()
```

---

# 30. `get()`

Returns one object.

```python
Student.objects.get(id=1)
```

Possible exceptions:

```text
DoesNotExist
MultipleObjectsReturned
```

---

# 31. `filter()`

Returns a QuerySet.

```python
Student.objects.filter(age=20)
```

It can contain zero, one, or many objects.

---

# 32. `exclude()`

Returns objects that don't match the condition.

```python
Student.objects.exclude(city="Kochi")
```

---

# 33. `first()`

```python
Student.objects.order_by("marks").first()
```

Returns an object or `None`.

---

# 34. `last()`

```python
Student.objects.order_by("marks").last()
```

---

# 35. `earliest()` and `latest()`

Useful with date/time fields.

```python
Student.objects.earliest("joined_date")
```

```python
Student.objects.latest("joined_date")
```

---

# 36. `count()`

```python
Student.objects.count()
```

Returns the number of records.

---

# 37. `exists()`

```python
Student.objects.filter(email="a@example.com").exists()
```

Checks whether at least one matching object exists.

---

# 38. `contains()`

Modern Django versions also provide QuerySet membership checking:

```python
Student.objects.all().contains(student)
```

This is useful when you want to check whether a particular object belongs to a QuerySet.

---

# 39. `update()`

Updates matching database rows directly.

```python
Student.objects.filter(
    city="Kochi"
).update(
    marks=90
)
```

---

# 40. `update_fields`

When saving an object, you can restrict which fields are updated:

```python
student.name = "Rahul"
student.save(update_fields=["name"])
```

---

# 41. `bulk_create()`

Creates many objects efficiently.

```python
Student.objects.bulk_create([
    Student(name="A", age=20),
    Student(name="B", age=21),
    Student(name="C", age=22),
])
```

---

# 42. `bulk_update()`

Updates multiple existing objects.

```python
Student.objects.bulk_update(
    students,
    ["marks", "attendance"]
)
```

---

# 43. `get_or_create()`

Gets an existing object or creates one if it doesn't exist.

```python
student, created = Student.objects.get_or_create(
    email="a@example.com",
    defaults={
        "name": "Rahul",
        "age": 21,
    }
)
```

`created` tells you whether a new object was created.

---

# 44. `update_or_create()`

Updates an existing object or creates it.

```python
student, created = Student.objects.update_or_create(
    email="a@example.com",
    defaults={
        "name": "Rahul",
        "marks": 90,
    }
)
```

---

# 45. Field Lookups

Django uses double underscores:

```text
field__lookup
```

Common lookups:

```text
exact
iexact
contains
icontains
startswith
istartswith
endswith
iendswith
gt
gte
lt
lte
in
range
isnull
regex
iregex
```

---

# 46. Exact

```python
Student.objects.filter(name__exact="Rahul")
```

Usually:

```python
Student.objects.filter(name="Rahul")
```

is enough.

---

# 47. Case-Insensitive Search

```python
Student.objects.filter(
    name__iexact="rahul"
)
```

---

# 48. Contains

```python
Student.objects.filter(
    name__contains="rah"
)
```

Case-insensitive:

```python
Student.objects.filter(
    name__icontains="rah"
)
```

---

# 49. Comparison

```python
marks__gt=80
marks__gte=80
marks__lt=80
marks__lte=80
```

---

# 50. `in`

```python
Student.objects.filter(
    age__in=[18, 20, 22]
)
```

---

# 51. `range`

```python
Student.objects.filter(
    marks__range=(50, 90)
)
```

---

# 52. `isnull`

```python
Student.objects.filter(
    city__isnull=True
)
```

---

# 53. Ordering

Ascending:

```python
Student.objects.order_by("marks")
```

Descending:

```python
Student.objects.order_by("-marks")
```

Multiple:

```python
Student.objects.order_by(
    "department",
    "-marks"
)
```

---

# 54. Reverse Ordering

```python
Student.objects.order_by("-marks")
```

---

# 55. Clear Ordering

```python
Student.objects.order_by()
```

---

# 56. Slicing

```python
Student.objects.all()[:5]
```

```python
Student.objects.all()[5:10]
```

Negative indexing is not supported directly on QuerySets.

---

# 57. `values()`

Returns dictionaries.

```python
Student.objects.values(
    "name",
    "marks"
)
```

---

# 58. `values_list()`

Returns tuples.

```python
Student.objects.values_list(
    "name",
    "marks"
)
```

Single field:

```python
Student.objects.values_list(
    "name",
    flat=True
)
```

---

# 59. `distinct()`

Removes duplicate results.

```python
Student.objects.values(
    "city"
).distinct()
```

---

# 60. `reverse()`

Reverses QuerySet ordering.

```python
Student.objects.order_by(
    "marks"
).reverse()
```

---

# 61. `none()`

Returns an empty QuerySet.

```python
Student.objects.none()
```

Useful when you need a QuerySet that intentionally contains no records.

---

# 62. QuerySet Combination

Django supports combining QuerySets using:

```python
qs1 | qs2
```

and:

```python
qs1 & qs2
```

There is also:

```python
qs1.union(qs2)
qs1.intersection(qs2)
qs1.difference(qs2)
```

Database support can vary for particular operations.

---

# 63. Relationships

Django has three primary relationship types:

```text
One-to-One
Many-to-One
Many-to-Many
```

---

# 64. One-to-One

```python
student = models.OneToOneField(
    Student,
    on_delete=models.CASCADE
)
```

One Student → one Profile.

---

# 65. ForeignKey

```python
department = models.ForeignKey(
    Department,
    on_delete=models.CASCADE
)
```

Many students can belong to one department.

---

# 66. Many-to-Many

```python
courses = models.ManyToManyField(
    Course
)
```

Many students can take many courses.

---

# 67. `related_name`

```python
department = models.ForeignKey(
    Department,
    on_delete=models.CASCADE,
    related_name="students"
)
```

Then:

```python
department.students.all()
```

---

# 68. `related_query_name`

Controls the name used when querying through the reverse relationship.

It is especially useful when constructing reverse relationship filters.

---

# 69. `on_delete`

Common options:

```text
CASCADE
PROTECT
RESTRICT
SET_NULL
SET_DEFAULT
SET()
DO_NOTHING
```

### CASCADE

Delete dependent objects.

### PROTECT

Prevent deletion when related objects exist.

### RESTRICT

Restrict deletion according to Django's restricted-deletion behavior.

### SET_NULL

Set the foreign key to `NULL`.

Requires:

```python
null=True
```

### SET_DEFAULT

Use the field's default value.

### DO_NOTHING

Django does not automatically handle the related deletion.

---

# 70. Reverse Relationships

If:

```python
department = models.ForeignKey(
    Department,
    related_name="students",
    ...
)
```

then:

```python
department.students.all()
```

---

# 71. Many-to-Many Operations

Add:

```python
student.courses.add(course)
```

Remove:

```python
student.courses.remove(course)
```

Clear:

```python
student.courses.clear()
```

Set:

```python
student.courses.set([course1, course2])
```

---

# 72. Through Model

If a Many-to-Many relationship needs additional information, use an intermediary model.

Example:

```text
Student
   ↓
Enrollment
   ↓
Course
```

Enrollment might contain:

```text
student
course
enrolled_date
grade
```

---

# 73. Q Objects

`Q` objects construct complex query conditions.

```python
from django.db.models import Q
```

OR:

```python
Student.objects.filter(
    Q(age__gt=20) |
    Q(marks__gt=90)
)
```

AND:

```python
Student.objects.filter(
    Q(age__gt=20) &
    Q(marks__gt=80)
)
```

NOT:

```python
Student.objects.filter(
    ~Q(city="Kochi")
)
```

---

# 74. F Expressions

`F()` refers to a database field.

```python
from django.db.models import F
```

Compare fields:

```python
Student.objects.filter(
    marks__gt=F("attendance")
)
```

Update based on existing value:

```python
Student.objects.update(
    marks=F("marks") + 5
)
```

---

# 75. Q vs F

```text
Q → complex query conditions

F → reference database fields
```

Memory:

> Q = Query conditions
> F = Field reference

---

# 76. Aggregation

Aggregation produces summary calculations over a QuerySet.

Functions:

```text
Count
Sum
Avg
Min
Max
```

Example:

```python
Student.objects.aggregate(
    Avg("marks")
)
```

---

# 77. Annotation

Adds calculated information to each object/group.

```python
Department.objects.annotate(
    student_count=Count("students")
)
```

---

# 78. Aggregate vs Annotate

```text
aggregate()
    ↓
overall result

annotate()
    ↓
result attached to each row/group
```

---

# 79. Conditional Expressions

Django provides:

```text
Case
When
```

Example concept:

```python
Student.objects.annotate(
    result=Case(
        When(marks__gte=50, then=Value("Pass")),
        default=Value("Fail")
    )
)
```

---

# 80. `Value()`

Represents a literal value in an ORM expression.

```python
Value("Pass")
```

---

# 81. `ExpressionWrapper`

Used when Django needs explicit output-field information around an expression.

```python
ExpressionWrapper(
    F("marks") + F("attendance"),
    output_field=models.IntegerField()
)
```

---

# 82. Database Functions

Django supports database functions such as:

```text
Lower
Upper
Length
Concat
Coalesce
Extract
```

Example:

```python
from django.db.models.functions import Lower

Student.objects.annotate(
    lower_name=Lower("name")
)
```

---

# 83. Subquery

`Subquery()` allows a QuerySet to be used inside another query expression.

Useful for advanced queries such as retrieving related values from another QuerySet.

---

# 84. `OuterRef`

`OuterRef` allows a subquery to refer to a field from the outer query.

Usually used with:

```text
Subquery
```

---

# 85. `Exists`

There are two concepts you should distinguish:

```python
queryset.exists()
```

and:

```python
Exists(...)
```

`queryset.exists()` checks whether a QuerySet has results.

`Exists()` is an ORM expression useful inside queries/subqueries.

---

# 86. `only()`

Loads only specified fields initially.

```python
Student.objects.only(
    "name",
    "marks"
)
```

Be careful: accessing deferred fields later can cause additional queries.

---

# 87. `defer()`

Defers selected fields.

```python
Student.objects.defer("address")
```

Useful when some large fields aren't needed immediately.

---

# 88. `select_related()`

Best suited to single-valued relationships:

```text
ForeignKey
OneToOneField
```

Uses SQL joins.

```python
Student.objects.select_related(
    "department"
)
```

---

# 89. `prefetch_related()`

Best suited to multi-valued relationships:

```text
ManyToMany
reverse ForeignKey
```

Uses separate queries and combines the results.

```python
Student.objects.prefetch_related(
    "courses"
)
```

---

# 90. `Prefetch`

`Prefetch()` allows customization of a prefetch operation.

For example, you can prefetch a filtered QuerySet or store the result under a different attribute using `to_attr`.

---

# 91. N+1 Query Problem

Suppose:

```python
students = Student.objects.all()

for student in students:
    print(student.department.name)
```

If related departments aren't loaded efficiently, you can end up with one query for students plus additional queries for departments.

Use:

```python
select_related()
```

when appropriate.

---

# 92. Transactions

A transaction groups operations into a unit.

Django provides:

```python
transaction.atomic()
```

Example:

```python
with transaction.atomic():
    ...
```

If an exception causes the transaction to roll back, the database changes within the atomic block are not committed as a successful unit.

---

# 93. `atomic()`

Can be used as:

```python
with transaction.atomic():
    ...
```

or as a decorator:

```python
@transaction.atomic
def create_student():
    ...
```

---

# 94. `select_for_update()`

Used inside transactions to lock selected rows where supported.

```python
with transaction.atomic():
    student = Student.objects.select_for_update().get(
        id=1
    )
```

Useful for preventing conflicting concurrent updates.

---

# 95. Signals

Signals allow code to react to events.

Important signals include:

```text
pre_save
post_save
pre_delete
post_delete
m2m_changed
```

---

# 96. `pre_save`

Runs before saving.

---

# 97. `post_save`

Runs after saving.

It receives information such as:

```text
instance
created
```

---

# 98. `m2m_changed`

Runs when a Many-to-Many relationship changes.

It can respond to operations such as adding/removing relationships.

---

# 99. Signal Caution

Signals are useful, but excessive signal usage can make application behavior harder to understand.

For business logic that should be explicit and easy to trace, a service/function can sometimes be clearer.

---

# 100. ModelForm

A ModelForm is a form generated from a model.

```python
class StudentForm(forms.ModelForm):

    class Meta:
        model = Student
        fields = "__all__"
```

---

# 101. ModelForm Validation

Important methods/concepts:

```text
clean()
clean_<field>()
is_valid()
```

---

# 102. `clean_<field>()`

Used for validation/cleaning of one specific field.

```python
def clean_age(self):
    age = self.cleaned_data["age"]

    if age < 18:
        raise forms.ValidationError(
            "Age must be at least 18."
        )

    return age
```

---

# 103. `clean()`

Used for validation involving multiple fields or general form-level cleaning.

---

# 104. `commit=False`

```python
student = form.save(commit=False)
```

Creates the model object without immediately saving it.

You can modify it:

```python
student.name = student.name.title()
student.save()
```

---

# 105. Migrations

Migrations synchronize model changes with database schema.

```bash
python manage.py makemigrations
```

Creates migration files.

```bash
python manage.py migrate
```

Applies migrations.

---

# 106. Migration Commands

Useful commands:

```bash
python manage.py showmigrations
```

```bash
python manage.py sqlmigrate app_name 0001
```

The second command shows SQL Django would execute for a migration.

---

# 107. Migration Workflow

```text
Change Model
     ↓
makemigrations
     ↓
Migration file
     ↓
migrate
     ↓
Database schema updated
```

---

# 108. Django Admin

Register a model:

```python
admin.site.register(Student)
```

You can also customize:

```python
@admin.register(Student)
class StudentAdmin(admin.ModelAdmin):
    list_display = ["name", "age", "marks"]
```

---

# 109. Admin ORM Connection

Django Admin uses the model and ORM to:

* display objects
* create objects
* update objects
* delete objects
* search/filter data

---

# 110. Raw SQL

Django supports raw SQL when ORM isn't suitable for a particular query.

```python
Student.objects.raw(
    "SELECT * FROM sample1_student"
)
```

Raw SQL should be used carefully and parameterized when accepting external values.

---

# 111. `connection.cursor()`

For lower-level SQL:

```python
from django.db import connection

with connection.cursor() as cursor:
    cursor.execute(...)
```

---

# 112. Query Inspection

You can inspect generated SQL:

```python
queryset = Student.objects.filter(
    marks__gte=80
)

print(queryset.query)
```

This is very useful for learning how ORM maps to SQL.

---

# 113. `explain()`

You can ask the database for a query execution plan:

```python
Student.objects.filter(
    marks__gte=80
).explain()
```

Useful for performance analysis.

---

# 114. Database Functions vs Python Functions

When possible, database-side expressions can avoid unnecessarily loading data into Python.

For example:

```python
Student.objects.filter(
    marks__gt=F("attendance")
)
```

lets the database compare fields.

---

# 115. Custom QuerySet

You can create reusable QuerySet methods.

Concept:

```python
class StudentQuerySet(models.QuerySet):

    def passed(self):
        return self.filter(marks__gte=50)
```

Then expose it through a manager.

---

# 116. Custom Manager vs Custom QuerySet

```text
Custom Manager
    → custom entry point

Custom QuerySet
    → reusable chainable query methods
```

---

# 117. Database Routing

Advanced Django supports database routers for deciding:

* which database reads use
* which database writes use
* whether relations are allowed
* whether migrations apply

Useful in multi-database systems.

---

# 118. Multiple Databases

Django ORM can work with multiple databases.

Example:

```python
Student.objects.using("analytics").all()
```

And:

```python
Student.objects.using("analytics").create(...)
```

---

# 119. `db_manager()`

Managers can be directed to a particular database connection using `db_manager()`.

---

# 120. `save(using=...)`

Models can also specify the database when saving:

```python
student.save(using="analytics")
```

---

# 121. `atomic(using=...)`

Transactions can target a particular database connection.

---

# 122. Important ORM Performance Principles

Remember:

```text
1. Avoid unnecessary queries
2. Use select_related appropriately
3. Use prefetch_related appropriately
4. Retrieve only required fields when useful
5. Use bulk operations for suitable large operations
6. Use indexes for suitable query patterns
7. Inspect generated SQL
8. Use explain() for query plans
9. Avoid unnecessary Python-side processing
10. Measure before optimizing
```

---

# PART B — COMPLETE DJANGO ORM PRACTICAL

Now let's build one connected practice system.

## Project

```text
sampleproject
│
└── sample1
```

We'll use:

```text
Department
Student
StudentProfile
Course
Enrollment
```

---

# 1. Complete Models

```python
from django.db import models


class Department(models.Model):
    name = models.CharField(
        max_length=100,
        unique=True
    )

    def __str__(self):
        return self.name


class Course(models.Model):
    name = models.CharField(
        max_length=100
    )

    fee = models.DecimalField(
        max_digits=10,
        decimal_places=2
    )

    def __str__(self):
        return self.name


class Student(models.Model):
    name = models.CharField(
        max_length=100
    )

    email = models.EmailField(
        unique=True
    )

    age = models.IntegerField()

    city = models.CharField(
        max_length=100
    )

    marks = models.IntegerField()

    attendance = models.IntegerField()

    department = models.ForeignKey(
        Department,
        on_delete=models.CASCADE,
        related_name="students"
    )

    courses = models.ManyToManyField(
        Course,
        related_name="students",
        blank=True
    )

    def __str__(self):
        return self.name


class StudentProfile(models.Model):
    student = models.OneToOneField(
        Student,
        on_delete=models.CASCADE,
        related_name="profile"
    )

    phone = models.CharField(
        max_length=15
    )

    address = models.CharField(
        max_length=200
    )

    def __str__(self):
        return self.student.name


class Enrollment(models.Model):
    student = models.ForeignKey(
        Student,
        on_delete=models.CASCADE,
        related_name="enrollments"
    )

    course = models.ForeignKey(
        Course,
        on_delete=models.CASCADE,
        related_name="enrollments"
    )

    enrolled_date = models.DateField(
        auto_now_add=True
    )

    grade = models.CharField(
        max_length=5,
        blank=True
    )

    def __str__(self):
        return f"{self.student} - {self.course}"
```

This one structure lets you practice almost everything.

---

# 2. Migrations

```bash
python manage.py makemigrations
```

Then:

```bash
python manage.py migrate
```

---

# 3. Open Shell

```bash
python manage.py shell
```

Import:

```python
from sample1.models import (
    Department,
    Student,
    StudentProfile,
    Course,
    Enrollment
)
```

---

# 4. CREATE

## Departments

```python
cs = Department.objects.create(
    name="Computer Science"
)

commerce = Department.objects.create(
    name="Commerce"
)

science = Department.objects.create(
    name="Science"
)
```

---

# 5. Courses

```python
python = Course.objects.create(
    name="Python",
    fee=5000
)

django = Course.objects.create(
    name="Django",
    fee=6000
)

sql = Course.objects.create(
    name="SQL",
    fee=4000
)
```

---

# 6. Students

```python
rahul = Student.objects.create(
    name="Rahul",
    email="rahul@example.com",
    age=21,
    city="Kochi",
    marks=85,
    attendance=90,
    department=cs
)
```

```python
arun = Student.objects.create(
    name="Arun",
    email="arun@example.com",
    age=22,
    city="Kannur",
    marks=72,
    attendance=80,
    department=cs
)
```

```python
vishnu = Student.objects.create(
    name="Vishnu",
    email="vishnu@example.com",
    age=20,
    city="Kozhikode",
    marks=92,
    attendance=95,
    department=science
)
```

---

# 7. READ

```python
Student.objects.all()
```

---

# 8. Get

```python
Student.objects.get(id=1)
```

---

# 9. Filter

```python
Student.objects.filter(
    age=21
)
```

---

# 10. Exclude

```python
Student.objects.exclude(
    city="Kochi"
)
```

---

# 11. Comparison

```python
Student.objects.filter(
    marks__gt=80
)
```

```python
Student.objects.filter(
    marks__gte=80
)
```

```python
Student.objects.filter(
    marks__lt=80
)
```

```python
Student.objects.filter(
    marks__lte=80
)
```

---

# 12. String Searches

```python
Student.objects.filter(
    name__icontains="rah"
)
```

```python
Student.objects.filter(
    name__startswith="A"
)
```

```python
Student.objects.filter(
    name__endswith="n"
)
```

---

# 13. `in`

```python
Student.objects.filter(
    age__in=[20, 21, 22]
)
```

---

# 14. `range`

```python
Student.objects.filter(
    marks__range=(60, 90)
)
```

---

# 15. Ordering

```python
Student.objects.order_by(
    "marks"
)
```

```python
Student.objects.order_by(
    "-marks"
)
```

---

# 16. Top Students

```python
Student.objects.order_by(
    "-marks"
)[:3]
```

---

# 17. Update

```python
rahul.marks = 90
rahul.save()
```

Bulk update:

```python
Student.objects.filter(
    city="Kochi"
).update(
    attendance=95
)
```

---

# 18. Delete

```python
Student.objects.get(
    id=1
).delete()
```

---

# 19. Bulk Create

```python
Student.objects.bulk_create([
    Student(
        name="Akhil",
        email="akhil@example.com",
        age=21,
        city="Kochi",
        marks=75,
        attendance=82,
        department=cs
    ),
    Student(
        name="Nikhil",
        email="nikhil@example.com",
        age=23,
        city="Kannur",
        marks=88,
        attendance=91,
        department=cs
    ),
])
```

---

# 20. `get_or_create`

```python
student, created = Student.objects.get_or_create(
    email="rahul@example.com",
    defaults={
        "name": "Rahul",
        "age": 21,
        "city": "Kochi",
        "marks": 85,
        "attendance": 90,
        "department": cs
    }
)
```

---

# 21. `update_or_create`

```python
student, created = Student.objects.update_or_create(
    email="rahul@example.com",
    defaults={
        "marks": 95
    }
)
```

---

# 22. Relationships

## ForeignKey

```python
rahul.department
```

Reverse:

```python
cs.students.all()
```

---

# 23. One-to-One

```python
StudentProfile.objects.create(
    student=rahul,
    phone="9876543210",
    address="Kochi"
)
```

Access:

```python
rahul.profile
```

---

# 24. Many-to-Many

```python
rahul.courses.add(
    python,
    django
)
```

View:

```python
rahul.courses.all()
```

Reverse:

```python
python.students.all()
```

---

# 25. Remove

```python
rahul.courses.remove(
    django
)
```

---

# 26. Clear

```python
rahul.courses.clear()
```

---

# 27. Set

```python
rahul.courses.set([
    python,
    sql
])
```

---

# 28. Enrollment

```python
Enrollment.objects.create(
    student=rahul,
    course=python,
    grade="A"
)
```

Now:

```python
rahul.enrollments.all()
```

and:

```python
python.enrollments.all()
```

---

# 29. Q PRACTICAL

```python
from django.db.models import Q
```

### OR

```python
Student.objects.filter(
    Q(marks__gte=90) |
    Q(attendance__gte=95)
)
```

### AND

```python
Student.objects.filter(
    Q(marks__gte=80) &
    Q(attendance__gte=80)
)
```

### NOT

```python
Student.objects.filter(
    ~Q(city="Kochi")
)
```

---

# 30. F PRACTICAL

```python
from django.db.models import F
```

Find:

```text
marks > attendance
```

```python
Student.objects.filter(
    marks__gt=F("attendance")
)
```

Increase all marks:

```python
Student.objects.update(
    marks=F("marks") + 5
)
```

---

# 31. Aggregation

```python
from django.db.models import (
    Avg,
    Sum,
    Count,
    Max,
    Min
)
```

```python
Student.objects.aggregate(
    average=Avg("marks"),
    total=Sum("marks"),
    highest=Max("marks"),
    lowest=Min("marks"),
    count=Count("id")
)
```

---

# 32. Department Annotation

```python
Department.objects.annotate(
    student_count=Count("students")
)
```

---

# 33. Average Marks by Department

```python
Department.objects.annotate(
    average_marks=Avg(
        "students__marks"
    )
)
```

---

# 34. Departments with More Than 2 Students

```python
Department.objects.annotate(
    student_count=Count("students")
).filter(
    student_count__gt=2
)
```

---

# 35. Course Count Per Student

```python
Student.objects.annotate(
    course_count=Count("courses")
)
```

---

# 36. Related Lookups

Students in CS:

```python
Student.objects.filter(
    department__name="Computer Science"
)
```

---

# 37. Multi-Level Lookup

For example:

```python
Student.objects.filter(
    department__name__icontains="computer"
)
```

---

# 38. `select_related`

```python
students = Student.objects.select_related(
    "department"
)
```

Then:

```python
for student in students:
    print(
        student.name,
        student.department.name
    )
```

---

# 39. `prefetch_related`

```python
students = Student.objects.prefetch_related(
    "courses"
)
```

Then:

```python
for student in students:
    print(student.name)

    for course in student.courses.all():
        print(course.name)
```

---

# 40. Both

```python
students = Student.objects.select_related(
    "department"
).prefetch_related(
    "courses"
)
```

---

# 41. `Prefetch`

Conceptually:

```python
from django.db.models import Prefetch

Student.objects.prefetch_related(
    Prefetch(
        "courses",
        queryset=Course.objects.filter(
            fee__gte=5000
        )
    )
)
```

This lets you customize what is prefetched.

---

# 42. `values`

```python
Student.objects.values(
    "name",
    "marks"
)
```

---

# 43. `values_list`

```python
Student.objects.values_list(
    "name",
    "marks"
)
```

---

# 44. Unique Cities

```python
Student.objects.values(
    "city"
).distinct()
```

---

# 45. Exists

```python
Student.objects.filter(
    marks__gte=90
).exists()
```

---

# 46. Count

```python
Student.objects.count()
```

---

# 47. First / Last

```python
Student.objects.order_by(
    "-marks"
).first()
```

```python
Student.objects.order_by(
    "marks"
).last()
```

---

# 48. Conditional Annotation

```python
from django.db.models import Case, When, Value, CharField
```

```python
Student.objects.annotate(
    result=Case(
        When(
            marks__gte=50,
            then=Value("Pass")
        ),
        default=Value("Fail"),
        output_field=CharField()
    )
)
```

---

# 49. Database Function

```python
from django.db.models.functions import Lower
```

```python
Student.objects.annotate(
    lower_name=Lower("name")
)
```

---

# 50. `Concat`

```python
from django.db.models.functions import Concat
from django.db.models import Value
```

Concept:

```python
Student.objects.annotate(
    label=Concat(
        "name",
        Value(" - "),
        "city"
    )
)
```

---

# 51. `Subquery` + `OuterRef`

Example concept:

```python
from django.db.models import OuterRef, Subquery
```

You can use a subquery to retrieve a related value from another QuerySet based on the current outer row.

This is an advanced ORM technique and is especially useful when a join/annotation alone doesn't express the required query clearly.

---

# 52. `Exists()` Expression

```python
from django.db.models import Exists, OuterRef
```

Concept:

```python
enrollments = Enrollment.objects.filter(
    student=OuterRef("pk")
)

Student.objects.annotate(
    has_enrollment=Exists(enrollments)
)
```

Now each student gets a boolean-like annotation indicating whether matching enrollment records exist.

---

# 53. `only`

```python
Student.objects.only(
    "name",
    "marks"
)
```

---

# 54. `defer`

```python
Student.objects.defer(
    "email"
)
```

---

# 55. `select_for_update`

```python
from django.db import transaction

with transaction.atomic():

    student = Student.objects.select_for_update().get(
        id=1
    )

    student.marks += 5
    student.save()
```

---

# 56. Transaction Practical

```python
from django.db import transaction

with transaction.atomic():

    student = Student.objects.create(
        name="New Student",
        email="new@example.com",
        age=21,
        city="Kochi",
        marks=80,
        attendance=90,
        department=cs
    )

    StudentProfile.objects.create(
        student=student,
        phone="9999999999",
        address="Kochi"
    )
```

---

# 57. Rollback Practical

```python
with transaction.atomic():

    student = Student.objects.create(
        name="Test",
        email="test@example.com",
        age=20,
        city="Kochi",
        marks=70,
        attendance=80,
        department=cs
    )

    raise Exception("Error")
```

The atomic block rolls back because the exception escapes the block.

---

# 58. Signals Practical

`signals.py`

```python
from django.db.models.signals import post_save
from django.dispatch import receiver

from .models import Student


@receiver(
    post_save,
    sender=Student
)
def student_saved(
    sender,
    instance,
    created,
    **kwargs
):

    if created:
        print("Student created")

    else:
        print("Student updated")
```

---

# 59. `pre_save`

```python
from django.db.models.signals import pre_save
```

```python
@receiver(
    pre_save,
    sender=Student
)
def before_save(
    sender,
    instance,
    **kwargs
):

    instance.name = instance.name.title()
```

---

# 60. ModelForm Practical

```python
from django import forms
from .models import Student


class StudentForm(forms.ModelForm):

    class Meta:
        model = Student
        fields = "__all__"
```

---

# 61. Form Validation

```python
def clean_age(self):

    age = self.cleaned_data["age"]

    if age < 18:
        raise forms.ValidationError(
            "Student must be at least 18."
        )

    return age
```

---

# 62. Form-Level `clean()`

```python
def clean(self):

    cleaned_data = super().clean()

    marks = cleaned_data.get("marks")
    attendance = cleaned_data.get("attendance")

    if (
        marks is not None
        and attendance is not None
        and marks < 0
    ):
        raise forms.ValidationError(
            "Invalid marks."
        )

    return cleaned_data
```

---

# 63. `commit=False`

```python
student = form.save(
    commit=False
)

student.name = student.name.title()

student.save()
```

---

# 64. Query SQL Inspection

```python
queryset = Student.objects.filter(
    marks__gte=80
)

print(queryset.query)
```

---

# 65. Query Execution Plan

```python
queryset.explain()
```

This is useful for understanding database execution plans and performance.

---

# 66. Custom QuerySet Practical

```python
class StudentQuerySet(models.QuerySet):

    def passed(self):
        return self.filter(
            marks__gte=50
        )

    def top_students(self):
        return self.filter(
            marks__gte=80
        )
```

Then expose it through a manager.

---

# 67. Custom Manager Practical

```python
class StudentManager(models.Manager):

    def passed(self):
        return self.get_queryset().filter(
            marks__gte=50
        )
```

Then:

```python
class Student(models.Model):

    ...

    objects = StudentManager()
```

Use:

```python
Student.objects.passed()
```

---

# 68. Multiple Database Practical

```python
Student.objects.using(
    "analytics"
).all()
```

---

# 69. Save to Specific Database

```python
student.save(
    using="analytics"
)
```

---

# 70. Raw SQL Practical

```python
students = Student.objects.raw(
    "SELECT * FROM sample1_student"
)
```

---

# 71. Cursor Practical

```python
from django.db import connection

with connection.cursor() as cursor:

    cursor.execute(
        "SELECT COUNT(*) FROM sample1_student"
    )

    result = cursor.fetchone()
```

When using user-supplied values, use parameterized queries rather than string concatenation.

---

# 72. COMPLETE ORM PRACTICAL FLOW

Practice everything in this exact order:

```text
1. Create project
        ↓
2. Create app
        ↓
3. Create models
        ↓
4. makemigrations
        ↓
5. migrate
        ↓
6. Create objects
        ↓
7. Read objects
        ↓
8. Update objects
        ↓
9. Delete objects
        ↓
10. get / filter / exclude
        ↓
11. Lookups
        ↓
12. Ordering
        ↓
13. Slicing
        ↓
14. values / values_list
        ↓
15. distinct
        ↓
16. exists / count
        ↓
17. CRUD shortcuts
        ↓
18. ForeignKey
        ↓
19. OneToOne
        ↓
20. ManyToMany
        ↓
21. related_name
        ↓
22. on_delete
        ↓
23. Q
        ↓
24. F
        ↓
25. aggregate
        ↓
26. annotate
        ↓
27. Case / When
        ↓
28. Database functions
        ↓
29. Subquery / OuterRef
        ↓
30. Exists
        ↓
31. select_related
        ↓
32. prefetch_related
        ↓
33. Prefetch
        ↓
34. only / defer
        ↓
35. Transactions
        ↓
36. select_for_update
        ↓
37. Signals
        ↓
38. ModelForms
        ↓
39. Custom Managers
        ↓
40. Custom QuerySets
        ↓
41. Constraints
        ↓
42. Indexes
        ↓
43. Query inspection
        ↓
44. explain()
        ↓
45. Raw SQL
        ↓
46. Multiple databases
```

---

# PART C — REVIEWER RAPID-FIRE

You should be able to answer these without looking.

### Fundamentals

1. What is ORM?
2. Why do we use ORM?
3. What is a model?
4. Model vs table?
5. Object vs row?
6. Field vs column?
7. What is a manager?
8. What is QuerySet?
9. What is lazy evaluation?
10. What is QuerySet caching?

### CRUD

11. `get()` vs `filter()`
12. `create()` vs `save()`
13. `update()` vs `save()`
14. `bulk_create()` vs `create()`
15. `bulk_update()`
16. `get_or_create()`
17. `update_or_create()`
18. `exists()`
19. `count()`
20. `first()` / `last()`

### Fields

21. `null` vs `blank`
22. `default`
23. `unique`
24. `primary_key`
25. `db_index`
26. `choices`
27. `editable`

### Relationships

28. One-to-One
29. ForeignKey
30. Many-to-Many
31. `related_name`
32. `related_query_name`
33. `on_delete`
34. `CASCADE`
35. `PROTECT`
36. `SET_NULL`
37. Through model

### Queries

38. Field lookups
39. `Q`
40. `F`
41. Q vs F
42. `values()`
43. `values_list()`
44. `distinct()`
45. QuerySet chaining

### Calculations

46. Aggregation
47. Annotation
48. `aggregate()` vs `annotate()`
49. `Count`
50. `Sum`
51. `Avg`
52. `Max`
53. `Min`

### Advanced expressions

54. `Case`
55. `When`
56. `Value`
57. `ExpressionWrapper`
58. Database functions
59. `Subquery`
60. `OuterRef`
61. `Exists`

### Optimization

62. What is N+1?
63. `select_related()`
64. `prefetch_related()`
65. `Prefetch`
66. Difference between select and prefetch
67. `only()`
68. `defer()`
69. `explain()`
70. Database indexes

### Transactions

71. What is a transaction?
72. What is `atomic()`?
73. What is rollback?
74. What is `select_for_update()`?
75. Why use row locking?

### Signals

76. What are signals?
77. `pre_save`
78. `post_save`
79. `pre_delete`
80. `post_delete`
81. `m2m_changed`

### Forms

82. What is ModelForm?
83. `is_valid()`
84. `clean()`
85. `clean_<field>()`
86. `commit=False`

### Advanced

87. Custom Manager
88. Custom QuerySet
89. Multiple databases
90. Database routers
91. Raw SQL
92. `connection.cursor()`
93. Migration system
94. Constraints
95. Indexes

---

# 🔥 THE FINAL DJANGO ORM MEMORY MAP

If your reviewer asks:

**"Explain Django ORM from basics to advanced."**

Think of this:

```text
                         DJANGO ORM
                             │
        ┌────────────────────┼────────────────────┐
        ↓                    ↓                    ↓
      MODEL               MANAGER              DATABASE
        │                    │                    │
      Fields              QuerySet              SQL
        │                    │                    │
        └──────────── CRUD ──┘                    │
                             │                    │
                 ┌───────────┴───────────┐        │
                 ↓                       ↓        │
             LOOKUPS                  Q / F       │
                 │                       │        │
                 └───────────┬───────────┘        │
                             ↓                    │
                    AGGREGATE / ANNOTATE          │
                             │                    │
                    ┌────────┴────────┐           │
                    ↓                 ↓           │
              RELATIONSHIPS      EXPRESSIONS      │
                    │                 │            │
              FK / O2O / M2M     Case / When      │
                    │             Subquery         │
                    │             OuterRef         │
                    │             Exists           │
                    ↓                 ↓            │
             SELECT_RELATED     PREFETCH           │
                    │                 │            │
                    └────────┬────────┘            │
                             ↓                     │
                       OPTIMIZATION                │
                             │                     │
                   ┌─────────┴─────────┐           │
                   ↓                   ↓           │
                INDEXES             explain()      │
                             │                     │
                             ↓                     │
                       TRANSACTIONS                │
                             │                     │
                      atomic / locking             │
                             │                     │
                             ↓                     │
                         SIGNALS                   │
                             │                     │
                             ↓                     │
                        MODEL FORMS                │
                             │                     │
                             ↓                     │
                  CUSTOM MANAGERS / QUERYSETS     │
                             │                     │
                             ↓                     │
                      RAW SQL / MULTI-DB ─────────┘
```

## ✅ Final completeness checklist

For your **Django ORM review**, the master set now includes:

**ORM fundamentals → Models → Fields → Field options → Meta → Constraints → Indexes → Managers → Custom Managers → QuerySets → Lazy evaluation → QuerySet caching → CRUD → Query methods → Lookups → Ordering → Slicing → Values → Values list → Distinct → Relationships → Reverse relationships → `related_name` → `related_query_name` → `on_delete` → Through models → Q → F → Aggregation → Annotation → Case/When → Value → ExpressionWrapper → Database functions → Subquery → OuterRef → Exists → `select_related` → `prefetch_related` → `Prefetch` → `only` → `defer` → N+1 → Transactions → `atomic` → `select_for_update` → Signals → ModelForms → validation → `commit=False` → migrations → admin → custom QuerySets → multiple databases → routers → raw SQL → cursor → SQL inspection → `explain()` → ORM performance.**
