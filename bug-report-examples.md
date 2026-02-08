# Bug Report Examples – Login & Lockout Flow

These bug reports demonstrate how QA findings are documented with
clear reproduction steps, expected behavior, and risk impact.

---

## Bug 1: User Enumeration via Login Error Message

**ID:** BR-01  
**Title:** Login error message reveals account existence  
**Severity:** High (Security)  
**Priority:** High  

### Description
The system displays different error messages when:
- a non-existing email is used
- an existing email with an incorrect password is used

This behavior allows attackers to determine whether a user account exists.

### Steps to Reproduce
1. Navigate to the Login page.
2. Enter a non-existing email and any password.
3. Click "Login".
4. Observe the error message.
5. Repeat steps 1–4 using an existing email with an incorrect password.

### Actual Result
- Non-existing email: “User not found”
- Existing email: “Incorrect password”

### Expected Result
A generic error message should be shown in both cases, e.g.:
“Invalid email or password”.

### Risk Impact
- Enables user enumeration.
- Increases risk of targeted brute-force and phishing attacks.

### QA Recommendation
Use a unified error message for all authentication failures.

---

## Bug 2: Failed Login Counter Not Reset After Successful Login

**ID:** BR-02  
**Title:** Failed login counter persists after successful authentication  
**Severity:** Medium  
**Priority:** Medium  

### Description
After multiple failed login attempts, the failedAttempts counter
is not reset when the user logs in successfully.

This may cause unexpected lockout behavior later.

### Steps to Reproduce
1. Attempt login with an incorrect password twice.
2. Login successfully using correct credentials.
3. Logout.
4. Attempt login again with an incorrect password.

### Actual Result
The system treats the new failure as the next failed attempt
(e.g. third attempt) and may trigger lockout.

### Expected Result
The failedAttempts counter should reset after a successful login.

### Risk Impact
- Unexpected user lockout.
- Poor user experience.
- Increased customer support requests.

### QA Recommendation
Explicitly reset the failedAttempts counter upon successful authentication.

---

## Bug 3: Lockout Duration Miscalculation

**ID:** BR-03  
**Title:** User allowed to retry login before lockout duration expires  
**Severity:** High  
**Priority:** High  

### Description
The lockout duration is defined as X minutes, but the system allows
login attempts before the full lockout period has elapsed.

### Steps to Reproduce
1. Trigger account lockout by exceeding the failed attempt threshold.
2. Note the lockout start time.
3. Attempt login again before X minutes have passed.

### Actual Result
The system allows a new login attempt earlier than expected.

### Expected Result
Login attempts should remain blocked until the full lockout duration expires.

### Risk Impact
- Weakens brute-force protection.
- Reduces effectiveness of the security policy.

### QA Recommendation
Calculate lockout duration using server-side timestamps
and enforce consistent time checks.

