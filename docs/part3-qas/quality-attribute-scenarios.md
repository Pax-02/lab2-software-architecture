# Quality Attribute Scenarios

**Project Name:** PRJ07: Food Delivery and Tracking Platform
**Team Members:**

- Ishimwe Pacis Hanyurwimfura
- Aditya Bhosale
- Alfarizy Alfarizy
  **Date:** 27th January 2026

---

## QAS-01: [Descriptive Name, e.g., "Search Response Under Load"]

**Quality Attribute:** Performance

| Component            | Specification |
| -------------------- | ------------- |
| **Source**           |               |
| **Stimulus**         |               |
| **Environment**      |               |
| **Artifact**         |               |
| **Response**         |               |
| **Response Measure** |               |

**Applicable Tactics (Bass Ch. 5):**

- [Tactic 1]: [How it achieves the response]
- [Tactic 2]: [How it achieves the response]

**Priority Assessment:**

- [ ] Architectural Driver (High Value, High Risk)
- [ ] Contractual Guarantee (High Value, Low Risk)
- [ ] Nice-to-Have (Low Value, Low Risk)
- [ ] Potential Risk (Low Value, High Risk)

**Justification:** [Why this priority?]

---

## QAS-02: [Descriptive Name, e.g., "Database Failover Recovery"]

**Quality Attribute:** Availability

| Component            | Specification |
| -------------------- | ------------- |
| **Source**           |               |
| **Stimulus**         |               |
| **Environment**      |               |
| **Artifact**         |               |
| **Response**         |               |
| **Response Measure** |               |

**Applicable Tactics (Bass Ch. 5):**

- [Tactic 1]: [How it achieves the response]
- [Tactic 2]: [How it achieves the response]

**Priority Assessment:**

- [ ] Architectural Driver (High Value, High Risk)
- [ ] Contractual Guarantee (High Value, Low Risk)
- [ ] Nice-to-Have (Low Value, Low Risk)
- [ ] Potential Risk (Low Value, High Risk)

**Justification:** [Why this priority?]

---

## QAS-03: Adding New Payment Provider

**Quality Attribute:** Modifiability

| Component            | Specification |
| -------------------- | ------------- |
| **Source**           |               |
| **Stimulus**         |               |
| **Environment**      |               |
| **Artifact**         |               |
| **Response**         |               |
| **Response Measure** |               |

- Source: Product owner/development team
- Stimulus: A new external payment provider must be added, while keeping the existing payment flow working
- Environment: During active development, with existing Order + Payment interactions already implemented and used by the UI
- Artifact: Payment service contract (API), payment integration logic inside the Payment service, and any service consumers (Order Service/UI)
- Response: The team implements a new payment provider by adding a new adapter/strategy inside the Payment Service and updating configuration/routing, without changing the Order Service contract and without changing more than minimal UI wiring. Existing provider behavior and contract-based tests continue to work/pass.
- Response Measure: 1 developer can add a new provider in <= 2 working days, with <= 3 files changed outside the Payment Service, and 0 breaking changes to the Payment Service public contract. All automated tests pass, and it can switch providers via config in <= 5 minutes.

**Applicable Tactics (Bass Ch. 5):**

- [Tactic 1]: [How it achieves the response]
- [Tactic 2]: [How it achieves the response]

- Increase semantic cohesion/localize changes: Keep all payment-specific change inside the Payment Service (one coarse-grained business capability), so other services don’t need to be edited.

- Use an intermediary (adapter/strategy) and maintain interface stability: Implement each provider behind a common PaymentProvider interface and keep the Payment Service contract stable for consumers (Order/UI).

**Priority Assessment:**

- [x] Architectural Driver (High Value, High Risk)
- [ ] Contractual Guarantee (High Value, Low Risk)
- [ ] Nice-to-Have (Low Value, Low Risk)
- [ ] Potential Risk (Low Value, High Risk)

**Justification:** [Why this priority?]
SOA is basically about reusable business capabilities with stable contracts. Payments are a classic “swap/extend” area (even if mocked), so designing it to accept new providers with minimal ripple effects tests whether our SOA boundaries and contracts are actually good.
