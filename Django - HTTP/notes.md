# 📚 FINAL NOTION NOTE — DJANGO + HTTP

> 🎯 **Goal:** Understand how HTTP and Django work together from the moment a user enters a URL until the browser displays the final page.
> 

---

# 🌐 PART 1 — HTTP

## 1. What is HTTP?

**HTTP = HyperText Transfer Protocol**

HTTP is an **application-layer protocol** used for communication between a client and a server.

### Basic Flow

```
Client
   ↓ HTTP Request
Server
   ↓ HTTP Response
Client
```

### Example

```
Browser → GET /home/ → Django
Browser ← 200 OK + HTML ← Django
```

---

## 2. Client-Server Architecture

### 🧑‍💻 Client

The application that sends requests.

Examples:

- Web Browser
- Mobile Application
- Frontend Application

### 🖥️ Server

Receives requests, processes them, and sends responses.

```
Browser
   ↓ Request
Django Server
   ↓ Response
Browser
```

### 💡 Remember

> **Client asks → Server processes → Server responds**
> 

---

# 🔄 3. Request-Response Cycle

HTTP communication follows:

```
Client
   ↓
HTTP Request
   ↓
Server
   ↓
Process Request
   ↓
HTTP Response
   ↓
Client
```

### HTTP Request Contains

- Method
- URL
- Headers
- Body

### HTTP Response Contains

- Status Code
- Headers
- Body

---

# 📤 4. HTTP Request

Example:

```
GET /products/ HTTP/1.1
Host: example.com
Accept: text/html
```

### Parts

| Part | Meaning |
| --- | --- |
| `GET` | HTTP method |
| `/products/` | URL/path |
| `Host` | Header |
| `Accept` | Header |

Some requests, such as POST, can also contain a **request body**.

---

# 📥 5. HTTP Response

Example:

```
HTTP/1.1 200 OK
Content-Type: text/html
```

```html
<h1>Hello</h1>
```

### Parts

```
Status Code
Headers
Body
```

---

# 🔧 6. HTTP Methods

| Method | Purpose |
| --- | --- |
| GET | Retrieve data |
| POST | Submit/Create data |
| PUT | Replace a resource |
| PATCH | Partially update a resource |
| DELETE | Delete a resource |

---

## GET

Used mainly to retrieve data.

```
GET /products/
```

> “Give me the products.”
> 

---

## POST

Used mainly to submit or create data.

```
POST /products/
```

> “Create this product.”
> 

---

## PUT

Usually replaces the complete representation of a resource.

```
PUT /products/1/
```

---

## PATCH

Updates only specific fields.

```
PATCH /products/1/
```

Example:

```json
{
    "price": 500
}
```

Only the price changes.

---

## DELETE

Deletes a resource.

```
DELETE /products/1/
```

---

# ⚖️ 7. GET vs POST

| GET | POST |
| --- | --- |
| Mainly retrieves data | Mainly submits/creates/processes data |
| Data can appear in URL/query parameters | Data commonly sent in request body |
| Should generally be safe | Usually changes server state |
| Can be cached | Generally not cached as a normal response |

### 🧠 Easy Memory

```
GET  → Give me data
POST → Here is some data
```

---

# ⚖️ 8. PUT vs PATCH

```
PUT
 ↓
Complete replacement

PATCH
 ↓
Partial update
```

### Example

Existing:

```json
{
    "name": "John",
    "age": 20,
    "city": "Kozhikode"
}
```

PATCH:

```json
{
    "age": 21
}
```

Only `age` changes.

---

# 📋 9. HTTP Headers

Headers provide additional information about a request or response.

### Common Headers

```
Content-Type
Authorization
Cookie
User-Agent
Accept
Cache-Control
Host
Origin
```

---

## Content-Type

Tells the receiver the format of the body.

```
Content-Type: application/json
```

Means:

> The body contains JSON.
> 

---

## Authorization

Used to send authentication credentials, commonly a token.

```
Authorization: Bearer <token>
```

---

# 🚦 10. HTTP Status Codes

Status codes tell the client what happened.

```
1xx → Informational
2xx → Success
3xx → Redirection
4xx → Client Error
5xx → Server Error
```

