# Dressed™ System – System Architecture (High-Level Design)

## 1. Purpose

This document describes the high-level system architecture of the Dressed™ platform.  
It outlines the identified microservices, their responsibilities, and how they collectively support the business workflows of designers, suppliers, and Dressed™ administrators.

---

## 2. Architecture Style

- Microservices-based architecture
- Backend services implemented using **.NET CORE (C#)**
- Frontend implemented using **React**
- Inter-service communication via **REST APIs**
- Containerized deployment using **Docker and Docker Compose**

---

## 3. Identified Microservices

The system is decomposed into multiple microservices, each responsible for a single business capability.

| Service Name | Responsibility |
|-------------|----------------|
| **API Gateway(ocelot)** | Acts as the single entry point for all client requests, routes requests to backend services, and performs basic request validation. |
| **User Service** | Manages user accounts, roles (Designer, Supplier, Admin), and basic authentication logic. |
| **Design Service** | Handles design submissions, file uploads (Image/PDF), categorization, and retrieval of designer posts. |
| **Quote Service** | Manages supplier quotations, quote retrieval, and negotiation-related interactions. |
| **Order Service** | Handles order placement, order status tracking, and the overall order lifecycle. |
| **Payment Service** | Simulates payment processing and updates payment status for orders. |
| **Notification Service** | Sends email notifications and system alerts for events such as quote submission, order placement, and shipping updates. |

---

## 4. Service Interaction Overview

- All frontend requests are routed through the **API Gateway**
- Backend services do not access each other’s databases
- Each service exposes RESTful APIs with clear contracts
- The **Notification Service** is triggered by events from other services

---

## 5. Design Rationale

- **Microservices decomposition** aligns with distinct business domains
- **API Gateway** simplifies frontend communication and future security enhancements
- **Single responsibility per service** improves maintainability
- **Independent services** allow future scaling and feature expansion

---

## 5. Notes

- High-Level Interaction Flow digram, sequence diagrams, ER diagrams, and deployment diagrams are provided separately.

- The architecture supports future enhancements such as asynchronous messaging and real payment gateway integrations.

