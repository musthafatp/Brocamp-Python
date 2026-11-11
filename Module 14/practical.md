# DRF Practical Brain Dump — Function-Based Views (FBV) Only

> **Scope:** This practical guide uses Django REST Framework Function-Based Views only. It does not cover Class-Based Views (CBV), `APIView`, generic views, mixins, or ViewSets.

The examples use a simple **Student API** so that each concept is easy to understand and test. Replace the example app/model names with your own project names when practising.

---

## 1. Create a Django project and install DRF

### Install Django and Django REST Framework

```bash
pip install django djangorestframework
```

### Create the project and app

```bash
django-admin startproject drf_project
cd drf_project
python manage.py startapp students
```

### Add apps in `settings.py`

```python
INSTALLED_APPS = [
    # Django apps...
    "rest_framework",
    "students",
]
```

### Run the project

```bash
python manage.py migrate
python manage.py runserver
```

---

## 2. First API without a model or serializer

**Goal:** Return a simple JSON response.

**File: `students/views.py`**

```python
from rest_framework.decorators import api_view
from rest_framework.response import Response

@api_view(["GET"])
def welcome_api(request):
    return Response({
        "message": "Welcome to my first DRF API"
    })
```

**File: `students/urls.py`**

```python
from django.urls import path
from . import views

urlpatterns = [
    path("welcome/", views.welcome_api, name="welcome_api"),
]
```

**File: project `urls.py`**

```python
from django.contrib import admin
from django.urls import path, include

urlpatterns = [
    path("admin/", admin.site.urls),
    path("api/", include("students.urls")),
]
```

**Test:** `GET http://127.0.0.1:8000/api/welcome/`

Expected response:

```json
{
    "message": "Welcome to my first DRF API"
}
```

### Important points

- `@api_view(["GET"])` allows only GET requests.
- `request` contains information about the incoming request.
- `Response()` creates a DRF response and renders the returned data as JSON by default when using the JSON renderer.

---

## 3. API without a model — using a Python list

**Goal:** Practise Create, Read, Update, and Delete without storing data in a database.

**File: `students/views.py`**

```python
from rest_framework.decorators import api_view
from rest_framework.response import Response
from rest_framework import status

students_data = [
    {"id": 1, "name": "Arun", "age": 21, "course": "Python"},
    {"id": 2, "name": "Maya", "age": 22, "course": "Django"},
]

@api_view(["GET", "POST"])
def student_list_create(request):
    if request.method == "GET":
        return Response(students_data)

    if request.method == "POST":
        new_student = {
            "id": max([student["id"] for student in students_data], default=0) + 1,
            "name": request.data.get("name"),
            "age": request.data.get("age"),
            "course": request.data.get("course"),
        }

        students_data.append(new_student)
        return Response(new_student, status=status.HTTP_201_CREATED)


@api_view(["GET", "PUT", "PATCH", "DELETE"])
def student_detail(request, student_id):
    student = next(
        (item for item in students_data if item["id"] == student_id),
        None
    )

    if student is None:
        return Response(
            {"error": "Student not found"},
            status=status.HTTP_404_NOT_FOUND
        )

    if request.method == "GET":
        return Response(student)

    if request.method == "PUT":
        student["name"] = request.data.get("name")
        student["age"] = request.data.get("age")
        student["course"] = request.data.get("course")
        return Response(student)

    if request.method == "PATCH":
        student.update(request.data)
        return Response(student)

    if request.method == "DELETE":
        students_data.remove(student)
        return Response(status=status.HTTP_204_NO_CONTENT)
```

**File: `students/urls.py`**

```python
from django.urls import path
from . import views

urlpatterns = [
    path("students/", views.student_list_create),
    path("students/<int:student_id>/", views.student_detail),
]
```

### Test the endpoints

| Method | URL | Purpose |
|---|---|---|
| GET | `/api/students/` | Get all students |
| POST | `/api/students/` | Add a student |
| GET | `/api/students/1/` | Get one student |
| PUT | `/api/students/1/` | Replace/update the student's fields |
| PATCH | `/api/students/1/` | Partially update the student |
| DELETE | `/api/students/1/` | Delete the student |

