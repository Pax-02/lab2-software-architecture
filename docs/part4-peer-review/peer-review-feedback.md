## Peer Review Feedback

**Reviewing Team:** Alfarizy Alfarizy - 3810253
                    Ishimwe Pacis Hanyurwimfur - 3787234
                    Aditya Bhosale - 3810398
**Reviewed Team:** JOYDIP DAS- 3804528
**Date:** 27-Jan-2026

### QAS-01 Feedback

### Strengths:
    - Clearly follows the Source–Stimulus–Environment–Artifact–Response–Response Measure template.
    - Quantified response measures: P95 ≤ 1500 ms, 5000 concurrent users, and 3-minute scale-out time make the scenario measurable.
    - Clear architectural driver: Correctly identified as High Value, High Risk—flight search latency directly impacts conversion and revenue.

###  Improvement needed:
    - “5000 concurrent users” does not specify request rate (e.g., searches/sec per user).
    - External dependencies omitted: Flight search typically relies on GDS/airline APIs—behavior under their latency or throttling is not addressed.
    -
###  Suggested revision:
    - During a promotional travel season, 5000 concurrent users generate an average of 2 flight search requests per second per user, resulting in ~10,000 RPS.
    - Response Measure: When P95 latency exceeds 1200 ms or CPU utilization exceeds 70% for 2 consecutive minutes, the system automatically scales out the Flight Search Service.

### QAS-02 Feedback

### Strengths
    -The quality attribute is well structured with all the 6 parts
    which makes it easy to understand and test.
    - Marked as an architecture driver as payment is a crucial feature 
    in the travel booking system.
    - Ensures smooth user exprience by retrying the payment and saves payment
    incase it fails which prevent frustration of re-inserting information
    - Use of fault detection and fault recovery availabily tactics by logging failures,
    retrying transactions and do a rollback.
    = Clearly stating that no double charges should be applied which is crucial in payment

###  Improvement needed:
    -Heartbeat checks would not work on third party payment providers like paypal,
    stripe. failure detection should be through timeouts, error response or 
    webhooks resposne.
    - Retry behaviour can be made clearer stating how many retries to happen in 60 sec and also
    specify if it will use delay or backoff technique to not overwhelm or be taken as DDOS attack and 
    prevent double charging also.
    -The failover mechanism is not well specified as you would not have access to the thirdy party instances
    - The response measure were well defined regarding time limits and by adding 
    clear success and failure response would make smooth testing 
###  Suggested revision:

#### Revised rresponse:
    -The Booking Service detects a payment failure, logs the error, retries the payment safely, 
    and shows a retry message to the user.If payment still fails, the system saves the booking info, 
    marks the booking as pending payment, and allows the user to retry later without risk of being charged twice.
#### Revised Tactic:
    - Detect payment failures using timeouts, error codes and callback
    - Use unique transaction to avoid duplicate charges
    - If retries fail, save the booking as Payment Pending so the user can retry later


### QAS-03 Feedback

- Strengths:
- Improvement needed:
- Suggested revision:
