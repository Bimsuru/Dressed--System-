# Dressed™ System – Requirements (FRD)

## 1. Purpose

This document defines the functional and non-functional requirements of the Dressed™ system.  

---

## 2. Functional Requirements

### 2.1 Designer Functional Requirements

Designers must be able to:

- Upload clothing designs in supported formats (Image or PDF)
- Categorize designs under predefined categories (e.g., Men, Women, Boy, Girl, Unisex)
- Submit design requests to receive quotations from suppliers
- View all quotations submitted by suppliers for a given design
- Communicate and negotiate with suppliers through the platform
- Select a preferred supplier quotation
- Place an order based on the selected quotation
- View the status of placed orders

---

### 2.2 Supplier Functional Requirements

Suppliers must be able to:

- Subscribe to one or more clothing categories they manufacture
- View design requests relevant to their subscribed categories
- Access full design details, including uploaded files and specifications
- Submit price quotations with optional descriptive text
- Communicate and negotiate with designers
- Accept or reject orders assigned to them
- Send shipping notices after order acceptance
- View the status of their active and completed orders

---

### 2.3 Dressed™ Administrator Functional Requirements

Administrators must be able to:

- Monitor platform activity across designers and suppliers
- View orders, quotations, and payment status
- Manage system configurations and operational workflows
- Access logs and system health information for operational oversight

---

## 3. Non-Functional Requirements

### 3.1 Scalability

- The system must support horizontal scaling of individual services
- Services must be stateless where possible to allow load balancing
- The system must handle increasing numbers of designers, suppliers, and concurrent requests

---

### 3.2 Fault Tolerance

- Failure of a single microservice must not cause system-wide failure
- Services must implement retry and timeout mechanisms where applicable
- The system must gracefully handle partial outages and degraded performance

---

### 3.3 Loose Coupling

- Each microservice must have a single, well-defined responsibility
- Services must communicate via well-defined APIs
- Direct database access between services is not permitted
- Changes in one service should not require changes in other services

---

### 3.4 Observability

- All services must produce structured logs
- Key metrics such as request rate, error rate, and latency must be captured
- Health check endpoints must be exposed for each service
- The system must support monitoring and troubleshooting in a production environment

---

## 4. Out of Scope

The following are considered out of scope for this implementation:

- Advanced authentication and authorization mechanisms
- Real-world payment gateway integrations
- Automated supplier vetting and grievance handling workflows

These can be added as future enhancements.