---

# ✅ 11. 2xx — Success

### 200 OK

Request succeeded.

### 201 Created

A resource was successfully created.

### 204 No Content

Request succeeded but there is no response body.

---

# 🔀 12. 3xx — Redirection

### 301

Moved permanently.

### 302

Temporary redirection.

### 304

Not Modified.

Commonly related to caching.

---

# ❌ 13. 4xx — Client Errors

### 400 — Bad Request

Request is invalid or malformed.

### 401 — Unauthorized

Authentication is required or failed.

> **Who are you?**
> 

### 403 — Forbidden

Server understands the request but refuses access.

> **I know who you are, but you’re not allowed.**
> 

### 404 — Not Found

Requested resource does not exist.

### 405 — Method Not Allowed

HTTP method is not allowed for that URL.

---

# 💥 14. 5xx — Server Errors

### 500 — Internal Server Error

Something went wrong on the server.

### 502 — Bad Gateway

Gateway/proxy received an invalid response from an upstream server.

### 503 — Service Unavailable

Server is temporarily unavailable.

---

# ⭐ 15. Important Status Code Differences

| Code | Remember |
| --- | --- |
| 200 | Success |
| 201 | Created |
| 204 | Success, no content |
| 301 | Permanent redirect |
| 302 | Temporary redirect |
| 304 | Not modified |
| 400 | Bad request |
| 401 | Authentication problem |
| 403 | Permission problem |
| 404 | Resource not found |
| 405 | Method not allowed |
| 500 | Server error |
| 502 | Bad gateway |
| 503 | Service unavailable |

### 🔥 401 vs 403

```
401 → Who are you?
403 → I know you, but you can't do this.
```

---

# 🧠 16. Why is HTTP Stateless?

HTTP itself does not remember previous requests.

```
Request 1 → Server

Request 2 → Server

Request 3 → Server
```

Each request is independent at the protocol level.

Applications use:

- Cookies
- Sessions
- Tokens

to maintain state.

### 💡 Interview Answer

> HTTP is stateless bec
> 

ause each request is independent and HTTP itself does not maintain application state between requests.

---

# 🍪 17. Cookies

Cookies are small pieces of information stored by the browser and sent with applicable requests.

Examples:

- Session identifier
- Preferences
- Other client-side state

---

# 👤 18. Sessions

Sessions allow a server-side application to remember information associated with a user across requests.

### Example

```
Login
  ↓
Session Created
  ↓
Session ID associated with browser
  ↓
Browser sends session cookie
  ↓
Django identifies session/user
```

---

# 🍪 Cookie vs Session

| Cookie | Session |
| --- | --- |
| Stored in browser | User state maintained server-side |
| Sent with requests | Associated with a session |
| Can contain a session identifier | Contains server-side session data/state |

### Important

> A cookie and a session are **not the same thing**.
> 

A common setup is:

```
Session ID
     ↓
Stored in Cookie
     ↓
Browser
```

---

# 🚀 19. HTTP Caching

Caching stores previously obtained responses/resources so they can potentially be reused.

### Benefits

- Faster loading
- Less network traffic
- Reduced server load

### Important Headers

```
Cache-Control
ETag
Last-Modified
Expires
```

---

# 🍪 Cache vs Cookie

```
Cookie
 ↓
Stores client-side information/state

Cache
 ↓
Stores reusable resources/responses for performance
```

---

# 🌍 20. DNS

**DNS = Domain Name System**

DNS translates a domain name into an IP address.

```
example.com
     ↓
    DNS
     ↓
IP Address
     ↓
Server
```

### Simplified

```
Browser
   ↓
DNS Resolver
   ↓
DNS
   ↓
IP Address
   ↓
Server
```

---

# 🌐 21. Browser Responsibilities

A browser is responsible for:

- DNS/network communication
- HTTP requests
- HTML parsing
- CSS parsing
- JavaScript execution
- DOM creation
- Rendering
- Cookies
- Caching
- CORS enforcement

---

# 🎨 22. How Browser Renders HTML

Simplified flow:

```
HTML
 ↓
DOM

CSS
 ↓
CSSOM

DOM + CSSOM
 ↓
Render Tree
 ↓
Layout
 ↓
Paint
 ↓
Screen
```

