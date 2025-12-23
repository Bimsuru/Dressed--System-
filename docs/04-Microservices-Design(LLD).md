# Dressed™ System – Microservices Design (Low-Level Design)

## 1. Purpose

This document provides a **low-level design (LLD)** for each microservice in the Dressed™ platform.  
It describes responsibilities, key APIs, database schema summaries, error handling strategies, and communication patterns.

---

## 2. API Gateway

### Responsibilities
- Acts as the single entry point for frontend requests
- Routes requests to appropriate backend services
- Performs basic request validation and authentication (mocked)

### Key APIs
- Forwards all client requests to internal services

### Database Schema
- None (stateless service)

### Error Handling
- Returns standardized HTTP error responses
- Handles invalid routes and malformed requests

### Communication Type
- REST (synchronous)

---

## 3. User Service

### Responsibilities
- Manages users (Designers, Suppliers, Admins)
- Handles basic authentication and role management

### Key APIs
- `POST /users`
- `GET /users/{id}`
- `GET /users?role=Supplier`

### Database Schema (Summary)
- **Users**
  - Id
  - Name
  - Email
  - Role

### Error Handling
- 400 for invalid input
- 404 for user not found
- 500 for internal errors

### Communication Type
- REST (synchronous)

---

## 4. Design Service

### Responsibilities
- Manages design submissions
- Stores design metadata and file references
- Categorizes designs

### Key APIs
- `POST /designs`
- `GET /designs`
- `GET /designs/{id}`

### Database Schema (Summary)
- **Designs**
  - Id
  - DesignerId
  - Category
  - FileUrl
  - CreatedAt

### Error Handling
- 400 for invalid file or metadata
- 404 for design not found
- 500 for storage failures

### Communication Type
- REST (synchronous)

---

## 5. Quote Service

### Responsibilities
- Handles supplier quotations for designs
- Manages quote retrieval and negotiation messages

### Key APIs
- `POST /quotes`
- `GET /quotes/by-design/{designId}`
- `GET /quotes/{id}`

### Database Schema (Summary)
- **Quotes**
  - Id
  - DesignId
  - SupplierId
  - Price
  - Message
  - Status

### Error Handling
- 400 for invalid quotation data
- 404 for quote not found
- 500 for internal processing errors

### Communication Type
- REST (synchronous)

---

## 6. Order Service

### Responsibilities
- Manages order creation and lifecycle
- Tracks order and shipping status

### Key APIs
- `POST /orders`
- `GET /orders/{id}`
- `PUT /orders/{id}/status`

### Database Schema (Summary)
- **Orders**
  - Id
  - DesignId
  - QuoteId
  - Status
  - PaymentStatus

### Error Handling
- 400 for invalid order data
- 404 for order not found
- 409 for invalid state transitions
- 500 for internal errors

### Communication Type
- REST (synchronous)

---

## 7. Payment Service

### Responsibilities
- Simulates payment processing
- Updates payment status for orders

### Key APIs
- `POST /payments`
- `GET /payments/{orderId}`

### Database Schema (Summary)
- **Payments**
  - Id
  - OrderId
  - Amount
  - Status

### Error Handling
- 400 for invalid payment request
- 500 for simulated payment failures

### Communication Type
- REST (synchronous)

---

## 8. Notification Service

### Responsibilities
- Sends email notifications and system alerts
- Handles order, quote, and shipping notifications

### Key APIs
- `POST /notifications`

### Database Schema
- None (stateless)

### Error Handling
- Logs failed notification attempts
- Does not block main business flows

### Communication Type
- REST (synchronous)  
- Async event-based messaging (future enhancement)

---

## 9. Communication Summary

| Service | Communication |
|-------|---------------|
| Frontend → API Gateway | REST |
| API Gateway → Backend Services | REST |
| Service → Notification Service | REST |
| Future Enhancements | Async messaging |

---

## 10. Notes

- Each service owns its database
- No direct database access between services
- API contracts are designed to be versionable
- Detailed sequence diagrams are provided separately

