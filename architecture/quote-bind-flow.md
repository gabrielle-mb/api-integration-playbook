## Quote → Bind Flow

**Scenario:** A partner requests a quote, then binds a policy.

---

### Flow

1. Partner sends quote request
2. API receives and validates payload
3. Underwriting calculations generate a premium
4. API returns quote response with quote ID and premium
5. Partner sends bind request using quote ID
6. Policy service creates the policy
7. Confirmation is returned

---

### Diagram
Partner → API Gateway → Rating Service → Policy Service → Response

```mermaid
flowchart LR
    A[Partner] --> B[API Gateway]
    B --> C[Rating Service]
    C --> D[Policy Service]
    D --> E[Response]

---

### Common Failure Points

- Missing required fields in payload
- Incorrect data types (string vs number)
- NULL vs empty values
- Timeouts between services
- Invalid quote ID during bind

---

### Notes from Experience

- Most issues happen at the payload level, not the system level  
- Clear error messages dramatically reduce back-and-forth with partners  
- Idempotency is important for bind requests to avoid duplicates  
