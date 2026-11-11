### 1. What is an API?

API stands for Application Programming Interface.

An API is a mechanism that allows two different software applications to communicate and exchange information through a defined set of rules.

**Example:** A mobile application sends login credentials to a Django backend. The backend validates the credentials and sends a response to the mobile application.

### 2. What are the advantages of APIs?

- Allow communication between different applications.
- Enable code and functionality reuse.
- Separate frontend and backend development.
- Support integration with third-party services.
- Make applications easier to scale.
- Allow different programming languages to communicate.
- Support mobile, web and desktop applications.

### 3. What are the disadvantages of APIs?

- Require proper security.
- Depend on network communication.
- Can introduce latency.
- Require maintenance and version management.
- Poorly designed APIs can expose sensitive information.
- Third-party API availability can affect applications.

### 4. What are the different types of APIs?

1. REST API
2. SOAP API
3. GraphQL API
4. RPC API
5. WebSocket API

### 5. What is a REST API?

REST stands for Representational State Transfer.

REST is an architectural style used to design APIs that allow clients and servers to communicate through resources and standard HTTP operations.

### 6. What is a RESTful API?

A RESTful API is an API that follows REST architectural principles.

### 7. What are the six principles of REST?

1. **Client-Server:** Frontend and backend work independently.
2. **Stateless:** Every request contains the information required to process it.
3. **Cacheable:** Responses indicate whether they can be cached.
4. **Uniform Interface:** Resources are accessed through a consistent interface.
5. **Layered System:** Communication can happen through multiple intermediate layers.
6. **Code on Demand:** The server can optionally send executable code to the client.

### 8. What is Statelessness?

Statelessness means the server does not rely on stored client-specific interaction state from previous requests to process a new REST request.

Each request should contain the required authentication and other information.

### 9. What is the difference between REST and RESTful?

- REST is an architectural style.
- RESTful describes an API that follows REST principles.

### 11. What is a Resource in REST?

A resource is an identifiable entity exposed through an API.

Examples:

- Students
- Users
- Products
- Memberships
- Payments

### 12. What is an Endpoint?

An endpoint is a URL through which a client accesses an API resource or operation.

Example:

`/api/students/`

### 13. What is a URI and URL?

**URI:** Uniform Resource Identifier. It identifies a resource.

**URL:** Uniform Resource Locator. It identifies a resource and provides its location or access mechanism.

A URL is a type of URI.

### 14. What is CRUD?

CRUD represents the four basic database operations:

- Create
- Read
- Update
- Delete

### 15. What is an API Request-Response Cycle?

1. Client sends an HTTP request.
2. Server receives the request.
3. Server processes authentication and permissions.
4. Application performs the required operation.
5. Server prepares the response.
6. Client receives and processes the response.

### 16. What is JSON?

JSON stands for JavaScript Object Notation.

It is a lightweight, language-independent data-interchange format used to exchange structured information between applications.

Example:

```json
{
    "id": 1,
    "name": "Rahul",
    "age": 22,
    "is_active": true
}
```

### 17. What are the advantages of JSON?

1. Lightweight and compact.
2. Easy for humans to read.
3. Easy for programming languages to parse.
4. Language independent.
5. Supports structured data.
6. Widely supported by modern applications.
7. Suitable for frontend-backend communication.
8. Usually requires less data than equivalent verbose XML.

### 18. What are the disadvantages of JSON?

1. Does not support comments in standard JSON.
2. Does not directly support dates.
3. Does not directly support binary data.
4. Does not have built-in schema validation.
5. Deeply nested JSON can be difficult to manage.
6. Large JSON documents can consume considerable memory.

### 19. What are the data types supported by JSON?

JSON supports six data categories:

1. String
2. Number
3. Boolean
4. Object
5. Array
6. Null

### 20. What is the difference between JSON and Python Dictionary?

| JSON | Python Dictionary |
|---|---|
| Data-interchange format | Python data structure |
| Uses true and false | Uses True and False |
| Uses null | Uses None |
| Object keys are strings | Keys can be other hashable types |
| Uses double-quoted strings | Supports single and double quotes |
| Language independent | Python specific |

### 21. What is JSON Serialization?

Serialization converts Python data into JSON-formatted text.

```python
import json

data = {
    "name": "Rahul",
    "age": 22
}

result = json.dumps(data)
```

### 22. What is JSON Deserialization?

Deserialization converts JSON-formatted text into Python data.

```python
python_data = json.loads(result)
```

### 23. Explain the important JSON methods.

| Method | Purpose |
|---|---|
| `json.dumps()` | Python object to JSON string |
| `json.dump()` | Python object to JSON file |
| `json.loads()` | JSON string to Python object |
| `json.load()` | JSON file to Python object |

### 28. Why is JSON commonly preferred in REST APIs?

JSON is lightweight, easy to parse, language independent and widely supported by frontend and backend technologies.

However, REST does not require JSON. Other representations are also possible.

### 33. What is HTTP?

HTTP stands for Hypertext Transfer Protocol.

It is an application-layer protocol used for communication between clients and servers.

### 34. What is HTTPS?