---

# ⚙️ 23. How Browser Handles JavaScript

```
Download JavaScript
        ↓
Parse
        ↓
Execute
        ↓
Modify DOM
        ↓
Make HTTP Requests
```

Common APIs:

```
fetch()
XMLHttpRequest
```

---

# ⚡ 24. AJAX

**AJAX = Asynchronous JavaScript and XML**

Modern AJAX commonly uses **JSON**, not XML.

### Purpose

> Make HTTP requests without requiring a complete page reload.
> 

### Example

```
User clicks button
       ↓
JavaScript fetch()
       ↓
Django
       ↓
JSON Response
       ↓
JavaScript updates page
```

---

# 🔀 25. CORS

**CORS = Cross-Origin Resource Sharing**

CORS is a **browser security mechanism** that controls whether JavaScript from one origin can access resources from another origin.

### Example

```
Frontend
http://localhost:3000

Backend
http://localhost:8000
```

Different ports = different origins.

The server may respond with:

```
Access-Control-Allow-Origin
```

### 🧠 Remember

> **CORS controls cross-origin browser access.**
> 

It does **not** simply mean “checking another URL.”

---

# 🛡️ 26. CSRF vs CORS

This is extremely important.

| CSRF | CORS |
| --- | --- |
| Cross-Site Request Forgery | Cross-Origin Resource Sharing |
| Protects against unwanted authenticated actions | Controls cross-origin browser access |
| Security protection | Browser cross-origin access mechanism |

### Easy Memory

```
CSRF → Request protection

CORS → Cross-origin access
```

---

# 🚀 PART 2 — DJANGO

# 27. What is Django?

Django is a **high-level Python web framework** used to build secure, maintainable, and scalable web applications.

Django provides built-in features such as:

- URL routing
- Views
- Templates
- ORM
- Authentication
- Sessions
- Forms
- Middleware
- Admin
- Security

---

# 🏗️ 28. Django Architecture — MVT

Django follows:

```
M → Model
V → View
T → Template
```

### Model

Handles data/database structure.

### View

Handles request/business logic.

### Template

Handles presentation/UI.

---

# 🔄 29. MVT Flow

```
User
 ↓
URL
 ↓
View
 ↓
Model
 ↓
Database
 ↓
View
 ↓
Template
 ↓
Response
 ↓
User
```

---

# 📁 30. Django Project vs App

## Project

The complete Django website/application configuration.

## App

A specific functional component.

Example:

```
myproject
│
├── users
├── products
├── orders
└── payments
```

Each can be a separate Django app.

---

# 🛠️ 31. `django-admin`

Django’s command-line utility.

Example:

```bash
django-admin startproject myproject
```

---

# 🛠️ 32. `manage.py`

Project-specific command-line utility.

### Common commands

```bash
python manage.py runserver

python manage.py startapp users

python manage.py makemigrations

python manage.py migrate
```

---

# ⚙️ 33. `settings.py`

Contains project configuration.

Important settings:

```
INSTALLED_APPS
MIDDLEWARE
ROOT_URLCONF
TEMPLATES
DATABASES
STATIC_URL
MEDIA_URL
SECRET_KEY
DEBUG
ALLOWED_HOSTS
```

---

# 🔗 34. `urls.py`

Responsible for URL routing.

Example:

```python
urlpatterns = [
    path("home/", views.home),
]
```

### Purpose

> Determines which view should handle a particular URL.
> 

---

# 👁️ 35. `views.py`

Contains request-handling logic.

Example:

```python
def home(request):
    return HttpResponse("Hello")
```

---

# 🗃️ 36. `models.py`

Defines database models.

Example:

```python
class Student(models.Model):
    name = models.CharField(max_length=100)
    age = models.IntegerField()
```

---

# 🛠️ 37. `admin.py`

Used to register models with Django Admin.

```python
from .models import Student

admin.site.register(Student)
```

---

# 📱 38. `apps.py`

Contains configuration for a Django application.

---

# 🔌 39. `wsgi.py`

**WSGI = Web Server Gateway Interface**