**POST body:**

```json
{
    "name": "Nikhil",
    "age": 23,
    "course": "DRF"
}
```

> **Note:** This list is only for learning. Data is held in memory, so it resets when the server restarts. A Python list is not a replacement for database storage.

---

## 4. Create a model

**Goal:** Store student records in the database.

**File: `students/models.py`**

```python
from django.db import models

class Student(models.Model):
    name = models.CharField(max_length=100)
    age = models.PositiveIntegerField()
    email = models.EmailField(unique=True)
    course = models.CharField(max_length=100)

    def __str__(self):
        return self.name
```

Create and apply migrations:

```bash
python manage.py makemigrations
python manage.py migrate
```

---

## 5. Create a ModelSerializer

**Goal:** Convert model instances to Python data that can be rendered as JSON, and validate incoming data before saving it.

**File: `students/serializers.py`**

```python
from rest_framework import serializers
from .models import Student

class StudentSerializer(serializers.ModelSerializer):
    class Meta:
        model = Student
        fields = "__all__"
```

### What does `ModelSerializer` do?

- Generates serializer fields based on the model.
- Provides default create and update behaviour.
- Performs validation.
- Converts model instances into serializable data.

---

## 6. GET — retrieve all records using FBV

**File: `students/views.py`**

```python
from rest_framework.decorators import api_view
from rest_framework.response import Response
from .models import Student
from .serializers import StudentSerializer

@api_view(["GET"])
def student_list(request):
    students = Student.objects.all()
    serializer = StudentSerializer(students, many=True)
    return Response(serializer.data)
```

### Important

- `Student.objects.all()` retrieves all student records.
- `many=True` is required when serializing a queryset or multiple objects.
- `serializer.data` contains the serialized representation.

---

## 7. GET — retrieve a single record

```python
from rest_framework.decorators import api_view
from rest_framework.response import Response
from rest_framework import status
from .models import Student
from .serializers import StudentSerializer

@api_view(["GET"])
def student_detail(request, student_id):
    try:
        student = Student.objects.get(id=student_id)
    except Student.DoesNotExist:
        return Response(
            {"error": "Student not found"},
            status=status.HTTP_404_NOT_FOUND
        )

    serializer = StudentSerializer(student)
    return Response(serializer.data)
```

**Test:** `GET /api/students/1/`

- `get()` retrieves one matching object.
- If the object does not exist, Django raises `Student.DoesNotExist`.
- A single object does not need `many=True`.

---

## 8. POST — create a record

```python
@api_view(["POST"])
def student_create(request):
    serializer = StudentSerializer(data=request.data)

    if serializer.is_valid():
        serializer.save()
        return Response(
            serializer.data,
            status=status.HTTP_201_CREATED
        )

    return Response(
        serializer.errors,
        status=status.HTTP_400_BAD_REQUEST
    )
```

**Example request body:**

```json
{
    "name": "Rahul",
    "age": 22,
    "email": "rahul@example.com",
    "course": "Django REST Framework"
}
```

### How it works

1. `request.data` reads the submitted request body.
2. `StudentSerializer(data=request.data)` passes incoming data to the serializer.
3. `is_valid()` checks the data.
4. `save()` creates the model object when validation succeeds.
5. `serializer.data` returns the created object's serialized data.
6. `serializer.errors` returns validation errors when the data is invalid.

---

## 9. PUT — complete update

```python
@api_view(["PUT"])
def student_update(request, student_id):
    try:
        student = Student.objects.get(id=student_id)
    except Student.DoesNotExist:
        return Response(
            {"error": "Student not found"},
            status=status.HTTP_404_NOT_FOUND
        )

    serializer = StudentSerializer(student, data=request.data)

    if serializer.is_valid():
        serializer.save()
        return Response(serializer.data)

    return Response(
        serializer.errors,
        status=status.HTTP_400_BAD_REQUEST
    )
```

**PUT request body:** Send all required fields.