HTTPS stands for Hypertext Transfer Protocol Secure.

It uses TLS encryption to protect communication between the client and server.

### 35. Difference between HTTP and HTTPS.

| HTTP | HTTPS |
|---|---|
| Not encrypted by default | Encrypted using TLS |
| Less secure | More secure |
| Default port 80 | Default port 443 |
| Data can be intercepted more easily | Protects data in transit |

### 36. What is an HTTP Request?

An HTTP request is a message sent by a client to a server to retrieve a resource or perform an operation.

It contains:

1. HTTP method
2. URL
3. Headers
4. Body (optional)

### 37. What is an HTTP Response?

An HTTP response is a message sent by the server back to the client.

It contains:

1. Status code
2. Headers
3. Response body (optional)

### 38. What are HTTP Methods?

HTTP methods define the type of operation the client wants to perform.

| Method | Purpose |
|---|---|
| GET | Retrieve data |
| POST | Create or process data |
| PUT | Replace a resource |
| PATCH | Partially update a resource |
| DELETE | Delete a resource |
| HEAD | Retrieve response headers |
| OPTIONS | Discover supported communication options |

### 39. Difference between GET and POST.

| GET | POST |
|---|---|
| Retrieves information | Submits information |
| Parameters often appear in URL | Data commonly appears in request body |
| Generally safe | Not generally safe |
| Generally cacheable | Not generally cacheable |
| Idempotent | Not generally idempotent |

### 40. Difference between PUT and PATCH.

**PUT:** Usually replaces the complete resource representation.

**PATCH:** Updates selected fields of a resource.

### 41. What are Safe HTTP Methods?

Safe methods are methods that are not intended to modify server-side resources.

Examples:

- GET
- HEAD
- OPTIONS

### 42. What are Idempotent HTTP Methods?

An HTTP method is idempotent if repeating the same request has the same intended effect on server state as making it once.

Examples:

- GET
- PUT
- DELETE
- HEAD
- OPTIONS

POST is generally not idempotent.

### 43. What are HTTP Status Codes?

Status codes indicate the result of an HTTP request.

**1xx – Informational**

- 100 Continue
- 101 Switching Protocols

**2xx – Success**

- 200 OK
- 201 Created
- 202 Accepted
- 204 No Content

**3xx – Redirection**

- 301 Moved Permanently
- 302 Found
- 304 Not Modified

**4xx – Client Errors**

- 400 Bad Request
- 401 Unauthorized
- 403 Forbidden
- 404 Not Found
- 405 Method Not Allowed
- 406 Not Acceptable
- 409 Conflict
- 415 Unsupported Media Type
- 422 Unprocessable Content
- 429 Too Many Requests

**5xx – Server Errors**

- 500 Internal Server Error
- 501 Not Implemented
- 502 Bad Gateway
- 503 Service Unavailable
- 504 Gateway Timeout

### 44. Difference between 200, 201 and 204.

- 200: Request succeeded.
- 201: A resource was successfully created.
- 204: Request succeeded but no response body is returned.

### 45. Difference between 400, 401 and 403.

- 400: Invalid request.
- 401: Authentication is missing or invalid.
- 403: Access is forbidden.

### 46. What are HTTP Headers?

HTTP headers provide additional information about requests and responses.

Examples:

- Content-Type
- Accept
- Authorization
- Cache-Control
- User-Agent
- Host
- Set-Cookie

### 47. What is Content-Type?

Content-Type identifies the media type of the request or response body.

Example:

`Content-Type: application/json`

### 48. What is Accept Header?

Accept specifies the response media types that the client can accept.

Example:

`Accept: application/json`

### 49. Difference between Content-Type and Accept.

- Content-Type describes the body being sent or returned.
- Accept describes the response formats the client is willing to receive.

### 50. What are HTTP Cookies?

Cookies are small pieces of data stored by the browser and sent to the server with applicable requests.

They are commonly used for session identification, preferences and tracking.

### 51. What is HTTP Caching?

Caching stores copies of responses so that they can be reused instead of repeatedly requesting the same data.

It can improve performance and reduce server load.

### 52. What is a Session?

A session allows the server to maintain user-related state across multiple HTTP requests.

In Django, session data is commonly stored server-side, with a session identifier maintained in a browser cookie.

### 53. What is the difference between Stateful and Stateless Communication?

| Stateful | Stateless |
|---|---|
| Maintains interaction state | Each request carries required context |
| May depend on previous requests | Does not depend on previous request state |
| Example: traditional session-based interaction | Example: stateless token-based API interaction |

---

### 54. What is Django REST Framework?

Django REST Framework is a third-party Django library used to build Web APIs.

It provides serializers, authentication, permissions, API views, validation, pagination, filtering and other API development features.

### 55. What are the advantages of DRF?

1. Easy API development.
2. Supports serialization and deserialization.
3. Provides authentication and permission classes.
4. Supports function-based and class-based views.
5. Provides reusable generic views.
6. Supports pagination and filtering.
7. Provides a browsable API.
8. Supports content negotiation.
9. Integrates with Django ORM.
10. Supports API testing and customization.

### 56. What are the disadvantages of DRF?