Provides an interface between Django and traditional synchronous web servers/deployment systems.

```
Web Server
    ↓
   WSGI
    ↓
  Django
```

---

# ⚡ 40. `asgi.py`

**ASGI = Asynchronous Server Gateway Interface**

Supports asynchronous Django applications and protocols.

```
Web Server
    ↓
   ASGI
    ↓
  Django
```

---

# 🔗 41. URLconf

URLconf is Django’s URL configuration system.

It maps:

```
URL
 ↓
View
```

Example:

```python
path("dashboard/", views.dashboard)
```

---

# 👨‍💻 42. Function-Based View — FBV

A view written as a function.

```python
def home(request):
    return HttpResponse("Hello")
```

### Advantages

- Simple
- Easy to understand
- Explicit
- Flexible

---

# 🏛️ 43. Class-Based View — CBV

A view written as a class.

```python
from django.views import View

class HomeView(View):

    def get(self, request):
        return HttpResponse("Hello")
```

### Advantages

- Reusable
- Supports inheritance
- Generic views
- Structured

---

# ⚖️ 44. FBV vs CBV

| FBV | CBV |
| --- | --- |
| Function-based | Class-based |
| Simple | More structured |
| Explicit | Supports inheritance |
| Good for simple/custom logic | Good for reusable/structured views |

---

# 🖼️ 45. `render()`

Used to render a template with context.

```python
return render(
    request,
    "home.html",
    {"name": "John"}
)
```

Conceptually:

```
Template + Context
       ↓
Rendered HTML
       ↓
HTTP Response
```

---

# 📦 46. Context

Context is data passed from a view to a template.

```python
context = {
    "name": "John",
    "age": 20
}
```

Template:

```
<h1>{{ name }}</h1>
<p>{{ age }}</p>
```

---

# 🏷️ 47. Template Tags

Template tags allow logic/actions inside Django templates.

### If

```
{% if user.is_authenticated %}
    Welcome
{% endif %}
```

### For

```
{% for student in students %}
    {{ student.name }}
{% endfor %}
```

### Important Tags

```
{% if %}
{% for %}
{% url %}
{% csrf_token %}
{% extends %}
{% block %}
{% include %}
```

---

# 🧩 48. Template Inheritance

### Base Template

```
{% block content %}
{% endblock %}
```

### Child Template

```
{% extends "base.html" %}

{% block content %}
    <h1>Hello</h1>
{% endblock %}
```

### Benefits

- Reusable layout
- Less duplication
- Consistent UI

---

# 🗄️ 49. Django ORM

**ORM = Object Relational Mapping**

ORM allows developers to interact with a database using Django/Python objects and QuerySets instead of manually writing SQL for every operation.

Example:

```python
Student.objects.all()
```

---

# 📝 50. CRUD

CRUD means:

```
C → Create
R → Read
U → Update
D → Delete
```

---

## Create

```python
Student.objects.create(
    name="John",
    age=20
)
```

---

## Read

```python
Student.objects.all()
```

```python
Student.objects.get(id=1)
```

```python
Student.objects.filter(age=20)
```

---

## Update

```python
student.name = "Alex"
student.save()
```

---

## Delete

```python
student.delete()
```

---

# 🔎 51. QuerySet

A QuerySet represents a collection of database query operations/results.

Example:

```python
Student.objects.filter(age__gte=18)
```

### Important

Django QuerySets are generally **lazy**.

Meaning:

> The database query is usually not executed until the results are actually needed.
> 

---

# 🔄 52. Migrations

Migrations track changes to database schema.

## `makemigrations`

Creates migration files.

```bash
python manage.py makemigrations
```

## `migrate`

Applies migrations to the database.

```bash
python manage.py migrate
```

### ⭐ Remember

```
makemigrations
      ↓
Create migration instructions

migrate
      ↓
Apply them to database
```

---

# 🔗 53. Model Relationships

## One-to-One

```python
OneToOneField
```

```
Person ↔ Passport
```

One object relates to one object.

---

## One-to-Many

```python
ForeignKey
```

```
Author
  ↓
Many Books
```

---

## Many-to-Many

```python
ManyToManyField
```

```
Students ↔ Courses
```