```json
{
    "name": "Rahul Kumar",
    "age": 23,
    "email": "rahul@example.com",
    "course": "Advanced Django"
}
```

**Remember:** PUT normally represents a full update. Required fields must be supplied unless the serializer defines otherwise.

---

## 10. PATCH — partial update

```python
@api_view(["PATCH"])
def student_partial_update(request, student_id):
    try:
        student = Student.objects.get(id=student_id)
    except Student.DoesNotExist:
        return Response(
            {"error": "Student not found"},
            status=status.HTTP_404_NOT_FOUND
        )

    serializer = StudentSerializer(
        student,
        data=request.data,
        partial=True
    )

    if serializer.is_valid():
        serializer.save()
        return Response(serializer.data)

    return Response(
        serializer.errors,
        status=status.HTTP_400_BAD_REQUEST
    )
```

**PATCH request body:**

```json
{
    "age": 24
}
```

**Important:** `partial=True` tells the serializer that omitted required fields do not need to be supplied for this partial update.

---

## 11. DELETE — delete a record

```python
@api_view(["DELETE"])
def student_delete(request, student_id):
    try:
        student = Student.objects.get(id=student_id)
    except Student.DoesNotExist:
        return Response(
            {"error": "Student not found"},
            status=status.HTTP_404_NOT_FOUND
        )

    student.delete()
    return Response(status=status.HTTP_204_NO_CONTENT)
```

**Remember:** HTTP 204 means the request succeeded and the response has no body.

---

## 12. Combine CRUD operations into two FBVs

Instead of creating a separate function for every operation, you can handle collection operations in one function and single-object operations in another.

**File: `students/views.py`**

```python
from rest_framework.decorators import api_view
from rest_framework.response import Response
from rest_framework import status
from .models import Student
from .serializers import StudentSerializer

@api_view(["GET", "POST"])
def student_list_create(request):
    if request.method == "GET":
        students = Student.objects.all()
        serializer = StudentSerializer(students, many=True)
        return Response(serializer.data)

    serializer = StudentSerializer(data=request.data)

    if serializer.is_valid():
        serializer.save()
        return Response(
            serializer.data,
            status=status.HTTP_201_CREATED
        )

    return Response(serializer.errors, status=status.HTTP_400_BAD_REQUEST)


@api_view(["GET", "PUT", "PATCH", "DELETE"])
def student_detail(request, student_id):
    try:
        student = Student.objects.get(id=student_id)
    except Student.DoesNotExist:
        return Response(
            {"error": "Student not found"},
            status=status.HTTP_404_NOT_FOUND
        )

    if request.method == "GET":
        serializer = StudentSerializer(student)
        return Response(serializer.data)

    if request.method == "PUT":
        serializer = StudentSerializer(student, data=request.data)

    elif request.method == "PATCH":
        serializer = StudentSerializer(
            student,
            data=request.data,
            partial=True
        )

    elif request.method == "DELETE":
        student.delete()
        return Response(status=status.HTTP_204_NO_CONTENT)

    if serializer.is_valid():
        serializer.save()
        return Response(serializer.data)

    return Response(serializer.errors, status=status.HTTP_400_BAD_REQUEST)
```

**File: `students/urls.py`**

```python
from django.urls import path
from . import views

urlpatterns = [
    path("students/", views.student_list_create, name="student_list_create"),
    path("students/<int:student_id>/", views.student_detail, name="student_detail"),
]
```

---

## 13. Serializer field validation

**Goal:** Validate one field before saving data.

**File: `students/serializers.py`**

```python
from rest_framework import serializers
from .models import Student

class StudentSerializer(serializers.ModelSerializer):

    class Meta:
        model = Student
        fields = "__all__"

    def validate_age(self, value):
        if value < 18:
            raise serializers.ValidationError(
                "Student age must be at least 18"
            )
        return value
```

### How it works

- The method name must follow `validate_<field_name>`.
- `value` is the submitted value for that field.
- Raise `serializers.ValidationError` when the value is invalid.
- Return the value when it is valid.

---

## 14. Object-level validation

