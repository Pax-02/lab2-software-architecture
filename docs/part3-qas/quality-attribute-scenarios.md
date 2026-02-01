# Quality Attribute Scenarios

**Project Name:** PRJ07: Food Delivery and Tracking Platform
**Team Members:**

- Ishimwe Pacis Hanyurwimfura
- Aditya Bhosale
- Alfarizy Alfarizy
  **Date:** 27th January 2026

---

## QAS-01: Order Placement During Payment Gateway Failure

**Quality Attribute:** Performance

| Component            | Specification                                                                                                                                                                                                                                                                    |
| -------------------- |----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| **Source**           | External payment gateway service                                                                                                                                                                                                                                                 |
| **Stimulus**         | Payment gateway becomes unresponsive or returns timeout/error responses during order placement                                                                                                                                                                                   |
| **Environment**      | Peak load during lunch/dinner hours with high number of concurrent users.                                                                                                                                                                                                        |
| **Artifact**         | Order Placement and Payment Processing services                                                                                                                                                                                                                                  |
| **Response**         | System detects payment failure due to timeout issue, aborts the payment transaction, preserves the order state as Pending Payment, and provides  an immediate feedback to the user without blocking the system and user can retry payment without creating the same order again. |
| **Response Measure** | Payment timeout detected ≤ 3 seconds<br/>User receives failure message ≤ 5 seconds<br/>No partial or duplicate orders created<br/>System throughput degradation ≤ 10%                                                                                                                                                                                                                                                                                 |

**Applicable Tactics (Bass Ch. 5):**

- Timeout & Retry: Limits the wait time for the payment gateway and retry for a  configurable number of times before failing.
- Graceful Degradation: Allows the users to retry the payment later or choose an alternative payment method without re-creating the order again.

**Priority Assessment:**

- [x] Architectural Driver (High Value, High Risk)
- [ ] Contractual Guarantee (High Value, Low Risk)
- [ ] Nice-to-Have (Low Value, Low Risk)
- [ ] Potential Risk (Low Value, High Risk)

**Justification:**
Payment processing is a critical path in the food delivery system. Failures during peak hours can directly impact revenue and user trust. Handling payment gateway failures efficiently is important for maintaining acceptable system performance and user experience under load, making this case an important architectural driver.

---

---


## QAS-02: [Descriptive Name, e.g., "Database Failover Recovery"]

**Quality Attribute:** Availability

| Component            | Specification                                                                                                                                                                              |
| -------------------- |--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| **Source**           | Delivery driver using the delivery app                                                                                                                                                     |
| **Stimulus**         | The delivery tracking crashes while a delivery is in progress                                                                                                                              |
| **Environment**      | Normal operation during an active delivery                                                                                                                                                 |
| **Artifact**         | Delivery tracking service                                                                                                                                                                  |
| **Response**         | The system continues displaying the last known location of the driver and automatically restores live tracking once the service restarts                                                   |
| **Response Measure** | - Application remain accessible to the customer <br/>-Order is not lost <br/>-Last know location is shown in 2 seconds.<br/>-live tracking resumes in 10-15 seconds after sercice recovery |


**Applicable Tactics (Bass Ch. 5):**

- Heart beat detection tactic: Periodic signals to detect that the delivery system is alive
- Schedule resources: Have resources to re-deploy a service when it goes down
- Graceful degradation: Still provide the last known location even if the live location is down

**Priority Assessment:**

- [X] Architectural Driver (High Value, High Risk)
- [ ] Contractual Guarantee (High Value, Low Risk)
- [ ] Nice-to-Have (Low Value, Low Risk)
- [ ] Potential Risk (Low Value, High Risk)

**Justification:** [Why this priority?] </br>
This is a priority cause if the delivery service goes down then the drivers won't get deliveries and the customers won't be able to continue the ordering process.
---

## QAS-03: Adding New Payment Provider
**Quality Attribute:** Modifiability

| Component            | Specification                                                                                                                                                                                                                                                                                                       |
|----------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| **Source**           | Product owner/development team.                                                                                                                                                                                                                                                                                     |
| **Stimulus**         | A new external payment provider must be added, while keeping the existing payment flow working.                                                                                                                                                                                                                     |
| **Environment**      | During active development, with existing Order + Payment interactions already implemented and used by the UI.                                                                                                                                                                                                       |
| **Artifact**         | Payment service contract (API), payment integration logic inside the Payment service, and any service consumers (Order Service/UI).                                                                                                                                                                                 |
| **Response**         | The team implements a new payment provider by adding a new adapter/strategy inside the Payment Service and updating configuration/routing, without changing the Order Service contract and without changing more than minimal UI wiring. Existing provider behavior and contract-based tests continue to work/pass. |
| **Response Measure** | 1 developer can add a new provider in <= 2 working days, with <= 3 files changed outside the Payment Service, and 0 breaking changes to the Payment Service public contract. All automated tests pass, and it can switch providers via config in <= 5 minutes.                                                      |

**Applicable Tactics (Bass Ch. 5):**

- [Tactic 1]: Increase semantic cohesion/localize changes: Keep all payment-specific change inside the Payment Service (one coarse-grained business capability), so other services don’t need to be edited.
- [Tactic 2]: Use an intermediary (adapter/strategy) and maintain interface stability: Implement each provider behind a common PaymentProvider interface and keep the Payment Service contract stable for consumers (Order/UI).

**Priority Assessment:**

- [x] Architectural Driver (High Value, High Risk)
- [ ] Contractual Guarantee (High Value, Low Risk)
- [ ] Nice-to-Have (Low Value, Low Risk)
- [ ] Potential Risk (Low Value, High Risk)

**Justification:** [Why this priority?]
SOA is basically about reusable business capabilities with stable contracts. Payments are a classic “swap/extend” area (even if mocked), so designing it to accept new providers with minimal ripple effects tests whether our SOA boundaries and contracts are actually good.