1. Additional learning complexity.
2. Can introduce overhead for very simple endpoints.
3. Requires careful configuration for security.
4. Complex serializer relationships can become difficult to maintain.
5. Improper queryset handling can cause performance problems.

### 57. What is the difference between Django and DRF?

| Django | DRF |
|---|---|
| Full-stack web framework | API development toolkit |
| Commonly returns HTML responses | Commonly returns JSON responses |
| Uses Django views | Provides APIView, ViewSets and generic views |
| Uses forms and model forms | Uses serializers |
| Supports traditional web applications | Supports REST-style APIs |

### 58. What is the difference between Django View and DRF APIView?

Django View is a base class for traditional Django class-based views.

DRF APIView extends Django's View and adds API functionality such as request parsing, authentication, permissions, content negotiation and exception handling.

### 59. What is a Browsable API?

The Browsable API is a DRF feature that provides a human-readable HTML interface for interacting with APIs through a web browser.

It is useful for development and testing.

### 60. What is Content Negotiation?

Content negotiation determines which response representation should be returned based on the client's request and the server's available renderers.

---

### 61. What is Serialization?

Serialization converts complex Python objects, such as Django model instances and QuerySets, into native Python data types that can be rendered into formats such as JSON.

### 62. What is Deserialization?

Deserialization converts incoming data into native Python data types so that it can be validated and used to create or update objects.

### 63. What is a Serializer?

A serializer is a DRF component that handles converting complex data into native Python data types and validating incoming data.

### 64. What is ModelSerializer?

ModelSerializer automatically generates serializer fields based on a Django model.

```python
class StudentSerializer(serializers.ModelSerializer):

    class Meta:
        model = Student
        fields = "__all__"
```

### 65. Difference between Serializer and ModelSerializer.

| Serializer | ModelSerializer |
|---|---|
| Fields are manually defined | Fields can be generated from a model |
| More control over field definitions | Less repetitive code |
| Create and update methods may need implementation | Default create and update are provided |
| Does not require a model | Usually associated with a model |

### 66. What are the advantages of Serializers?

- Convert complex data.
- Validate incoming information.
- Reduce repetitive code.
- Support nested representations.
- Support create and update operations.
- Help control which fields are exposed.

### 67. What are Serializer Fields?

Serializer fields define how individual pieces of data are represented and validated.

Examples:

- CharField
- IntegerField
- BooleanField
- EmailField
- DateField
- DateTimeField
- DecimalField
- ChoiceField
- ListField
- DictField
- SerializerMethodField

### 68. What is the difference between read_only and write_only?

**read_only=True:** Field is included in serialized output but ignored as an input field.

**write_only=True:** Field can be accepted as input but is excluded from serialized output.

Example:

```python
password = serializers.CharField(write_only=True)
```

### 69. What is required=True?

It indicates that the field must be supplied during deserialization unless other field settings or defaults alter that requirement.

### 70. What is allow_null=True?

It allows a field to accept `None` as a valid value.

### 71. What is allow_blank=True?

It allows an empty string as a valid value for applicable string fields.

### 72. What is many=True?

It tells a serializer to handle multiple objects or multiple input items.

```python
serializer = StudentSerializer(
    Student.objects.all(),
    many=True
)
```

### 73. What is Meta class in ModelSerializer?

The Meta class provides configuration for a ModelSerializer.

Important options:

- model
- fields
- exclude
- read_only_fields
- extra_kwargs
- depth

### 74. What is SerializerMethodField?

It is a read-only serializer field that obtains its value through a custom method.

```python
total = serializers.SerializerMethodField()

def get_total(self, obj):
    return obj.price * obj.quantity
```

### 75. What is Nested Serialization?

Nested serialization represents related objects inside another serializer.

Example: A student response can include the student's related address.

### 76. What is HyperlinkedModelSerializer?

It is a ModelSerializer variant that represents relationships and object identity using hyperlinks instead of only primary-key values.

### 77. What is the difference between PrimaryKeyRelatedField and StringRelatedField?

- PrimaryKeyRelatedField represents a relationship using the related object's primary key.
- StringRelatedField represents a relationship using the related object's string representation.

---

### 78. What is Validation?

Validation checks incoming data against defined rules before it is accepted or saved.

### 79. What are the types of Serializer Validation?

1. Field-level validation.
2. Object-level validation.
3. Custom validators.
4. Built-in field validation.

### 80. What is Field-Level Validation?

It validates an individual field using a method named `validate_<field_name>`.

```python
def validate_age(self, value):

    if value < 18:
        raise serializers.ValidationError(
            "Age must be at least 18"
        )

    return value
```

### 81. What is Object-Level Validation?

It validates multiple fields together using the `validate()` method.

```python
def validate(self, data):

    if data["start_date"] > data["end_date"]:
        raise serializers.ValidationError(
            "Invalid date range"
        )

    return data
```

### 82. What is a Custom Validator?

A custom validator is a reusable function or callable used to validate a field or value.

```python
def validate_name(value):

    if len(value) < 3:
        raise serializers.ValidationError(
            "Name must contain at least 3 characters"
        )
```