**Goal:** Validate multiple fields together.

```python
class StudentSerializer(serializers.ModelSerializer):

    class Meta:
        model = Student
        fields = "__all__"

    def validate(self, data):
        name = data.get("name", getattr(self.instance, "name", None))
        course = data.get("course", getattr(self.instance, "course", None))

        if name and course and name.lower() == course.lower():
            raise serializers.ValidationError(
                "Name and course cannot be the same"
            )

        return data
```

**Difference:**

- `validate_age()` validates one field.
- `validate()` validates the complete set of submitted values together.

---

## 15. Use a normal Serializer without a model

**Goal:** Validate data without creating a database model.

**File: `students/serializers.py`**

```python
from rest_framework import serializers

class EmployeeSerializer(serializers.Serializer):
    name = serializers.CharField(max_length=100)
    age = serializers.IntegerField()
    email = serializers.EmailField()
    department = serializers.CharField(max_length=100)

    def validate_age(self, value):
        if value < 18:
            raise serializers.ValidationError("Age must be at least 18")
        return value
```

**File: `students/views.py`**

```python
@api_view(["POST"])
def employee_data(request):
    serializer = EmployeeSerializer(data=request.data)

    if serializer.is_valid():
        return Response({
            "message": "Data is valid",
            "data": serializer.validated_data
        })

    return Response(serializer.errors, status=status.HTTP_400_BAD_REQUEST)
```

**Important:** A normal `Serializer` does not automatically create a model record. You define `create()`/`update()` if you want it to save something, or handle the validated data yourself.

---

## 16. Read query parameters

**Goal:** Receive values from the URL query string.

Example URL:

`/api/students/search/?name=Rahul&course=Django`

```python
@api_view(["GET"])
def search_students(request):
    name = request.query_params.get("name")
    course = request.query_params.get("course")

    students = Student.objects.all()

    if name:
        students = students.filter(name__icontains=name)

    if course:
        students = students.filter(course__icontains=course)

    serializer = StudentSerializer(students, many=True)
    return Response(serializer.data)
```

### Important

- `request.query_params` reads query-string values.
- `request.query_params.get("name")` reads the `name` parameter.
- `icontains` performs a case-insensitive partial match.
- Query parameters are not the same as JSON body data in `request.data`.

---

## 17. Filter by a specific field

Example URL:

`/api/students/filter/?age=22`

```python
@api_view(["GET"])
def filter_students(request):
    age = request.query_params.get("age")

    students = Student.objects.all()

    if age:
        students = students.filter(age=age)

    serializer = StudentSerializer(students, many=True)
    return Response(serializer.data)
```

**Practice:** Add filters for `course`, `name`, and `age`.

---

## 18. Search using multiple fields

Example URL:

`/api/students/search/?search=rah`

```python
from django.db.models import Q

@api_view(["GET"])
def search_students(request):
    search = request.query_params.get("search")

    students = Student.objects.all()

    if search:
        students = students.filter(
            Q(name__icontains=search) |
            Q(email__icontains=search) |
            Q(course__icontains=search)
        )

    serializer = StudentSerializer(students, many=True)
    return Response(serializer.data)
```

**Important:** `Q` objects allow OR conditions. The `|` operator means OR.

---

## 19. Ordering records

Example URLs:

- `/api/students/order/?ordering=name`
- `/api/students/order/?ordering=-age`

```python
@api_view(["GET"])
def order_students(request):
    ordering = request.query_params.get("ordering", "name")

    allowed_fields = ["name", "age", "course", "-name", "-age", "-course"]

    if ordering not in allowed_fields:
        return Response(
            {"error": "Invalid ordering field"},
            status=status.HTTP_400_BAD_REQUEST
        )

    students = Student.objects.all().order_by(ordering)
    serializer = StudentSerializer(students, many=True)
    return Response(serializer.data)
```

**Remember:**

- `name` means ascending order.
- `-name` means descending order.
- Validate client-provided ordering fields instead of passing arbitrary values blindly.

---

## 20. Combine filtering, searching, and ordering