---

# 🧱 54. Middleware

Middleware is a layer in Django’s **request/response processing pipeline**.

It can process:

- Request before the view
- Response after the view

### Flow

```
Request
   ↓
Middleware
   ↓
Middleware
   ↓
View
   ↓
Middleware
   ↓
Response
```

---

# 🎯 55. Why Middleware?

Common uses:

- Authentication
- Security
- Sessions
- Cookies
- CSRF
- Logging
- Request processing
- Response processing

---

# ⚖️ 56. Middleware vs URLconf

### Middleware

> Processes requests/responses globally.
> 

### URLconf

> Determines which view matches a URL.
> 

Simplified:

```
Request
   ↓
Middleware
   ↓
URLconf
   ↓
View
```

---

# 📝 57. Django Forms

Django Forms help with:

- Input validation
- Data cleaning
- Error handling
- Form generation

Example:

```python
class StudentForm(forms.Form):
    name = forms.CharField()
    age = forms.IntegerField()
```

---

# 🔀 58. GET and POST in Django

```python
if request.method == "GET":
    ...
```

GET is commonly used to retrieve/display data.

```python
if request.method == "POST":
    ...
```

POST is commonly used to submit data or perform state-changing operations.

---

# 🔐 59. Authentication

Authentication answers:

> **Who are you?**
> 

Example:

```
Username + Password
```

---

# 🔑 60. Authorization

Authorization answers:

> **What are you allowed to do?**
> 

Example:

```
Admin
 ↓
Can delete users

Normal User
 ↓
Cannot delete users
```

---

# 🔍 61. `authenticate()`

Checks whether supplied credentials are valid.

```python
user = authenticate(
    username=username,
    password=password
)
```

Returns a user if successful, otherwise typically `None`.

---

# 🔓 62. `login()`

Establishes authentication for the user in the current session.

```python
login(request, user)
```

### ⭐ Remember

```
authenticate()
      ↓
Verify credentials

login()
      ↓
Establish authenticated session
```

---

# 🚪 63. `logout()`

Logs the user out.

```python
logout(request)
```

---

# 👤 64. `request.user`

Django provides the current user through:

```python
request.user
```

Check authentication:

```python
request.user.is_authenticated
```

---

# 🔒 65. `@login_required`

Restricts a view to authenticated users.

```python
@login_required
def dashboard(request):
    ...
```

Unauthenticated users are redirected to the configured login URL.

---

# 🛂 66. `@permission_required`

Checks whether the user has a particular permission.

```python
@permission_required("app.change_student")
def edit_student(request):
    ...
```

---

# 👤 67. Session-Based Authentication

Typical flow:

```
User enters username/password
          ↓
authenticate()
          ↓
Credentials valid?
          ↓
login(request, user)
          ↓
Django establishes session
          ↓
Session ID associated with browser
          ↓
Browser sends session cookie
          ↓
Django identifies user
```

---

# 🔐 68. Password Hashing

Passwords should **never be stored as plain text**.

Django’s authentication system stores passwords using password hashing.

Conceptually:

```
Password
   ↓
Hashing
   ↓
Stored Password Hash
```

During login:

```
Entered Password
       ↓
Password Verification
       ↓
Stored Hash
       ↓
Match / No Match
```

---

# 🛡️ 69. CSRF

**CSRF = Cross-Site Request Forgery**

An attack where a malicious website attempts to make a user’s browser send an unwanted request to another website where the user is authenticated.

Django provides CSRF protection.

In a POST form:

```
<form method="POST">
    {% csrf_token %}
```

---

# 🧠 70. Why CSRF Token?

The CSRF token helps Django verify that a state-changing request came through a trusted application flow.

### Remember

```
CSRF
 ↓
Protects against unwanted authenticated actions
```

---

# 🕵️ 71. XSS

**XSS = Cross-Site Scripting**

An attacker attempts to inject malicious JavaScript into a page viewed by other users.

Django templates provide automatic escaping for normal variable output, which helps reduce XSS risks.

---

# 💉 72. SQL Injection

SQL Injection occurs when untrusted input is improperly incorporated into SQL.

Django ORM normally uses parameterized queries rather than unsafe string concatenation for database operations.