### 83. What is is_valid()?

`is_valid()` runs serializer validation and checks whether incoming data satisfies the defined rules.

```python
serializer = StudentSerializer(data=request.data)

if serializer.is_valid():
    serializer.save()
else:
    print(serializer.errors)
```

### 84. What is raise_exception=True?

It raises a ValidationError automatically if serializer validation fails.

```python
serializer.is_valid(raise_exception=True)
```

DRF's exception handling normally converts this into a 400 Bad Request response.

### 85. What is validated_data?

`validated_data` contains the validated native Python data after successful serializer validation.

### 86. What is serializer.errors?

It contains validation errors when incoming data fails validation.

### 87. Difference between data, validated_data and errors.

- `data`: Input supplied to the serializer.
- `validated_data`: Validated input after successful validation.
- `errors`: Validation errors when validation fails.

### 88. What is save()?

`save()` creates a new object or updates an existing object based on whether the serializer was initialized with an existing instance.

It must be called after successful validation when using the normal serializer save workflow.

### 89. What is create()?

`create()` defines how a new object is created from validated data.

### 90. What is update()?

`update()` defines how an existing object is modified using validated data.

### 91. Difference between save(), create() and update().

- `save()` decides whether to create or update.
- `create()` defines new object creation.
- `update()` defines existing object modification.

### 92. What is partial=True?

It allows a serializer to perform partial validation when updating an existing object.

```python
serializer = StudentSerializer(
    instance,
    data=request.data,
    partial=True
)
```

### 93. What is extra_kwargs?

It allows additional configuration of automatically generated ModelSerializer fields.

Example:

```python
class Meta:
    model = User
    fields = ["username", "password"]

    extra_kwargs = {
        "password": {"write_only": True}
    }
```

---

### 94. What is a Function-Based View?

A Function-Based View is a view implemented using a Python function.

In DRF, `@api_view` converts a Django function into a DRF API view.

### 95. What is @api_view?

`@api_view` is a decorator used to define function-based API views.

```python
@api_view(["GET", "POST"])
def student_view(request):

    if request.method == "GET":
        return Response({"message": "Student list"})

    if request.method == "POST":
        return Response({"message": "Student created"})
```

### 96. What is a Class-Based View?

A Class-Based View is a view implemented using a Python class.

It allows us to organize request handling through class methods.

### 97. What is APIView?

APIView is a DRF class-based view that extends Django's View and provides API-specific functionality.

```python
class StudentView(APIView):

    def get(self, request):
        return Response({"message": "Students"})

    def post(self, request):
        return Response({"message": "Created"})
```

### 98. What are the advantages of APIView?

- Supports HTTP method handlers.
- Supports authentication and permissions.
- Supports parsers and renderers.
- Provides API exception handling.
- Allows custom business logic.

### 99. Difference between FBV and CBV.

| FBV | CBV |
|---|---|
| Uses functions | Uses classes |
| Uses decorators | Uses class attributes and methods |
| Simple for small endpoints | Better for organizing complex endpoints |
| Uses conditional request handling | Uses separate HTTP handler methods |
| Less inheritance | Supports inheritance and reuse |

### 100. What is GenericAPIView?

GenericAPIView extends APIView and adds reusable functionality for working with querysets and serializers.

Important attributes and methods:

- `queryset`
- `serializer_class`
- `get_queryset()`
- `get_serializer()`
- `get_serializer_class()`
- `get_object()`
- `filter_queryset()`
- `pagination_class`

### 101. What are Mixins?

Mixins are reusable classes that provide common API operations.

Important mixins:

| Mixin | Function |
|---|---|
| ListModelMixin | List objects |
| CreateModelMixin | Create objects |
| RetrieveModelMixin | Retrieve one object |
| UpdateModelMixin | Update objects |
| DestroyModelMixin | Delete objects |

### 102. What are Generic Views?

Generic views combine GenericAPIView and commonly used mixins to provide ready-made API functionality.

Important generic views:

1. ListAPIView
2. CreateAPIView
3. RetrieveAPIView
4. UpdateAPIView
5. DestroyAPIView
6. ListCreateAPIView
7. RetrieveUpdateAPIView
8. RetrieveDestroyAPIView
9. RetrieveUpdateDestroyAPIView

### 103. What is ViewSet?

A ViewSet groups related API actions into one class.

Common actions:

- list()
- retrieve()
- create()
- update()
- partial_update()
- destroy()

### 104. What is ModelViewSet?

ModelViewSet provides the standard CRUD actions for a model.

It combines GenericAPIView and the standard CRUD mixins.

### 105. What is ReadOnlyModelViewSet?

It provides only read operations:

- list()
- retrieve()

It does not provide create, update or delete actions.

### 106. What is GenericViewSet?

GenericViewSet provides GenericAPIView functionality and ViewSet action handling.

CRUD actions are added by combining it with appropriate mixins.

### 107. Difference between APIView, GenericAPIView, Generic Views and ViewSet.

| Type | Main purpose |
|---|---|
| APIView | Custom API request handling |
| GenericAPIView | Reusable queryset and serializer functionality |
| Generic Views | Ready-made common API operations |
| ViewSet | Groups related API actions |
| ModelViewSet | Complete model-based CRUD |

---

### 108. What is Routing in DRF?

Routing maps incoming URLs to the appropriate API views or ViewSet actions.

### 109. What is a Router?

A router automatically generates URL patterns for ViewSets.

### 110. What is DefaultRouter?

DefaultRouter generates standard ViewSet routes and provides an API root view.

### 111. What is SimpleRouter?

SimpleRouter generates standard ViewSet routes without the automatically generated API root view.

### 112. Difference between DefaultRouter and SimpleRouter.

| DefaultRouter | SimpleRouter |
|---|---|
| Generates ViewSet routes | Generates ViewSet routes |
| Includes API root view | Does not include API root view |
| Supports format suffix patterns | Does not automatically generate format suffix patterns |

### 113. What is @action?

`@action` is a decorator used to create custom actions inside a ViewSet.

It supports custom API operations beyond standard CRUD actions.

### 114. What is basename in Router?

`basename` defines the base name used to generate URL names for a registered ViewSet.

It is useful when the router cannot automatically determine the basename from a queryset.

### 115. What is the difference between Path Parameters and Query Parameters?

**Path parameter:**

`/api/students/10/`

Used to identify a particular resource.

**Query parameter:**

`/api/students/?age=20`

Used for filtering, searching, sorting and other optional query operations.

---

### 116. What is Authentication?

Authentication verifies the identity of the user making an API request.

It answers: Who are you?

### 117. What is Authorization?

Authorization determines what an authenticated user is allowed to access or perform.

It answers: What are you allowed to do?

### 118. Difference between Authentication and Authorization.

| Authentication | Authorization |
|---|---|
| Verifies identity | Checks access rights |
| Identifies the user | Determines allowed actions |
| Happens before permission checks in the normal DRF request flow | Enforced through permissions and other access controls |

### 119. What is Authentication in DRF?

DRF authentication classes identify the user associated with an incoming request.

Important authentication classes:

- SessionAuthentication
- BasicAuthentication
- TokenAuthentication

JWT authentication is commonly added using a third-party package.

### 120. What is SessionAuthentication?

SessionAuthentication uses Django's session framework to authenticate users.

The client sends its session cookie with applicable requests.

Unsafe requests from authenticated sessions require CSRF protection.

### 121. What is BasicAuthentication?

BasicAuthentication uses a username and password sent through the HTTP Authorization header using Base64 encoding.

It should only be used over HTTPS.

### 122. What is TokenAuthentication?

TokenAuthentication uses a token associated with a user to authenticate API requests.

Example:

`Authorization: Token abc123`

### 123. What is JWT?

JWT stands for JSON Web Token.

It is a compact token format used to transmit claims between parties.

A JWT contains three parts:

1. Header
2. Payload
3. Signature

Format:

`header.payload.signature`

### 124. What are the advantages of JWT?

- Compact token format.
- Can carry claims.
- Supports stateless token verification.
- Suitable for distributed applications.
- Can include expiration information.

### 125. What are the disadvantages of JWT?

- Revocation can be difficult without additional mechanisms.
- A stolen token can be misused until it expires or is revoked.
- Large payloads increase request size.
- Signing does not automatically encrypt the payload.
- Requires careful key and token management.

### 126. Difference between DRF Token Authentication and JWT.

| DRF Token | JWT |
|---|---|
| Commonly database-backed | Signed claims-based token |
| Simple token structure | Header, payload and signature |
| Usually checks token against database | Can validate signature and claims |
| Built-in DRF token authentication has no built-in expiration | Supports expiration claims |
| Simpler setup | Requires additional JWT integration |

### 127. What is Access Token?

An access token is a credential used to access protected resources.

### 128. What is Refresh Token?

A refresh token is used to obtain a new access token without requiring the user to log in again.

### 129. What is Authentication Class?

An authentication class defines how an incoming request is authenticated.

### 130. What is Permission Class?

A permission class determines whether a request is allowed to access a view or object.

---

### 131. What are Permissions in DRF?

Permissions control whether a request should be allowed to access an API view or object.

### 132. What are the built-in permission classes?

1. AllowAny
2. IsAuthenticated
3. IsAdminUser
4. IsAuthenticatedOrReadOnly

### 133. What is AllowAny?

Allows any user to access the API, whether authenticated or not.

### 134. What is IsAuthenticated?

Allows access only to authenticated users.

### 135. What is IsAdminUser?

Allows access to users whose Django `is_staff` attribute is True.

It does not automatically mean that the user has every possible business-level owner permission.

### 136. What is IsAuthenticatedOrReadOnly?

Allows read-only access to everyone but requires authentication for unsafe operations.

### 137. What is Custom Permission?

A custom permission is a permission class created to implement application-specific access rules.

Example:

A gym owner can manage all memberships, while a member can access only their own membership.

### 138. What is Object-Level Permission?

Object-level permissions determine whether a user can access or modify a specific object.

### 139. Difference between View-Level and Object-Level Permissions.

