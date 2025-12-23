# Dressed™ System – Data Model (ER Diagram)

## 1. Purpose

This document describes the core data entities of the Dressed™ system and their relationships.  
It provides a logical data model that supports the business workflows while aligning with a microservices architecture.

---

## 2. Core Entities

### Designer
- Id
- Name
- Email

### Supplier
- Id
- Name
- Email

### Design
- Id
- DesignerId
- Category
- FileUrl
- CreatedAt

### Quote
- Id
- DesignId
- SupplierId
- Price
- Message
- Status

### Order
- Id
- DesignId
- QuoteId
- Status
- PaymentStatus

### Payment
- Id
- OrderId
- Amount
- Status

---

## 3. Entity Relationships