---

# 🚫 73. `never_cache`

Used to prevent a response from being cached under normal HTTP caching behavior.

```python
from django.views.decorators.cache import never_cache

@never_cache
def dashboard(request):
    ...
```

Useful for pages containing sensitive or frequently changing information.

---

# 🔥 PART 3 — COMPLETE DJANGO + HTTP FLOW

## ⭐ The Most Important Flow

Suppose the user visits:

```
http://example.com/dashboard/
```

---

### 1️⃣ Browser

Browser prepares an HTTP request.

```
GET /dashboard/
```

---

### 2️⃣ DNS

Domain is resolved to an IP address.

```
example.com
     ↓
IP Address
```

---

### 3️⃣ Web Server

The request reaches the web server.

---

### 4️⃣ WSGI / ASGI

The request enters Django through WSGI or ASGI.

```
Web Server
    ↓
WSGI / ASGI
    ↓
Django
```

---

### 5️⃣ Middleware

Django middleware processes the request.

```
Request
   ↓
Middleware
```

---

### 6️⃣ URLconf

Django checks `urls.py`.

```python
path("dashboard/", views.dashboard)
```

---

### 7️⃣ View

Django calls the matching view.

```python
dashboard(request)
```

---

### 8️⃣ Authentication

The view may check:

```python
request.user.is_authenticated
```

---

### 9️⃣ ORM

The view may request database data.

```python
Student.objects.all()
```

---

### 🔟 Database

Django ORM communicates with the database.

---

### 1️⃣1️⃣ View

The view receives/processes the data.

---

### 1️⃣2️⃣ Template

The view renders the template.

```python
return render(
    request,
    "dashboard.html",
    context
)
```

---

### 1️⃣3️⃣ HTTP Response

Django creates the response.

```
HTTP 200 OK
```

---

### 1️⃣4️⃣ Middleware

The response travels back through middleware.

---

### 1️⃣5️⃣ Browser

Browser receives the HTML.

Then:

```
HTML
 ↓
DOM
 ↓
CSS
 ↓
JavaScript
 ↓
Render
 ↓
Screen
```

---

# 🧠 ULTIMATE FLOW TO MEMORIZE

```
                    BROWSER
                       ↓
                      DNS
                       ↓
               HTTP REQUEST
                       ↓
                  WEB SERVER
                       ↓
                  WSGI / ASGI
                       ↓
                  MIDDLEWARE
                       ↓
                    URLconf
                       ↓
                     VIEW
                       ↓
                 AUTHENTICATION
                       ↓
                     ORM
                       ↓
                   DATABASE
                       ↓
                     VIEW
                       ↓
                   TEMPLATE
                       ↓
                HTTP RESPONSE
                       ↓
                  MIDDLEWARE
                       ↓
                    BROWSER
                       ↓
                HTML / CSS / JS
                       ↓
                   RENDERED PAGE
```

---

# 🚨 PART 4 — MOST IMPORTANT DIFFERENCES

| Concept | Meaning |
| --- | --- |
| HTTP | Communication protocol |
| DNS | Domain → IP |
| Request | Client → Server |
| Response | Server → Client |
| GET | Retrieve |
| POST | Submit/Create |
| PUT | Full replacement |
| PATCH | Partial update |
| DELETE | Delete |
| Cookie | Browser-stored data |
| Session | Server-side user state |
| Cache | Reusable stored response/resource |
| CORS | Cross-origin browser access |
| CSRF | Protection against unwanted authenticated actions |
| Authentication | Who are you? |
| Authorization | What can you do? |
| 401 | Authentication problem |
| 403 | Permission denied |
| 404 | Resource not found |
| 500 | Server error |
| Model | Database structure/data |
| View | Request/business logic |
| Template | Presentation |
| ORM | Database interaction |
| Middleware | Request/response processing |
| URLconf | URL → View |
| `render()` | Template + Context → Response |
| `authenticate()` | Verify credentials |
| `login()` | Establish authenticated session |
| `logout()` | End authentication |
| `makemigrations` | Create migration files |
| `migrate` | Apply migrations |
| WSGI | Synchronous web interface |
| ASGI | Asynchronous web interface |