Example URL:

`/api/students/list/?course=django&search=rah&ordering=-age`

```python
from django.db.models import Q

@api_view(["GET"])
def student_filter_search_order(request):
    students = Student.objects.all()

    course = request.query_params.get("course")
    search = request.query_params.get("search")
    ordering = request.query_params.get("ordering", "name")

    if course:
        students = students.filter(course__icontains=course)

    if search:
        students = students.filter(
            Q(name__icontains=search) |
            Q(email__icontains=search)
        )

    allowed_fields = ["name", "age", "-name", "-age"]

    if ordering not in allowed_fields:
        return Response(
            {"error": "Invalid ordering field"},
            status=status.HTTP_400_BAD_REQUEST
        )

    students = students.order_by(ordering)
    serializer = StudentSerializer(students, many=True)
    return Response(serializer.data)
```

---

## 21. Pagination manually in an FBV

**Goal:** Return a limited number of records per page.

Example URL: `/api/students/paginated/?page=1&page_size=5`

```python
from rest_framework.pagination import PageNumberPagination

@api_view(["GET"])
def student_pagination(request):
    students = Student.objects.all().order_by("id")

    paginator = PageNumberPagination()
    paginator.page_size = 5

    page = paginator.paginate_queryset(students, request)
    serializer = StudentSerializer(page, many=True)

    return paginator.get_paginated_response(serializer.data)
```

To allow a client to request a different page size safely:

```python
class StudentPagination(PageNumberPagination):
    page_size = 5
    page_size_query_param = "page_size"
    max_page_size = 50
```

Use it in the FBV:

```python
@api_view(["GET"])
def student_pagination(request):
    students = Student.objects.all().order_by("id")

    paginator = StudentPagination()
    page = paginator.paginate_queryset(students, request)
    serializer = StudentSerializer(page, many=True)

    return paginator.get_paginated_response(serializer.data)
```

---

## 22. Custom action — get students above a particular age

Example URL: `/api/students/above-age/?age=21`

```python
@api_view(["GET"])
def students_above_age(request):
    age = request.query_params.get("age")

    if age is None:
        return Response(
            {"error": "Please provide age"},
            status=status.HTTP_400_BAD_REQUEST
        )

    try:
        age = int(age)
    except ValueError:
        return Response(
            {"error": "Age must be a number"},
            status=status.HTTP_400_BAD_REQUEST
        )

    students = Student.objects.filter(age__gt=age)
    serializer = StudentSerializer(students, many=True)
    return Response(serializer.data)
```

**Practice variations:**

- Students older than 25: `age__gt=25`
- Students younger than 25: `age__lt=25`
- Students aged 18 or above: `age__gte=18`
- Students aged 18 or below: `age__lte=18`

---

## 23. Count records

```python
@api_view(["GET"])
def student_count(request):
    total_students = Student.objects.count()

    return Response({
        "total_students": total_students
    })
```

## 24. Return distinct values

```python
@api_view(["GET"])
def student_courses(request):
    courses = (
        Student.objects
        .values_list("course", flat=True)
        .distinct()
    )

    return Response(list(courses))
```

## 25. Use `get_object_or_404`

This is a shorter alternative to writing a `try/except` block for a missing object.

```python
from django.shortcuts import get_object_or_404

@api_view(["GET"])
def student_detail(request, student_id):
    student = get_object_or_404(Student, id=student_id)
    serializer = StudentSerializer(student)
    return Response(serializer.data)
```

Django returns a 404 response when the object does not exist. DRF handles the resulting `Http404` exception.

---

## 26. Add authentication and permissions to an FBV

**Goal:** Allow only authenticated users to access an endpoint.

First, configure a DRF authentication method in `settings.py`. For token authentication, install and add the token app:

```bash
pip install djangorestframework
```

```python
INSTALLED_APPS = [
    # ...
    "rest_framework",
    "rest_framework.authtoken",
]
```

Configure DRF:

