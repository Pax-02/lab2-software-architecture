## Peer Review Feedback

**Reviewing Team:** Alfarizy Alfarizy - 3810253
                    Ishimwe Pacis Hanyurwimfur - 3787234
                    Aditya Bhosale - 3810398
**Reviewed Team:** JOYDIP DAS- 3804528
**Date:** 27-Jan-2026

### QAS-01 Feedback

- Strengths: 
  - Clearly follows the Source–Stimulus–Environment–Artifact–Response–Response Measure template.
  - Quantified response measures: P95 ≤ 1500 ms, 5000 concurrent users, and 3-minute scale-out time make the scenario measurable.
  - Clear architectural driver: Correctly identified as High Value, High Risk—flight search latency directly impacts conversion and revenue.

- Improvement needed: 
  - “5000 concurrent users” does not specify request rate (e.g., searches/sec per user).
  - External dependencies omitted: Flight search typically relies on GDS/airline APIs—behavior under their latency or throttling is not addressed.
  - 
- Suggested revision: 
  - During a promotional travel season, 5000 concurrent users generate an average of 2 flight search requests per second per user, resulting in ~10,000 RPS.
  - Response Measure: When P95 latency exceeds 1200 ms or CPU utilization exceeds 70% for 2 consecutive minutes, the system automatically scales out the Flight Search Service.

### QAS-02 Feedback

- Strengths:
- Improvement needed:
- Suggested revision:

### QAS-03 Feedback

- Strengths:
- Improvement needed:
- Suggested revision:
