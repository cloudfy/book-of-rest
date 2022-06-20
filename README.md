# Book of REST
Doctrine for programming REST APIs. Guidance for using, responding and providing APIs. Use this book of REST as a cheat sheet for design principles.

## Introduction

## Authorization
Authentication and authorization is key to a secure infrastructure. Keep to standardized methods of authentication including, not excluding:

* Basic authentication. Cross-origion posts will be affected. Consider wisely.
* Bearer authentication. Simplifies the format.
* OAuth/OAuth2.
* JWT.

## Versioning
Your API will change over time, so might as well version it from the first go. Two approaches applies to versioning an API.
My recommendating will be to use URL, as this eases the use of API from various consumers.

### Path based versioning either by query-string or by URL. 

```
GET /api/v1/foo
Accept: application/json; version=1
```

### Header based versioning.

```
GET /api/foo
Accept: application/json; version=1
```

or

```
GET /api/foo
Accept: application/json;
X-Version: v1
```

## HTTP Responses 

| Code | Response | Description |
|---|---|---|
| 200 | Ok | Successful get, patch (return a JSON object) |
| 201 | Created | Successful post (return a JSON object) |
| 202 | Accepted | Successful post, delete, path - async. Task is queued. |
| 204 | No content | Successful delete |
| 206 | Partial content | Successful get - async |
| 400 | Bad request | Data issues such as invalid JSON, etc. |
| 401 | Unauthorized | Not authenticated |
| 403 | Forbidden | Authenticated, but no permissions |
| 404 | Not found | Resource not found |
| 409 | Conflict | Duplicate data or invalid data state would occur. |
| 422 | Unprocessable entity | Validation failed |
| 500 | Internal Server Error | Unhandled error |

### Provide a known error response

```
HTTP/1.1 401 Unauthorized
Content-Type: application/json
{
  'id': 'auth_failed',
  'message': "You're not logged in."
}
```

## HTTP Methods

| Method | Example | Description |
|---|---|---|
| GET | /animal/1 | Read. Should return object (200) |
| PUT | /animal/1 | Edit. Should return object (202) |
| DELETE | /animal/1 | Delete. Should return no-content (204) |
| POST | /animal/ | Create. Should return object (201) |
| PATCH | /animal/1 | Partial edit. Should return object (202) |

### Use sub-classes for sub actions

| Method | Example | Description |
|---|---|---|
| GET | /student/1/teachers | Read. Return teachers of student 1 (200) |
| GET | /student/1/teachers/A | Read. Return teacher A of student 1 (200) |
| POST | /student/1/courses | Create. Return newly created course of student 1 (201) |
| PUT | /student/1/teachers/A | Edit. Edit the relationship or data between student 1 and teacher A. (202) |

### Common Guidance

**Good practise**
* Minimum two URLs (endpoints) per resource:
  * The resource collection (e.g. /orders)
  * Individual resource within the collection (e.g. /orders/{orderId}).
* Naming: Use plural forms (‘orders’ instead of ‘order’).
* Alternate resource names with IDs as URL nodes (e.g. /orders/{orderId}/items/{itemId})
* Keep URLs as short as possible. Preferably, no more-than three nodes per URL.
* Always return paging of lists. Large recordset must be broken down.
  * Support filtering, sorting, and pagination on collections
* Use nouns as resource names (e.g. don’t use verbs in URLs).
* Make resource representations meaningful.
  * “No Naked IDs!” No plain IDs embedded in responses. Use links and reference objects.
  * Design resource representations. Don’t simply represent database tables.
  * Merge representations. Don’t expose relationship tables as two IDs.
* Use ISO 8601 timepoint formats for dates in representations.

**Suggestions**
* Support link expansion of relationships. Allow clients to expand the data contained in the response by including additional representations instead of, or in addition to, links.
* Support field projections on resources. Allow clients to reduce the number of fields that come back in the response.
* Ensure that your GET, PUT, and DELETE operations are all idempotent. There should be no adverse side affects from operations

### Avoid

* Avoid using WSDL/SOAP, method based url and methods.

**Don'ts**
```
GET /student/waiveAtTeacher/
Accept: application/json;
```

```
POST /student/askToDrinkABeer/2/
Accept: application/json;
```
