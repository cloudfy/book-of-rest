# Book of REST
Doctrine for programming REST APIs. Guidance for using, responding and providing API.

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

* Path based versioning either by query-string or by URL. 
* Header based versioning.

## HTTP Responses 