| View-Level | Object-Level |
|---|---|
| Checks access to the endpoint | Checks access to a particular object |
| Applies to the view | Applies to an individual resource |
| Example: only authenticated users | Example: only the owner can edit a membership |

### 140. What is the difference between Authentication and Permission Classes?

Authentication identifies the user.

Permission classes determine whether the identified user is allowed to perform the requested operation.

### 141. What is IsAuthenticatedOrReadOnly used for?

It is useful for APIs where everyone can retrieve information but only authenticated users can create, update or delete resources.

---

### 142. What are Parsers?

Parsers determine how incoming request-body data is interpreted and converted into native Python data.

### 143. What are the important Parser Classes?

1. JSONParser
2. FormParser
3. MultiPartParser
4. FileUploadParser

### 144. What is JSONParser?

JSONParser parses incoming JSON request data.

### 145. What is FormParser?

FormParser parses URL-encoded form data.

### 146. What is MultiPartParser?

MultiPartParser parses multipart form data, commonly used for file uploads.

### 147. What is FileUploadParser?

FileUploadParser handles raw file uploads.

### 148. What are Renderers?

Renderers determine how native Python response data is converted into the final response format.

### 149. What are the important Renderer Classes?

1. JSONRenderer
2. BrowsableAPIRenderer
3. TemplateHTMLRenderer

### 150. What is JSONRenderer?

JSONRenderer converts response data into JSON-formatted content.

### 151. What is BrowsableAPIRenderer?

It renders the API response as an interactive, human-readable HTML interface.

### 152. Difference between Parser and Renderer.

| Parser | Renderer |
|---|---|
| Handles incoming data | Handles outgoing data |
| Request processing | Response generation |
| JSONParser | JSONRenderer |
| Converts request content to Python data | Converts Python data to response content |

---

### 153. What is request.data?

`request.data` contains parsed request-body data.

It can handle JSON and form data depending on configured parsers.

### 154. What is request.query_params?

It provides access to query-string parameters.

Example:

```python
course = request.query_params.get("course")
```

### 155. What is request.user?

It represents the user associated with the current request after authentication.

### 156. What is request.auth?

It contains the authentication information returned by the authentication class, if any.

### 157. What is Response?

DRF Response is used to return API response data.

```python
return Response(
    {"message": "Success"},
    status=200
)
```

### 158. Difference between Django HttpResponse and DRF Response.

| HttpResponse | DRF Response |
|---|---|
| Django component | DRF component |
| Returns HTTP content | Accepts unrendered response data |
| Does not provide DRF content negotiation | Supports content negotiation |
| Commonly used in Django views | Commonly used in DRF API views |

### 159. What is APIException?

APIException is the base exception class for many DRF API exceptions.

### 160. What is the Default Exception Handler?

It converts recognized exceptions into appropriate HTTP responses.

DRF allows developers to configure a custom exception handler.

### 161. What is Response Status?

The status parameter specifies the HTTP status code returned with the API response.

Example:

```python
return Response(
    {"message": "Created"},
    status=status.HTTP_201_CREATED
)
```

---

### 162. What is Filtering?

Filtering retrieves records based on specified conditions.

Example:

`/api/students/?course=Python`

### 163. What is Searching?

Searching finds records that match specified search terms.

DRF provides SearchFilter.

### 164. What is Ordering?

Ordering sorts API results according to specified fields.

Example:

`/api/students/?ordering=name`

Descending:

`/api/students/?ordering=-name`

### 165. What is DjangoFilterBackend?

DjangoFilterBackend integrates django-filter with DRF to provide field-based filtering.

It requires the `django-filter` package.

### 166. What is SearchFilter?

SearchFilter provides search functionality using configured search fields.

```python
search_fields = ["name", "email", "course"]
```

### 167. What is OrderingFilter?

OrderingFilter allows clients to control the ordering of API results.

```python
ordering_fields = ["name", "age"]
```

### 168. Difference between Filtering, Searching and Ordering.

| Filtering | Searching | Ordering |
|---|---|---|
| Select records based on conditions | Find matching text | Sort records |
| Often exact or field-based | Text matching | Ascending or descending |

---

### 169. What is Pagination?

Pagination divides a large collection of API results into smaller pages.

### 170. Why is Pagination important?

- Reduces response size.
- Improves performance.
- Reduces unnecessary data transfer.
- Makes large datasets easier to navigate.
- Helps control database and application load.

### 171. What are the types of Pagination in DRF?

1. PageNumberPagination
2. LimitOffsetPagination
3. CursorPagination

### 172. What is PageNumberPagination?

It divides results into numbered pages.

Example:

`/api/students/?page=2`

### 173. What is LimitOffsetPagination?

It uses limit and offset parameters to control which records are returned.

Example:

`/api/students/?limit=10&offset=20`

### 174. What is CursorPagination?

It uses cursor-based navigation to move through ordered results.

It is particularly useful for large datasets and relatively stable ordered feeds.

### 175. Difference between the three pagination types.

| Pagination | Working |
|---|---|
| PageNumber | Uses page numbers |
| LimitOffset | Uses limit and offset |
| Cursor | Uses an encoded cursor for navigation |