```python
REST_FRAMEWORK = {
    "DEFAULT_AUTHENTICATION_CLASSES": [
        "rest_framework.authentication.TokenAuthentication",
    ],
    "DEFAULT_PERMISSION_CLASSES": [
        "rest_framework.permissions.IsAuthenticated",
    ],
}
```

Run migrations:

```bash
python manage.py migrate
```

Create a token for a user (for example, from Django shell):

```bash
python manage.py shell
```

```python
from django.contrib.auth import get_user_model
from rest_framework.authtoken.models import Token

User = get_user_model()
user = User.objects.get(username="your_username")
token, created = Token.objects.get_or_create(user=user)
print(token.key)
```

Use the token in the request header:

```text
Authorization: Token YOUR_TOKEN
```

**FBV with authentication and permission decorators:**

```python
from rest_framework.decorators import (
    api_view,
    authentication_classes,
    permission_classes
)
from rest_framework.authentication import TokenAuthentication
from rest_framework.permissions import IsAuthenticated
from rest_framework.response import Response

@api_view(["GET"])
@authentication_classes([TokenAuthentication])
@permission_classes([IsAuthenticated])
def protected_api(request):
    return Response({
        "message": "You are authenticated",
        "username": request.user.username
    })
```

> If default authentication and permission classes are already configured globally, you do not need to repeat these decorators on every view. Add per-view decorators when you want to override the defaults.

---

## 27. Custom permission for an FBV

**File: `students/permissions.py`**

```python
from rest_framework.permissions import BasePermission

class IsStaffUser(BasePermission):
    def has_permission(self, request, view):
        return (
            request.user
            and request.user.is_authenticated
            and request.user.is_staff
        )
```

**File: `students/views.py`**

```python
from rest_framework.decorators import (
    api_view,
    permission_classes
)
from rest_framework.response import Response
from .permissions import IsStaffUser

@api_view(["GET"])
@permission_classes([IsStaffUser])
def staff_only_api(request):
    return Response({
        "message": "Only staff users can access this endpoint"
    })
```

**Important:** A permission class checks whether the request is allowed. The `@permission_classes` decorator attaches the permission rule to the FBV.

---

## 28. Return the logged-in user's records

Assume the `Student` model has a foreign key to the user model:

```python
from django.conf import settings
from django.db import models

class Student(models.Model):
    user = models.ForeignKey(
        settings.AUTH_USER_MODEL,
        on_delete=models.CASCADE,
        related_name="student_records"
    )
    name = models.CharField(max_length=100)
    age = models.PositiveIntegerField()
    email = models.EmailField(unique=True)
    course = models.CharField(max_length=100)
```

**FBV:**

```python
from rest_framework.decorators import api_view, permission_classes
from rest_framework.permissions import IsAuthenticated
from rest_framework.response import Response
from .models import Student
from .serializers import StudentSerializer

@api_view(["GET"])
@permission_classes([IsAuthenticated])
def my_student_records(request):
    students = Student.objects.filter(user=request.user)
    serializer = StudentSerializer(students, many=True)
    return Response(serializer.data)
```

**Security point:** Filter by `request.user` on the server. Do not trust a client-supplied user ID to decide whose private records should be returned.

---

## 29. Create a record for the logged-in user

In this example, the client does not send the owner/user field. The backend assigns it from the authenticated request.

```python
@api_view(["POST"])
@permission_classes([IsAuthenticated])
def create_my_student_record(request):
    serializer = StudentSerializer(data=request.data)

    if serializer.is_valid():
        serializer.save(user=request.user)
        return Response(
            serializer.data,
            status=status.HTTP_201_CREATED
        )

    return Response(serializer.errors, status=status.HTTP_400_BAD_REQUEST)
```

**Important:** This example assumes the serializer/model includes a `user` field that is not required from the client. For a production API, define the serializer fields deliberately, for example by excluding `user` from client input.

---

## 30. Handle an unsupported HTTP method

The `@api_view` decorator automatically rejects methods that are not listed.

```python
@api_view(["GET"])
def only_get_api(request):
    return Response({"message": "GET request accepted"})
```

If a client sends POST to this endpoint, DRF returns **405 Method Not Allowed**.

