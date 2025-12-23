# Dressed™ System – API Design

## 1. Purpose

This document defines the public REST APIs exposed by the backend services.
It ensures **consistent, predictable, and industry-standard communication** between frontend, backend, and third-party consumers.

---

## 2. Design Principles

* RESTful endpoints
* JSON request/response format
* Stateless APIs
* Clear and meaningful HTTP status codes
* **Standardized response envelope** for all APIs
* **Consistent pagination model** for list endpoints
* **Centralized error handling**

---

## 3. Common API Response Format (Industry Standard)

All APIs (success or error) MUST follow the same response structure.

### 3.1 Base Response Envelope

```json
{
  "success": true,
  "statusCode": 200,
  "message": "Request processed successfully",
  "data": {},
  "errors": null,
  "meta": {
    "requestId": "9f2c1a3e",
    "timestamp": "2025-12-23T12:30:45Z"
  }
}
```

### Field Explanation

| Field      | Type         | Description                  |
| ---------- | ------------ | ---------------------------- |
| success    | boolean      | Indicates success or failure |
| statusCode | number       | HTTP status code             |
| message    | string       | Human-readable message       |
| data       | object/array | Actual response payload      |
| errors     | array/null   | Error details if failed      |
| meta       | object       | Traceability & diagnostics   |

---

## 4. Pagination Standard (For List APIs)

Used for endpoints returning collections (e.g. `GET /designs`, `GET /quotes`).

### 4.1 Request Parameters

```http
GET /designs?page=1&pageSize=10
```

| Parameter | Description           | Default |
| --------- | --------------------- | ------- |
| page      | Page number (1-based) | 1       |
| pageSize  | Records per page      | 10      |

### 4.2 Paginated Response Format

```json
{
  "success": true,
  "statusCode": 200,
  "message": "Designs retrieved successfully",
  "data": [
    {
      "id": "d101",
      "name": "Summer Dress"
    }
  ],
  "errors": null,
  "meta": {
    "pagination": {
      "page": 1,
      "pageSize": 10,
      "totalRecords": 57,
      "totalPages": 6,
      "hasNext": true,
      "hasPrevious": false
    },
    "requestId": "abc123",
    "timestamp": "2025-12-23T12:35:00Z"
  }
}
```

### Pagination Rules

* Page numbers start from **1**
* Sorting and filtering are optional extensions
* Cursor-based pagination can be introduced later if required

---

## 5. Standard Error Response Model

Errors MUST follow a predictable structure across all services.

### 5.1 Error Response Format

```json
{
  "success": false,
  "statusCode": 400,
  "message": "Validation failed",
  "data": null,
  "errors": [
    {
      "code": "INVALID_INPUT",
      "field": "email",
      "message": "Email format is invalid"
    }
  ],
  "meta": {
    "requestId": "err789",
    "timestamp": "2025-12-23T12:40:00Z"
  }
}
```

---

## 6. Standard Error Codes (Industry Practice)

| Error Code          | HTTP | When Used                     |
| ------------------- | ---- | ----------------------------- |
| INVALID_INPUT       | 400  | Validation failures           |
| UNAUTHORIZED        | 401  | Missing/invalid auth          |
| FORBIDDEN           | 403  | Access denied                 |
| NOT_FOUND           | 404  | Resource not found            |
| CONFLICT            | 409  | Duplicate or state conflict   |
| RATE_LIMITED        | 429  | Too many requests             |
| INTERNAL_ERROR      | 500  | Unhandled server error        |
| SERVICE_UNAVAILABLE | 503  | Downstream dependency failure |

---

## 7. API Endpoints

### Design Service

* `POST /designs` → Upload a design
* `GET /designs` → List designs (Paginated)
* `GET /designs/{id}` → Get design details

### Quote Service

* `POST /quotes` → Submit a quote
* `GET /quotes/by-design/{designId}` → View quotes for a design (Paginated)

### Order Service

* `POST /orders` → Place an order
* `GET /orders/{id}` → Get order details
* `PUT /orders/{id}/status` → Update order status

### Payment Service

* `POST /payments` → Process payment
* `GET /payments/{orderId}` → Get payment status

---

## 8. Standard HTTP Status Codes

* 200 OK
* 201 Created
* 400 Bad Request
* 401 Unauthorized
* 403 Forbidden
* 404 Not Found
* 409 Conflict
* 429 Too Many Requests
* 500 Internal Server Error
* 503 Service Unavailable

---

## 9. Best Practices & Notes

* Always return the **standard response envelope**
* Never expose stack traces to clients
* Use **requestId** for distributed tracing
* Swagger / OpenAPI for documentation
* APIs are versionable (e.g. `/api/v1`)
* Follow backward compatibility rules

---

This design aligns with **enterprise-grade, industry-standard REST API practices**.