---

### 176. What is Throttling?

Throttling controls how frequently a client can make API requests.

### 177. Why is Throttling important?

- Controls excessive API usage.
- Helps protect server resources.
- Reduces abuse.
- Limits repeated requests.
- Helps enforce usage policies.

### 178. What are the types of DRF Throttling?

1. AnonRateThrottle
2. UserRateThrottle
3. ScopedRateThrottle

### 179. What is AnonRateThrottle?

It limits requests from unauthenticated clients.

### 180. What is UserRateThrottle?

It limits the request rate for authenticated users.

### 181. What is ScopedRateThrottle?

It applies rate limits based on a configured scope.

### 182. What is Rate Limiting?

Rate limiting is the practice of restricting the number of requests allowed within a particular period.

---

### 183. What is CORS?

CORS stands for Cross-Origin Resource Sharing.

It is a browser security mechanism that controls whether a frontend from one origin can access resources from another origin.

### 184. What is an Origin?

An origin consists of:

- Scheme
- Host
- Port

For example:

`http://localhost:3000`

### 185. What is CSRF?

CSRF stands for Cross-Site Request Forgery.

It is an attack in which an attacker tricks a user's browser into sending an unwanted authenticated request to a website.

### 186. What is CSRF Protection?

CSRF protection uses a token-based mechanism to verify that certain browser requests originate from a legitimate interaction rather than an attacker-controlled page.

### 187. Difference between CORS and CSRF.

| CORS | CSRF |
|---|---|
| Controls cross-origin browser access | Protects against forged requests |
| Browser security mechanism | Web application security protection |
| Controls whether cross-origin responses can be accessed | Verifies the legitimacy of applicable requests |

### 188. Does DRF require CSRF protection?

DRF SessionAuthentication requires CSRF validation for unsafe requests from authenticated sessions.

Other authentication mechanisms have different CSRF considerations.

---

### 189. What is API Versioning?

API versioning allows developers to introduce API changes without breaking existing clients.

### 190. Why is API Versioning important?

- Maintains backward compatibility.
- Supports gradual API upgrades.
- Allows different clients to use different versions.
- Prevents sudden breaking changes.

### 191. What are the different API Versioning methods in DRF?

1. URLPathVersioning
2. NamespaceVersioning
3. AcceptHeaderVersioning
4. QueryParameterVersioning
5. HostNameVersioning

### 192. What is URLPathVersioning?

It identifies the API version through the URL path.

Example:

`/api/v1/students/`

### 193. What is QueryParameterVersioning?

It identifies the version through a query parameter.

Example:

`/api/students/?version=1`

### 194. What is AcceptHeaderVersioning?

It identifies the API version using the HTTP Accept header.

---

### 195. What is QuerySet?

A QuerySet represents a collection of database queries used to retrieve objects from a Django model.

### 196. What is Lazy Evaluation?

Django QuerySets are lazy, meaning database queries are generally not executed until the results are evaluated.

### 197. What is the N+1 Query Problem?

The N+1 query problem occurs when one query retrieves a collection and additional queries are executed for each object to retrieve related data.

For example, retrieving 100 memberships and accessing each membership's user individually can generate 101 queries.

### 198. What is select_related()?

`select_related()` retrieves related objects using SQL JOIN operations.

It is generally used for:

- ForeignKey
- OneToOneField

### 199. What is prefetch_related()?

`prefetch_related()` retrieves related objects using separate queries and joins the results in Python.

It is useful for:

- ManyToManyField
- Reverse ForeignKey
- Other supported relationships

### 200. Difference between select_related() and prefetch_related().

| select_related() | prefetch_related() |
|---|---|
| Uses SQL JOIN | Uses separate queries |
| Single-valued relationships | Commonly multi-valued relationships |
| ForeignKey | ManyToMany |
| OneToOne | Reverse ForeignKey |

### 201. What is Query Optimization?

Query optimization improves database query efficiency to reduce execution time and resource usage.

Common techniques:

- select_related()
- prefetch_related()
- only()
- defer()
- values()
- values_list()
- Appropriate indexes
- Avoiding unnecessary queries

### 202. What is Database Indexing?

An index is a database structure that helps retrieve records faster.

It can improve read performance but may increase storage requirements and write overhead.

### 203. Why should we optimize get_queryset() in DRF?

Because the queryset determines which database records are retrieved for an API endpoint.

Optimizing it reduces unnecessary queries and improves API performance.

---

### 204. What are Django Signals?

Signals allow certain senders to notify registered receivers when particular events occur.

They are Django features rather than DRF-specific features.

### 205. What are the common Django Signals?

- pre_save
- post_save
- pre_delete
- post_delete
- m2m_changed

### 206. What is perform_create()?

It is a hook provided by DRF generic views to customize object creation.

Example:

```python
def perform_create(self, serializer):
    serializer.save(user=self.request.user)
```

### 207. What is perform_update()?

It is a hook used to customize object updates.

### 208. What is perform_destroy()?

It is a hook used to customize object deletion.

### 209. What is get_queryset()?

It dynamically returns the queryset used by a view.

Example:

