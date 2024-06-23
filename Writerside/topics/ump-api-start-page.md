# UAS Management Portal - REST API

## Introduction

This document provides an overview of the UAS Management Portal (UMP) RESTful API, designed to manage personnel and
equipment related to unmanned aerial systems (UAS), including drones and their ground support equipment.
The API is designed using RESTful web services, JSON for structured data, and Active Directory for secure user
authentication and authorization. The goal is to create a robust and scalable REST API that enables efficient
communication between various information components related to UAS operations.

## What you can do using this API

The UAS Management Portal (UMP) RESTful API allows for the efficient management and operation of unmanned aerial
systems (UAS), including:

1. Training pilot-operators
2. Planning crew deployment
3. Managing aerial equipment
4. Managing computing and communication devices
5. Managing ground support equipment
6. Accessing products created by UAS sensors

## Context overview

<img src="context_vision.png" alt="Alttext"/>

## Authentication

The API uses Active Directory for secure user authentication and authorization on Windows servers. This ensures that
only authorized
personnel can access and manage the data.
Authentication is handled via Role-Based Access Control (RBAC) to provide appropriate access levels to different users.

## Base URLs

###### placeholder

<deflist collapsible="true">
    <def title="URLs for docs" default-state="collapsed">
<ul>
        <li>Diagrams: <a href="https://tech.docs/diagrams"></a></li>
        <li>Swagger docs: <a href="https://tech.docs/swagger"></a></li>
</ul>
    </def>
</deflist>

## Rate Limiting

The UAS Management Portal (UMP) limits the number of API requests a single client can make to ensure fair usage and
prevent system overload. The standard rate limit is set to 70 requests per minute (rpm). If this limit is exceeded,
a `429 Too Many Requests` response is returned with a `Retry-After` header specifying the amount of time to wait before
making another request.

All responses from the API contain the following headers to help manage rate limits:

- **X-Rate-Limit-Limit**: The rate limit period (e.g., 1m, 1h).
- **X-Rate-Limit-Remaining**: The number of requests remaining in the current rate limit period.
- **X-Rate-Limit-Reset**: The UTC date and time (ISO 8601) when the rate limit resets.

### Example Response with Rate Limiting Headers

```cURL
HTTP/1.1 200 OK
X-Rate-Limit-Limit: 1m
X-Rate-Limit-Reset: 2024-06-23T20:39:22.1494434Z
```

This rate limiting strategy ensures that while general usage remains smooth and responsive, specific critical resources
such as image materials are protected from overuse by external users.

## Error Handling

> This section to be rewritten.
>
{style="warning"}

The API uses standard HTTP status codes to indicate the success or failure of an API request. Common error codes
include:

- `400 Bad Request`: The request was invalid.
- `401 Unauthorized`: Authentication failed or user does not have permissions.
- `404 Not Found`: The requested resource was not found.
- `500 Internal Server Error`: An error occurred on the server.

## Versioning

> This section to be rewritten.
>
{style="warning"}

The API supports versioning to ensure compatibility with different client versions. Specify the desired API version in
the request header using the `Accept` parameter, e.g., `Accept: application/vnd.ump.v1+json`.

## Technical Overview

### API Gateway

The API is hosted on a supported application server and communicates via operating system processes with other systems.
The API Gateway handles all incoming requests and routes them to the appropriate service.

### Staff Information System (SIS) and Logistics Information System (LIS)

SIS is needed for authentication and authorization. Connection to these systems is secured via HTTPS protocols.
They provide essential logistical and personnel information for UMP.

### Specific APIs for individual portals

- **UA Portal API**: Manages UAS operations data.
- **Crew Portal API**: Manages crew data and operations.
- **GSE Portal API**: Manages ground support equipment.
- **ICT Devices Portal API**: Manages ICT devices used in UAS operations.

## Documentation

The technical documentation includes diagrams and schematics detailing the architecture, components, and their
interactions within the UAS Management Portal (UMP). These are available in the appendices of this document.

<seealso>

- **API Tutorials**: [Link to tutorials]
- **API Guides**: [Link to guides]

</seealso>

---

This description aligns with the provided outline and covers the key aspects of the UAS Management Portal REST API.