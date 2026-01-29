# ARC42 Documentation: Sections 1–3

**Project Name:** PRJ07: Food Delivery and Tracking Platform
**Team Members:**

- Ishimwe Pacis Hanyurwimfura
- Aditya Bhosale
- Alfarizy Alfarizy

  **Date:** 27th January 2026
  **Version:** 1.0 (Lab 2 Draft)

---

## Section 1: Introduction and Goals

### 1.1 Requirements Overview

**What is the system?**
[2-3 sentences describing what your system does and why it exists]

The system is a food delivery and tracking platform that connects customers, restaurants, drivers, and payments in one workflow.

Customers can browse menus, place orders, pay, and then follow their delivery progress via live (simulated in this case) status updates and driver location tracking.

**Core Features:**

1. Restaurant and menu browsing (availability, items, pricing)
2. Order placement and processing (create order, confirm, pay, update status)
3. Delivery assignment, tracking, and customer notifications (driver assignment, simulated GPS, order progress updates)

### 1.2 Quality Goals

| Priority | Quality Attribute    | Motivation         |
| -------- | -------------------- | ------------------ |
| 1        | [e.g., Availability] | [Why this matters] |
| 2        | [e.g., Performance]  | [Why this matters] |
| 3        | [e.g., Security]     | [Why this matters] |

- Priority: 1
- Quality Attribute: Reliability/Availability
- Motivation: As the customers, they would expect ordering and tracking to work consistently. Missed on updates or downtime will break the trust and cause support problems.

- Priority: 2
- Quality Attribute: Performance/Responsiveness
- Motivation: Browsing menus and seeing status updates should feel fast and seamless. Slow APIs will make the app feel "broken" even if it is technically working.

- Priority: 3
- Quality Attribute: Maintainability + Reusability
- Motivation: Services should be self-contained and high-level (like Order, Payment, and Delivery). This will make them easy to reuse later for things like catering or meal-prep, and it will allow teams to improve or change one service without touching the rest of the system.

### 1.3 Stakeholders

| Role          | Description     | Expectations         |
| ------------- | --------------- | -------------------- |
| End User      | [Who are they?] | [What do they need?] |
| Administrator | [Who are they?] | [What do they need?] |
| Developer     | [Who are they?] | [What do they need?] |

- Role: End user (customer)
- Description: Person who orders food and trakcs delivery
- Expectations: Easy restaurant/menu browsing, simple checkout, clear order status updates, and accurate delivery tracking

- Role: Administrator (restaurant staff/admin)
- Description: Managing restaurant availability and menu, receiving and fulfilling orders
- Expectations: See incoming orders, update order preparation status, manage menu items/availability, and minimal confusion/duplicate orders

- Role: Developer (project team)
- Description: Building and evolving the system
- Expectations: Clear service boundaries and contracts, good testability, stable APIs, and a design that matches SOA (coarse-grained, reusable services)

- Role: System administrator
- Description: Maintain platform configuration and monitor health
- Expectations: Basic monitoring/logs, ability to manage restaurant/driver accounts in the system, and visibility into failures (payment mock failures, delivery issues)

---

## Section 2: Constraints

### 2.1 Technical Constraints

| Constraint                | Explanation                  |
| ------------------------- | ---------------------------- |
| [e.g., Must use Java 17+] | [Why this constraint exists] |

### 2.2 Organizational Constraints

| Constraint        | Explanation              |
| ----------------- | ------------------------ |
| [e.g., Team of 4] | [Impact on architecture] |

### 2.3 Conventions

| Convention       | Explanation         |
| ---------------- | ------------------- |
| [e.g., REST API] | [Standard followed] |

---

## Section 3: Context and Scope

### 3.1 Business Context

**System Context Diagram:**
![img.png](C4 Diagram for food ordering Service drawio.png)

**External Interfaces:**

| Interface                       | Description                                                                                            | Technology                          |
|---------------------------------|--------------------------------------------------------------------------------------------------------|-------------------------------------|
| Customer Mobile/Web App         | Allows customers to browse restaurants, place orders, make payments, and track deliveries in real time | Web Dashboard (React), REST APIs    |
| Restaurant Management Interface | Enables restaurant staff to manage menus, accept/rejects orders, and update preparation status         | Web Dashboard (React), REST APIs    |
| Delivery Partner App            | Allows delivery partners to accept delivery requests, update order status, and share live location     | Mobile App, REST APIs, GPS          |
| Payment Gateway Interface       | Processes online payments and returns payment status                                                   | REST APIs, Cards/Wallets            |
| Notification Service Interface  | Sends order confirmations, status updates, and delivery alerts                                         | REST APIs, Webhooks, SMS/Email/Push |
| Maps / GPS Interface            | Provides routing, distance calculation, and live location tracking.                                    | GPS, API                            |

### 3.2 Technical Context

| Component                    | Technology                   | Purpose                                                                         |
|------------------------------|------------------------------|---------------------------------------------------------------------------------|
| Customer Application         | React (Web),Flutter (Mobile) | User-facing interface for browsing, ordering, payment, and tracking             |
| Restaurant Dashboard         | React                        | Interface for restaurant staff to manage orders and menus                       |
| Delivery Partner Application | Flutter                      | Interface for delivery agents to manage deliveries and share location           |
| Food Delivery Backend System | Spring Boot (Microservices)  | Core business logic for order processing, tracking, payments, and notifications |
| Payment Gateway              | Paypal                       | Secure payment processing                                                       |
| Notification Service         | Firebase Cloud Messaging     | Sends real-time alerts and updates                                              |
| Maps / GPS Service           | Google Maps API              | Provides routing and real-time delivery tracking                                |
| Database                     | PostgreSQL                   | Stores orders, users, restaurants, and delivery data                            |
---

_This document will be expanded in M2 to include Sections 4–5._
