# Dressed™ System – Overview

## 1. Purpose

The purpose of this document is to provide a high-level overview of the Dressed™ software system, describing the business problem it addresses, the goals of the system, the primary users, and the proposed high-level solution architecture.

---

## 2. Business Problem

Dressed™ operates as an intermediary platform connecting fashion designers with garment manufacturers (suppliers).  
With a recent surge in both designers and suppliers, manual processes for handling design submissions, supplier quotations, order placement, and communication have become inefficient and difficult to scale.

Additionally, designers have requested Dressed™ to:
- Manage supplier discovery and quotations
- Handle order placement and lifecycle management
- Facilitate payment handling on their behalf

Without a centralized and scalable software solution, Dressed™ faces challenges in:
- Managing growing transaction volumes
- Ensuring reliable communication between designers and suppliers
- Maintaining operational efficiency and transparency

---

## 3. Goals of the System

The primary goals of the Dressed™ system are:

- Provide a centralized digital platform for designers, suppliers, and Dressed™ administrators
- Enable designers to submit clothing designs and receive competitive supplier quotes
- Allow suppliers to discover relevant design requests and submit quotations
- Support order placement, order tracking, and basic payment processing
- Improve scalability, reliability, and operational efficiency using a microservices-based architecture
- Lay a foundation that can be extended with additional features such as analytics, grievance handling, and advanced payments in the future

---

## 4. Users of the System

### 4.1 Designers
Designers use the system to:
- Upload clothing designs (images or PDFs)
- Request quotations from suppliers
- View and compare supplier quotes
- Communicate and negotiate with suppliers
- Place orders through the platform

### 4.2 Suppliers
Suppliers use the system to:
- Subscribe to clothing categories they produce
- View design submissions relevant to their capabilities
- Submit quotations for design requests
- Communicate with designers
- Accept orders and manage shipping notices

### 4.3 Dressed™ Administrators
Dressed™ administrators use the system to:
- Oversee platform activity
- Monitor orders, payments, and supplier participation
- Manage system configurations and operational workflows

---

## 5. High-Level Solution

The proposed solution is a **microservices-based web application** consisting of:

- A **React-based frontend** providing separate interfaces for designers, suppliers, and administrators
- Multiple **.NET backend microservices**, each responsible for a specific business capability such as design management, quotations, orders, and payments
- Containerized services using **Docker and Docker Compose** to ensure consistency across environments
- RESTful APIs for communication between frontend and backend services

This architecture promotes:
- Loose coupling between services
- Independent scalability
- Easier maintenance and future enhancements