```python
def get_queryset(self):
    return Membership.objects.filter(
        user=self.request.user
    )
```

### 210. What is get_serializer_class()?

It dynamically chooses the serializer class based on the current request or ViewSet action.

### 211. What is get_serializer_context()?

It provides additional context to a serializer.

For example, request information can be passed to a serializer.

### 212. What is get_object()?

It retrieves an individual object using the configured queryset and lookup configuration.

### 213. What is @action in ViewSets?

It defines a custom ViewSet action that is not part of the standard CRUD operations.

Example: A custom action to cancel a membership.

### 217. What is API Security?

API security involves protecting API endpoints, data and operations from unauthorized access and misuse.

### 218. How can we secure a DRF API?

- Use HTTPS.
- Apply proper authentication.
- Configure permissions.
- Validate incoming data.
- Protect against unauthorized object access.
- Apply throttling.
- Avoid exposing sensitive information.
- Store secrets securely.
- Restrict CORS origins appropriately.
- Use secure token management.
- Validate uploaded files.
- Keep dependencies updated.

### 219. What is SQL Injection?

SQL Injection is an attack in which malicious SQL statements are inserted into application inputs to manipulate database queries.

Django ORM parameterizes normal query operations and helps protect against SQL injection.

### 220. What is XSS?

XSS stands for Cross-Site Scripting.

It is an attack in which malicious scripts are injected into web content and executed in another user's browser.

### 221. What is Password Hashing?

Password hashing converts a password into a one-way cryptographic hash for secure storage.

Django provides password hashing utilities.

### 222. What is the difference between Encryption and Hashing?

| Encryption | Hashing |
|---|---|
| Reversible with the correct key | Designed to be one-way |
| Used to protect recoverable information | Used for verification and integrity |
| Requires decryption to recover original data | Original password should not be recovered |

### 223. What is an Idempotency Key?

An idempotency key is a unique identifier sent with a request to prevent duplicate processing of the same operation.

It is particularly useful for payment APIs.

### 224. What is API Documentation?

API documentation describes how developers can interact with an API.

It includes:

- Endpoint URLs
- HTTP methods
- Request parameters
- Request body
- Authentication requirements
- Response formats
- Status codes

### 225. What is OpenAPI?

OpenAPI is a specification used to describe REST APIs in a standardized machine-readable format.

### 226. What is Swagger?

Swagger is a collection of tools used to work with OpenAPI specifications.

Swagger UI provides interactive API documentation.

### 227. What is Postman?

Postman is an API development and testing platform used to send HTTP requests, inspect responses, manage environments and organize API collections.

### 228. What is API Testing?

API testing verifies whether API endpoints work correctly according to their expected behavior.

It checks:

- Status codes
- Response body
- Validation
- Authentication
- Permissions
- CRUD operations
- Error handling

### 229. What is APITestCase?

APITestCase is a DRF testing class that provides an APIClient for testing API endpoints.

### 230. What is APIClient?

APIClient is a testing client used to make API requests and test DRF endpoints.

### 231. What is APIRequestFactory?

APIRequestFactory creates request objects for testing API views directly.

### 232. Difference between APIClient and APIRequestFactory.

| APIClient | APIRequestFactory |
|---|---|
| Tests through the application request flow | Creates request objects for direct view testing |
| Useful for endpoint testing | Useful for isolated view testing |
| More similar to client interaction | More focused on view behavior |

---

### 233. What is Content Negotiation?

Content negotiation determines the appropriate response format based on the client's accepted media types and the server's available renderers.

### 234. What is API Throttling Scope?

A throttle scope identifies a category of API operations to which a particular request limit applies.

### 235. What is Backward Compatibility?

Backward compatibility means newer versions of an API continue to support existing clients and their expected behavior.

### 236. What is a Webhook?

A webhook is a mechanism where one application sends an HTTP request to another application when a particular event occurs.

Example: A payment gateway sends a webhook when a payment succeeds.

### 237. What is Synchronous Communication?

Synchronous communication means the client waits for the operation's response before continuing with that interaction.

### 238. What is Asynchronous Communication?

Asynchronous communication allows operations to continue without requiring the client to wait for the final result.

### 239. What is the difference between API and Webhook?

| API | Webhook |
|---|---|
| Usually client initiates the request | Event triggers the request |
| Client asks for information or an operation | Server notifies another system |
| Often request-response based | Often event-driven |

### 240. What is API Gateway?

An API Gateway is an entry point that routes API requests to appropriate backend services.

It may also handle authentication, rate limiting, logging and request transformation.

### 241. What is Microservices Architecture?

Microservices architecture divides an application into smaller, independently deployable services that communicate through defined interfaces.

### 242. What is GraphQL?

GraphQL is a query language and runtime for APIs that allows clients to request specific data fields.

### 243. Difference between REST and GraphQL.

| REST | GraphQL |
|---|---|
| Usually uses multiple resource endpoints | Commonly uses one query endpoint |
| Server defines response structure | Client specifies requested fields |
| May require multiple requests | Can retrieve related data in one query |
| Commonly uses HTTP methods for operations | Uses queries, mutations and subscriptions |
