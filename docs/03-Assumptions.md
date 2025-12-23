# Dressed™ System – Assumptions

## 1. Purpose

This document lists the assumptions made while designing and implementing the Dressed™ system.  

---

## 2. Functional Assumptions

- User authentication and authorization are implemented in a basic or mocked manner.
- Role separation (Designer, Supplier, Admin) is assumed to be handled via simple role flags.
- Communication between designers and suppliers is assumed to be text-based only.
- Supplier quotations are submitted as text with pricing information.
- Shipping notices are limited to status updates without integration to external logistics providers.

---

## 3. Technical Assumptions

- The backend is implemented using **C# and .NET CORE** following a microservices architecture.
- Each microservice owns its own database to maintain loose coupling.
- Databases are implemented using  **PostgreSQL** for containerized environments.
- Inter-service communication is primarily synchronous via REST APIs.
- Asynchronous messaging is not required for the scope of this assessment.

---

## 4. Payment Assumptions

- The payment processing service is simulated and does not integrate with a real payment gateway.
- Payment status updates are mocked to demonstrate order flow.
- Payment failures are simulated using predefined conditions.

---

## 5. Deployment Assumptions

- The system is deployed in a **single cloud region**.
- Services are containerized using **Docker** and orchestrated using **Docker Compose**.
- Kubernetes is considered a future enhancement but is not required for this implementation.
- Environment-specific configurations are managed via environment variables.

---

## 6. Storage Assumptions

- Uploaded design files (Images/PDFs) are stored using local file storage for simplicity.
- The design allows future migration to cloud object storage (e.g., Azure Blob Storage).
- File size limits and validation are kept minimal.

---

## 7. Operational Assumptions

- Basic logging is implemented for all services.
- Centralized monitoring and alerting are not fully configured.
- Manual inspection of logs is sufficient for this assessment.

---

## 8. Security Assumptions

- Data is transmitted over HTTP within a trusted local network.
- Advanced security mechanisms such as OAuth, encryption at rest, and rate limiting are out of scope.
- These aspects can be introduced as future enhancements.