---

## 31. Use status codes correctly

```python
from rest_framework import status
```

| Status constant | Code | Common use |
|---|---:|---|
| `HTTP_200_OK` | 200 | Successful GET or update |
| `HTTP_201_CREATED` | 201 | Successful creation |
| `HTTP_204_NO_CONTENT` | 204 | Successful deletion with no response body |
| `HTTP_400_BAD_REQUEST` | 400 | Invalid input |
| `HTTP_401_UNAUTHORIZED` | 401 | Missing or invalid authentication credentials |
| `HTTP_403_FORBIDDEN` | 403 | Authenticated user is not allowed |
| `HTTP_404_NOT_FOUND` | 404 | Resource does not exist |
| `HTTP_405_METHOD_NOT_ALLOWED` | 405 | HTTP method is not supported |

Example:

```python
return Response(
    {"message": "Student created"},
    status=status.HTTP_201_CREATED
)
```

---

## 32. Common request data sources

| DRF/Django expression | What it reads | Example |
|---|---|---|
| `request.data` | Parsed request body | JSON sent by POST |
| `request.query_params` | URL query parameters | `?age=22` |
| `request.user` | Authenticated user | Current logged-in user |
| `request.method` | HTTP method | `GET`, `POST`, `PATCH` |
| `request.headers` | Request headers | Authorization header |

---

## 33. Common serializer patterns

### ModelSerializer — all fields

```python
class StudentSerializer(serializers.ModelSerializer):
    class Meta:
        model = Student
        fields = "__all__"
```

### ModelSerializer — selected fields

```python
class StudentSerializer(serializers.ModelSerializer):
    class Meta:
        model = Student
        fields = ["id", "name", "age"]
```

### Read-only field

```python
class StudentSerializer(serializers.ModelSerializer):
    class Meta:
        model = Student
        fields = "__all__"
        read_only_fields = ["id"]
```

### Write-only password field

```python
class RegisterSerializer(serializers.Serializer):
    username = serializers.CharField()
    password = serializers.CharField(write_only=True)
```

`write_only=True` allows a field to be accepted as input without including it in serialized output.

---

## 34. Practical URL collection

A possible `students/urls.py` for the exercises:

```python
from django.urls import path
from . import views

urlpatterns = [
    path("welcome/", views.welcome_api),

    path("students/", views.student_list_create),
    path("students/<int:student_id>/", views.student_detail),

    path("students/search/", views.search_students),
    path("students/filter/", views.filter_students),
    path("students/order/", views.order_students),
    path("students/list/", views.student_filter_search_order),
    path("students/paginated/", views.student_pagination),

    path("students/above-age/", views.students_above_age),
    path("students/count/", views.student_count),
    path("students/courses/", views.student_courses),

    path("protected/", views.protected_api),
    path("staff-only/", views.staff_only_api),
    path("my-records/", views.my_student_records),
]
```

> Add only the URL patterns for views that you have actually created. If two examples use the same function name, keep one final version or rename the functions before adding the URL patterns.

---

# 35. Postman testing checklist

For each endpoint, select the correct HTTP method and enter the URL.

| Operation | Method | Body |
|---|---|---|
| Welcome | GET | None |
| Get all students | GET | None |
| Get one student | GET | None |
| Create student | POST | Raw JSON |
| Complete update | PUT | All required fields |
| Partial update | PATCH | Only changed fields |
| Delete student | DELETE | None |
| Search | GET | Query parameters |
| Filter | GET | Query parameters |
| Ordering | GET | Query parameters |
| Pagination | GET | Query parameters |
| Protected endpoint | GET | Token in Authorization header |

For JSON requests, select **Body → raw → JSON** in Postman.

Example JSON:

```json
{
    "name": "Anu",
    "age": 22,
    "email": "anu@example.com",
    "course": "Python"
}
```

---

# 36. FBV practical questions — practise without looking at the solutions

## Beginner level