---

# 🎯 PART 5 — FINAL REVIEW CHECKLIST

## 🌐 HTTP

- [ ]  What is HTTP?
- [ ]  What is client-server architecture?
- [ ]  What is request-response cycle?
- [ ]  What is an HTTP request?
- [ ]  What is an HTTP response?
- [ ]  GET
- [ ]  POST
- [ ]  PUT
- [ ]  PATCH
- [ ]  DELETE
- [ ]  HTTP headers
- [ ]  Status codes
- [ ]  200 vs 201
- [ ]  401 vs 403
- [ ]  404 vs 500
- [ ]  Why HTTP is stateless
- [ ]  Cookies
- [ ]  Sessions
- [ ]  Caching
- [ ]  DNS
- [ ]  Browser responsibilities
- [ ]  HTML rendering
- [ ]  JavaScript execution
- [ ]  AJAX
- [ ]  CORS
- [ ]  CSRF

---

## 🚀 Django

- [ ]  What is Django?
- [ ]  MVT architecture
- [ ]  Project vs App
- [ ]  `django-admin`
- [ ]  `manage.py`
- [ ]  `settings.py`
- [ ]  `urls.py`
- [ ]  `views.py`
- [ ]  `models.py`
- [ ]  `admin.py`
- [ ]  `apps.py`
- [ ]  `wsgi.py`
- [ ]  `asgi.py`
- [ ]  URLconf
- [ ]  FBV
- [ ]  CBV
- [ ]  FBV vs CBV
- [ ]  `render()`
- [ ]  Context
- [ ]  Template Tags
- [ ]  Template inheritance
- [ ]  ORM
- [ ]  CRUD
- [ ]  QuerySet
- [ ]  Migrations
- [ ]  Model relationships
- [ ]  Middleware
- [ ]  Middleware vs URLconf
- [ ]  Forms
- [ ]  GET/POST in Django
- [ ]  Authentication
- [ ]  Authorization
- [ ]  `authenticate()`
- [ ]  `login()`
- [ ]  `logout()`
- [ ]  `request.user`
- [ ]  `@login_required`
- [ ]  `@permission_required`
- [ ]  Sessions
- [ ]  Password hashing
- [ ]  CSRF
- [ ]  CORS
- [ ]  XSS
- [ ]  SQL Injection
- [ ]  `never_cache`

---

# 🏆 20 QUESTIONS YOU MUST BE ABLE TO ANSWER

1. **What is HTTP?**
2. **Why is HTTP stateless?**
3. **Explain client-server architecture.**
4. **Explain the request-response cycle.**
5. **Explain GET, POST, PUT, PATCH and DELETE.**
6. **What is the difference between PUT and PATCH?**
7. **What is the difference between 401 and 403?**
8. **What is the difference between cookies, sessions and cache?**
9. **What is DNS?**
10. **What is CORS?**
11. **What is CSRF?**
12. **What is Django?**
13. **Explain MVT architecture.**
14. **Explain Django’s complete request flow.**
15. **What is middleware?**
16. **What is Django ORM?**
17. **Explain CRUD operations.**
18. **What is the difference between `makemigrations` and `migrate`?**
19. **What is the difference between `authenticate()` and `login()`?**
20. **What is the difference between authentication and authorization?**

---

# 🔥 FINAL 30-SECOND REVISION

If you have **almost no time**, remember this:

```
HTTP
↓
Client sends Request
↓
Server processes Request
↓
Server sends Response
```

```
Django
↓
Middleware
↓
URLconf
↓
View
↓
ORM
↓
Database
↓
Template
↓
Response
```

```
Authentication
→ Who are you?

Authorization
→ What can you do?

CSRF
→ Protect unwanted authenticated actions

CORS
→ Control cross-origin browser access

Cookie
→ Browser-side information

Session
→ Server-side user state

Cache
→ Performance/reuse
```

### ⭐ The one sentence to remember

> **A browser sends an HTTP request, Django receives it through WSGI/ASGI and middleware, URLconf finds the appropriate view, the view can use the ORM to communicate with the database, Django renders a template, and finally sends an HTTP response back to the browser.**
>
