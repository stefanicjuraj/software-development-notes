# RESTful Web Services

A web service, same as a web application, is a software that runs on a web server, but instead of returning web pages to users, it returns data to other applications and gives access to its services.

- A **web application** is user friendly.
- A **web application** provides a user interface (UI).

- A **web service** is application friendly.
- A **web service** provides an application programming interface (API).

Web services (WS) promote reusability of code. WS are small components that can be reused by multiple systems (web app, mobile app, ...). Web Services make sense when you need to reuse the same data in several different applications.

Over time, different architectures & protocols have been developed and used in a WS. There are mainly two types of web services, depending on the underlying architecture & protocol:

## SOAP-Based Web Services

SOAP, an acronym for Simple Object Access Protocol, is an XML-based messaging protocol for exchanging information. Although SOAP can be delivered via a variety of transport protocols, the initial focus of SOAP is remote procedure calls performed via HTTP.

## RESTful Web Services

RESTful WS are newer than SOAP-based WS. They were next in line of evolution of WS. They have been named RESTful because they conform to the REST (Representational State Transfer) architecture (next slide) that utilizes the HTTP/HTTPS protocol (unlike those with a specific protocol like SOAP).

## REST Architecture

**REST** is a resource-oriented architectural style.

A **resource** is any data that can be uniquely identified by an & which state (current data values) can be represented (transfered) to the clients in different formats (e.g. xml, json).

Hence the name **Representational State Transfer**.

Four HTTP verbs are used to provide a basic set of CRUD functionality:

- **GET** to retrieve a resource.
- **POST** to create a resource.
- **PUT** to update a resource.
- **DELETE** to remove a resource.

A web service that conforms to REST is called a RESTful WS.

## REST Resource

A resource can be a singleton or a collection. For example, “customers” is a collection resource and “customer” is a singleton resource.

We can identify “customers” collection resource using the URI

**/customers**

We can identify a single “customer” resource using the URI

**/customers/{customerId}.**

A resource may contain sub-collection resources. This happens when you are dealing with data & relationships.

For example, sub-collection resource “accounts” of a particular “customer” can be identified using the URI

**/customers/{customerId}/accounts**

Similarly, a singleton resource “account” inside the sub-collection resource “accounts” can be identified as follows:

**/customers/{customerId}/accounts**

### Best Practices

- Use nouns to represent resources

  - http://api.example.com/users

- Use hyphens ( - ) to improve the readability of URIs

  - http://api.example.com/managed-devices

- Do not use underscores ( \_ ).

- Use lowercase letters in URIs

- Do not use file extensions

- Never use CRUD function names in URIs. URIs should only be used to uniquely identify the resources and not any action upon them. Use HTTP request methods to indicate which CRUD function is performed.

  - HTTP GET http://api.example.com/managed-devices
    - Get all devices
  - HTTP GET http://api.example.com/managed-devices/{id}
    - Get device for given Id
  - HTTP POST http://api.example.com/managed-devices
    - Create new Device
  - HTTP PUT http://api.example.com/managed-devices/{id}
    - Update device for given Id
  - HTTP DELETE http://api.example.com/managed-devices/{id}
    - Delete device for given Id

- Use query parameters to filter URI collection
  - http://api.example.com/managed-devices?region=Croatia&brand=HP

## API

**API** is a software program that knows how to further process requests for data that is going to be used by other applications. It acts as an intermediary layer between the server and the rest of the application, that processes data transfer between systems.

**Web APIs** are HTTP/HTTPS based, meaning, they know how to process HTTP requests for data.

Whereas a user interface is designed for use by humans, APIs are designed for use by an application.

User interface of an application allows a human to interact with that application.

API of an application allows other programs to interact with that application.

## Consuming RESTful WS Using Postman

Use the Postman API Network to discover APIs.

The Postman API Network provides a central place for both API consumers and API producers to easily discover, explore, and share APIs. Postman has a worldwide community of 12 million developers, and the Public API Network is this community’s go-to place to discover, explore, and share APIs.

![[consuming-restful-web-service.png]]

![[consuming-restful-web-service-browser.png]]