1. Create a GET API that returns a welcome message.
2. Create a GET API that returns a list of employees without using a model.
3. Create a POST API that accepts name, age, and email without a model.
4. Create a `Student` model with name, age, email, and course.
5. Create a `StudentSerializer` using `ModelSerializer`.
6. Create an FBV to retrieve all students.
7. Create an FBV to retrieve one student using its ID.
8. Create an FBV to add a student.
9. Create an FBV to delete a student.
10. Return a proper 404 response when a student does not exist.

## Intermediate level

11. Create an FBV that supports GET and POST in the same function.
12. Create an FBV that supports GET, PUT, PATCH, and DELETE.
13. Explain and implement the difference between PUT and PATCH.
14. Validate that student age must be at least 18.
15. Validate that an email address is unique.
16. Create a normal `Serializer` without a model.
17. Read a name from query parameters.
18. Filter students by course.
19. Search students by name and email.
20. Order students by name and age in ascending or descending order.
21. Combine filter, search, and ordering in one FBV.
22. Return students above a given age.
23. Return the total number of students.
24. Return unique course names.
25. Implement pagination in an FBV.

## Advanced level

26. Create an authenticated endpoint using token authentication.
27. Create an endpoint accessible only to staff users.
28. Create a custom permission class and apply it to an FBV.
29. Return only the records belonging to the logged-in user.
30. Create a record and assign its owner using `request.user`.
31. Prevent a user from retrieving another user's record.
32. Handle missing fields and invalid data using serializer errors.
33. Validate multiple fields together using object-level validation.
34. Restrict ordering to an approved list of fields.
35. Build a complete Employee CRUD API using FBVs, serializers, validation, search, filtering, and ordering.

---

# 37. Mini project — Employee Management API using FBV only

Build the following API from scratch.

### Employee model

Fields:

- `name`
- `age`
- `email`
- `department`
- `salary`
- `created_at`

### Required endpoints

| Method | Endpoint | Requirement |
|---|---|---|
| GET | `/api/employees/` | List all employees |
| POST | `/api/employees/` | Create an employee |
| GET | `/api/employees/<id>/` | Retrieve one employee |
| PUT | `/api/employees/<id>/` | Complete update |
| PATCH | `/api/employees/<id>/` | Partial update |
| DELETE | `/api/employees/<id>/` | Delete an employee |
| GET | `/api/employees/search/?search=python` | Search employees |
| GET | `/api/employees/filter/?department=IT` | Filter by department |
| GET | `/api/employees/order/?ordering=-salary` | Order by salary |
| GET | `/api/employees/count/` | Count employees |
| GET | `/api/employees/paginated/?page=1` | Paginate employees |

### Required validations

- Age must be at least 18.
- Salary must not be negative.
- Email must be unique.
- Name must not be blank.

### Rules

1. Use `@api_view` for every API view.
2. Use serializers for input validation and output serialization.
3. Use `ModelSerializer` for the Employee model.
4. Use correct HTTP methods and status codes.
5. Handle records that do not exist.
6. Test every endpoint in Postman.
7. Do not use CBV, `APIView`, generics, mixins, or ViewSets.

---

# 38. Important FBV revision points

- `@api_view()` converts a Django function into a DRF function-based API view.
- `Response()` returns API response data.
- `request.data` reads parsed request-body data.
- `request.query_params` reads query-string parameters.
- `serializer.is_valid()` checks submitted data.
- `serializer.validated_data` contains validated input.
- `serializer.errors` contains validation errors.
- `serializer.save()` creates or updates an object.
- `many=True` is used when serializing multiple objects.
- `partial=True` allows partial updates.
- `get_object_or_404()` returns a 404 when an object is missing.
- `@permission_classes()` attaches permission rules to an FBV.
- `@authentication_classes()` specifies authentication methods for an FBV.
- `request.user` represents the authenticated user.
- `status.HTTP_201_CREATED` is commonly used after successful creation.
- `status.HTTP_204_NO_CONTENT` is commonly used after successful deletion.

**End goal:** Be able to build a complete CRUD API, validate data, search/filter/order records, paginate results, and protect endpoints using Function-Based Views only.
